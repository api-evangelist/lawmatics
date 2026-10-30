# Lawmatics

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

Lawmatics is a legal CRM, client-intake and marketing-automation platform for law firms, from solo practices to multi-office firms. Its public developer surface is the Lawmatics OAuth API — a REST API of 177 operations across matters (called prospects in the API), contacts, companies, custom intake forms and form entries, custom fields, collections, pipelines, stages, practice areas, marketing sources and campaigns, events, tasks, notes, files, tags, users, time entries, expenses, invoices and transactions — plus a set of signed outbound webhooks. Access is OAuth 2.0 authorization code, gated on a Lawmatics support representative enabling developer settings on the account, and the resulting access token is non-expiring, unscoped and grants full CRUD over the firm.

**Areas:** Legal · CRM · Law Firms · Client Intake · Marketing Automation · Matter Management · E-Signature · Workflow Automation · Legal Tech · Time and Billing · Webhook · Authentication

## Lawmatics on APIs.io

Everything profiled for Lawmatics is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/lawmatics/](https://apis.io/providers/lawmatics/)** — or go straight to one of the APIs or properties below.

### APIs (27)

- [Lawmatics Addresses API](https://apis.io/apis/lawmatics/lawmatics-addresses-api/) — An Address belongs to a Firm, a Contact, or Company.
- [Lawmatics Collections API](https://apis.io/apis/lawmatics/lawmatics-collections-api/) — The Collections API from Lawmatics — 4 operation(s) for collections.
- [Lawmatics Companies API](https://apis.io/apis/lawmatics/lawmatics-companies-api/) — The Companies API from Lawmatics — 5 operation(s) for companies.
- [Lawmatics Contacts API](https://apis.io/apis/lawmatics/lawmatics-contacts-api/) — A Contact can be thought of as a collection of data about a "Person". A Contact record is the base for all Contactables (Matters, Clients, and Companies).…
- [Lawmatics Custom Emails API](https://apis.io/apis/lawmatics/lawmatics-custom-emails-api/) — The Custom Emails API from Lawmatics — 2 operation(s) for custom emails.
- [Lawmatics Custom Fields API](https://apis.io/apis/lawmatics/lawmatics-custom-fields-api/) — The Custom Fields API from Lawmatics — 2 operation(s) for custom fields.
- [Lawmatics Custom Forms API](https://apis.io/apis/lawmatics/lawmatics-custom-forms-api/) — NOTE: Field IDs for fields that are not considered "Standard", such as General fields, and Custom fields, are referred to by special long-form uuids that…
- [Lawmatics Email Addresses API](https://apis.io/apis/lawmatics/lawmatics-email-addresses-api/) — A Email Address is contact information that belongs to a Firm, Contact, or Company.
- [Lawmatics Email Campaign Stats API](https://apis.io/apis/lawmatics/lawmatics-email-campaign-stats-api/) — The Email Campaign Stats API from Lawmatics — 1 operation(s) for email campaign stats.
- [Lawmatics Email Campaigns API](https://apis.io/apis/lawmatics/lawmatics-email-campaigns-api/) — The Email Campaigns API from Lawmatics — 2 operation(s) for email campaigns.
- [Lawmatics Event Locations API](https://apis.io/apis/lawmatics/lawmatics-event-locations-api/) — These are Firm related Locations (for events) that can be configured in Firm settings.
- [Lawmatics Event Types API](https://apis.io/apis/lawmatics/lawmatics-event-types-api/) — Event Types define Event defaults, and can trigger automations, for common types of Events created in Lawmatics. Configuring Calendar Availability defaults…
- [Lawmatics Events (Appointments) API](https://apis.io/apis/lawmatics/lawmatics-events-appointments-api/) — Events are also referred to in the app as "Appointments"
- [Lawmatics Files API](https://apis.io/apis/lawmatics/lawmatics-files-api/) — The Files API from Lawmatics — 3 operation(s) for files.
- [Lawmatics Folders API](https://apis.io/apis/lawmatics/lawmatics-folders-api/) — The Folders API from Lawmatics — 2 operation(s) for folders.
- [Lawmatics Matters (Prospects) API](https://apis.io/apis/lawmatics/lawmatics-matters-prospects-api/) — A Matter is a legal case, and the primary object in Lawmatics. NOTE: You may see Matters referenced as "Prospects" or "PNCs". This is for legacy reasons,…
- [Lawmatics Notes API](https://apis.io/apis/lawmatics/lawmatics-notes-api/) — The Notes API from Lawmatics — 2 operation(s) for notes.
- [Lawmatics Payment Expenses API](https://apis.io/apis/lawmatics/lawmatics-payment-expenses-api/) — The Payment Expenses API from Lawmatics — 2 operation(s) for payment expenses.
- [Lawmatics Payment Invoices API](https://apis.io/apis/lawmatics/lawmatics-payment-invoices-api/) — The Payment Invoices API from Lawmatics — 2 operation(s) for payment invoices.
- [Lawmatics Payment Time Entries API](https://apis.io/apis/lawmatics/lawmatics-payment-time-entries-api/) — The Payment Time Entries API from Lawmatics — 2 operation(s) for payment time entries.
- [Lawmatics Payment Transactions API](https://apis.io/apis/lawmatics/lawmatics-payment-transactions-api/) — The Payment Transactions API from Lawmatics — 2 operation(s) for payment transactions.
- [Lawmatics Phone Numbers API](https://apis.io/apis/lawmatics/lawmatics-phone-numbers-api/) — A Phone Number is contact information that belongs to a Firm, Contact, or Company.
- [Lawmatics Tags API](https://apis.io/apis/lawmatics/lawmatics-tags-api/) — The Tags API from Lawmatics — 4 operation(s) for tags.
- [Lawmatics Task Statuses API](https://apis.io/apis/lawmatics/lawmatics-task-statuses-api/) — The Task Statuses API from Lawmatics — 2 operation(s) for task statuses.
- [Lawmatics Tasks API](https://apis.io/apis/lawmatics/lawmatics-tasks-api/) — The Tasks API from Lawmatics — 6 operation(s) for tasks.
- [Lawmatics Timeline Activities API](https://apis.io/apis/lawmatics/lawmatics-timeline-activities-api/) — The Timeline Activities API from Lawmatics — 2 operation(s) for timeline activities.
- [Lawmatics Users API](https://apis.io/apis/lawmatics/lawmatics-users-api/) — The Users API from Lawmatics — 3 operation(s) for users.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Lawmatics Webhooks](https://apis.io/asyncapis/lawmatics/lawmatics-webhooks/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Lawmatics Agentic Access](https://apis.io/agentic-access/lawmatics/lawmatics-agentic-access/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Lawmatics Context](https://apis.io/jsonld/lawmatics/lawmatics-context/)

#### Collections (1)

Postman and Open Collection request collections.

- [Lawmatics OAuth API v1.22.0](https://apis.io/collections/lawmatics/postman-lawmatics-oauth-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Lawmatics Openapi Overlay](https://apis.io/overlays/lawmatics/lawmatics-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Lawmatics Authentication](https://apis.io/security/lawmatics/lawmatics-authentication/)
- [Lawmatics Domain Security](https://apis.io/security/lawmatics/lawmatics-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Lawmatics Scopes](https://apis.io/scopes/lawmatics/lawmatics-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Lawmatics Plans Pricing](https://apis.io/plans/lawmatics/lawmatics-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Lawmatics Rate Limits](https://apis.io/rate-limits/lawmatics/lawmatics-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Lawmatics Finops](https://apis.io/finops/lawmatics/lawmatics-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.lawmatics.com/)
- [Documentation](https://docs.lawmatics.com/)
- [Getting started](https://help.lawmatics.com/en/articles/10699983-lawmatics-open-api)
- [API reference](https://docs.lawmatics.com/)
- [Pricing](https://www.lawmatics.com/pricing)
- [Support](https://help.lawmatics.com/)
- [Blog](https://www.lawmatics.com/blog)
- [Compliance](https://www.lawmatics.com/security)
- [Terms of service](https://www.lawmatics.com/terms-of-use)
- [Privacy policy](https://www.lawmatics.com/privacy-policy)
- [GitHub](https://github.com/boost-legal)
- [Status](https://status.lawmatics.com/)

## API Evangelist rating

**Kin Score 54.4** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 66.1 |
| Contract quality | 32.5 |
| Contract governance | 18.2 |
| Operational transparency | 55.3 |
| Developer ergonomics | 53.7 |
| Access clarity | 77.6 |

**Agent readiness 40.2** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | negotiable (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | documented (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | mostly |

**Regulatory alignment 39.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/lawmatics/](https://apis.io/providers/lawmatics/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Lawmatics: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/lawmatics/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
