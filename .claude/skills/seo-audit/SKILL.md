---
name: seo-audit
description: Run a dedicated SEO audit of the Resto-Reso website (restoreso.ca) — keyword targeting and search intent, on-page optimization, technical/indexability checks, structured data, and content gaps — reviewing BOTH the live site and the repo source, then produce a prioritized, self-contained HTML SEO report. Use when the user asks about SEO, search ranking, keywords, discoverability, meta tags, Schema.org, "why can't people find us", or wants an SEO check on the site. This is the SEO counterpart to the broader site-review skill.
---

# SEO Audit — Resto-Reso

## What this skill does
A focused search-engine-optimization audit of the marketing site: can a restaurant owner searching for a solution actually find Resto-Reso, and is the page built to rank and convert that traffic? It reviews the **live site** and the **repo source** (so it can check real files like `robots.txt`, `sitemap.xml`, and the page HTML/meta) and outputs one prioritized **HTML report**.

## Product context (pin this — never contradict it)
Resto-Reso is an **AI phone call agent for restaurants** that handles **reservations** (book/modify/cancel) and **direct phone orders** (pickup) and includes its **own dashboard**. It does **NOT** integrate with OpenTable, Resy, Reserve with Google, or any in-house system — never recommend keywords or copy implying integration. It's an all-in-one alternative that avoids platform per-cover and delivery-app fees.
Live site: https://restoreso.ca • Repo: the site source in this repository (`index.html`, `robots.txt`, `sitemap.xml`).

## How to run it
Run your Claude Code session on **Fable 5**. You can do this as a single thorough pass, or (better for depth) spawn the four audit tracks below as parallel subagents (Task tool, `subagent_type: general-purpose`, one message) and then synthesize. Every track reviews the live site AND the repo source.

**Track 1 — Keyword targeting & search intent**
- What is this page actually optimized for today vs. what its buyers search? Map realistic queries an owner would type: "AI phone answering service for restaurants", "restaurant reservation phone system", "stop missing restaurant calls", "reduce delivery app fees", "restaurant answering service".
- Separate **reservation-intent** keywords from **order/pickup-intent** keywords — is one being ignored in copy people actually search? Recommend a primary keyword + a short secondary set per section.

**Track 2 — On-page optimization**
- Title tag, meta description (length, keyword, click-appeal), a single clear H1, logical H2/H3 hierarchy, keyword usage in headings/body/alt text, descriptive link text, image alt text, URL/slug quality, Open Graph / Twitter card tags for link sharing.

**Track 3 — Technical & indexability**
- Check the real `robots.txt` and `sitemap.xml` in the repo (are they correct, complete, referencing the live URLs?). Canonical tag, mobile-friendliness, page weight / speed signals, render-blocking assets, broken links, HTTPS, and whether the page is crawlable/indexable.

**Track 4 — Structured data & content gaps**
- Schema.org opportunities: `Organization` / `LocalBusiness`, `Product`/`Offer` for pricing, and especially **`FAQPage`** for the existing FAQ section (currently an unused rich-result opportunity). 
- Content gaps: searchable topics that would pull qualified traffic but aren't covered (pricing/fee comparisons, "how AI answers restaurant calls", reservation how-tos). Suggest concrete page or section additions.

## Output — self-contained HTML SEO report
Build a **single self-contained HTML file** (all CSS inline, no external assets) and save it to `docs/seo-audit-<YYYY-MM-DD>.html`. Print the executive summary in chat. Sections, in order:
1. **Header** — "Resto-Reso SEO Audit" + date.
2. **Executive summary** — current SEO health in 4–6 sentences + the single biggest opportunity.
3. **Scorecard** — a small table rating each area (Keywords / On-page / Technical / Structured data / Content) as Good / Needs work / At risk.
4. **Findings by track** — the four tracks above, each with what's wrong and why it matters.
5. **Recommended keyword map** — a table: Page section → primary keyword → secondary keywords → intent (reservation vs order).
6. **Prioritized action table** — columns: # | Fix | Impact | Effort | Where in the site. Put quick wins (title/meta/alt/FAQ schema) at the top.
7. **Copy-paste snippets** — ready-to-use suggested `<title>`, meta description, and a JSON-LD FAQPage block built from the site's actual FAQ questions.
Keep it clean and professional (system font, restrained accent color).

## Notes
- Keep every recommendation honest to the product context — no integration keywords/claims.
- This skill audits and recommends; it does **not** edit the site. End by asking if the user wants the quick wins implemented.
- For messaging/flow/conversion/accessibility feedback, use the separate `site-review` skill.
