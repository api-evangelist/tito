# Tito (tito)

Tito (ti.to) is an event registration and ticketing platform from Team Tito (Team Tito Limited, Dublin, Ireland). Organizers sell tickets and collect registrations for conferences and events through Tito-hosted event pages or an embeddable widget, then check attendees in with Tito's mobile and web apps.

## Access model (read this first)

- **Public, documented REST API.** The Tito **Admin API** is a REST/JSON API with base URL `https://api.tito.io/v3`. Its paths, methods, and authentication are documented at [ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0).
- **Authentication is a secret API token.** You generate a token at [id.tito.io](https://id.tito.io/api-access-tokens) and send it as `Authorization: Token token=YOUR-API-TOKEN` along with `Accept: application/json`. Tokens are scoped to a `live` or `test` mode. There is no public/anonymous access to the Admin API.
- **Resources are addressed by slug.** Most endpoints are nested under an `account_slug` and `event_slug` (for example `GET https://api.tito.io/v3/:account_slug/:event_slug/tickets`).
- **Events, not sockets, for real time.** Tito delivers real-time notifications via **outbound webhooks** — Tito POSTs a JSON payload to endpoints you register. This is server-to-endpoint HTTP, **not** a WebSocket. There is **no documented public WebSocket API** (see `review.yml`).
- **Separate Check-in API.** Tito also runs an unauthenticated Check-in API at `https://checkin.tito.io` that scopes access by putting a Check-in List slug in the URL. It is noted here for completeness and is not the focus of this catalog entry.
- **Honesty note on the artifacts.** Tito does **not** publish a machine-readable OpenAPI/JSON Schema. In `openapi/tito-openapi.yml`, every **path, HTTP method, path parameter, query filter, and the auth scheme are grounded** in Tito's official Admin API v3.0 docs, but the request/response **body schemas are modeled** (loosely typed) from the documented attribute tables and example payloads. Treat field-level schemas as a reasonable model, not an exhaustive contract.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/tito/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/tito/refs/heads/main/apis.yml)

## Tags

- Event Ticketing
- Events
- Registration
- Ticketing
- Conferences
- Event Management
- Attendees
- Webhooks
- SaaS

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

All APIs share the base URL `https://api.tito.io/v3` and the secret-token authentication described above.

### Tito Events API

Create, list (upcoming, past, archived), retrieve, update, delete, and duplicate Events under an Account. An Event is the parent of releases, tickets, registrations, and most other resources.

- **Human URL:** [https://ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0)
- **Base URL:** `https://api.tito.io/v3`

### Tito Releases API

Manage Releases — the ticket types sold for an Event. Create, retrieve, update, delete, and duplicate releases, put them on sale or pause them (activation/deactivation), archive/unarchive them, and toggle public/secret visibility (publication).

- **Human URL:** [https://ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0)
- **Base URL:** `https://api.tito.io/v3`

### Tito Tickets API

List, filter (by state, type, release, activity, dates, and free-text `q`), retrieve, create, and update Tickets, reassign a ticket to a different attendee, and void or unvoid tickets.

- **Human URL:** [https://ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0)
- **Base URL:** `https://api.tito.io/v3`

### Tito Registrations API

Manage Registrations — the orders that group one or more tickets. List, filter, retrieve, create, and update registrations, and mark a registration as paid or unpaid via the confirmations endpoint.

- **Human URL:** [https://ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0)
- **Base URL:** `https://api.tito.io/v3`

### Tito Discount Codes API

Create, list, retrieve, update, and delete Discount Codes that apply percentage or fixed discounts to an Event's releases at checkout.

- **Human URL:** [https://ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0)
- **Base URL:** `https://api.tito.io/v3`

### Tito Activities API

Manage Activities — capacity-bound sessions (for example workshops or tracks) that releases can be attached to via `release_ids`. Create, list, retrieve, update, delete, and duplicate activities.

- **Human URL:** [https://ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0)
- **Base URL:** `https://api.tito.io/v3`

### Tito Check-in Lists API

Create, list, retrieve, update, and delete Check-in Lists for an Event. Check-in Lists define which tickets can be checked in and are consumed at the door by Tito's separate Check-in API and mobile/web check-in apps.

- **Human URL:** [https://ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0)
- **Base URL:** `https://api.tito.io/v3`

### Tito Refunds API

List and retrieve Refunds issued against an Event's registrations. A read-only view of refund records.

- **Human URL:** [https://ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0)
- **Base URL:** `https://api.tito.io/v3`

### Tito Webhook Endpoints API

Register, list, retrieve, update, and delete Webhook Endpoints that Tito POSTs event notifications to. Confirmed triggers include `ticket.created`, `ticket.completed`, `ticket.reassigned`, `ticket.updated`, `ticket.unsnoozed`, `ticket.unvoided`, `ticket.voided`, `registration.updated`, `registration.finished`, `registration.completed`, `registration.cancelled`, `checkin.created`, `interested_user.created`, `interested_user.updated`, and `interested_user.deleted`.

- **Human URL:** [https://ti.to/docs/api/admin/3.0](https://ti.to/docs/api/admin/3.0)
- **Base URL:** `https://api.tito.io/v3`

## Common Properties

- [Domain Security](security/tito-domain-security.yml)
- [Authentication](authentication/tito-authentication.yml)
- [GitHub Organization](https://github.com/teamtito)
- [LinkedIn](https://www.linkedin.com/company/usetito)
- [Website](https://ti.to)
- [Documentation](https://ti.to/docs/api)
- [Plans](plans/tito-plans-pricing.yml)
- [Rate Limits](rate-limits/tito-rate-limits.yml)
- [Fin Ops](finops/tito-finops.yml)
- [Blog](https://blog.tito.io/)

## Pricing (summary)

No setup fee, no monthly subscription, no premium-feature surcharge. **Free events are free.** Paid events: **3% per ticket** standard, **2.5%** for approved charity/non-profit/community organizations, with the per-ticket fee **capped at 25 EUR per ticket**. Payment-processing fees (e.g. Stripe) are charged separately by the gateway. See [ti.to/pricing](https://ti.to/pricing). Rates are not reconciled against an invoice; verify current pricing before relying on it.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
