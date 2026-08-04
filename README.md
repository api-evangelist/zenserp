# Zenserp

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Zenserp is a Google SERP API that enables developers to fetch live, structured search engine results in real time without interruption. The API supports web, image, video, news, shopping, maps, YouTube, Bing, Yandex, DuckDuckGo, reverse image, and trends search types across 200+ countries, returning clean JSON responses. It offers geolocation-based queries, batch endpoints, keyword search volume and CPC data, and a bulk index checker tool, with a 99.9% uptime SLA on paid plans.

- **Website:** [https://zenserp.com/](https://zenserp.com/)
- **Documentation:** [https://app.zenserp.com/documentation](https://app.zenserp.com/documentation)
- **Pricing:** [https://zenserp.com/pricing-plans/](https://zenserp.com/pricing-plans/)
- **Status Page:** [https://zenserp.freshstatus.io](https://zenserp.freshstatus.io)
- **Blog:** [https://zenserp.com/blog/](https://zenserp.com/blog/)
- **GitHub:** [https://github.com/zenserp](https://github.com/zenserp)
- **LinkedIn:** [https://www.linkedin.com/company/apilayer/](https://www.linkedin.com/company/apilayer/)
- **X:** [https://twitter.com/apilayer](https://twitter.com/apilayer)

## APIs

### Zenserp Search API

Base URL: `https://app.zenserp.com/api/v2`

Supported search endpoints:
- Google Web Search (organic, ads, featured snippets, knowledge graph, related questions)
- Google Image Search
- Google News Search
- Google Shopping Search
- Google Maps / Local Business Search
- YouTube Search
- Reverse Image Search
- Bing Search
- Yandex Search
- DuckDuckGo Search
- Google Trends / Search Popularity
- Batch Search (Medium plan and above)

## Plans

| Plan | Monthly Price | Searches/Month |
|------|--------------|----------------|
| Free | $0 | 50 |
| Small | $49.99 | 25,000 |
| Medium | $149.99 | 100,000 |
| Large | $299.99 | 250,000 |
| Premium | $499.99 | 500,000 |
| Enterprise | $899.99 | 1,000,000 |

A 20% discount applies to all paid plans with annual billing. Only successful responses count against the monthly quota.

## Repository Structure

```
zenserp/
  apis.yml                          # APIs.json 0.19 provider index
  README.md                         # This file
  plans/
    zenserp-plans-pricing.yml       # API Commons Plans 0.1
  rate-limits/
    zenserp-rate-limits.yml         # API Commons Rate Limits 0.1
  finops/
    zenserp-finops.yml              # FinOps Framework 1.0 FOCUS-aligned
```

## Maintainers

- Kin Lane (kin@apievangelist.com)
