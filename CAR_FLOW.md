# Car Flow — chat-based rating questions

This document covers the car-quote rating questions added to the Lemonade Graduation Engine prototype (`index.html` / `prototype.html`). It complements the original [README](README.md) and is kept in sync with the actual code on this branch.

## Why this exists

The original Graduation Engine prototype short-circuited the car-quote flow: scan plate → coverage card → bundle. That works for the demo's pitch ("we already know everything about you from your renters policy") but it skips the rating questions a real car carrier needs to price a policy.

We compared the prototype against Lemonade's production car flow (see screenshots in `/Users/danielodes/Desktop/car flow/`) and identified the questions a personal-details-only profile is missing. The ones below are now wired into the chat between car detection and the coverage card.

## What's in the chat now

The user starts on the lock screen, taps the push notification, and goes through Maya's chat. The shape of each message is the same as the rest of the prototype: a Maya bubble, then either chips or an inline widget for the answer. Everything below appears between **car detection** and the **coverage card**.

```
Maya: "Got it 🚗" → 2021 Honda Civic LX card
Maya: "A few quick questions and we're done."  [Sounds good]
  ↓
1. Annual mileage                  [slider widget, 12,000 mi/yr default]
2. Business use                    [No / Yes]   — rideshare, delivery, visiting customers
3. Safety / anti-theft features    [multi-select: garage, alarm, GPS, dashcam, ADAS]
4. Current insurance status        [Yes / No / lapsed / Never had it]
5. Provider + duration             [Geico ▼ / 3+ years ▼]   (only if "Yes" above)
6. Prior accidents (5 yrs)         [None / 1 / 2+]
7. Traffic tickets (5 yrs)         [None / 1–2 / 3+]
  ↓
Maya: "Locked in 🔒" → coverage card → "Looks good" → bundle reveal (existing)
```

State written by these steps is on the `state` object: `state.miles`, `state.businessUse`, `state.safetyFeatures`, `state.hasInsurance`, `state.priorAccidents`, `state.violations`. The rest of the existing flow (coverage toggles, bundle reveal, bind, home dashboard) is unchanged.

## Where the code lives

Everything is in `index.html` (and the identical mirror `prototype.html`).

- **Step functions** — `step_milesQ`, `step_primaryUseQ`, `step_safetyQ`, `step_hasInsuranceQ`, `step_currentInsurerQ`, `step_priorAccidentsQ`, `step_violationsQ`. Each one follows the existing pattern: `appendUser(prevAnswer)` → `clearChips()` → `mayaSay([...])` → `appendWidget(...)` (optional) → `setChips([...])`.
- **Widgets** — `milesSliderHTML`, `safetyChecksHTML`, `insurerSelectHTML`. Wrapped in the same `.widget` container as the existing prototype widgets.
- **CSS** — three new widget blocks: `.w-miles`, `.w-checks`, `.w-insurer`. They live in the main `<style>` block right above the existing `.w-coverage` rules and reuse the same design tokens (`--pink`, `--ink`, `--border`, etc.).
- **Multi-select handler** — added to the global delegated click handler at the bottom of the script. It toggles `.on` on `[data-check]` rows and updates `state.safetyFeatures`.

## Conditional branches

- **No prior insurance** — picking "No / lapsed" or "Never had it" on step 4 skips the provider/duration step (5) and goes straight to accidents (6). The `hasInsurance` field on `state` is set to `false`.

There are no other branches. We removed the SR-22 and good-student-discount questions to keep the chat tight; if they need to come back, they were `step_sr22Q` and `step_studentQ` and chained between violations and `step_showCoverage`.

## What's intentionally NOT asked

These either belong to the "personal details we already have" assumption or were judged too friction-heavy for the chat:

- Address, DOB, marital status, license info — pre-filled from renters in `step_confirmDetails`.
- VIN — auto-detected from plate scan in `step_carDetected`.
- Driver list — only the policyholder; the prototype is single-driver.
- SR-22 — removed (very rare; can be re-added if needed).
- Good-student discount — removed (driver-specific; prototype is single adult).

## Updating this doc

If you add or remove a question, update the **flow diagram** in *What's in the chat now* and the **step list** in *Where the code lives* in the same commit. The rest of the doc is structural and rarely needs touching.
