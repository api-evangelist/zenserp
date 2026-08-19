---
name: zenserp-ad-verification
description: Verify whether a Google Ad is actually being served for a keyword in a specific city, using the Zenserp SERP API.
api: zenserp:zenserp-search-api
operations:
  - listLocations
  - search
  - getStatus
generated: '2026-08-13'
method: generated
source: openapi/zenserp-search-api-openapi.yml, openapi/zenserp-lists-api-openapi.yml, https://app.zenserp.com/documentation#adVerification
---

# Ad verification with Zenserp

Check whether a specific advertisement is being delivered for a query, as seen
from a particular place. This is the workflow Zenserp documents under "Ad
verification".

## Steps

1. **Get an exact location string.** Call `listLocations` (`GET /locations` on
   `https://app.zenserp.com/api/v2`). Zenserp's own guidance: "To obtain accurate
   results, it is very important that we specify a location that is provided by
   google." A near-miss location string does not error — it quietly returns a
   SERP for somewhere else, which is the failure mode that makes ad-verification
   results wrong without looking wrong.

2. **Run the search from that location.** Call `search` (`GET /search`) with `q`
   and the canonical `location`, e.g.
   `q=Iphone 12&location=New York,New York,United States`.

3. **Read `paid_results`, not `organic_results`.** Ads live in `paid_results`,
   each with `position`, `title`, `url`, `domain`, `description` and
   `displayed_url`. Match the advertiser on `domain` or `displayed_url`.

4. **An empty `paid_results` is a real answer.** It means no ads were served for
   that query from that location at that moment — not that the call failed.
   Google ad delivery is probabilistic and budget-paced, so a single miss is not
   proof of absence. Sample repeatedly over time before concluding anything.

## Rules

- **Every check is a live scrape.** There is no cached mode, no sandbox and no
  fixture data. Each call costs one search from the plan quota and takes roughly
  5–7 seconds.
- **403** = wrong key, exhausted quota, or unentitled plan. Disambiguate with
  `getStatus` (`GET /status`) → `remaining_requests`.
- **404** = no results found, not a routing error.
- **500** = retry with backoff; failed requests do not consume quota.
- Pin `location`, `hl`, `gl` and `device` across a measurement series, or the
  runs are not comparable to each other.
- For a whole portfolio of keyword × location pairs, do not loop this skill —
  use `zenserp-bulk-serp-batch` instead and let the batch endpoint do the fan-out.
