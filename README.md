# DBA.dk Marketplace Listings Scraper

Extract structured classified listings from [DBA.dk](https://www.dba.dk) — Denmark's largest online marketplace with 2M+ monthly visitors. Get prices, condition, GPS coordinates, up to 10 images, seller info, and full descriptions as clean JSON.

**[DBA.dk Marketplace Listings Scraper on Apify →](https://apify.com/blackfalcondata/dba-listings-scraper)**

---

## Key features



**Search with filters** — Search by keyword and location. Filter by category, condition, region, and more.

**Detail enrichment** — Fetch full job descriptions, structured metadata for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

---

## Use cases



**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from dba.dk on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from dba.dk.

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

---

## Related products by Black Falcon Data



- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings

---

*Last updated: 2026-03*
