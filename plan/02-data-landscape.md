# 02 — The Four Buckets + The Join Graph

Deep dive of all local MySQL, 2026-06-21. The point of this doc is not "what data exists" —
it's **how the buckets connect**, because the joins are what make the algorithm possible.

## The join graph (confirmed)

```
   CUSTOMERS                TRANSACTIONS              PRODUCTS            CONTENT
   verified_leads           konnektive_transactions  (from txn stream)   content_reviews
   612,968 rows             77,990 rows / $938K       128 offers          378 reviews
        │                        │     │                   │                  │
        │   id  ◄────────────────┘     │                   │                  │
        │   verified_lead_id           │ product_name ─────┘                  │
        │   (CONFIRMED join,           │                                      │
        │    56,897 buyers)            │                          ??? NO LINK YET ???
        └──────────────────────────────────────────────────────────────────┘
```

**Spine (live):** `Customer ── Transaction ── Product`. This is real and queryable today.
**Gap (to build):** `Product ── Content`. The content is beauty; the products are supplements.
No shared key, and largely no shared subject matter. Closing this is an [04](04-unification.md) task.

## Bucket 1 — Customers (`portal_stealth_local.verified_leads`)

- 611,968 records. ~310K emails; 1.15M-row `lead_contact_points` graph.
- Enrichment: ~221K age, ~220K homeowner, ~153K credit band, plus net worth, marital,
  children, income range, job/industry, full geo (state/city/zip).
- **Join key:** `id` (matched by transactions). Also `uuid`, `external_id` available.

## Bucket 2 — Transactions (`work_hub.konnektive_transactions`)

- $938,623.69 / 77,990 rows / Oct 2023 → Jan 2026 / 128 products / 38 campaigns.
- **All rows carry `verified_lead_id` → 56,897 distinct customers.** This is the spine.
- Columns that matter for the algorithm: `amount_usd`, `transaction_type`, `billing_cycle`
  (subscription signal), `status`, `product_name`, `affid`, `campid`, `transaction_at`.
- Subscription/repurchase behavior is *in here* — the raw material for real retention scoring.

## Bucket 3 — Products (derived from the transaction stream)

- Today products exist only as `product_name` strings + offer variants (e.g. "Citralis -
  Buy 3, Get 2 (Sub)"). There is **no clean product master table** — building one is a
  unification task.
- Real performers: Citralis (~$565K, 3,131+ buyers/offer), Alpha Male Max (~$155K),
  Elite Testo Max (~$63K), Titan Surge (~$40K).

## Bucket 4 — Content (`customerreports_articles`)

- 12,995 articles, 378 reviews (327 Beauty), 38 listicles, 14 categories.
- Quality issues: encoding corruption in names, slug/name mismatches.
- **Not linked to products.** Beauty editorial vs. supplement products = subject mismatch too.
  Decide whether content is repurposed, regenerated for the real products, or deprioritized.

## Cross-DB reality

All three databases live on the same local MySQL instance, so cross-database joins
(`db.table`) work directly. The slow part is missing indexes on the join columns — a unified
model (04) fixes that.

## Other databases (not buckets)

`historical_cem_data` (curated revenue rollups), `santa_funnel` / `quoterocket_db` (empty),
`local_wiki` (small).
