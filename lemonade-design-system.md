# Lemonade Design System Reference

Sourced from: live UI inspection (chat.lemonade.com in Safari), their open-source iOS component (LMDFloatingLabelTextField), Dribbble portfolio, brand registrations, and UX analyses. Use this as the ground truth for building Lemonade-lookalike products.

---

## 1. Design Principles

| Principle | Description |
|-----------|-------------|
| **Radical restraint** | Only three colors: pink, grey, white. Never more. |
| **Conversational over forms** | Replace form fields with one-question-at-a-time chat flows |
| **Round and dimensional** | All shapes use generous border radius; avoid sharp corners |
| **Instant feedback** | Real-time price recalculation, animated progress, immediate quotes |
| **Deferred friction** | No legal jargon up front; no progress bars to signal effort |
| **Mobile-first** | Every interaction designed for thumb reach first |
| **Playful but trusted** | Whimsy through illustration and copy, not color chaos |

---

## 2. Color Tokens

### Primary Palette

```css
--color-pink:          #FF0083;  /* Lemonade Pink — primary brand, CTA, active states, checkmarks */
--color-dark:          #4A4A4A;  /* Charcoal — body text, borders, focused field outlines */
--color-logo:          #282828;  /* Near-black — wordmark only */
--color-white:         #FFFFFF;  /* White — backgrounds, text on pink buttons */
```

### Neutral Scale

```css
--color-neutral-100:   #FFFFFF;  /* Pure white — card/page backgrounds */
--color-neutral-200:   #F7F7F7;  /* Off-white — disabled field backgrounds, subtle fills */
--color-neutral-400:   #B7B7B7;  /* Mid-grey — placeholder text, disabled text */
--color-neutral-600:   #888888;  /* Grey — completed step indicators */
--color-neutral-800:   #4A4A4A;  /* Dark charcoal — primary text */
--color-neutral-900:   #282828;  /* Near-black — logo/wordmark only */
```

### Pink Scale

```css
--color-pink-50:       #FCD1EE;  /* Pale pink — backgrounds, tinted sections */
--color-pink-100:      #F49BD0;  /* Soft pink — hover states, secondary accents */
--color-pink-300:      #ED4E9F;  /* Medium pink — intermediate tints */
--color-pink-500:      #FF0083;  /* Lemonade Pink — PRIMARY (all main CTAs, active states) */
```

### Semantic Tokens

```css
--color-primary:       var(--color-pink-500);
--color-error:         var(--color-pink-500);  /* Errors use brand pink, not red */
--color-success:       var(--color-pink-500);  /* Checkmarks also use brand pink */
--color-text-primary:  var(--color-neutral-800);
--color-text-muted:    var(--color-neutral-400);
--color-text-disabled: var(--color-neutral-400);
--color-bg-default:    var(--color-neutral-100);
--color-bg-subtle:     var(--color-neutral-200);
--color-border:        var(--color-neutral-400);
--color-border-focus:  var(--color-neutral-800);
```

---

## 3. Typography

### Logo / Wordmark
- **Style**: Custom handwritten/script font (proprietary — not available commercially)
- **Color**: `#282828`
- **Usage**: Wordmark only. Never use as body or UI text.
- **Closest free alternative**: Nothing exact — the script is distinctive and custom.

### UI Typeface
- **Platform**: iOS uses **SF Pro** (system font), Android uses **Roboto**
- **Web**: Clean geometric sans-serif (inspect-confirmed as system or custom sans-serif in Lemonade pink; based on visual analysis likely **Graphik** or similar neutral grotesque)
- **Fallback stack**: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`

### Type Scale

```css
--text-xs:    12px / 1.4;   /* Captions, fine print */
--text-sm:    14px / 1.5;   /* Placeholder text, helper text, secondary labels */
--text-base:  16px / 1.5;   /* Body text, form labels, chat messages */
--text-lg:    18px / 1.4;   /* Sub-headings, list items */
--text-xl:    20px / 1.3;   /* Section headings */
--text-2xl:   24px / 1.2;   /* Screen titles, hero sub-headings */
--text-3xl:   32px / 1.1;   /* Hero headlines */
--text-4xl:   48px / 1.0;   /* Marketing hero, large price display */
```

### Font Weights

```css
--font-regular:   400;  /* Body copy, chat messages */
--font-medium:    500;  /* Labels, nav items */
--font-semibold:  600;  /* Buttons, price amounts, strong emphasis */
--font-bold:      700;  /* Agent messages, headings */
```

### Floating Label Behavior (text fields)
- Placeholder at rest: 14px, `#B7B7B7`
- On focus, label shrinks to **70% of size** (9.8px) and floats above the field
- Caret color: `#FF0083`

---

## 4. Spacing System

8-point base grid. All spacing is a multiple of 4 or 8.

```css
--space-1:   4px;
--space-2:   8px;
--space-3:   12px;
--space-4:   16px;
--space-5:   20px;
--space-6:   24px;
--space-8:   32px;
--space-10:  40px;
--space-12:  48px;
--space-16:  64px;
--space-20:  80px;
--space-24:  96px;
```

---

## 5. Border Radius & Shape

Lemonade's shapes are consistently **round**. Never use sharp rectangles.

```css
--radius-sm:   4px;    /* Subtle rounding — tags, badges */
--radius-md:   8px;    /* Buttons, inputs, small cards */
--radius-lg:   12px;   /* Cards, modals, chat bubbles */
--radius-xl:   16px;   /* Large cards, bottom sheets */
--radius-2xl:  24px;   /* Large containers */
--radius-full:  9999px; /* Pills, avatars, step indicators, toggle switches */
```

**Key observations from live UI:**
- Primary CTA buttons: `--radius-md` (8px) to `--radius-lg` (12px)
- Ghost/secondary buttons: same radius, light gray border
- Step indicator dots: `--radius-full` (perfect circles)
- Avatars: `--radius-full`

---

## 6. Shadows & Elevation

Lemonade uses minimal shadows — the design is predominantly flat on white.

```css
--shadow-none:  none;
--shadow-sm:    0 1px 3px rgba(0, 0, 0, 0.08);   /* Subtle card lift */
--shadow-md:    0 4px 12px rgba(0, 0, 0, 0.10);  /* Modals, popovers */
--shadow-lg:    0 8px 24px rgba(0, 0, 0, 0.12);  /* Floating panels */
```

Cards on white backgrounds typically use either no shadow (flat, border-separated) or `--shadow-sm`. Pink brand color never receives shadows.

---

## 7. Components

### 7.1 Primary Button (Pink CTA)

```css
.btn-primary {
  background-color: #FF0083;
  color: #FFFFFF;
  font-weight: 600;
  font-size: 16px;
  padding: 14px 28px;
  border-radius: 8px;      /* or 12px for pill style */
  border: none;
  cursor: pointer;
  transition: opacity 0.15s ease;
}
.btn-primary:hover   { opacity: 0.90; }
.btn-primary:active  { opacity: 0.80; }
.btn-primary:disabled {
  background-color: #B7B7B7;
  cursor: not-allowed;
}
```

### 7.2 Ghost / Secondary Button

Observed on chat.lemonade.com as the "See my quote" button:

```css
.btn-ghost {
  background-color: #FFFFFF;
  color: #4A4A4A;
  font-weight: 600;
  font-size: 16px;
  padding: 14px 28px;
  border-radius: 8px;
  border: 1.5px solid #D0D0D0;
  cursor: pointer;
  transition: border-color 0.15s ease;
}
.btn-ghost:hover  { border-color: #4A4A4A; }
.btn-ghost:active { background-color: #F7F7F7; }
```

### 7.3 Text Input (Floating Label)

Directly derived from their open-source `LMDFloatingLabelTextField` iOS component:

```
States:
  Rest:     border bottom only, placeholder at 14px in #B7B7B7
  Focus:    border #4A4A4A, label floats to 9.8px (0.7×), caret #FF0083
  Error:    border #FF0083, label stays floated, error message below
  Disabled: text #B7B7B7, background #F7F7F7
  Enabled:  background #FFFFFF

Dimensions:
  Height: 48pt / 48px
  Min-width: 200px
```

```css
.input-wrapper {
  position: relative;
  height: 48px;
  background: #FFFFFF;
  border-bottom: 1.5px solid #B7B7B7;
}
.input-wrapper:focus-within {
  border-bottom-color: #4A4A4A;
}
.input-wrapper.error {
  border-bottom-color: #FF0083;
}
.input-wrapper.disabled {
  background: #F7F7F7;
}
.input-label {
  position: absolute;
  top: 16px;
  font-size: 14px;
  color: #B7B7B7;
  transition: all 0.2s ease;
  pointer-events: none;
}
.input-label.floating {
  top: 4px;
  font-size: 9.8px;  /* 14 × 0.7 */
}
input {
  caret-color: #FF0083;
  color: #4A4A4A;
  font-size: 16px;
}
```

### 7.4 Step Progress Indicator

Vertical stepper observed in the chat.lemonade.com quote flow:

```
Structure:
  [Circle] ─ Label text
     │
  [Circle] ─ Label text
     │
  [Circle] ─ Label text   ← Active (pink outline ring)

States:
  Done:     Filled dark-gray circle (#6E6E6E), white checkmark icon
  Active:   Outlined circle, stroke #FF0083, ~2px stroke, no fill
  Upcoming: Outlined circle, light gray stroke, no fill

Connector: 1px vertical line, #E0E0E0
Label text: 16px, #4A4A4A, font-weight 500
Active label text: #4A4A4A, same weight (no bold change)
```

```css
.step-dot {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.step-dot.done {
  background-color: #6E6E6E;  /* confirmed via screenshot */
}
.step-dot.done::after {
  content: "✓";
  color: #FFFFFF;
  font-size: 11px;
}
.step-dot.active {
  background-color: transparent;
  border: 2px solid #FF0083;
}
.step-dot.upcoming {
  background-color: transparent;
  border: 2px solid #D0D0D0;
}
.step-connector {
  width: 1px;
  height: 24px;
  background-color: #E0E0E0;
  margin: 2px auto;
}
```

### 7.5 Chat Message Interface (Maya AI)

The core interaction pattern — conversational, not form-based.

```
Layout:
  - Agent messages: left-aligned, avatar on top-left (40px circle photo)
  - User messages (answers): right-aligned or displayed as selections below
  - Agent name: none (just avatar)
  - Message text: 16px, #4A4A4A, font-weight 700 for agent questions
  - Response options: shown as selectable buttons/chips below message

Avatar:
  - Circular crop, 40–48px diameter
  - Real human photo (not illustrated avatar)
  - Positioned top-left of message

Loading state:
  - "One sec while I crunch some numbers..." text
  - Animated checklist items appear with pink ✓ checkmarks
  - Then CTA button appears
```

### 7.6 Checklist / Verification List

```css
.checklist-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0;
  font-size: 16px;
  color: #4A4A4A;
  font-weight: 400;
}
.checklist-icon {
  color: #FF0083;
  font-size: 18px;
  font-weight: 700;
}
```

### 7.7 Navigation / Selection Chips

Used for one-tap answers in the chat flow:

```css
.chip {
  display: inline-flex;
  align-items: center;
  padding: 10px 20px;
  border-radius: 999px;  /* always pill */
  border: 1.5px solid #D0D0D0;
  background: #FFFFFF;
  color: #4A4A4A;
  font-size: 15px;
  font-weight: 500;
  cursor: pointer;
}
.chip:hover,
.chip.selected {
  border-color: #FF0083;
  color: #FF0083;
}
.chip.selected-filled {
  background-color: #FF0083;
  border-color: #FF0083;
  color: #FFFFFF;
}
```

### 7.8 Card

```css
.card {
  background: #FFFFFF;
  border-radius: 16px;
  padding: 24px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}
.card-outlined {
  background: #FFFFFF;
  border-radius: 16px;
  padding: 24px;
  border: 1.5px solid #E8E8E8;
  box-shadow: none;
}
```

### 7.9 Avatar / Circular Image

```css
.avatar {
  border-radius: 50%;
  object-fit: cover;
}
.avatar-sm  { width: 32px;  height: 32px; }
.avatar-md  { width: 40px;  height: 40px; }
.avatar-lg  { width: 48px;  height: 48px; }
.avatar-xl  { width: 64px;  height: 64px; }
```

### 7.10 Toggle Switch

```css
/* Active state uses brand pink, standard iOS/Android style */
.toggle:checked {
  background-color: #FF0083;
}
```

---

## 8. Layout & Grid

### Web (Marketing + Web App)
- Max content width: **1200px**
- Side padding: `24px` mobile / `48px` tablet / `80px` desktop
- Column grid: 12-column, `24px` gutters
- Layout style: **centered single-column** for checkout/quote flows

### Mobile App
- Standard iOS/Android safe areas
- Horizontal padding: `20px` (mobile standard)
- Chat area: full-width, `16px` internal horizontal padding
- Side nav/stepper: `~100px` wide, separated by a faint divider

---

## 9. Motion & Animation

Lemonade is heavily animated — this is a core differentiator.

| Type | Spec |
|------|------|
| **Base easing** | `ease-out` for entering, `ease-in` for exiting |
| **Duration — micro** | 150ms (hover, selection state changes) |
| **Duration — standard** | 300ms (panel slides, fades) |
| **Duration — complex** | 500–800ms (page transitions, loading sequences) |
| **Format** | Lottie (exported from Adobe After Effects → JSON) |
| **Scroll animations** | Scroll-triggered reveal on marketing pages |
| **3D** | Three.js / WebGL for car product landing page |

Key animated moments:
- Checklist items animate in one-by-one during loading (staggered fade+slide)
- Progress step transitions (old step fills gray, new step ring turns pink)
- Quote price counts up or recalculates with animation
- Maya avatar has subtle idle animation
- Giveback page: animated floating particles and ribbons

---

## 10. Illustration & Iconography

### Illustration Style
- **Web/marketing**: Black line-art hand drawings on white; minimal fill; humanistic sketchy quality
- **Characters**: Rounded, friendly mascots (cat + dog for pet insurance)
- **Car product**: 3D rendered, dimensional, green-tinted
- **General**: Never photorealistic; always intentionally "drawn" feeling
- **Color in illustrations**: Monochrome (black lines) with selective pink accent — never full color scenes

### Icons
- Simple, outline-style icons
- Rounded endpoints (no sharp terminations)
- Consistent stroke width (~1.5–2px at 24px icon size)
- Color: `#4A4A4A` default, `#FF0083` for active/accent states

---

## 11. Voice & Microcopy Patterns

Lemonade's copy is as much a part of the design system as the visuals.

| Pattern | Example |
|---------|---------|
| **Casual, direct** | "One sec while I crunch some numbers..." |
| **Humor in loading states** | "Pumping jams" as a fake loading step |
| **Human warmth** | Emoji usage in appropriate contexts |
| **No insurance-speak** | "What's covered" not "Coverage terms" |
| **First person** | "Get my quote" not "Get a quote" |
| **Short sentences** | One question at a time, max one idea per screen |

---

## 12. Key Design Decisions (UX Patterns)

1. **No progress bar** — intentional. Removing it reduces perceived effort during onboarding.
2. **Chat replaces forms** — Maya asks one question at a time. No multi-field forms.
3. **Automagical registration** — Email/account creation deferred until after the quote.
4. **Real-time pricing** — Slider adjustments update the price instantly with animation.
5. **Loading as delight** — Fake-busy loading screen ("Pumping jams") makes wait feel fun.
6. **Charity selection post-purchase** — Giveback program reinforces brand ethos.
7. **Human avatar** — Real photo of an agent (not a cartoon), makes AI feel human.

---

## 13. Complete Color Reference (All Known Values)

| Token | Hex | Use |
|-------|-----|-----|
| `pink-500` | `#FF0083` | Primary CTA, active, success, error, checkmarks |
| `pink-300` | `#ED4E9F` | Hover, secondary accents |
| `pink-100` | `#F49BD0` | Subtle tints |
| `pink-50`  | `#FCD1EE` | Background tints |
| `dark-900` | `#282828` | Wordmark only |
| `dark-800` | `#4A4A4A` | Body text, borders, focused inputs |
| `dark-600` | `#6E6E6E` | Done/completed step indicators |
| `gray-400` | `#B7B7B7` | Placeholders, disabled text |
| `gray-200` | `#F7F7F7` | Disabled field backgrounds |
| `gray-100` | `#FFFFFF` | All default backgrounds |
| `border`   | `#D0D0D0` | Default input and button borders |
| `divider`  | `#E0E0E0` | Step connectors, subtle separators |

---

## 14. React / CSS Quick-Start

```css
/* Paste into your :root {} */
:root {
  --lm-pink:          #FF0083;
  --lm-pink-hover:    #ED4E9F;
  --lm-pink-light:    #FCD1EE;
  --lm-dark:          #4A4A4A;
  --lm-logo:          #282828;
  --lm-muted:         #B7B7B7;
  --lm-surface:       #F7F7F7;
  --lm-white:         #FFFFFF;
  --lm-border:        #D0D0D0;
  --lm-divider:       #E0E0E0;

  --lm-radius-sm:     4px;
  --lm-radius-md:     8px;
  --lm-radius-lg:     12px;
  --lm-radius-xl:     16px;
  --lm-radius-pill:   9999px;

  --lm-shadow-sm:     0 1px 3px rgba(0,0,0,0.08);
  --lm-shadow-md:     0 4px 12px rgba(0,0,0,0.10);
  --lm-shadow-lg:     0 8px 24px rgba(0,0,0,0.12);

  --lm-font-xs:       12px;
  --lm-font-sm:       14px;
  --lm-font-base:     16px;
  --lm-font-lg:       18px;
  --lm-font-xl:       20px;
  --lm-font-2xl:      24px;
  --lm-font-3xl:      32px;
  --lm-font-4xl:      48px;

  --lm-space-1:  4px;
  --lm-space-2:  8px;
  --lm-space-3:  12px;
  --lm-space-4:  16px;
  --lm-space-5:  20px;
  --lm-space-6:  24px;
  --lm-space-8:  32px;
  --lm-space-10: 40px;
  --lm-space-12: 48px;
  --lm-space-16: 64px;
}
```

---

## Sources

- Live UI screenshot: `chat.lemonade.com` (Safari, Apr 2026)
- iOS component source: [github.com/lemonade-hq/LMDFloatingLabelTextField](https://github.com/lemonade-hq/LMDFloatingLabelTextField)
- Brand color confirmation: Lemonade Medium publication [FF0083](https://medium.com/ff0083/what-is-ff0083-e8d5d01167b6)
- Extended palette: brandfetch.com/lemonade.com
- UX analysis: GoodUX/Appcues, ProductSins/Medium
- Design portfolio: [dribbble.com/lemonade_inc](https://dribbble.com/lemonade_inc)
