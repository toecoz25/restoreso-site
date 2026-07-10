# How to run the site review in Claude Code (Fable 5)

There are two ways to run this. Use whichever you like — they produce the same result.

---

## Option A — Just invoke the skill (simplest)
Once the skill is installed (see SETUP.md), in your `restoreso-site` repo run Claude Code on Fable 5 and type:

```
/site-review
```

The skill does everything: reads the personas, spawns the four reviewers, and writes the merged report to `docs/`.

---

## Option B — Paste this prompt (no skill needed / full control)
Copy everything in the box below into Claude Code (session set to **Fable 5**), from inside the `restoreso-site` repo. It works with or without the skill installed.

```
You are the orchestrator of a 4-person expert review panel for our marketing website.

PRODUCT CONTEXT (give this verbatim to every reviewer — do not let anyone contradict it):
Resto-Reso is an AI phone call agent for restaurants. It answers incoming calls and handles
reservations (book/modify/cancel) AND direct phone orders (pickup). It includes Resto-Reso's own
simple dashboard where bookings and orders live. It does NOT integrate or sync with OpenTable, Resy,
Reserve with Google, or any in-house reservation software — never suggest copy that claims integration.
Position it as an all-in-one alternative that avoids platform per-cover and delivery-app fees.
Live site: https://restoreso.ca   Repo source: the index.html / page templates in this repository.

TASK:
Spawn FIVE subagents IN PARALLEL (one message, five Task calls, subagent_type general-purpose).
The five personas are:
  1. Expert web designer / UX — visual hierarchy, layout, flow, mobile, CTA prominence, trust signals.
  2. Marketing expert — message clarity, positioning, differentiation, proof, copy, reservation-vs-order story.
  3. Sales expert — does it generate demo bookings? objections, urgency, funnel friction, pricing presentation.
  4. Restaurant owner (the real target buyer) — honest gut reaction; would they book the demo or close the tab?
  5. Accessibility auditor (WCAG 2.2 AA) — color contrast, semantic structure, keyboard operability + focus,
     labelled forms, alt text/transcripts; flag each issue Critical/Serious/Moderate/Minor.
(SEO is intentionally NOT here — it has its own dedicated seo-audit skill. Run that separately.)

Give EACH subagent: the PRODUCT CONTEXT above, its persona lens, and these EIGHT questions to answer
through that lens. Tell each one to review BOTH the live site (fetch https://restoreso.ca and read every
section: Problem, Direct Pickup, How It Works, Features, Pricing, Why Direct, FAQ, Get Started) AND the
site source in this repo. Check mobile if a browser is available.

THE EIGHT QUESTIONS (every reviewer answers all of them):
  1. Message — in one sentence, what is this business from the site alone? Is it clear and compelling?
  2. Value — is the value to a restaurant obvious and quantified? Strongest and weakest claim?
  3. Flow — does it flow problem → solution → proof → action? Where does attention break?
  4. Clarity — could a busy owner get it in under 10 seconds?
  5. Demo intent — does it make an owner WANT to book a demo? What drives or kills that?
  6. Reservation vs order balance — enough about RESERVATION features vs ORDER/pickup features? Is the split right?
  7. What's missing — what content/proof/reassurance is absent before this persona would act?
  8. Media — should it add (a) dashboard screenshots and (b) an audio sample of a reservation call and/or a
     direct-order call? Why, and where would each go?

Each subagent returns: a one-line verdict, answers to all eight questions, its top 3 ranked fixes (with
effort S/M/L), and the one thing that's working and should be kept. The accessibility reviewer also
returns a "Specialty findings" block (issues tagged by WCAG severity).

When all five return, SYNTHESIZE into a SINGLE SELF-CONTAINED HTML FILE (all CSS inline, no external
assets — a designer should be able to open it anywhere) and save it to docs/site-review-<today's date>.html:
  - Header: title, date, the five reviewers
  - Executive summary (biggest opportunity + top 3 cross-panel priorities)
  - Consensus (all/most reviewers agree — do first)
  - Split decisions (reviewers disagreed — your call + why)
  - Direct answers to my specific questions: is the message clear, does it flow, reservation-vs-order
    coverage, should we add dashboard screenshots, should we add an audio sample of a reservation and/or
    order call, and the single biggest thing it's missing
  - A prioritized action <table> (Change | Impact | Effort | Owner note)
  - An Accessibility appendix pulling that reviewer's findings together (issues tagged by WCAG severity)
  - The full raw per-reviewer notes in collapsible <details> sections at the end
Keep it clean and professional (system font, restrained accent color, comfortable spacing).
Then print the executive summary in chat and ask me if I want the top fixes implemented.
```

---

## Why the prompt is structured this way (so you can tweak it)
- **Product context is pinned at the top and marked "verbatim."** Reviewers love to invent features. The one thing that would wreck this review is someone recommending "add an OpenTable sync badge." Locking the context prevents that.
- **Five parallel subagents, not one pass.** Separate agents keep the lenses genuinely independent — the sales critique doesn't get watered down by the designer's. Running them in one message makes them concurrent, so it's fast. Four are business/experience lenses; accessibility is a technical audit that also protects against legal risk. (SEO runs as its own skill so you can audit search separately without paying for the full panel.)
- **The same eight questions go to everyone.** That's what lets you compare answers and spot consensus vs. disagreement. Your original questions map 1:1 onto them (message, flow, clarity, demo intent, reservation-vs-order, what's missing, screenshots, audio). The accessibility reviewer adds a "Specialty findings" block on top.
- **A fixed output format per reviewer.** Structured returns are what make the final merge clean instead of four essays you have to reconcile by hand.
- **Synthesis is a distinct final step** that deduplicates and ranks — that's where the actual decisions come from, not the raw persona dumps.
- **It saves to `docs/` and ends by asking** whether to implement — so the review is a decision aid, not an auto-edit of your live site.

### Easy tweaks
- **Add or drop a lens** by editing the persona list here and in `personas.md` (five ship by default: designer, marketing, sales, owner, accessibility). Drop accessibility if you want a leaner, faster run.
- Need SEO? Run the separate **`/seo-audit`** skill — it's a dedicated deeper audit than a single persona could give.
- Point it at a **staging** URL instead of production by swapping the live URL.
- The report is already **self-contained HTML**; ask for Markdown instead if you'd rather diff it in git.
