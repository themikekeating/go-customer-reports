# CEM Data Engine — Plan

**What this is:** a system that **unifies 4 buckets of first-party data** and runs the CEM
methodology as an **algorithm** on top of the unified set. The output is product + customer
intelligence. Any website (a buyer's guide, etc.) is just a *surface* that renders the
engine's output — it is **not** the project.

**Repo:** `go-customer-reports` (host for the rebuild; the old "Customer Reports" brand is dead)
**Last updated:** 2026-06-21
**Status:** Data joins confirmed. Algorithm output priority not yet chosen.

---

## The one fact everything rests on (confirmed 2026-06-21)

The buckets **physically join**:

```
CUSTOMER ──< TRANSACTION >── PRODUCT ──(gap)── CONTENT
612,968       77,990          offers           13k articles
leads         txns / $938K    (Citralis…)      378 reviews
(demographics)
```

- `konnektive_transactions.verified_lead_id` → `verified_leads.id` — **confirmed**, all 77,990
  txns linked, **56,897 distinct customers**, demographics attach (age/state/homeowner/income/credit).
- Products live in the transaction stream (`product_name`) with real buyer counts.
- **Content ↔ Product is the only missing link** — the gap to engineer.

This means: every dollar of revenue is tied to a real person with a full demographic profile.
That is the asset. The algorithm exploits it.

---

## The plan documents

| # | Doc | Covers | Status |
|---|-----|--------|--------|
| 01 | [What we're building](01-concept.md) | The data-engine thesis (not a website) | Defined |
| 02 | [The four buckets](02-data-landscape.md) | The buckets + the confirmed join graph | Mapped |
| 03 | [The algorithm](03-the-algorithm.md) | What we compute from the unified data | Candidates |
| 04 | [Unification](04-unification.md) | Identity resolution, keys, gaps, the unified model | Engineering |
| 05 | [Surfaces](05-surfaces.md) | Outputs that consume the engine (incl. the guide) | Outline |
| 06 | [Open decisions](06-open-decisions.md) | Everything unresolved, with recommendations | Live log |

---

## The decision that gates everything

**What does the algorithm output *first*?** (see [06](06-open-decisions.md))
1. **Product intelligence** — the real buyer profile + retention behind each product.
2. **Audience matching** — score the 612K leads for who-buys-what (targeting).
3. **Public product score** — the CEM-graded rating, rendered on a guide.

These reuse the same unified data but build in different orders. Pick one to lead.
