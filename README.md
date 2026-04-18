# DBA.dk Marketplace Listings Scraper

Extract structured classified listings from [DBA.dk](https://www.dba.dk) — Denmark's largest online marketplace with 2M+ monthly visitors. Get prices, condition, GPS coordinates, up to 10 images, seller info, and full descriptions as clean JSON.

**[DBA Scraper - Denmark’s Largest Marketplace on Apify →](https://apify.com/blackfalcondata/dba-listings-scraper?fpr=1h3gvi)**

---

## Key features





**Search with filters** — Search by keyword and location. Filter by category, condition, region, and more.

**Detail enrichment** — Fetch full job descriptions, structured metadata for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 5.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases





**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from dba.dk on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from dba.dk.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "iPhone",
  "region": "copenhagen",
  "maxResults": 20,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Search keywords (e.g. "iPhone", "sofa", "cykel"). |
| `category` | enum | `"all"` | Filter by DBA category (11 categories). |
| `condition` | enum | `"all"` | Item condition: new, as new, good, worn, needs repair. |
| `region` | enum | `"all"` | Danish region (10 regions from København to Bornholm). |
| `priceMin` | integer | `0` | Minimum price in DKK. |
| `priceMax` | integer | `0` | Maximum price in DKK. 0 = no limit. |
| `sellerType` | enum | `""` | Seller type: private or dealer. |
| `sortBy` | enum | `"relevance"` | Sort: relevance, newest, oldest, price asc/desc, closest. |
| `maxResults` | integer | `50` | Maximum results to return. 0 = unlimited. |
| `includeDetails` | boolean | `true` | Fetch full descriptions, images, category paths, and attributes. |
| `descriptionMaxLength` | integer | `0` | Truncate description to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `incrementalMode` | boolean | `false` | Only return new/changed listings compared to previous run. |
| `stateKey` | string | — | Stable identifier for tracked listing universe. |

---

## FAQ

**Does it support all DBA categories?**
Yes — 11 categories including Møbler, Elektronik, Sport, Forældre & børn, Mode, Have, Dyr, Kunst, Erhverv, Underholdning, and Bil/båd/MC.

**Can I filter by region?**
Yes — 10 Danish regions are supported: København, Nordsjælland, Vestsjælland, Sydsjælland, Nordjylland, Østjylland, Midt- og Vestjylland, Syd- og Sønderjylland, Fyn, and Bornholm.

**Does it handle free items ("Gives væk")?**
Yes. Free items have `price: 0` and `tradeType: "Gives væk"`.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

**Is it legal to scrape DBA.dk?**
This actor accesses publicly available data. Always check the target site's terms of service for your specific use case.

---

## Known limitations

- Seller profile details (member since, rating, response time) require login and are not available.
- Contact information (phone, email) is not available — sellers use DBA's built-in messaging system.
- Condition, description, and category fields require `includeDetails: true` (slower but more complete).
- Promoted listings may appear in results regardless of filter settings.


## Output fields

Every listing returns the same 35-field schema. Missing values are `null` — never omitted.

- `listingId`
- `title`
- `description`
- `price`
- `currency`
- `condition`
- `conditionDetails`
- `brand`
- `model`
- `category`
- `categoryPath`
- `location`
- `zipCode`
- `latitude`
- `longitude`
- `imageUrl`
- `imageUrls`
- `imageCount`
- `sellerName`
- `sellerType`
- `tradeType`
- `postedAt`
- `editedAt`
- `url`
- `portalUrl`
- `sellerId`
- `isPromoted`
- `shippingAvailable`
- `freeShipping`
- `buyNowAvailable`
- `disposed`
- `isWebstore`
- `attributes`
- `scrapedAt`
- `source`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "listingId": "dc82461422eb6937e0d5d4a43445542ca004166fc675ad1eea2c7fefd83c9acf",
  "title": "Apple iPhone X Smartphone 256 GB Space Grey",
  "description": "Apple iPhone X smartphone med 256 GB lagerplads i Space Grey farve. Telefonen leveres i original emballage. Velegnet til daglig brug og opbevaring af større mængder data. Oplader o…",
  "price": 950,
  "currency": "DKK",
  "condition": "good",
  "conditionDetails": "Brugt - men i god stand",
  "brand": "Apple",
  "model": "iPhone 2G-11",
  "category": "Mobiltelefoner",
  "categoryPath": "Elektronik og hvidevarer > Telefoner og telefontilbehør > Mobiltelefoner",
  "location": "8600 Silkeborg"
}
```

*Truncated — full records contain 35 fields. See Output fields for the complete schema.*


**[Try DBA Scraper - Denmark’s Largest Marketplace now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/dba-listings-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.002 |

See the [actor on Apify](https://apify.com/blackfalcondata/dba-listings-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data





- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal


## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---
---

*Last updated: 2026-03*
