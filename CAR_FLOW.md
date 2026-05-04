# Car Flow — Lemonade Graduation Engine

Complete walkthrough of the chat-based car-quote flow in `index.html` (and its mirror `prototype.html`). Covers every screen, step, widget, and branch from lock screen to home dashboard.

---

## End-to-end flow

```
Lock screen
  Push notification: "New address, new wheels? 🚗"
  → tap → Maya chat opens
  
startConversation
  Maya: Hey James 👋 (3 messages)
  Widget: Savings card (up to $312/yr, bundle perks)
  Chips: [Yes, let's see 🍋]  [Maybe later]
  
  ── "Maybe later" branch ────────────────────────────────
  step_maybeLater
    Maya: "offer holds 30 days"
    Chips: [Actually, show me]  [Restart demo]
    → "Actually, show me" → step_letsGo
  ────────────────────────────────────────────────────────

step_letsGo
  Maya: "Three quick steps, ~60 seconds."
  Widget: Steps card (1 Confirm details · 2 Choose coverage · 3 Bundle & save)
  Chips: [Let's go]

step_confirmDetails
  Maya: "Pulled these from your renters policy."
  Widget: Details card (address · DOB · marital status · license)
  Chips: [All correct ✓]  [Edit something] (toast only — not wired)

step_selectCars
  Maya: "These are the cars I found at your address. Which would you like to insure?"
  Widget: Car-select list with toggles + "Add car" (toast only)
  Chips: [Next →]

step_carFromList
  User answer: selected car name(s)
  Maya: "Got it 🚗"
  Widget: Detected-car card (name · "Registered at 47 Elm St, Westchester NY")
  Maya: "A few quick questions and we're done."
  Chips: [Sounds good]

── Rating questions ────────────────────────────────────────────────────────

step_milesQ
  Maya: "About how many miles do you drive a year?"
  Widget: Miles slider (2,000–30,000, step 500, default 12,000)
  Chips: [Looks right]

step_primaryUseQ
  User answer: ~{miles} mi/yr
  Maya: "Do you ever use it for business — rideshare, deliveries, visiting customers?"
       "(Regular commuting doesn't count.)"
  Chips: [No]  [Yes]
  → sets state.businessUse

step_safetyQ
  User answer: No / Yes
  Maya: "Got any of these? Each one bumps your discount."
  Widget: Safety checklist (multi-select)
         🏠 Parked in a garage
         🔒 Factory alarm / immobilizer
         📍 GPS tracker (LoJack, OnStar…)
         📷 Dashcam
         🚗 Lane-keep / auto-brake
  Chips: [Continue]
  → sets state.safetyFeatures

step_hasInsuranceQ
  User answer: Continue
  Maya: "Do you have car insurance right now?"
  Chips: [Yes]  [No / lapsed]  [Never had it]
  → sets state.hasInsurance

  ── "Yes" branch ────────────────────────────────────────
  step_currentInsurerQ
    Maya: "Who's your provider, and how long?"
    Widget: Insurer widget
            Provider dropdown (Geico · State Farm · Progressive · Allstate · USAA · Liberty Mutual · Other)
            Duration dropdown (< 6 mo · 6–12 mo · 1–3 yrs · 3+ yrs)
    Chips: [Continue]
    → step_priorAccidentsQ
  ────────────────────────────────────────────────────────
  ── "No / lapsed" or "Never had it" → skip to step_priorAccidentsQ

step_priorAccidentsQ
  Maya: "Any accidents in the last 5 years? (At-fault or not.)"
  Chips: [None 🙏]  [1]  [2+]
  → sets state.priorAccidents (0 / 1 / 2)

step_violationsQ
  Maya: "Traffic tickets in the last 5 years?"
       "(Parking tickets don't count.)"
  Chips: [None]  [1–2]  [3+]
  → sets state.violations (0 / 1 / 3)

── Coverage & bundle ───────────────────────────────────────────────────────

step_showCoverage
  Maya: "Locked in 🔒"
       "Here are smart defaults for your profile. Toggle anything — price updates live."
  Widget: Coverage card
          🛡️ Liability 100/300/100 — always on, disabled toggle
          💥 Collision ($500 deductible) — toggle
          🌧️ Comprehensive ($500 deductible) — toggle
          🛣️ Pay-per-mile — toggle (shows range price $89–$132/mo)
          Price strip: live estimated monthly price
  Chips: [Looks good]

step_bundleReveal
  Maya: "Now the fun part 🎉" + "Here's what bundling does to the price:"
  Confetti burst
  Widget: Compare card — "Car only · standalone" vs "Renters + Car bundle · BEST"
          (count-up animation on bundle price)
  Widget: Plus card — trees offset · AI Jim claims · roadside · Giveback charity
  Chips: [Bundle & save 🍋]  [What's Giveback?]

  ── "What's Giveback?" branch ────────────────────────────────
  step_givebackExplain
    Maya: explains flat-fee model, $2.3M donated, B-Corp
    Chips: [Bundle & save 🍋]
  ─────────────────────────────────────────────────────────────

step_bind
  Maya: (no pre-message)
  Widget: Bind card — 3-row animated checklist
          ✓ Verified your details (700 ms)
          ✓ Calculated your premium (700 ms)
          ✓ Activating coverage (700 ms)
  Maya: "You're bundled! 💛"
  Widget: Bound summary card (renters + car prices, total bundle, coverage start)
  Confetti burst
  Widget: Trees pill (count = miles / 2000, e.g. 12k mi → 6 trees)
  Maya: "~{N} trees on the way… One last thing — pick a Giveback charity?"
  Widget: Charity card (radio select)
          📚 Malala Fund
          🌳 One Tree Planted
          🐾 ASPCA
  Chips: [View my policies]  [Restart demo]

step_goHome → renderHome
  Home screen: pink hero "Hi James 👋 · Your Lemonade"
  Tabs: Policies · Claims · Giveback · Settings
  Policy cards: 🚗 Car (active, bundled) · 🏠 Renters (active)
```

---

## State written during the flow

| Field | Set by | Values |
|---|---|---|
| `state.selectedCarName` | `step_carFromList` | car name string |
| `state.miles` | miles slider | 2000–30000, default 12000 |
| `state.businessUse` | `step_primaryUseQ` | bool |
| `state.safetyFeatures` | safety checklist | array of feature ids |
| `state.hasInsurance` | `step_hasInsuranceQ` | bool |
| `state.priorAccidents` | `step_priorAccidentsQ` | 0 / 1 / 2 |
| `state.violations` | `step_violationsQ` | 0 / 1 / 3 |
| `state.coverage` | coverage toggles | `{ collision, comprehensive, ppm }` bools |
| `state.charity` | charity card | `'malala'` / `'trees'` / `'aspca'` |

---

## Pricing

```js
PRICE = { base: 89, collision: 22, comprehensive: 14, standalone: 127, rentersAlone: 14 }
carPrice() = base + (collision if on) + (comprehensive if on)
```

Bundle price shown on compare card = `carPrice()`. Standalone = `$127/mo`. Savings = difference × 12/yr.

---

## Widgets reference

| Function | Description |
|---|---|
| `savingsCardHTML()` | Bundle savings teaser (up to $312/yr, 3 perks) |
| `stepsCardHTML()` | 3-step "Quick. Promise." preview card |
| `detailsCardHTML()` | Personal details pulled from renters policy |
| `carsWidgetHTML()` | Registered car list with toggles |
| `detectedCarFromListHTML(car)` | Single confirmed car card (from list) |
| `milesSliderHTML()` | Annual miles range input with live pill |
| `safetyChecksHTML()` | 5-row multi-select safety/anti-theft list |
| `insurerSelectHTML()` | Provider + duration dropdowns |
| `coverageCardHTML()` | Coverage toggles + live price strip |
| `compareCardHTML()` | Standalone vs bundle price comparison |
| `plusCardHTML()` | Lemonade perks list |
| `bindCardHTML()` | 3-row animated bind checklist |
| `boundSummaryHTML()` | Post-bind policy summary with total |
| `treesPillHTML()` | Trees-offset pill (miles / 2000) |
| `charityCardHTML()` | Giveback charity radio picker |

---

## What's intentionally not asked

These are either pre-filled from the renters policy or excluded to keep the chat tight:

- **Address, DOB, marital status, license** — shown in `step_confirmDetails` as pre-filled from renters
- **VIN** — auto-identified from the registered-cars list (plate scan path exists as `step_carDetected` / `detectedCarHTML` but is not in the primary flow)
- **Driver list** — single-driver prototype only
- **SR-22** — removed (rare; was `step_sr22Q`, can be re-added between violations and showCoverage)
- **Good-student discount** — removed (driver-specific; was `step_studentQ`)

---

## Conditional branches

- **Insurance status → No / lapsed / Never had it**: skips `step_currentInsurerQ` entirely, goes straight to `step_priorAccidentsQ`
- **Maybe later**: dead-end branch with a "holds 30 days" message and an escape hatch back to `step_letsGo`
- **What's Giveback?**: informational detour before `step_bind`, does not affect state

---

## Updating this doc

When adding or removing a step: update the flow diagram, the state table (if applicable), and the widgets table in the same commit.
