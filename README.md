# Zenserp

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
