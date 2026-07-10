# Resto-Reso Marketing Site

Single-page static site (`index.html`, self-contained CSS/JS, no build step) for restoreso.ca.
The product repo is `~/projects/Resto-reso`.

## ⚠ Pricing — read before touching the pricing section or calculator

**Canonical pricing lives in `~/projects/Resto-reso/docs/PRICING.md`** (rev. 2026-07-09,
direct-pickup model). Summary:

- Starter · Orders: $55/mo + $0.95/completed phone order, plan limit 150 orders (≈$198 at limit; above → Growth)
- Growth · Orders: $85/mo + $0.85/order, plan limit 300 ($340 at limit; above → custom pricing)
- Reservations: $199/mo, 120 eligible reservation calls included, $0.90/additional eligible call
- Complete (bundle tier, formerly "Bundle"): $249/mo + $0.85/order, plan limit 300 ($504 at limit), 120 reservation calls included, $0.90/extra
- Setup $150 one-time. Direct online orders unlimited & free with Starter/Growth/Complete (NOT the Reservations-only plan)
- Plan limits are hard cut-offs, not overage caps — never write "capped at $X" in customer copy
- Positioning: direct-pickup first — "Keep Delivery Apps for Delivery. Take Pickup Back." Say "delivery apps", never "marketplace"; "no percentage fees on direct orders", not "commission-free". AI persona = "AI phone assistant".
- Customer-facing terminology: "completed phone orders", "plan order limit"

## Other facts

- Product features that are true and safe to claim: AI answers & takes phone orders 24/7,
  scheduled orders up to 7 days ahead, owners edit menus via dashboard, SMS confirmations,
  manager alerts, reservations book/modify/cancel by phone.
- NO OpenTable/Resy/Google integration exists — never claim booking-platform sync.
- Branch note: repo is on `main`; the 2026-07 pricing + direct-pickup update is merged and live (PR #1). Feature branch `pricing-update-2026-07` has been deleted.
- Contact form posts to Formspree; demo bookings via calendar.app.google link.
