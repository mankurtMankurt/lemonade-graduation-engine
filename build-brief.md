# Build Brief: Lemonade Graduation Engine Prototype
**For: an LLM building an interactive web prototype**
**Audience: a product interview panel at Lemonade**

---

## 1. What you're building

A single-file, interactive web prototype that mimics the Lemonade mobile app and walks through a renter→car bundle conversion flow called **The Graduation Engine**. The user is **James, 31**, who just moved from urban to suburban (his renters policy address changed). The engine detects this and surfaces a personalized bundled car insurance offer.

The prototype must feel like the real Lemonade app. It is the visual centerpiece of an interview presentation — judged on craft, not just function.

**Deliverable:** one self-contained `.html` file. No build step, no framework dependencies beyond a CDN. Should open and work by double-clicking. Vanilla JS only — no React build tooling. Tailwind via CDN is acceptable but custom CSS is probably cleaner for the brand-specific styling.

---

## 2. The 6 screens (in order)

The user advances through these by tapping CTAs. Each screen has a **specific job** — don't add elements that don't serve that job.

### Screen 1 — Push notification (lock screen)
The "trigger fired" moment. James's phone is sitting on the table; a Lemonade push notification appears.

- Full-screen lock screen visual: dark navy/indigo background (`#151530`)
- Lock-screen chrome: large clock "9:41" centered, date "Tuesday, June 3" in muted text above it
- A push notification card appears in the middle of the screen with a soft fade-and-slide-down animation on page load:
  - Lemonade pink app icon (rounded square with white "L" inside)
  - "LEMONADE" label · "now" timestamp on the right
  - Bold heading: "New address, new wheels? 🚗"
  - Body: "Welcome to the suburbs, James! Tap to see your bundled car quote in 60 seconds."
- The whole notification card is tappable. Tap → advances to Screen 2 (the app opens).
- Subtle dismissal hint: small "Swipe to dismiss" caption below in low-opacity gray. (Don't actually wire dismissal — tapping anywhere on the card advances.)

This screen is short and atmospheric. Don't add the app's normal chrome here — it's a lock screen.

### Screen 2 — Welcome
The "we know you, we get it" moment when James opens the app from the push.

- Pink hero band fills the top ~40% of the screen (no status bar overlap)
- Inside the pink band:
  - Back chevron (top left, white)
  - Heading: "Hey James 👋" (medium size)
  - Larger heading below: "Welcome to Westchester!"
  - Subtitle in lighter pink/cream: a Maya line — see Section 6 for exact copy
- Below the hero, on white background, a soft-pink card:
  - Tiny uppercase label: "ESTIMATED BUNDLE SAVINGS"
  - Big number: "Up to $312/yr"
  - Subtext: "on combined renters + car"
- Then a "Quick. Promise." section listing three steps:
  - 1  Confirm details
  - 2  Choose coverage
  - 3  Bind & save
- Primary CTA pill button: "See my quote →"
- Secondary text link below: "Not now"

### Screen 3 — Confirm details (Step 1 of 3)
- Top: back chevron · "Step 1 of 3" centered · progress bar (33%, pink fill)
- Heading: "Confirm a few details"
- Subtitle (Maya speaking): "Pulled from your renters policy — just check it's right."
- Pre-filled input fields. Each is a card showing the field label tiny on top, the value below in bold ink, and an "Edit" link on the right (or a green ✓ for the verified one):
  - Address: 47 Elm St, Westchester NY · Edit
  - Date of birth: March 14, 1993 · Edit
  - Marital status: Single · Edit
  - Driver's license: Verified ✓ (mint check, not editable)
- Below those: "Your vehicle" header + an empty pink-bordered field "VIN or scan plate" with a 📷 camera icon on the right. (Tappable but doesn't open anything — see "Edit" behavior in Section 7.)
- Primary CTA pill: "Continue →"

### Screen 4 — Coverage (Step 2 of 3)
- Top: back · "Step 2 of 3" · progress bar (66%)
- Heading: "Your coverage"
- Subtitle (Maya speaking): "Smart defaults. Tap to customize."
- Coverage rows (each a rounded card with a toggle on the right):
  - **Liability** · 100/300/100 · pink "Recommended" badge · ON (toggle disabled — required)
  - **Collision** · $500 ded. · ON
  - **Comprehensive** · $500 ded. · ON
  - **Pay-per-mile** · "Save with low miles" · pink "Try it" badge · OFF · *(special pink-bordered card to make it stand out)*
- A dark "Estimated $118/mo" pill near the bottom of the screen that updates **live** as toggles change
- Primary CTA pill: "Review my quote →"

**Live price logic:**
- Base (Liability only): $68/mo
- + Collision: +$32/mo
- + Comprehensive: +$18/mo
- All defaults on (no PPM): $118/mo
- If Pay-per-mile is toggled ON: replace fixed price with "$89–$132/mo · varies with miles" in italic, slightly smaller

### Screen 5 — Bundle reveal (Step 3 of 3)
The hero moment.

- Top: back · "Step 3 of 3" · progress bar (100%)
- Heading: "You bundle, you save 🍋"
- **Side-by-side comparison stack:**
  - White card (greyed-out look): "Car only · $132/mo · standalone"
  - Pink card with shadow (highlighted, slightly larger): "Renters + Car bundle" header with a yellow "BEST" badge in the corner. Big "$118/mo" number. "Save $14/mo · $168/yr 🎉" line below. Subtext: "Combined w/ your renters policy ($26/mo)"
- Below: a soft-pink "Plus, with Lemonade you get:" card listing:
  - 🌳 Trees planted to offset your miles
  - 🚗 AI Jim handles 50%+ of claims instantly
  - 🛟 Free roadside assistance with the app
  - 💛 Giveback: leftover premium goes to charity
- Primary CTA pill: "Bundle & save →"

**On tap of "Bundle & save":** Maya takes over (see Section 6 for the binding sequence).

### Screen 6 — You're bundled (confirmation)
- Pink hero band fills the top ~30% of the screen
- Inside the hero: a white circle (centered) containing a big pink ✓ checkmark — **scales in with a slight overshoot** when the screen mounts
- "You're bundled!" headline below the circle (in white)
- "Coverage starts tomorrow at 12:01 AM" subtitle (in lighter cream)
- Below the hero, a white summary card:
  - 🏠 Renters · $26/mo
  - 🚗 Car · 2021 Honda Civic · $118/mo
  - thin divider
  - **Total bundle · $144/mo** (in pink, slightly larger)
- "Next, want to..." section header
- Soft-pink opt-in card with a subtle pink border:
  - 📊 Turn on safe-driver tracking
  - "Save up to 30% more on miles" (subtext)
  - Right-arrow chevron
- Outline CTA pill: "View my policies" (white background, 1.5px pink border, pink text)
- Tiny "↺ Restart demo" link at the bottom (resets to Screen 1)

---

## 3. Brand colors

The Lemonade palette is small, opinionated, and high-contrast. Pink is the brand. Everything else is in service of pink.

### 3.1 The exact values
```css
/* Primary brand */
--lemonade-pink:        #FF0083;   /* THE pink. Everywhere. */
--lemonade-pink-dark:   #D6006D;   /* hover/pressed states only */
--lemonade-pink-light:  #FFE5F1;   /* soft fills, badge backgrounds */
--lemonade-pink-soft:   #FFF0F7;   /* card backgrounds, gentle highlights */

/* Sharp accent — use sparingly */
--lemonade-yellow:      #FFD93D;   /* "BEST" badges, lemon, special-occasion only */

/* Text */
--ink:                  #1A1A2E;   /* primary text — almost-black, not pure black */
--ink-soft:             #4A4A5E;   /* secondary text */
--gray:                 #8A8A9A;   /* tertiary text, captions, "Not now" link */

/* Surfaces */
--cream:                #FFFFFF;   /* card surfaces, app background */
--gray-light:           #F4F4F8;   /* subtle gray fields, scrollable section bg */
--border:               #E8E8EE;   /* card outlines, dividers */

/* Success — narrow use */
--mint:                 #00C896;   /* verified checks, "policy active" indicators */
--mint-light:           #D9F7EE;   /* success backgrounds (not the toggle on-state — see below) */

/* Lock screen only */
--lock-bg:              #151530;   /* deep navy for Screen 1 */
```

### 3.2 The 60/30/10 rule
On any given screen, use roughly:
- **60% white/cream** — the page breathes. Never let pink dominate by area.
- **30% pink** — hero bands, primary CTAs, accents, soft-pink card backgrounds.
- **10% ink/gray** — text and subtle chrome.
- **Yellow:** never more than one element per screen. The "BEST" badge on Screen 5 is the only place it appears.
- **Mint:** only for things that are actually verified or successful. Not for general positive vibes.

### 3.3 Pairing rules

| Background | Text color | Use for |
|---|---|---|
| White/cream | Ink (`#1A1A2E`) | All body text on white surfaces |
| White/cream | Pink | Headings inside pink-themed sections, links, prices |
| Pink | White/cream | Hero band copy, primary CTA labels |
| Pink-soft (`#FFF0F7`) | Ink | Card body text |
| Pink-soft | Pink | Card labels and highlighted text |
| Lock-bg | Cream | Push notification time/date |
| Mint background | White | Verified checkmarks |

**Never do:**
- Gray text on pink (low contrast, looks washed out)
- Pure black (`#000`) anywhere — Lemonade ink is `#1A1A2E`
- White text on yellow (illegible)
- Mint as a CTA color (reserved for verified states)
- Gradient pinks — Lemonade pink is flat

### 3.4 Specific application notes
- **Toggles ON state:** mint (`#00C896`). When OFF: gray (`#8A8A9A`). Knob is always cream.
- **Progress bars:** pink fill on a `--border` track.
- **Pressed state on primary CTAs:** drop opacity to 90% + `translateY(1px)`. Don't darken to pink-dark — that's hover, not press.
- **The yellow "BEST" badge** on Screen 5: pill shape, ink text on yellow background. About 11px font, weight 700, letter-spacing 0.08em.
- **Page background outside the phone frame:** `#FAFAFC` with a very soft pink radial gradient (`radial-gradient(circle at 80% 20%, #FFE5F1 0%, transparent 60%)`). This is the *only* gradient in the prototype.

---

## 4. Tone of voice

This is what makes a Lemonade screen feel like a Lemonade screen. Get the colors right and miss this and it'll still feel like a generic insurance app.

### 4.1 Five voice principles

**1. Talk like a person, not a policy.**
Insurance copy defaults to "Please review your information to ensure accuracy." Lemonade copy says "Just check it's right." The bar: would a smart friend say this out loud?

**2. Lowercase-leaning, but not affected.**
Sentence case for headlines (not Title Case). Lowercase is fine in casual moments ("hey james 👋"). Don't go full e.e.cummings — it should feel relaxed, not edgy.

**3. Brevity is friendliness.**
If you can say it in five words instead of nine, do. Long sentences feel formal. Short sentences feel kind.

**4. Emoji as punctuation, not decoration.**
Emoji land best when they replace a word or amplify an emotion: "🚗" instead of "your car," "🎉" after a savings number. Don't sprinkle emoji at the start of sentences for fun. One per sentence, maximum.

**5. Direct about money, never sneaky.**
"Save $14/mo" — not "Save up to ~$14/mo (terms apply)*." If there's a caveat, write it cleanly: "Combined with your renters policy ($26/mo)." Customers smell hedge copy instantly.

### 4.2 Do / Don't side-by-side

| ✅ Lemonade voice | ❌ Generic insurance voice |
|---|---|
| "Pulled from your renters policy — just check it's right." | "Please verify the following information from your existing policy." |
| "You bundle, you save 🍋" | "Combined Policy Discount Available" |
| "Smart defaults. Tap to customize." | "Recommended coverage selected. Modify as needed." |
| "Welcome to the suburbs, James!" | "We have detected a change in your residential address." |
| "Bundle & save →" | "Proceed to combine policies" |
| "Coverage starts tomorrow at 12:01 AM" | "Your policy will become effective at the next billing cycle." |
| "Save with low miles" | "Mileage-based discount eligibility" |
| "Trees planted to offset your miles" | "Carbon offset program enrollment" |

### 4.3 Specific copy rules
- **Buttons** are verb-led and short: "See my quote," "Continue," "Bundle & save," "View my policies." Never "Click here" or "Submit."
- **Errors** (none in this prototype, but in case): warm, not blamey. "Hmm, that doesn't look right" beats "Invalid input."
- **Loading states**: tell people what's happening, not just that something is happening. "Maya is binding your policy..." beats "Loading..."
- **Numbers**: dollar signs and slashes, no spaces. "$118/mo" not "$118 / mo" or "$118 per month." For dual amounts: "$14/mo · $168/yr" with a middle dot separator.
- **Sentence-ending punctuation**: most micro-copy ends without a period. "Just check it's right" not "Just check it's right." Headlines and full sentences keep their periods.

### 4.4 What to absolutely never write
- "Click here"
- "Please" (in CTAs — sounds servile; fine in genuine politeness contexts)
- "Submit"
- "We're sorry for any inconvenience"
- "Terms and conditions apply" (footnote, not body copy)
- Anything that sounds like it was translated from a legal document

---

## 5. Typography & shapes

### 5.1 Type
Lemonade uses **Maison Neue** in production. We don't have it. Fallback:

```css
font-family: 'Trebuchet MS', 'Helvetica Neue', system-ui, -apple-system, sans-serif;
```

For headlines, set `letter-spacing: -0.01em` to tighten them slightly — gets closer to Maison's geometric feel.

**Type scale (mobile sizes):**
- Hero headline: 28px / weight 700 / line-height 1.15
- Screen heading: 22px / weight 700 / line-height 1.2
- Subhead: 16px / weight 600
- Body: 14px / weight 400
- Caption / label: 11px / weight 600 / letter-spacing 0.08em / uppercase
- Big-number stat: 36–44px / weight 700

### 5.2 Shapes & spacing
- **Border radius:** Cards `16px`. Buttons `999px` (full pill). Input fields `12px`. Nothing sharper than 8px.
- **Card padding:** 16–20px minimum.
- **Vertical rhythm:** 16px between major sections, 8px between related items, 24px between unrelated sections.
- **Shadows:** Soft, almost imperceptible.
  - Resting cards: `0 2px 12px rgba(26, 26, 46, 0.06)`
  - Elevated/active (the bundle card): `0 8px 24px rgba(26, 26, 46, 0.12)`
- **Buttons:**
  - Primary: full-width pink pill, white text, 14–16px vertical padding.
  - Secondary outline: white background, 1.5px pink border, pink text, full pill.
- **Toggles:** iOS-style, ~32×20px, mint when on, gray when off, smooth knob transition.

### 5.3 Iconography
- **Emoji** for content moments (🏠 🚗 🛟 🌳 💛 📊 🍋 👋 📷). Lemonade uses emoji liberally.
- **Inline SVG** for UI chrome (back chevron, edit pencil, check, camera-in-field). Don't pull in Font Awesome.
- 16–20px in chrome contexts, 24–32px paired with text in cards.

---

## 6. Maya — the AI character

Maya is Lemonade's AI onboarding agent. In the real product, she's the chatbot that sells policies in 90 seconds. In this prototype, she's the personality behind the experience.

### 6.1 Who Maya is
- **A character, not a chatbot.** Maya is named and personified, but she doesn't show up as a chat bubble or an avatar. She's the *voice* of the screens — the implicit narrator.
- **Friendly, fast, slightly delighted by her own cleverness.** Think helpful concierge, not customer-service rep.
- **Uses contractions, light humor, never sarcasm.** "I've got you" yes. "Wow, you're really making me work today" no.
- **Confident with money, never apologetic.** Maya doesn't say "I'm sorry to ask, but..." She says "Here's what you'd save."
- **Knows things about the user.** She references James's address change, his existing renters policy, his neighborhood by name. The whole point of the Graduation Engine is that Maya already knows.

### 6.2 What Maya looks like in the UI
**Never as an avatar or chat bubble.** No floating "Maya 🤖" badge, no chat interface. She's invisible — felt in the copy.

The one place she becomes visually explicit is the **binding sequence** (Section 6.4). When she's actively "doing work," her name appears in the loading state. That's the only moment she steps forward.

### 6.3 Maya's voice — what she says where

**Screen 2 (Welcome) — pink hero subtitle:**
> "New zip, new commute. Want to see what bundled car would cost?"

(Maya is welcoming James with knowledge of his move. Cheerful, brief, no hard sell.)

**Screen 3 (Confirm) — subtitle:**
> "Pulled from your renters policy — just check it's right."

(Maya is showing she's already done the work. The em-dash makes it feel conversational, not list-like.)

**Screen 4 (Coverage) — subtitle:**
> "Smart defaults. Tap to customize."

(Maya has made an opinion. She's not asking James to figure it out alone.)

**Screen 5 (Bundle reveal) — no Maya copy needed.** The math speaks. Maya stays out of the moment.

**Screen 6 (Confirmation) — the headline is Maya's voice:**
> "You're bundled!"

(Triumphant, brief, on-brand. Not "Your bundled policy has been successfully activated.")

### 6.4 Maya's binding sequence — the one place she steps forward

This is the prototype's signature interaction. On tap of "Bundle & save" (Screen 5), Maya takes over the CTA button and runs a 2.7-second bind sequence before navigating to Screen 6.

**The sequence:**

1. **t = 0ms (tap):** The CTA button transforms in place — no navigation yet.
   - Background dims slightly (90% opacity)
   - Button becomes unclickable
   - Button label changes to: **"Maya is binding your policy"** followed by an animated dot trio (`. . .`) cycling at ~400ms intervals

2. **t = 700ms:** First checkmark fades in just below the button:
   - **✓ Verified your details** (mint check, ink text)

3. **t = 1400ms:** Second checkmark fades in below the first:
   - **✓ Calculated your premium**

4. **t = 2100ms:** Third checkmark fades in:
   - **✓ Activating coverage**

5. **t = 2700ms:** Auto-navigate to Screen 6 with the standard slide-in transition.

**The point of this sequence:** it sells the "instant claims" / "AI-first" Lemonade brand promise without requiring an actual chat interface. Maya is doing real work in the background, fast, and showing James her receipts.

**Don't make this longer than 2.7s.** Maya is fast. That's the whole point.

### 6.5 Maya tone reference card

| Situation | Maya says | Maya does NOT say |
|---|---|---|
| Greeting James who just moved | "Welcome to Westchester!" | "We have updated our records to reflect your new address." |
| Showing pre-filled data | "Pulled from your renters policy" | "The following information has been retrieved from your account." |
| Asking him to choose coverage | "Smart defaults. Tap to customize." | "Please review and modify your coverage selections as needed." |
| Working on the bind | "Maya is binding your policy" | "Processing your request, please wait." |
| Confirming success | "You're bundled!" | "Your policy bundle has been successfully created." |
| Suggesting next step | "Save up to 30% more on miles" | "Activate telematics for additional discount eligibility." |

### 6.6 What Maya is NOT
- Not an avatar. No face, no robot icon, no chat bubble UI in this prototype.
- Not gendered in a heavy-handed way. Maya is a name; the voice is warm but not feminine-coded beyond that.
- Not apologetic. She doesn't hedge. If something needs to be said, she says it.
- Not chatty for the sake of it. If a screen doesn't need her voice (like Screen 5's bundle reveal), she's silent.
- Not a sparkle-emoji AI. No ✨, no 🤖, no "powered by AI" badges. Lemonade's AI is invisible until it does something useful.

---

## 7. Phone frame

Render the prototype inside an iPhone-style frame, centered on the page. **Frame is always shown — no responsive drop.**

- **Phone frame:** 375×812px (iPhone 13 dimensions)
- **Frame body:** dark navy (`#1A1A2E`), rounded corners `48px`, drop shadow `0 24px 64px rgba(0,0,0,0.3)`
- **Notch:** small rounded pill, ~120×24px, same dark navy, centered, ~8px from frame top
- **Status bar inside the screen:** "9:41" left, signal/wifi/battery glyphs right, transparent or matched-to-screen background. ~44px tall. *(Hide the status bar entirely on Screen 1 — the lock screen has its own clock treatment.)*
- **Page background outside the phone:** `#FAFAFC` with a soft pink radial gradient in one corner — keeps focus on the phone.

### Inside the phone screen
- Screen content area: 375×812 minus status bar (~44px on screens 2-6, 0 on screen 1)
- Use `overflow-y: auto` on the screen container. Coverage and Bundle reveal will scroll within the viewport.
- Bottom CTAs sticky-bottom on scrolling screens.

---

## 8. Interactivity & state

### Navigation
- Tapping any primary CTA advances to the next screen.
- Tapping the back chevron goes to the previous screen.
- Tapping "Not now" on Screen 2 returns to Screen 1.
- Tapping the "↺ Restart demo" link on Screen 6 resets to Screen 1.
- Single state variable `currentScreen` (1-6) and a render function. No multiple HTML files.

### Animations between screens
- 250ms slide-in-from-right (CSS transform + opacity). Back navigation slides from left.
- No animation library — `transition: transform 250ms ease, opacity 250ms ease` is enough.

### Screen 1 (Push) — entry animation
On page load, the notification card starts off-screen above and slides down + fades in over 400ms.

### Screen 4 (Coverage) — live price
Bottom price pill updates in real time as toggles change. Math in Section 2.

When Pay-per-mile is toggled on, the price pill shows the range string in italic. Toggling back off restores the fixed number.

### Screen 5 (Bundle reveal) — entry animation
When this screen mounts:
- Standalone price ($132/mo) fades in first (300ms delay)
- Bundle price counts up from $132 to $118 over 600ms — `requestAnimationFrame` with ease-out
- "Save $14/mo · $168/yr 🎉" pops in last with scale (0.85 → 1) and fade

Emotional payoff. Make it feel celebratory, not robotic.

### Screen 5 → Screen 6 — Maya binding
See Section 6.4 for the full sequence and timing.

### Screen 6 (Confirmation) — entry animation
On mount, the white circle with the checkmark scales in (0 → 1) with a slight overshoot. `cubic-bezier(0.34, 1.56, 0.64, 1)` over 500ms.

### "Edit" links and the camera/VIN field on Screen 3
Tapping any Edit link or the VIN scan field shows a small toast at the bottom: "Edit not wired in this prototype." Toast slides up, holds 1.5s, slides down. Don't open an actual edit flow.

---

## 9. Code structure

Single HTML file:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  <title>Lemonade · Graduation Engine Prototype</title>
  <style>
    /* CSS custom properties for the palette */
    /* Reset + base typography */
    /* Page background (outside the phone) */
    /* Phone frame styles */
    /* Status bar styles */
    /* Component styles: button, card, input, toggle, progress-bar, badge, toast */
    /* Per-screen styles where needed */
    /* Animations: slide-in, count-up, scale-pop, dot pulse, toast */
  </style>
</head>
<body>
  <div id="phone-frame">
    <div id="notch"></div>
    <div id="screen">
      <div id="status-bar"></div>
      <div id="screen-content"><!-- screens render here --></div>
      <div id="toast" class="hidden"></div>
    </div>
  </div>
  <script>
    // State: currentScreen, coverageState, computedPrice
    // Render functions: renderScreen1, renderScreen2, ... renderScreen6
    // Helpers: navigate(screen, direction), updatePrice(), animateCountUp(), showToast(msg), runMayaSequence()
    // Init on DOMContentLoaded
  </script>
</body>
</html>
```

**Coding rules:**
- No frameworks. Vanilla JS only.
- No external font imports.
- All SVG inline. No external image URLs.
- Comment each render function with which screen it builds.
- Template literals → `innerHTML`. No manual DOM construction.
- Re-attach event listeners after each render (event delegation on `#screen-content` is cleanest).

---

## 10. What "done" looks like

The prototype is done when:

1. **It opens by double-clicking the .html file.** No server, no build step.
2. **All 6 screens are reachable** via the tap flow, with working back navigation.
3. **The visual feels like Lemonade.** Pink dominates. Type is tight. Cards are rounded. Buttons are full pills. Spacing breathes. Anyone familiar with the Lemonade app should recognize it within 2 seconds.
4. **The voice is right.** A panel member should be able to read any screen aloud and have it sound like Lemonade copy, not generic insurance copy.
5. **Maya is felt, not seen.** Her voice carries the screens. Her one explicit moment — the bind sequence — feels fast and confident.
6. **The four signature interactions work:**
   - Push notification slide-in on load (Screen 1)
   - Live price as toggles change (Screen 4)
   - Count-up + celebratory entry (Screen 5)
   - "Maya is binding..." sequence with checkmarks before navigating (Screen 5 → 6)
7. **The iPhone frame renders correctly** with notch, soft shadow, and a calm off-white page background.
8. **Nothing looks unfinished.** Every CTA does something (even if just a "not wired" toast). No lorem ipsum. No placeholder images.

---

## 11. Things to avoid

- ❌ Material Design components or icons. Lemonade is anti-corporate.
- ❌ Generic blue, green, or purple anywhere. The palette is pink + yellow + ink. That's it.
- ❌ Gradients except the page background outside the phone. Lemonade UI is flat.
- ❌ "AI sparkle" emoji (✨ 🤖). Maya doesn't need decoration to feel AI.
- ❌ Maya as an avatar, chat bubble, or named badge. She's a voice, not a UI element.
- ❌ Serif fonts.
- ❌ Formal insurance copy. Re-read Section 4 if tempted.
- ❌ Footers, logo bars, settings menus, or chrome that isn't in the spec.
- ❌ Dark mode, theme switchers, accessibility toggles. Out of scope.
- ❌ Maya binding sequence longer than 2.7s. People forgive a fake AI delay; they don't forgive a slow demo.

---

## 12. Reference & context

The spec for these screens comes from a Lemonade product interview deck: a feature called **The Graduation Engine** — a lifecycle-event detection system that surfaces tailored bundle offers when a Lemonade renter hits a life event (move, marriage, teen driver). James-moves-to-the-suburbs is the hero scenario. The prototype is the visual proof point that the engine produces a frictionless, on-brand experience.

If anything in this brief is ambiguous, **default to whatever feels most like the real Lemonade app** — friendly, fast, pink, light on chrome, voiced by Maya.

If you have access to [lemonade.com](http://lemonade.com) or screenshots of the Lemonade iOS app, reference them for the pink shade, the rounded card style, and the friendly emoji-forward voice. The fallback Trebuchet stack is decent but Maison Neue (their real font) has a slightly more geometric feel — favor tighter letter-spacing and slightly heavier weights to compensate.

---

**End of brief.**
