---
name: Query and report on Lawmatics matters
description: Use the Lawmatics filter, sort, pagination and field-selection grammar correctly to pull matter, contact and activity data for a report without burning the per-firm rate limit.
api: openapi/lawmatics-openapi.yml
operations:
  - getMatters
  - getContacts
  - getActivities
  - getPracticeAreas
  - getStages
  - getUsers
generated: '2026-08-13'
method: generated
source: openapi/lawmatics-openapi.yml + conventions/lawmatics-conventions.yml
---

# Query and report on Lawmatics matters

Base URL `https://api.lawmatics.com`, `Authorization: Bearer <access_token>`.

Lawmatics has one query grammar and it applies to every list endpoint. Learn it once.

## The grammar

| Concern | Parameters | Notes |
|---|---|---|
| Field selection | `fields` | Comma-separated, one level deep. `fields=all` expands everything. Order is preserved. |
| Pagination | `page` | 1-based. Page size is not settable. Metadata sits at the bottom of the list response. |
| Sorting | `sort_by`, `sort_order` | `asc`/`desc`. `id`, `created_at`, `updated_at` always sort; so do most `fields=all` fields. `sort_order` alone defaults to `id`. |
| Filtering | `filter_by`, `filter_on`, `filter_with` | Aliases: `filter_field`, `filter_value`, `filter_operator`. |

Operators for `filter_with`: `=`, `!=`, `<=`, `<`, `>=`, `>`, `like`, `ilike`, `null`, `not_null`
(aliases `empty`, `present`, `blank`). Default is `=`, and `ilike` for string fields.

## Steps

1. **Pick the filter field.** Association fields need the `_id` suffix — `practice_area_id`,
   `stage_id`, `source_id`. Currency fields filter in cents. You do NOT have to select a field with
   `fields` in order to filter on it.
2. **Run the query.** `getMatters` (`GET /v1/prospects`) is the workhorse — the spec carries the
   provider's own worked filter examples on it (filter by practice area, by actual value in cents,
   by status). `getContacts` and `getActivities` take the same parameters.
3. **Page through.** Increment `page` until the returned list is short. Sort by `id asc` while
   paging so new records created during the walk do not shift the window under you.
4. **Resolve relationship ids.** Expanded relationships return `{id, type}` only. Batch-fetch the
   lookup tables once (`getPracticeAreas`, `getStages`, `getUsers`) and join locally rather than
   calling the related endpoint per row — per-row lookups are what exhaust the rate limit.

## Traps

- **One filter per request.** There is no AND/OR. Two conditions means two calls and a local
  intersection.
- **`filter_by` without `filter_on` returns 422**, `"Filter By Parameter Not Available"` — except for
  the presence operators `null` / `not_null`, which take no value.
- **Fuzzy matching needs your own `%`.** `like`/`ilike` do not add wildcards; you place them, and
  `%` must be URL-encoded as `%25`.
- **Rate limit is per firm, not per token.** Every app the firm authorized shares the budget.
  429 arrives with `Retry-After: 60` and no advance signal. Sleep, do not tighten the loop.
- **Default sort is `id` descending**, so an unsorted page 1 is the newest records.

## Read-only by construction

Every operation in this skill is a `GET`. Reporting should never need a write; if a flow appears to,
stop and confirm with a human — this API has no scopes, so the token you hold can also delete.
