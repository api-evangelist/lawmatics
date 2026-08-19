---
name: Intake a new lead as a Lawmatics matter
description: Take an inbound lead, deduplicate it against existing contacts, create the matter (called a prospect in the API), and attach the source, practice area and pipeline stage a firm reports on.
api: openapi/lawmatics-openapi.yml
operations:
  - findContactByEmailAddress
  - findContactByPhoneNumber
  - getPracticeAreas
  - getSources
  - getPipelines
  - getStages
  - createMatter
  - getMatter
generated: '2026-08-13'
method: generated
source: openapi/lawmatics-openapi.yml + conventions/lawmatics-conventions.yml
---

# Intake a new lead as a Lawmatics matter

Base URL `https://api.lawmatics.com`. Every request carries
`Authorization: Bearer <access_token>`.

**Read this first: the API calls a Matter a `prospect`.** The endpoint is `/v1/prospects`,
the path parameter is `prospect_id`, and the entity `type` in every response is `prospect`.
Nothing in the product UI or the help centre uses that word. Do not go looking for `/v1/matters`.

## Steps

1. **Deduplicate before you create.** Call `findContactByEmailAddress`
   (`GET /v1/contacts/find_by_email/{email_address}`) and, if you have a phone number,
   `findContactByPhoneNumber` (`GET /v1/contacts/find_by_phone/{phone_number}`).
   There is no idempotency key on this API — a retried `createMatter` creates a second matter,
   so this lookup is the only protection you have against duplicates.
2. **Resolve the reference data the firm reports on** before creating anything, because the
   matter body takes ids, not names: `getPracticeAreas` (`GET /v1/practice_areas`),
   `getSources` (`GET /v1/sources`), `getPipelines` (`GET /v1/pipelines`) and
   `getStages` (`GET /v1/stages`). Cache these — they change rarely and each call spends
   rate-limit budget.
3. **Create the matter** with `createMatter` (`POST /v1/prospects`). Lawmatics deduplicates the
   contact side for you: if the email or phone you pass matches an existing contact, it attaches
   that contact instead of creating a new one (changelog 1.13.1). To create a matter against a
   company, pass either the company id or `company_name`; any contact details you pass are set on
   the company matter's primary contact.
4. **Confirm what was actually stored** with `getMatter` (`GET /v1/prospects/{prospect_id}`) using
   `?fields=all`. Without `fields`, the response returns only a small default attribute set and you
   will not see whether your source, practice area or stage landed.

## Conventions that apply

- **Field selection** — `?fields=` is a comma-separated list, one level deep. An expanded
  relationship returns only `{id, type}`; fetch the related record from its own endpoint if you need
  more. `?fields=all` expands everything and is the way to discover what a record actually carries.
- **Envelope** — `{"data": {"id", "type", "attributes", "relationships"}}`. Ids are strings.
- **Currency** — money attributes are in cents (`actual_value_cents`, `estimated_value_cents`).
- **Rate limit** — per firm, per minute, shared across every app the firm has authorized.
  Lawmatics' API docs say 50/min and its help centre says 150/min; design to 50. On exhaustion you
  get `429` with `Retry-After: 60` and no advance warning — there are no `X-RateLimit-*` headers.
- **Errors** — `{"errors":[{"status","title","detail"}]}`, `application/json`, not RFC 9457.

## Safety

`createMatter` writes into a live legal CRM that drives client-facing automations — creating a matter
can fire intake emails and SMS to a real person. There is no sandbox and no test mode. Confirm with a
human before the first write against a firm's account, and never retry a failed `POST /v1/prospects`
blindly: check with a finder call first.
