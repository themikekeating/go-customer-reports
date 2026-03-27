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
