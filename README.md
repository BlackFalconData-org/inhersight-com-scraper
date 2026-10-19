# InHerSight Scraper [Just 💰$0.9]

Extract structured data from [inhersight.com](https://inhersight.com) — InHerSight company ratings and employee reviews for women in the workplace. Get overall scores, rating breakdowns and full review text per company from company URLs, search terms or the Best Companies to Work For list.

**[InHerSight Scraper [Just 💰$0.9] on Apify →](https://apify.com/blackfalcondata/inhersight-com-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword. Filter by 📝 description format, and more.

**Detail enrichment** — Fetch structured metadata for each job.

**Incremental mode** — Only get new or changed jobs since your last run. Content hash per job — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how jobs evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N jobs (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every job returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured jobs from inhersight.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor jobs, track trends, and analyze market dynamics with structured, deduplicated data from inhersight.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per job is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "bestCompaniesList": true,
  "includeReviews": true,
  "maxReviewsPerCompany": 25,
  "maxResults": 10,
  "includeDetails": true,
  "descriptionMaxLength": 0,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "emitUnchanged": false,
  "emitExpired": false,
  "skipReposts": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all"
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Company name or keyword to look up (e.g. "Percepta"); each term returns up to 5 matching companies, which is the most the site's search gives back. Use a JSON array for several terms, e.g. ["Percepta","Deloitte"]. Leave empty to use Start URLs or the best-companies list. |
| `maxResults` | integer | `100` | Maximum number of companies to return (0 = unlimited). Each company's reviews come on top. The best-companies list has 50 companies and a search term returns at most 5. |
| `startUrls` | array | `[]` | Paste company page URLs from inhersight.com (e.g. https://www.inhersight.com/company/percepta/ratings). Each URL becomes its own company; results are merged and deduped. When provided, Start URLs REPLACE the search terms and the best-companies list (unsupported URLs are skipped, and if none is supported the run stops with an input error). |
| `bestCompaniesList` | boolean | — | Return the ranked "Best Companies to Work For" list (top 50 companies for women, with rank and list name). Combine with search terms to add more companies; ignored when Start URLs are given. |
| `includeDetails` | boolean | `true` | Fetch each company's full profile, rating breakdown and employee reviews (one extra record per review). Turn off for the list/search data only, with no further requests. |
| `includeRatingBreakdown` | boolean | `true` | Add the per-category ratings (Women in Leadership, Equal Opportunities, Pay and more) and category groups to each company. Needs Include Company Details. |
| `includeReviews` | boolean | `true` | Emit each company's employee reviews as separate records (recordType "review"). Needs Include Company Details. |
| `maxReviewsPerCompany` | integer | `25` | Stop after this many reviews per company (0 = all reviews). Default 25: a first run stays quick; raise it or set 0 for full review histories. |
| `minRating` | number | `0` | Only return companies with an overall score of at least this (0-5, 0 = no filter). Companies without a score are kept. |
| `descriptionMaxLength` | integer | `0` | Truncate each review text to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null / empty-string / empty-array fields (and fully-null nested objects like socialProfiles) from each output record. Off by default to preserve dataset schema compatibility; turn on to slim output for LLM / agent consumption. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from search inputs (company names, startUrls) so different company sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `emitUnchanged` | boolean | `false` | Also emit records that have not changed since the last run (incrementalMode only). |
| `emitExpired` | boolean | `false` | Also emit records that have disappeared since the last run (incrementalMode only). |
| `skipReposts` | boolean | `false` | When incremental, skip records whose content matches a record that disappeared in a prior run (cross-run repost detection). |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED records. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of records included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |

---

## Output fields

Every job returns the same 59-field schema. Missing values are `null` — never omitted.

- `recordType`
- `listingId`
- `companyId`
- `companyUuid`
- `name`
- `slug`
- `profileUrl`
- `portalUrl`
- `score`
- `ratingCount`
- `participantCount`
- `reviewCount`
- `topCompany`
- `underReview`
- `industry`
- `industryGroup`
- `companyType`
- `headquarters`
- `otherLocations`
- `employeeCount`
- `companySize`
- `websiteUrl`
- `logoUrl`
- `briefOverview`
- `jobsUrl`
- `hasIndeedJobs`
- `sourceType`
- `sourceList`
- `listRank`
- `scoreTrend`
- `ratingBreakdown`
- `ratingGroups`
- `reviewId`
- `text`
- `descriptionMarkdown`
- `satisfactionScore`
- `satisfactionLabel`
- `jobLevel`
- `jobLevelLabel`
- `featured`
- `replyCount`
- `createdAt`
- `companyName`
- `companySlug`
- `companyProfileUrl`
- `extractedEmails`
- `extractedPhones`
- `extractedUrls`
- `socialProfiles`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `scrapedAt`
- `source`
- `contentHash`
- `changeType`
- `isRepost`
- `repostOfId`
- `repostDetectedAt`

---

## Sample output

One object per job. Here is a real example from a production run:

```json
{
  "recordType": "company",
  "listingId": "27ccd36b1266192c9ba7d53bde1178f6b771938474bc5bef9ea6f984eca53c66",
  "companyId": 26065,
  "companyUuid": "a602c8d8-36a8-4dc8-8183-34935b2a3351",
  "name": "Percepta",
  "slug": "percepta",
  "profileUrl": "https://www.inhersight.com/company/percepta/ratings",
  "portalUrl": "https://www.inhersight.com/company/percepta/ratings",
  "score": 4.8,
  "ratingCount": 847,
  "participantCount": 52,
  "reviewCount": null
}
```

*Truncated — full records contain 59 fields. See Output fields for the complete schema.*

**[Try InHerSight Scraper [Just 💰$0.9] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/inhersight-com-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.009 |
| Result | $0.0009 |

See the [actor on Apify](https://apify.com/blackfalcondata/inhersight-com-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape inhersight.com?**
Use this actor on Apify to extract structured data from inhersight.com. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get inhersight.com data as JSON, CSV, or Excel?**
The actor writes each job to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape inhersight.com?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check inhersight.com's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each job gets a content hash. On subsequent runs, only new or changed jobs are emitted — saving time, compute, and storage. Expired jobs can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

- [Djinni Scraper](https://apify.com/blackfalcondata/djinni-scraper?fpr=1h3gvi) — Ukraine & CEE tech jobs with salary and English level
- [Work.ua Scraper](https://apify.com/blackfalcondata/work-ua-scraper?fpr=1h3gvi) — Ukraine's work.ua job listings
- [NoFluffJobs Scraper](https://apify.com/blackfalcondata/nofluffjobs-scraper?fpr=1h3gvi) — Poland & CEE IT jobs with transparent salary ranges
- [OLX Jobs Scraper](https://apify.com/blackfalcondata/olx-jobs-scraper?fpr=1h3gvi) — OLX job listings across 7 CEE countries
- [Prace.cz Scraper](https://apify.com/blackfalcondata/prace-scraper?fpr=1h3gvi) — Czech Republic's prace.cz job board
- [Profession.hu Scraper](https://apify.com/blackfalcondata/profession-scraper?fpr=1h3gvi) — Hungary's profession.hu job board

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [InHerSight Scraper [Just 💰$0.9]](https://apify.com/blackfalcondata/inhersight-com-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
