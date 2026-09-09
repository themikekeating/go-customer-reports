# 04 — Unification (the engineering)

This is the actual build: turning 3 separate databases into one queryable model the algorithm
runs on. Identity resolution + a product master + closing the content gap.

## What already joins (confirmed)

| Link | Key | Status |
|------|-----|--------|
| Transaction → Customer | `konnektive_transactions.verified_lead_id = verified_leads.id` | **Works** (77,990 txns, 56,897 customers) |
| Transaction → Product | `konnektive_transactions.product_name` | Works, but messy strings |

## What has to be built

### 1. Product master (normalize the offers)
Products today are raw strings with offer noise: "Citralis - Buy 3, Get 2 (Sub)",
"Citralis - Buy 1 (Sub)" are the *same product* in different offers. Need a `products` table:
- one row per real product (Citralis, Alpha Male Max, …)
- offer variants mapped to it
- so the algorithm aggregates by product, not by offer string.

### 2. Customer identity resolution
`verified_leads` may hold duplicates (same person, multiple rows) — needs dedupe on
email/phone (the `lead_contact_points` graph helps). A clean customer = accurate buyer
profiles and LTV.

### 3. Close the Content ↔ Product gap
The missing link. Options, in order of likely value:
- Link content to the **products you sell** (write/score around Citralis et al.), or
- Treat legacy beauty content as a separate SEO asset not tied to the engine, or
- Regenerate content for the real product catalog (ties to the content-creation component).
Decision: [06 — D5/D8](06-open-decisions.md).

### 4. The unified model — where it lives
Two paths:
- **Lightweight:** SQL views / a materialized rollup table joining the three DBs on this
  local instance. Fast to stand up, good enough to prototype the algorithm.
- **Proper:** a warehouse (DuckDB or Postgres) + dbt models + scheduled refresh. The right
  end-state once an algorithm output is chosen and worth productionizing.
Recommendation: start lightweight to validate Output A/B, graduate to a warehouse when one
output earns it.

## Data-quality blockers to clear

- Encoding corruption in content names.
- Offer-string noise in transactions (handled by the product master).
- Missing indexes on join columns (`verified_lead_id`, `verified_leads.id`) — add before
  large joins or they full-scan.
- Demographic coverage is partial (e.g. age on ~221K of 612K) — the algorithm must handle
  nulls, not assume full enrichment.
