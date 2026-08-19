---
name: Consume and verify Lawmatics outbound webhooks
description: Receive Lawmatics event pushes, verify the HMAC-SHA256 signature, deduplicate on event id, and hydrate the referenced record over the REST API.
api: openapi/lawmatics-openapi.yml
operations:
  - getMatter
  - getContact
  - getInvoice
  - getCustomFormEntries
generated: '2026-08-13'
method: generated
source: asyncapi/lawmatics-webhooks.yml + https://help.lawmatics.com/en/articles/15438485-outbound-webhooks
---

# Consume and verify Lawmatics outbound webhooks

Webhooks are **not part of the REST API**. There is no endpoint that creates a subscription — a firm
administrator registers your HTTPS URL in the Lawmatics dashboard under **Settings > Webhooks**, and
the signing secret (`whsec_…`) is shown exactly once at creation. Get it from the administrator
through a secure channel and store it as an environment variable.

## The envelope

```json
{
  "event_id": "evt_550e8400-e29b-41d4-a716-446655440000",
  "firm_id": 123,
  "event_type": "matter.converted",
  "version": "v1",
  "timestamp": "2026-06-02T18:30:00.000Z",
  "data": { "matter_id": 456 }
}
```

Headers: `X-Lawmatics-Signature`, `X-Lawmatics-Timestamp`, `X-Lawmatics-Event-Id`.

## Steps

1. **Verify the signature before parsing anything.** Build the signed payload as
   `"<X-Lawmatics-Timestamp>" + "." + "<raw request body>"` — the raw bytes, not a re-serialized
   object. Compute `HMAC-SHA256(secret, signed_payload)`, hex-encode it, prefix `sha256=`, and
   compare to `X-Lawmatics-Signature` with a **constant-time** comparison.
2. **Reject replays.** Drop anything whose `X-Lawmatics-Timestamp` is more than 5 minutes old.
3. **Deduplicate on `event_id`.** Delivery is at-least-once: Lawmatics retries up to 7 attempts
   (immediate, ~15s, ~1m, ~5m, ~30m, ~1h, ~2h). You will see the same event twice.
4. **Acknowledge fast.** Return any `2xx` within **10 seconds**; the body is ignored. Do the work
   asynchronously. A `4xx` other than `429` is treated as a **permanent** failure and Lawmatics will
   never retry that event.
5. **Hydrate over REST.** The payload carries ids, not records. Fetch the referenced object with
   `getMatter` (`GET /v1/prospects/{prospect_id}?fields=all`), `getContact`, `getInvoice` or
   `getCustomFormEntries` as the event type requires. Note again that `data.matter_id` addresses
   `/v1/prospects/{prospect_id}` — matter and prospect are the same thing.

## Events

`matter.converted`, `matter.created`, `matter.status_changed`, `matter.updated`,
`matter.note_added`, `matter.task_completed`, `form.submitted`, `invoice.created`, `invoice.paid`,
`document.signed`, `contact.updated`, `contact.merged`, `contact.deleted`.

**Check before you depend on any of these.** The Webhooks section inside the published API
documentation says `matter.converted` is currently the only event actually delivered, while the help
centre developer guide lists all thirteen. The two provider documents disagree; see
`asyncapi/lawmatics-webhooks.yml`.

## Limits

- Your endpoint must be HTTPS.
- Two subscriptions per event type per firm (the API docs phrase the same limit as two per endpoint
  per firm).
- Hydration calls count against the firm's shared per-minute REST budget. A burst of events can rate
  limit your own hydration — queue it.
