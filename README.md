# DBA.dk Marketplace Listings Scraper

Extract structured classified listings from [DBA.dk](https://www.dba.dk) — Denmark's largest online marketplace with 2M+ monthly visitors. Get prices, condition, GPS coordinates, up to 10 images, seller info, and full descriptions as clean JSON.

**[Run on Apify →](https://apify.com/blackfalcondata/dba-listings-scraper)**

---

## Key features

🔍 **Search with filters**

Search by keyword across all DBA categories. Filter by condition, region, price range, seller type, and sort order.

📦 **35 structured output fields**

Every listing includes price, condition (normalized), brand, category path, GPS coordinates, up to 10 images, seller type (private/dealer), shipping and buy-now availability, and product attributes.

🔄 **Incremental mode**

Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

⚡ **Compact output for AI agents**

Core-fields-only mode optimized for MCP and AI agent workflows. Description truncation to control output size.

---

## Use cases

**Price monitoring and market research**
Track prices across DBA categories over time. Monitor competitor pricing, identify undervalued items, or analyze market trends for specific product segments in Denmark.

**Inventory and supply sourcing**
Find specific products, parts, or materials across Denmark. Filter by region and price to locate the best deals near you. GPS coordinates enable distance-based filtering in your pipeline.

**Reseller and arbitrage intelligence**
Compare DBA prices against retail or other marketplaces. Identify products selling below market value for resale opportunities. Track sold listings via the `disposed` flag.

**AI-agent and MCP workflows**
Feed compact, structured listing data into ranking, classification, or recommendation pipelines. The 35-field schema with GPS coordinates enables location-aware agent workflows.

**Recurring alerts and monitoring**
Use incremental mode with scheduled runs to get notified about new listings matching your criteria — ideal for rare items, collectibles, or specific product searches.

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

| Product | Description |
|:--------|:------------|
| [Bilbasen Scraper](https://github.com/BlackFalconData-org/bilbasen-scraper) | Denmark's largest car marketplace (same owner as DBA.dk) |
| [StepStone Jobs API](https://github.com/BlackFalconData-org/stepstone-jobs-api) | Job listings from 18 European portals |
| [Company Jobs Tracker](https://github.com/BlackFalconData-org/company-jobs-tracker-api) | Track new/removed jobs per company |
| [Indeed Jobs Feed](https://github.com/BlackFalconData-org/indeed-jobs-feed) | Indeed job listings with salary data |
| [Glassdoor Jobs Feed](https://github.com/BlackFalconData-org/glassdoor-jobs-feed) | Glassdoor listings with company ratings |
| [Arbeitsagentur Jobs Feed](https://github.com/BlackFalconData-org/arbeitsagentur-jobs-feed) | Germany's federal job portal (1M+ listings) |
| [Naukri Jobs Feed](https://github.com/BlackFalconData-org/naukri-jobs-feed) | India's largest job portal |

---

*Last updated: 2026-03*
