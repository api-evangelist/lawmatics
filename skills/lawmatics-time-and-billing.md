---
name: Record time, expenses and read billing on a Lawmatics matter
description: Log billable time and expenses against a matter and read back invoices and transactions, using the Time and Billing surface added to the API in versions 1.20 and 1.21.
api: openapi/lawmatics-openapi.yml
operations:
  - getMatter
  - getUsers
  - createTimeEntry
  - getTimeEntries
  - updateTimeEntry
  - createExpense
  - getExpenses
  - getInvoices
  - getInvoice
  - getTransactions
generated: '2026-08-13'
method: generated
source: openapi/lawmatics-openapi.yml + conventions/lawmatics-conventions.yml
---

# Record time, expenses and read billing on a Lawmatics matter

Base URL `https://api.lawmatics.com`, `Authorization: Bearer <access_token>`.

Time and Billing is a paid add-on in Lawmatics, so these endpoints only return data for firms that
have it. Expect empty lists rather than a distinct error if the firm does not.

## Steps

1. **Resolve the matter and the timekeeper.** `getMatter`
   (`GET /v1/prospects/{prospect_id}?fields=all`) and `getUsers` (`GET /v1/users`). Remember that a
   Matter is a `prospect` in every path and payload.
2. **Log time** with `createTimeEntry` (`POST /v1/time_entries`). Read it back with
   `getTimeEntries` (`GET /v1/time_entries?fields=all`) — the default field set is small, so use
   `fields=all` to see what actually stored. Correct with `updateTimeEntry`
   (`PUT /v1/time_entries/{time_entry_id}`).
3. **Log expenses** with `createExpense` (`POST /v1/expenses`), read with
   `getExpenses` (`GET /v1/expenses?fields=all`).
4. **Read billing outcomes.** `getInvoices` (`GET /v1/invoices`), `getInvoice`
   (`GET /v1/invoices/{invoice_id}`) and `getTransactions` (`GET /v1/transactions?fields=all`).

## Money and money-shaped traps

- **Everything monetary is in cents.** Filtering on currency fields uses cents too — a filter for
  matters over $2,500 is `filter_by=actual_value_cents&filter_on=250000&filter_with=>`.
- **Invoices are read-only over the API.** There is `GET /v1/invoices` and `GET /v1/invoices/{id}`,
  and no create, update or delete. Transactions support `GET` and `POST` only.
- **There is no idempotency key.** A retried `createTimeEntry` or `createExpense` writes a second
  billable line onto a client's matter. Before any retry, list back with a filter on the matter and
  check whether the entry landed. This is the failure mode with actual money attached.
- **No sandbox exists.** Every write in this skill lands in the firm's live billing data.

## Errors and limits

- `429` with `Retry-After: 60` on the shared per-firm budget; no `X-RateLimit-*` headers.
- Errors come back as `{"errors":[{"status","title","detail"}]}` — not RFC 9457.
- `filter_by` without `filter_on` returns `422 Filter By Parameter Not Available`.
