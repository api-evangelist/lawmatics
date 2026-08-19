---
name: Push a website form submission into Lawmatics
description: Send a firm's own website form straight into a Lawmatics custom form using the one unauthenticated endpoint on the API, then read back the resulting entries.
api: openapi/lawmatics-openapi.yml
operations:
  - getCustomForms
  - getCustomForm
  - submitCustomFormEntryFormDataBody
  - getCustomFormEntries
generated: '2026-08-13'
method: generated
source: openapi/lawmatics-openapi.yml + https://help.lawmatics.com/en/articles/10699870-connecting-your-webform-to-lawmatics-via-api
---

# Push a website form submission into Lawmatics

Base URL `https://api.lawmatics.com`.

This is the only flow on the Lawmatics API that needs **no** access token and no developer app. The
form UUID is the whole credential.

## Steps

1. **Create a matching custom form in Lawmatics first.** The form must exist, be of the Matter type,
   and carry fields corresponding to what your website form collects. Its field ids are the keys you
   will post.
2. **Get the form UUID and the field ids.** Either from the app — the "Form API Details" button on
   the form, at `https://app.lawmatics.com/custom-forms/:custom_form_id/api-details` — or from the
   API with `getCustomForms` (`GET /v1/forms`) and `getCustomForm`
   (`GET /v1/forms/{custom_form_uuid}?fields=all`). Both of those reads DO require a bearer token.
3. **Submit.** `submitCustomFormEntryFormDataBody`
   (`POST /v1/forms/{custom_form_uuid}/submit`), unauthenticated. The body is either
   `multipart/form-data` (so a plain HTML5 form can post directly) or JSON. Keys are the custom
   form field ids from step 2.
4. **Verify** with `getCustomFormEntries` (`GET /v1/forms/{custom_form_uuid}/entries?fields=all`).

## What happens downstream

A submission registers as a form entry, creates or matches a matter, and fires whatever automations
the firm has attached to that form — intake emails, SMS, task assignment. Submitting is a real
side-effecting action against a live firm's clients, not a test write.

## Security notes

- The submit endpoint is public. Anyone holding the form UUID can post to it, so treat the UUID as
  semi-secret and expect unsolicited traffic once it is embedded in a public page. Put your own bot
  protection in front of it.
- There is no idempotency key. A double-submitted form creates two entries; deduplicate on your side
  before posting.
- Rate limiting is per firm across all endpoints, so a burst of form traffic consumes the same budget
  as the firm's other integrations.
- The alternative to this flow is the Lawmatics-generated embed snippet, which hosts the form for
  you. See `components/lawmatics-components.yml`.
