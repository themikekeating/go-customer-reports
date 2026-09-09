# 06 — Open Decisions (live log)

Reframed around the data engine. When a decision is made, mark **DECIDED**, record date +
choice, and update the affected doc.

| ID | Decision | Recommendation | Status |
|----|----------|----------------|--------|
| D1 | **First algorithm output** — Product Intelligence (A) / Audience Matching (B) / Public Score (C) | **A then B** (internal value, no website needed; C later) | OPEN |
| D2 | **Scope of the engine** — only products you sell, or all products incl. unsold | Start with sold products (rich data); add unsold as a labeled second tier | OPEN |
| D3 | **The product score dimensions** (Output C) — Effectiveness/Value/Quality/Experience/Staying Power | Confirm; Staying Power is the only data-backed one today | OPEN |
| D4 | **Name of the product score** (distinct from operator CEM Score) | "CEM Verdict" or "CEM Product Score" | OPEN |
| D5 | **Content ↔ Product gap** — repurpose beauty content / regenerate for real products / deprioritize | Deprioritize legacy beauty; regenerate around real products later | OPEN |
| D6 | **Unified model location** — SQL views/rollup vs. warehouse (DuckDB/Postgres + dbt) | Lightweight first, warehouse once an output earns it | OPEN |
| D7 | **Cold-start** — scoring products with no transaction history | Two-tier: data-backed vs editorial-only, never mixed silently | OPEN |
| D8 | **Content-creation component** — what it actually is | Need Mike to identify it | OPEN |
| D9 | **Customer dedupe strategy** — identity resolution on verified_leads | Dedupe on email/phone via contact-point graph | OPEN |

## The gating decision

**D1 — what the algorithm outputs first.** Everything sequences off this:

- **A (Product Intelligence)** — the real buyer profile + retention behind each product.
  Pure data work on the confirmed spine. No website. Tells you what's working and to whom.
- **B (Audience Matching)** — propensity-score the 612K leads per product. Directly drives
  revenue (targeted outbound to your own list). Builds on A.
- **C (Public Score)** — the CEM-graded rating on a guide. Needs the theme rebuild AND a
  trustworthy score. Slowest; highest cold-start exposure.

Recommendation: **A → B first** (they monetize the data you already have without building a
site), **C after**. This inverts the original plan, which started with the website.

## Confirmed facts (not decisions — settled by the data)

- Transaction ↔ Customer join works (verified_lead_id → verified_leads.id).
- 56,897 distinct customers behind $938K, with demographics.
- Content is not linked to products (the gap, D5).
