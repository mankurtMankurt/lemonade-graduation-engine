# Lemonade · Graduation Engine

A high-fidelity interactive prototype of **The Graduation Engine** — a lifecycle-event detection feature that surfaces a personalized bundled car-insurance offer when a Lemonade renter hits a life trigger (in this scenario: an urban → suburban move).

The whole product is a chat with **Maya**, Lemonade's AI agent. Widgets render inline in the conversation: savings preview, verified details, plate scan, coverage toggles with live pricing, bundle comparison, bind sequence, bound summary, Giveback charity picker.

## Run

Open `index.html` in any modern browser. No build step, no server. Single self-contained HTML file plus image assets.

## What's in the prototype

- **Lock screen + push notification** — the trigger moment, with the real Lemonade app icon and a soft pink pulse.
- **Maya chat** — typing dots, message bubbles, reply chips, Maya's photo as the avatar, persistent chat history.
- **Inline widgets** — savings card with a 💎 chip, three-step "Quick. Promise.", verified renter details, plate-scan card, coverage toggles with live price strip, bundle comparison with count-up animation + confetti, in-chat bind sequence (3 mint checks), bound hero with overshoot ✓, trees pill, Giveback charity radios.
- **Home dashboard** — bonus screen reachable from "View my policies": active policies, Giveback stats, tree counter, B-Corp chip.

## Files

- `index.html` / `prototype.html` — the prototype (vanilla JS, no framework)
- `maya.png`, `lemonade-icon.png` — image assets used in the UI
- `illust-*.png` — additional Lemonade brand illustrations (not currently rendered)
- `build-brief.md` — the build spec
- `lemonade-design-system.md` — design-system reference (colors, typography, components)

## Stack

Vanilla JavaScript. CSS custom properties. No dependencies.
