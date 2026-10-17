# UI Redesign Plan

## Objectives

This redesign updates the visual treatment of the existing gateway without changing the payment logic. The goal is to align the current checkout and admin screens with the styling and layout in the design reference under `stitch_self_hosted_upi_payment_gateway` while preserving the same IDs, API calls, SSE behavior, and webhooks.

## Screen-to-File Mapping

| Design reference screen | Primary target file | Notes |
| --- | --- | --- |
| Bharat Gateway admin dashboard shell | `apps/merchant-admin/src/views/admin.html` | Main dashboard shell, header, navigation, KPIs, tables, cards, and layout. |
| Payments list + CSV export | `apps/merchant-admin/src/views/admin.html` | Payment table, filters, status badges, export action area, and list styling. |
| Payment detail + webhook inspector | `apps/merchant-admin/src/views/admin.html` | Detail drawer/panel, metadata panel, webhook payload display, tabs, and tracing data. |
| Observers heartbeat status | `apps/merchant-admin/src/views/admin.html` | Observer health cards, status badges, heartbeat timeline, and alert ribbon. |
| Branding settings | `apps/merchant-admin/src/views/admin.html` | Branding form sections, color pickers, logo upload styling, merchant identity panel. |
| Developer settings + webhooks | `apps/merchant-admin/src/views/admin.html` | API keys, webhook endpoint cards, secret fields, and HMAC settings layout. |
| Customer management + VPAs | `apps/merchant-admin/src/views/admin.html` | VPA list card, customer records, search/filter controls, action buttons. |
| UPI dashboard merchant telemetry | `apps/merchant-admin/src/views/admin.html` | Telemetry widgets, chart panels, segment cards, and real-time metrics. |
| Checkout flow: phone, OTP, queue, QR, verifying, result screens | `apps/checkout-portal/src/views/checkout.html` | Single-file redesign for all payment states and responsive mobile drawer experience. |

## Design Execution Strategy

1. Apply the shared design tokens first in the current HTML/CSS definitions for the checkout and admin shell.
2. Update the checkout flow styling to match the new Bharat Gateway visual language: mobile-first layout, clearer transaction states, stronger hierarchy, and consistent status colors.
3. Update the admin experience with the new dashboard patterns and settings layouts while keeping the existing data fields and server endpoints untouched.
4. Validate that all existing IDs and JS hooks continue to work after the styling pass.

## Expected Files to Touch

- `apps/checkout-portal/src/views/checkout.html`
- `apps/merchant-admin/src/views/admin.html`

## Out of Scope for This Redesign

- Payment logic, queue logic, OTP logic, webhook verification, database operations, and observer backends.
- Any changes to API contracts, SSE handling, or `youpi.js` behavior.
- Hidden secret values or `.env` configuration updates.

## Verification Checkpoints

- Run the root test suite after each redesign pass.
- Check the checkout portal in both desktop and mobile widths.
- Check admin sections for layout and responsiveness without disturbing interactions.
