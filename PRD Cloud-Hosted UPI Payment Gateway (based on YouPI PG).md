# PRD: Cloud-Hosted UPI Payment Gateway (based on YouPI PG)

Version 1.0 · Draft · Owner: You · Base repo: github.com/gxurav1710/YouPI-PG

## 1. Summary

We will fork YouPI PG, deploy it on a cloud server, and use it as the payment backend for our own app (the "Main App"). Customers pay through UPI QR or app deep links straight into our bank account. The gateway detects the credit via bank SMS, notifications or Gmail alerts, then sends a signed webhook to the Main App so it can fulfil the order.

## 2. Goals and non-goals

**Goals**

- Accept UPI payments in the Main App with no per-transaction aggregator fee.
- Run the gateway 24/7 on a cloud host with HTTPS and our own domain (for example pay.ourdomain.com).
- Confirm payments automatically and notify the Main App within about 30 seconds of the customer paying.
- Keep the gateway white-labelled with our branding.

**Non-goals (v1)**

- Card, netbanking or wallet payments.
- Automated refunds or payouts (refunds are done manually from the bank app).
- Multi-merchant or SaaS resale of the gateway.
- Rewriting the upstream codebase. We configure, harden and deploy; we only patch what we must.

## 3. Users

- **Customer:** pays in the Main App on mobile or desktop.
- **Merchant/Admin (us):** configures VPA, branding, observers; reviews failed or suspicious orders.
- **Main App backend:** creates payment sessions and receives webhooks.

## 4. User flow

1. Customer taps Pay in the Main App.
2. Main App opens the YouPI checkout (modal or drawer via youpi.js) with order\_id and amount.
3. Customer verifies their phone with a WhatsApp OTP (first time only).
4. Gateway assigns the single payment slot (or queues the customer), then shows the QR and UPI app buttons.
5. Customer pays; the bank sends an SMS, notification or email.
6. An observer parses the alert and the gateway matches amount and UTR.
7. Gateway marks the order SUCCESS and sends a signed webhook to the Main App.
8. Main App verifies the signature, fulfils the order, and redirects the customer to the success page.

## 5. Functional requirements

| ID | Requirement | Priority |
| --- | --- | --- |
| F1 | Fork the repo, run locally, and pass the full test suite (npm test) before any change | P0 |
| F2 | Configure our VPA, merchant name, logo and colours in the Admin Panel | P0 |
| F3 | Embed youpi.js in the Main App with a declarative button or window.Youpi.pay() | P0 |
| F4 | Main App webhook endpoint verifies X-Gateway-Signature over the raw request body using timing-safe comparison | P0 |
| F5 | Webhook handler is idempotent: the same paymentId or utr never fulfils an order twice | P0 |
| F6 | Main App also checks the amount received equals the order amount before fulfilling | P0 |
| F7 | At least one reliable observer in production (Android APK on a dedicated phone, plus Gmail OAuth as backup) | P0 |
| F8 | WhatsApp OTP login works from the cloud host, with session persisted across restarts | P1 |
| F9 | Outcome pages (success, failed, expired, cancelled, suspicious) are branded and wired to the Main App | P1 |
| F10 | Admin alerts (email or WhatsApp) when an observer goes offline or an order is flagged | P1 |
| F11 | Manual reconciliation view: list orders with status, UTR and timestamps, exportable as CSV | P2 |

## 6. Cloud deployment requirements

- **Host type:** a small always-on VPS or VM (2 vCPU, 2 to 4 GB RAM, Ubuntu LTS). Avoid serverless or autoscaling platforms: the gateway keeps long-running processes, a WhatsApp socket and a local SQLite file.
- **Persistence:** SQLite data directory and WhatsApp auth state on a persistent disk, with daily off-server backups.
- **Process management:** run under PM2 or systemd with auto-restart and log rotation.
- **Networking:** reverse proxy (Caddy or Nginx) with HTTPS on pay.ourdomain.com, or a Cloudflare Tunnel. Only expose the checkout portal and payment API publicly.
- **Admin protection:** the Admin Panel (6001) and Control Center (8090) must not be public. Restrict by VPN, IP allowlist or Cloudflare Access, plus strong credentials.
- **Secrets:** all keys (webhook secret, observer HMAC secret, OAuth credentials) live in environment variables or a secrets manager, never in git. Rotate any default values from .env.example.
- **Observers on cloud:** prefer the Android APK and Gmail OAuth API. Headless-Chrome observers (Google Messages Web, Gmail CDP) are heavier and more fragile on a small server.
- **Single instance only:** one gateway instance, because the single-slot queue and SQLite assume one writer.

## 7. Main App integration contract

- **Client:** include youpi.js with our public key; pass order\_id, amount and currency (INR).
- **Server webhook:** POST to our endpoint with headers X-Gateway-Signature, X-Gateway-Event, X-Gateway-Delivery-Id and X-Gateway-Timestamp. Payload fields: event, orderId, amount, amountPaise, utr, paymentId.
- **Rules:** never trust the browser callback alone; verify HMAC on raw bytes; reject stale timestamps; return 200 quickly and process asynchronously; dedupe by paymentId.

## 8. Non-functional requirements

- **Reliability:** target 99% uptime; the gateway restarts automatically after a crash or reboot.
- **Latency:** payment confirmed in the Main App within 30 seconds of the bank alert in 95% of cases.
- **Accuracy:** zero mismatched or double-credited payments in testing.
- **Security:** HTTPS everywhere, secrets out of the repo, admin surfaces private, dependencies audited (npm audit), and the Android APK built from source rather than trusting the committed binary.
- **Observability:** structured logs, health checks, and an alert when no observer heartbeat is seen for 5 minutes.

## 9. Constraints and risks

| Risk | Impact | Mitigation |
| --- | --- | --- |
| Collecting business payments on a personal UPI account may breach NPCI or bank terms | Account restriction or freeze | Use a current account with a business VPA; confirm with the bank and an accountant; handle GST and records |
| Bank changes SMS or email format | Payments not detected | Keep two observer channels; add parser tests with real sample messages; manual reconcile fallback |
| Phone with bank SIM goes offline | Payments pending | Dedicated phone on charger, battery optimisation off, heartbeat alerts |
| Baileys is an unofficial WhatsApp client | Number ban or breakage | Use a dedicated number; keep a fallback OTP method; monitor upstream updates |
| Single-slot queue limits concurrency | Customers wait during peaks | Acceptable for low volume; measure queue wait; revisit if volume grows |
| Licence terms | Legal exposure | Read LICENSE and confirm commercial use is allowed before launch |
| Server compromise | Fraudulent confirmations | Signed observer payloads, private admin, OS updates, minimal open ports, backups |

## 10. Milestones

1. **Setup (day 1):** fork, clone, npm install, run locally, npm test passes.
2. **Local integration (days 2 to 3):** Main App button, checkout flow and webhook verified against local gateway with a test order.
3. **Observers (days 4 to 6):** Android APK built and paired; Gmail observer connected; real small-value payments detected.
4. **Cloud deploy (days 7 to 9):** VPS, domain, HTTPS, PM2, backups, private admin, secrets rotated.
5. **Hardening and UAT (days 10 to 12):** idempotency, amount checks, failure drills (observer offline, duplicate webhook, expired session), branding.
6. **Soft launch (day 13+):** low-value live payments, daily reconciliation, then full rollout.

## 11. Acceptance criteria

- A real ₹1 payment from GPay, PhonePe and Paytm each reaches SUCCESS and triggers exactly one verified webhook.
- A tampered webhook body or wrong signature is rejected with 401.
- Replaying the same webhook does not fulfil the order twice.
- Paying the wrong amount does not mark the order paid.
- After a server reboot, all services and the WhatsApp session recover without manual steps.
- Admin Panel and Control Center are unreachable from the public internet.

## 12. Open questions

- Which bank account and VPA will receive payments (business or personal)?
- Expected daily transaction volume and peak concurrency?
- Which cloud provider and region (for example a Mumbai region for latency)?
- What stack is the Main App built on, so we can write the webhook handler in the right language?
