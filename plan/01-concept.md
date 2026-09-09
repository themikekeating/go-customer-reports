# 01 — What We're Building

## Not a website. A data engine.

The earlier framing (rebuild a content site, bolt on a score) was wrong. The project is:

> **Unify 4 buckets of first-party data into one model, then run the CEM methodology as an
> algorithm on top to produce product + customer intelligence no competitor can replicate.**

Websites are *surfaces* that render the engine's output. They come last and they're
interchangeable. The engine is the asset.

## Why this is defensible

Anyone can build a content site. Almost no one has **first-party transaction data joined to
demographically-enriched customer records**. You do:

- **$938K of real transactions** (buy / repurchase / subscription / cancel behavior)
- **joined to 56,897 distinct real customers**
- **inside a 612K-lead base** with age, income, homeowner, credit, geography

When you can compute "Citralis is bought and *re-bought* by homeowners 55–70 in these states
with this income band," that's not opinion — it's measured truth. The CEM methodology is what
turns that raw join into evidence-graded, defensible outputs. That's the moat.

## The four buckets (the inputs)

| Bucket | What it is | Where |
|--------|-----------|-------|
| **Customers** | 612K enriched leads (demographics + contact graph) | `portal_stealth_local.verified_leads` |
| **Transactions** | $938K / 77,990 txns / 56,897 buyers | `work_hub.konnektive_transactions` |
| **Products** | The offers being sold (Citralis, Alpha Male Max…) | derived from the transaction stream |
| **Content** | 13K articles + 378 reviews (the editorial layer) | `customerreports_articles` |

## The algorithm (the output)

The CEM methodology applied to the unified data — see [03](03-the-algorithm.md). Candidate
outputs: real product performance, customer→product matching, evidence-graded scores.

## The relationship

```
4 buckets  →  unify (join)  →  CEM algorithm  →  outputs  →  surfaces
[02]          [04]             [03]              [03]        [05]
```

Read in that order. The surface (a buyer's guide or anything else) is the last box, not the
first.
