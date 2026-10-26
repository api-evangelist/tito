# Tito (tito)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
