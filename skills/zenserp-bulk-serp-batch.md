---
name: zenserp-bulk-serp-batch
description: Fetch thousands of SERPs asynchronously with the Zenserp batch endpoint and receive the results on a webhook.
api: zenserp:zenserp-batch-api
operations:
  - submitBatch
  - listBatches
  - getBatch
  - getStatus
generated: '2026-08-13'
method: generated
source: openapi/zenserp-batch-api-openapi.yml, https://app.zenserp.com/documentation#batches
---

# Bulk SERP collection with Zenserp batches

For datasets too large to fetch synchronously. You submit jobs, Zenserp works
through them, and it POSTs the results to a URL you own.

## Prerequisites

- **A Medium plan or above.** The batch endpoint is not available on Free or
  Small. An unentitled call returns 403 — the same status as a bad key.
- **A different base URL from the rest of the API.** Batches live under
  `https://app.zenserp.com/api/v1`, not `/api/v2`. This trips people up: the
  search endpoint is v2, the batch endpoint is v1, and both are current.

## Steps

1. **Check your quota first.** Call `getStatus`
   (`GET https://app.zenserp.com/api/v2/status`). A batch of 5,000 jobs against
   3,000 remaining searches will not fail loudly at submission time.

2. **Stand up the receiver before you submit.** Zenserp will POST to
   `webhook_url` when the batch completes. Use an unguessable path — deliveries
   carry **no signature, no HMAC, no shared secret and no timestamp**, so an
   unguessable URL plus job-id matching is the only verification available to you.

3. **Submit the batch.** Call `submitBatch` (`POST /batches`):

   ```json
   {
     "webhook_url": "https://your-host.example/zenserp/<unguessable>",
     "name": "nightly-rank-check",
     "jobs": [
       { "type": "search", "custom_id": "acme-widgets-nyc",
         "q": "widgets", "location": "New York,New York,United States", "hl": "en" },
       { "type": "search", "custom_id": "acme-widgets-uk",
         "q": "widgets", "gl": "GB", "hl": "en" }
     ]
   }
   ```

   - `jobs` is required. `webhook_url` and `name` are optional but you want both.
   - `jobs[].type` is one of `search`, `shopping`, `trends`. It defaults to
     `search`.
   - Set `custom_id` on **every** job. It is the only caller-controlled
     correlation handle in the API — it comes back inside the `request` object of
     the response. Without it you are matching results to inputs by query string.

4. **Receive the results.** The webhook body is an array of responses shaped like
   the corresponding synchronous API, each with an added `job_id`. Acknowledge
   with a 2xx and process asynchronously.

5. **Poll only as a fallback.** `getBatch` (`GET /batches/{id}`) returns the
   batch status and any available results. Zenserp explicitly recommends the
   webhook over polling. Use `listBatches` (`GET /batches`) to enumerate what you
   have submitted.

## Rules

- **Submission is not idempotent.** There is no idempotency key. If you retry a
  submission because the connection dropped, you may create a second batch and
  pay for the same work twice. Record the batch id from the response before you
  retry anything, and check `listBatches` first.
- **Retry and delivery guarantees for the webhook are undocumented.** Assume
  nothing about redelivery. If your receiver was down, fall back to
  `getBatch`.
- **Only successful responses consume quota.** Failed and invalid jobs do not.
- **403 on submit is more likely a plan problem than a key problem** on this
  endpoint. Confirm with `getStatus` before you go looking for a credential bug.
