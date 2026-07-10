---
name: site-review
description: Run a multi-persona expert review of the Resto-Reso website (restoreso.ca). Spawns five reviewer subagents — a web designer, a marketing expert, a sales expert, a target-buyer restaurant owner, and an accessibility auditor — who each review BOTH the live site and the repo source, then synthesizes one prioritized, self-contained HTML report. Use when the user wants feedback on the site's messaging, flow, clarity, conversion, accessibility, what's missing, reservation-vs-order balance, or whether to add dashboard screenshots or an audio call sample. For a dedicated SEO audit, use the separate seo-audit skill instead.
---

# Site Review — Multi-Persona Expert Panel

## What this skill does
It reviews the Resto-Reso marketing site through five independent expert lenses at once, then merges their findings into a single, deduplicated, prioritized **HTML report**. Each reviewer looks at the **live site** and the **repo source** so feedback is grounded in what visitors actually see AND what's in the code. (SEO lives in its own `seo-audit` skill — run that separately for search/technical SEO.)

## Product context (give this to every reviewer)
Resto-Reso is an **AI phone call agent for restaurants**. It answers incoming calls and handles **reservations** (book / modify / cancel) and **direct phone orders** (pickup). Buying it includes Resto-Reso's **own simple dashboard** where bookings and orders live.

Critical accuracy rule — do NOT invent or assume features:
- It does **NOT** integrate or sync with OpenTable, Resy, Reserve with Google, or any third-party / in-house reservation system. Never suggest copy that claims integration.
- Position it as an all-in-one alternative that avoids pricey platform per-cover / delivery-app fees.
- Live site: https://restoreso.ca  •  Dashboard: https://resto-reso-production.up.railway.app/login

## How to run it

1. **Read the persona briefs** in `personas.md` (same folder as this file) — there are five: web designer, marketing, sales, restaurant owner, accessibility auditor.
2. **Spawn five subagents in parallel** — one per persona — using the Task tool (`subagent_type: general-purpose`). Run your Claude Code session on **Fable 5** so the subagents inherit that model. Send all five Task calls in a single message so they run concurrently.
3. Give **each** subagent:
   - The full **Product context** block above (verbatim — so no one invents integrations).
   - Its **persona brief** from `personas.md`.
   - The **shared question set** below (every reviewer answers all of it, through their own lens).
   - Instruction to review **both** sources: fetch/open the live site `https://restoreso.ca` (all sections: Problem, Direct Pickup, How It Works, Features, Pricing, Why Direct, FAQ, Get Started) **and** read the site source in this repo (the `index.html` / page templates). Check the mobile view too if a browser is available.
   - Instruction to return findings in the **per-reviewer output format** below — nothing else.
4. **Synthesize.** When all five return, merge into one report using the **final report format** below. Deduplicate overlapping points, and flag where reviewers **agree** (high-confidence) vs **disagree** (judgment call). Build it as a **single self-contained HTML file** (all CSS inline, no external assets) and save it to `docs/site-review-<YYYY-MM-DD>.html` in the repo. Print the executive summary in chat.

## Shared question set (every reviewer answers all eight)
1. **Message** — In one sentence, what is this business, from the site alone? Is it clear and compelling?
2. **Value** — Is the value to a restaurant obvious and quantified? What's the strongest and weakest value claim?
3. **Flow** — Does the page flow logically from problem → solution → proof → action? Where does attention break or drop?
4. **Clarity** — Could a busy restaurant owner understand what this is and why it matters in under 10 seconds?
5. **Demo intent** — Does the page make a restaurant owner *want* to book a demo? What specifically drives or kills that intent?
6. **Reservation vs. order balance** — Is there enough about the **reservation** features vs the **order/pickup** features? Is the split right for the target buyer, or is one under-sold?
7. **What's missing** — What content, proof, or reassurance is absent that this persona would expect before acting?
8. **Media** — Should the site add (a) **dashboard screenshots** and (b) an **audio sample** of a reservation call and/or a direct-order call? Why or why not, and where would each go?

## Per-reviewer output format (require this from each subagent)
```
## Reviewer: <persona name>

### One-line verdict
<single sentence: would this persona endorse the site as-is?>

### Answers to the eight questions
1. Message: ...
2. Value: ...
3. Flow: ...
4. Clarity: ...
5. Demo intent: ...
6. Reservation vs order balance: ...
7. What's missing: ...
8. Media (screenshots / audio): ...

### Top 3 fixes (ranked, most impactful first)
1. <fix> — why it matters — rough effort (S/M/L)
2. ...
3. ...

### Specialty findings (Accessibility reviewer only)
<contrast, alt text, keyboard nav, semantic HTML, labelled forms — list WCAG issues each tagged with a severity: Critical / Serious / Moderate / Minor.>

### Best thing about the site (keep this)
<one thing that's working and should not change>
```

## Final report format (the synthesis you produce)
Produce a **single self-contained HTML file** — all CSS inline in a `<style>` block, no external fonts/scripts/images, so it opens anywhere and can be handed straight to a designer. Use a clean, readable layout (system font stack, generous spacing, a sticky or clearly-styled section nav is a plus). Include these sections in this order:

1. **Header** — "Resto-Reso Site Review", the date, and a one-line list of the five reviewers.
2. **Executive summary** — 5–7 sentences: overall verdict, the single biggest opportunity, and the top 3 cross-panel priorities.
3. **Consensus** — points all/most reviewers agree on (do these first).
4. **Split decisions** — where reviewers disagreed, with your call + reasoning.
5. **Answers to the owner's specific questions** — as a definition-style list: Message clear? • Does it flow? • Reservation-vs-order coverage (verdict + recommendation) • Dashboard screenshots? (yes/no, where, what to show) • Audio sample of a reservation and/or order call? (yes/no, where, format) • Biggest thing it's missing.
6. **Prioritized action table** — an HTML `<table>` with columns: # | Change | Impact | Effort | Owner note. Color-code or badge Impact (High/Med/Low) if you like.
7. **Accessibility appendix** — a short dedicated block pulling the accessibility reviewer's findings together, each issue tagged by WCAG severity.
8. **Full per-reviewer notes** — each of the five reviewers' raw output, in collapsible `<details>` sections so the report stays scannable.

Keep it visually calm and professional (a restrained accent color, clear headings, comfortable line length). This file IS the deliverable.

## Notes
- Keep every reviewer honest to the **Product context** — reject any recommendation that implies OpenTable/Resy/Google integration.
- If a browser tool isn't available, reviewers use WebFetch on the live URL plus the repo source; note in the report that mobile/visual review was source-only.
- This is a review skill — it does **not** edit the site. End by asking the user if they want the top fixes implemented.
