# Go Customer Reports

## What This Is
US content site — publishes articles, reviews, and listicles across multiple verticals. Article engine pulls from `customerreports_articles` database.

## Type
Plain PHP with custom app structure (app/, config/, views/)

## Local URL
`http://localhost/go-customer-reports/`

## Database
`customerreports_articles` (local MySQL, root, no password). 219 MB, 12K+ articles.

## Key Rules
- Content is the product — don't delete articles
- Multiple brand subdirectories (cr, eb, ee25) serve different verticals
- SEO is critical — don't change URL structures or meta tags without understanding impact

## Connections
- **Portal** — can route leads to Portal if lead gen forms are added
- **Content database** — standalone, not shared with other repos

## Design discipline (forbidden everywhere, forever)
These apply to every project on this machine. Never to be relaxed, never to be "just this once" exceptions. Also recorded in `c:\xampp\htdocs\CLAUDE.md` and `~/.claude/CLAUDE.md` for redundancy.

- **No Tailwind, ever.** Never install, suggest, or wire `tailwindcss` / `@tailwindcss/vite` / `@tailwindcss/*` into this repo. Never recommend Tailwind utility classes (`text-red-500`, `flex`, `p-4`, `border-l-*`, etc.) in templates. If `tailwindcss` appears in `package.json`, it is dead weight — remove it. As of 2026-05-12 every htdocs repo is Tailwind-free.
- **No left borders, ever.** `border-left` (and any shorthand that produces a left-only border) is a forbidden CSS pattern. Never add it to new CSS, never re-introduce it during refactors, never suggest it as a styling solution. Use other separators (full borders, background tints, spacing, top/bottom rules) instead.
