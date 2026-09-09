# 03 — The Algorithm (what we compute)

The unified data (Customer ── Transaction ── Product) lets us compute things that are
**measured, not opinion**. The CEM methodology is the layer that grades each output by how
much real evidence backs it. These are the candidate outputs — [06](06-open-decisions.md)
picks which to build first.

## Output A — Product Intelligence (who really buys & keeps it)

For each product, computed from real transactions joined to customer demographics:

- **Buyer profile** — age / state / homeowner / income band / credit band of actual buyers.
- **Retention** — repurchase rate, subscription survival, cancel/refund rate (from
  `billing_cycle` + `transaction_type` + `status` over time).
- **Economics** — revenue per buyer, LTV, average order value.

> Example the data can already answer: *"Citralis is bought and re-bought primarily by
> homeowners 55–70 in [states], income band X, who stay subscribed N cycles."*

This is the raw truth nobody else has. It feeds everything below.

## Output B — Audience Matching (who to sell what to)

Turn Output A into a **propensity model**: score every one of the 612K leads for likelihood
to buy (and retain) each product, based on demographic similarity to proven buyers.

- Input: the demographic signature of each product's real buyers (from A).
- Output: ranked target lists per product → outbound / targeting.
- This is where the 612K base becomes a *revenue weapon*, not a dormant list.

## Output C — The Product Score (public, CEM-graded)

A 1.0–5.0 score per product, rendered on a surface. **Distinct from the canonical operator
CEM Score** (which scores how a human works with AI — locked). This is a parallel,
product-facing instrument. Candidate dimensions, each backed by a data source where one
exists:

| Dimension | Backed by | Evidence strength |
|-----------|-----------|-------------------|
| Effectiveness | editorial + claims | weak (opinion) unless proxied |
| Value | price vs. outcome | medium |
| Quality | composition / build | medium |
| Experience | support / reviews | medium |
| **Staying Power** | **real repurchase/subscription data** | **strong (measured)** |

**CEM evidence-tier principle:** a dimension backed by N real transactions visibly outranks
an editorial estimate. A score that's mostly "strong" evidence means more than a competitor's
five-star guess. That grading IS the methodology applied to products.

## The hard problem — cold start

A product with **no transaction history** (every beauty review; any new product) has no
Staying Power, no buyer profile, no retention. The algorithm's best outputs (A, B, the strong
part of C) only exist where transactions exist. Options:
- Restrict the engine to products you actually sell (where the data is rich), or
- Proxy from external signals for unsold products (weaker, clearly labeled), or
- Two-tier output: "data-backed" vs. "editorial-only" products, never mixed silently.

This is logged as [06 — D7](06-open-decisions.md) and must be resolved before any score is
called universal.
