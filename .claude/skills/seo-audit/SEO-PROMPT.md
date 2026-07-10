# How to run the SEO audit in Claude Code (Fable 5)

## Option A — invoke the skill
From inside your `restoreso-site` repo, Claude Code on Fable 5:
```
/seo-audit
```

## Option B — paste this prompt
Copy the box below into Claude Code (session on **Fable 5**), from inside the `restoreso-site` repo.

```
Run a dedicated SEO audit of our marketing site.

PRODUCT CONTEXT (pin this — never contradict it):
Resto-Reso is an AI phone call agent for restaurants that handles reservations (book/modify/cancel) and
direct phone orders (pickup) and includes its own dashboard. It does NOT integrate with OpenTable, Resy,
Reserve with Google, or any in-house system — never recommend keywords or copy implying integration.
Position it as an all-in-one alternative that avoids platform per-cover and delivery-app fees.
Live site: https://restoreso.ca   Repo source: index.html, robots.txt, sitemap.xml in this repository.

TASK — audit BOTH the live site and the repo source across four tracks (you may run them as four parallel
subagents, subagent_type general-purpose, then synthesize):
  1. Keyword targeting & search intent — what the page targets today vs. what buyers actually search
     ("AI phone answering for restaurants", "restaurant reservation phone system", "stop missing restaurant
     calls", "reduce delivery app fees"). Separate reservation-intent from order/pickup-intent keywords and
     say if one is being ignored. Recommend a primary + secondary keyword per section.
  2. On-page — title tag, meta description, single H1, H2/H3 hierarchy, keyword usage, image alt text,
     descriptive link text, URL/slug, Open Graph / Twitter card tags.
  3. Technical & indexability — read the real robots.txt and sitemap.xml in the repo and verify they're
     correct and reference the live URLs; check canonical, mobile-friendliness, page weight/speed,
     render-blocking assets, broken links, crawlability/indexability.
  4. Structured data & content gaps — Schema.org opportunities (Organization/LocalBusiness, Product/Offer
     for pricing, and especially FAQPage for the existing FAQ section, currently unused); plus searchable
     content the site is missing (fee comparisons, "how AI answers restaurant calls", reservation how-tos).

OUTPUT — build a SINGLE SELF-CONTAINED HTML FILE (all CSS inline, no external assets) and save it to
docs/seo-audit-<today's date>.html, with:
  - Header (title + date)
  - Executive summary + the single biggest opportunity
  - A scorecard table (Keywords / On-page / Technical / Structured data / Content = Good / Needs work / At risk)
  - Findings by track (what's wrong + why it matters)
  - A recommended keyword map table (section → primary → secondary → reservation-vs-order intent)
  - A prioritized action table (# | Fix | Impact | Effort | Where in the site), quick wins first
  - Copy-paste snippets: a suggested <title>, meta description, and a JSON-LD FAQPage block built from the
    site's ACTUAL FAQ questions
Then print the executive summary in chat and ask if I want the quick wins implemented.
```

## Why it's split from the site review
SEO is a technical audit with its own outputs (keyword maps, schema snippets, robots/sitemap checks) that a single "reviewer persona" can't do justice to. Keeping it separate means you can run a quick SEO check without spinning up the whole five-person panel — and vice-versa. Run `/site-review` for messaging, flow, conversion, and accessibility; run `/seo-audit` for search.
