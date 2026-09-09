# 05 — Surfaces (what consumes the engine)

Surfaces render the engine's output. They are downstream and interchangeable. None of them is
the project — the engine ([03](03-the-algorithm.md)) is. Listed by who they serve.

## Internal surfaces (operator-facing — likely first value)

- **Product intelligence dashboard** — Output A: per-product buyer profile, retention,
  economics. The thing that tells you *what's actually working and to whom*.
- **Audience targeting tool** — Output B: ranked lead lists per product for outbound. Turns
  the 612K base into directed revenue.

These need no public website — they're internal tools on top of the unified model. Fastest
path from "data joins" to "money/insight."

## Public surface (the buyer's guide)

- The CEM-graded product score (Output C) rendered for search traffic → conversion.
- Reuses the kept content engine (`app/Core/Router.php`, `app/Models/*`) under a new
  foundation/shell/component theme.
- This is where the old content-site rebuild work lives — but it's now **one output channel,
  not the plan.** Only worth building once Output C (the score) is real and trustworthy.
- Design discipline still applies: no Tailwind, no left borders, no pure-white text.

## Sequencing principle

Build the **engine and one internal output first** (A or B — they pay off without a website).
Stand up the **public guide** only after the score (C) is data-backed enough to be honest.
Don't rebuild the theme before the algorithm exists — that was the original mistake.
