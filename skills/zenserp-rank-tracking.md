---
name: zenserp-rank-tracking
description: Track where a domain ranks for a keyword on Google, in a specific country, language and city, using the Zenserp SERP API.
api: zenserp:zenserp-search-api
operations:
  - listLocations
  - listCountries
  - listLanguages
  - search
  - getStatus
generated: '2026-08-13'
method: generated
source: openapi/zenserp-search-api-openapi.yml, openapi/zenserp-lists-api-openapi.yml, https://app.zenserp.com/documentation
---

# Rank tracking with Zenserp

Find the position of a target domain in Google's organic results for a keyword,
localized to a specific place.

## Before you call anything

Authenticate with the `apikey` **header**, not the query parameter — the query
form leaks the key into logs and browser history.

```
apikey: <key>
```

Base URL for every operation in this skill: `https://app.zenserp.com/api/v2`

## Steps

1. **Resolve the location string — do not invent it.**
   Call `listLocations` (`GET /locations`). Zenserp only accepts canonical
   Google geo-targeting strings, e.g. `New York,New York,United States`. A
   location Google does not publish will silently change your results rather than
   error. If you are only targeting a country, call `listCountries`
   (`GET /gl`) and use a `gl` code instead.

2. **Resolve the interface language.**
   Call `listLanguages` (`GET /hl`) and pick the `hl` value. Language changes the
   SERP, so a rank measured at `hl=en` is not the same measurement as `hl=de`.

3. **Run the search.**
   Call `search` (`GET /search`) with `q`, plus `location` (or `gl`) and `hl`.
   Set `num=100` and page with `start` if the domain may rank below 10 — the
   default page size is 10.

4. **Read the position out of `organic_results`.**
   Each entry has `position`, `title`, `url` and `domain`. Match on `domain`, not
   on a substring of `url`. If your domain is absent from the first 100, call
   again with `start=100`, then `start=200`. **Stop at 300** — Google returns no
   more than 300 results and Zenserp cannot page past it. `number_of_results` in
   the response is Google's corpus estimate; it is not how many you can retrieve.

5. **Check the ads separately if you care about them.**
   `paid_results` is a distinct array. An organic position of 3 with two ads
   above it is a different real-world position.

## Rules

- **A 403 is ambiguous.** It means a wrong key, an exhausted quota, *or* a plan
  that does not entitle the endpoint. Before retrying, call `getStatus`
  (`GET /status`) and read `remaining_requests`. If it is greater than zero, the
  key or the entitlement is the problem and retrying will not fix it.
- **A 404 means "no results found"**, not "no such endpoint". Treat it as an
  empty SERP.
- **A 500 is retryable** with backoff. Zenserp does not charge quota for failed
  requests, so a retry is not billed twice.
- **There are no rate-limit headers.** Nothing in a response tells you how much
  quota is left. Poll `getStatus` on your own schedule; do not expect
  `Retry-After`.
- **Stay under 400 concurrent connections** unless you have arranged a higher
  limit with support.
- Repeat the *same* `location`, `hl` and `gl` on every run or the time series is
  not comparable.
