# Design System Specification: Gintic.ai

## 1. Overview & Creative North Star: "The Quiet Authority"

This design system governs the visual language of the Gintic.ai marketing site -- an enterprise AI workforce platform for back-office finance. The Creative North Star is **"The Quiet Authority"**: a philosophy that treats complex financial automation as a calm, composed intelligence rather than a loud technological spectacle.

We reject the dense dashboard aesthetic common in enterprise SaaS. Instead, we use **Generous Whitespace**, **Tonal Depth**, and a **Three-Voice Typographic System** to create an experience that feels like a bespoke financial consultancy -- structured by grids, softened by restraint. The AI workforce should feel inevitable: authoritative without asserting itself, sophisticated without ornamentation.

**Guiding principles:**

- **Restraint over decoration.** Every element earns its place. If removing something changes nothing, it should not exist.
- **Tonal hierarchy over hard boundaries.** Color shifts and spacing define structure -- not lines.
- **The machine serves the insight.** Data is presented through a lens of clarity: large typographic statements for conclusions, monospaced whispers for metadata.
- **Breathing room signals confidence.** Dense layouts suggest anxiety. We let 80px and 120px margins between sections communicate that the product has nothing to prove.

---

## 2. Colors: Tonal Architecture

Color is structural material. We use a deep forest green as the anchor of authority, tempered by warm neutrals that reduce eye strain and a navy secondary for analytical contexts.

### 2.1 The Palette

#### Primary -- The Anchor (Forest Green)

| Token              | Hex       | Role                                                        |
| ------------------ | --------- | ----------------------------------------------------------- |
| `--primary`        | `#033A00` | Hero backgrounds, primary buttons, high-authority moments    |
| `--primary-mid`    | `#597D58` | Hover states, section labels, secondary emphasis             |
| `--primary-light`  | `#9DB29C` | Hero subtext, de-emphasized copy on dark surfaces            |
| `--primary-lighter`| `#CDD7CD` | Proof lines, footer links on dark backgrounds                |
| `--primary-dim`    | `#E9EEEA` | Secondary button hover fill, light tinted backgrounds        |

#### Secondary -- The Analytical Accent (Navy)

| Token                | Hex       | Role                                               |
| -------------------- | --------- | -------------------------------------------------- |
| `--secondary`        | `#1F3A5F` | Data-heavy contexts, analytical visualizations      |
| `--secondary-mid`    | `#495F7D` | Supporting data labels                              |
| `--secondary-light`  | `#A7B2BF` | Muted analytical indicators                         |
| `--secondary-lighter`| `#D1D7DC` | Light analytical backgrounds                        |
| `--secondary-dim`    | `#EBEEEE` | Wash backgrounds for data panels                    |

#### Neutrals -- The Structure

| Token            | Hex       | Role                                                  |
| ---------------- | --------- | ----------------------------------------------------- |
| `--neutral-900`  | `#0F1412` | Primary text color (body default). Never use `#000`.   |
| `--neutral-500`  | `#707170` | Secondary body text, descriptions, supporting copy     |
| `--neutral-300`  | `#AEB1B0` | Placeholder text, disabled states                      |
| `--neutral-100`  | `#DFE1E0` | Borders (when absolutely necessary), dividers          |
| `--neutral-50`   | `#F3F5F4` | Page-level background tint, light surface areas        |
| `--white`        | `#FFFFFF` | Card surfaces, floating elements, hero text on dark    |

#### Semantic -- Status Indicators

| Token           | Hex       | Background Token  | Background Hex |
| --------------- | --------- | ----------------- | -------------- |
| `--success`     | `#069A11` | `--success-bg`    | `#E8F5E9`      |
| `--pending`     | `#0D47A1` | `--pending-bg`    | `#E3F2FD`      |
| `--error`       | `#D40404` | `--error-bg`      | `#FDECEA`      |
| `--warning`     | `#E65100` | `--warning-bg`    | `#FFF8E1`      |

Semantic colors always appear with their paired background. Never use a semantic color on a raw white surface -- the tinted background provides visual containment.

### 2.2 The "No Pure Black" Rule

**Explicit instruction:** Never use `#000000` for text, backgrounds, or borders. The darkest permissible text color is `--neutral-900` (`#0F1412`), a green-tinted near-black that harmonizes with the primary palette. Pure black creates a jarring optical weight that disrupts tonal flow.

### 2.3 The "Tinted Shadow" Convention

All shadows use rgba tints of the primary green-black `(3, 58, 0)`, not generic grey. This anchors elevation to the brand palette:

```css
/* Correct -- tinted to primary */
box-shadow: 0 12px 32px rgba(3, 58, 0, 0.08);

/* Wrong -- generic grey */
box-shadow: 0 12px 32px rgba(0, 0, 0, 0.08);
```

### 2.4 Surface Hierarchy

Treat the UI as a series of physical layers. Background shifts define structure -- not borders.

| Layer                 | Hex / Value                   | Use                                            |
| --------------------- | ----------------------------- | ---------------------------------------------- |
| **Floating**          | `#FFFFFF`                     | Cards, modals, elevated panels                  |
| **Page**              | `#FFFFFF` / `--white`         | Default body background                         |
| **Recessed**          | `#F3F5F4` / `--neutral-50`   | Trust strip, alternating sections               |
| **Inset**             | `#E9EEEA` / `--primary-dim`  | Secondary button hover, tinted wells            |
| **Deep**              | `#033A00` / `--primary`       | Hero, final CTA, dark card variants             |

### 2.5 Glass & Gradient Treatments

**Glassmorphism** is reserved for the navigation bar and modal backdrops -- two elements that float above content:

```css
/* Navigation glass */
background: rgba(255, 255, 255, 0.92);
backdrop-filter: blur(20px);
-webkit-backdrop-filter: blur(20px);

/* Dialog backdrop */
background: rgba(15, 20, 18, 0.7);
backdrop-filter: blur(8px);
```

**Gradients** serve two purposes:

- **Accent bars** on cards: `linear-gradient(90deg, var(--primary) 0%, var(--primary-mid) 100%)` -- a subtle warmth that flat color cannot achieve.
- **Overlay depth** on dark interactive surfaces: `linear-gradient(135deg, var(--primary) 0%, #0a5a04 100%)` -- used on accordion hover states and deep CTA panels.
- **Edge fades** on infinite-scroll strips: `linear-gradient(to right, var(--neutral-50), transparent)` -- 80px wide pseudo-elements that mask content overflow.

---

## 3. Typography: The Three-Voice System

Typography carries three distinct voices, each representing a different register of communication.

### 3.1 Voice 1 -- "The Architect" (Space Grotesk)

The display voice. Geometric, tech-forward, and authoritative. Used for headlines, data points, and statements of fact.

| Context             | Weight | Size   | Line Height | Letter Spacing | Responsive               |
| ------------------- | ------ | ------ | ----------- | -------------- | ------------------------ |
| Hero h1             | 500    | 60px   | 1.1         | -0.01em        | 48px at 1024, 40px at 768|
| Section headline    | 500    | 40px   | 1.3         | -0.01em        | 32px at 1024, 24px at 768|
| Final CTA headline  | 500    | 48px   | 1.15        | -0.01em        | 40px at 1024, 32px at 768|
| Customer quote      | 500    | 24px   | 1.3         | normal         | 18px at 768              |
| Stat number         | 500    | 120px  | 1           | normal         | 80px at 768              |
| Card/panel title    | 500    | 24px   | 1.3         | normal         | --                       |
| Sub-heading         | 500    | 18px   | normal      | normal         | --                       |
| Nav logo            | 500    | 24px   | normal      | normal         | --                       |
| Footer column title | 500    | 14px   | normal      | normal         | --                       |

**Constraint:** Apply `letter-spacing: -0.01em` to any Space Grotesk text above 32px. This tightening prevents large geometric type from feeling too loose.

### 3.2 Voice 2 -- "The Advisor" (DM Sans)

The body voice. Warm, highly readable, optimized for financial contexts. Optical sizing range `9..40`.

| Context             | Weight | Size | Line Height | Notes                              |
| ------------------- | ------ | ---- | ----------- | ---------------------------------- |
| Body text (default) | 400    | 14px | 1.4         | Base for all body copy              |
| Section description | 400    | 16px | 1.5         | `max-width: 560px`, `--neutral-500`|
| Hero subtitle       | 400    | 16px | 1.5         | `max-width: 480px`                  |
| Nav links           | 400    | 14px | --          | `--neutral-500`, hover to primary   |
| Button text         | 500    | 14px | --          | Weight 500 for actionable UI        |
| FAQ question        | 500    | 16px | --          | Clickable, needs visual weight      |
| FAQ answer          | 400    | 14px | 1.6         | Extended line height for readability|
| Proof line          | 300    | 12px | --          | Weight 300 for whisper-level copy   |

**Rule:** Use weight 300 sparingly -- only for tertiary text that should recede (proof lines, fine print). Weight 400 is the workhorse. Weight 500 is reserved for interactive elements and titles.

### 3.3 Voice 3 -- "The Machine" (DM Mono)

The metadata voice. Monospaced, uppercase, tightly tracked. This is how the AI system "speaks" -- status indicators, labels, timestamps.

| Context             | Weight | Size   | Letter Spacing | Transform   |
| ------------------- | ------ | ------ | -------------- | ----------- |
| Section label       | 400    | 12px   | 2px            | `uppercase` |
| Hero label          | 400    | 12px   | 2px            | `uppercase` |
| Feature label       | 400    | 12px   | 1px            | `uppercase` |
| Mockup metadata     | 400    | 10-11px| 1-2px          | `uppercase` |

**Signature styling:** The combination of `uppercase`, `10-12px`, and `2px letter-spacing` creates a technical "stamp" aesthetic -- as if the system itself is annotating the interface. This voice should never exceed 12px or appear in sentence case.

### 3.4 Font Loading

Fonts are loaded via Google Fonts with `preconnect` for performance:

```
DM Sans:  opsz 9..40, weights 300, 400, 500
DM Mono:  weight 400
Space Grotesk: weights 400, 500
```

Anti-aliasing is enforced globally: `-webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale`.

---

## 4. Spacing & Layout: The 4-Point Grid

### 4.1 The Scale

All spacing values derive from a strict 4-point base:

```
4  8  12  16  20  24  32  40  48  60  80  120
```

No arbitrary values. If a measurement does not appear in this scale, it does not belong in the system.

### 4.2 The Container

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}
```

The 1200px container is the maximum content width. The 24px horizontal padding ensures content never touches viewport edges on any device.

### 4.3 Section Rhythm

Major sections breathe with `80px` vertical padding by default. The goal is to let each section exist as a distinct thought, not a row in a stack.

| Section Type     | Vertical Padding | Notes                                |
| ---------------- | ---------------- | ------------------------------------ |
| Standard section | `80px 0`         | Use cases, product, how it works     |
| Quote section    | `80px 24px`      | Horizontal padding added             |
| Trust strip      | `48px 0`         | Compressed -- supporting, not hero   |
| Hero             | `120px 0 80px`   | Extra top padding to clear fixed nav |
| Nav bar          | --               | Fixed `60px` height                  |

### 4.4 Grid Gaps

| Context                  | Gap    | Notes                               |
| ------------------------ | ------ | ----------------------------------- |
| Hero inner grid          | `48px` | Two-column layout                    |
| Use case card grid       | `20px` | Compact card grid                    |
| Feature panel            | `48px` | Content + mockup columns             |
| Why Gintic blocks        | `60px` | Between stat and checklist blocks     |
| How It Works columns     | `24px` | Three-step process                   |
| Security badges          | `20px` | 2x2 grid at desktop                  |
| Footer grid              | `40px` | Four-column link layout              |
| Button group (hero CTAs) | `16px` | Horizontal button pair               |
| Form elements            | `12px` | Input + button rows                  |

### 4.5 Component-Level Spacing

- **Heading to description:** `16px` (`.section-headline` margin-bottom)
- **Label to heading:** `16px` (`.section-label` margin-bottom)
- **Description max-width:** `560px` for section descriptions, `480px` for hero subtitle. This prevents body text from stretching to uncomfortable line lengths.

---

## 5. Elevation & Depth: Atmospheric Layering

Depth is achieved through tonal shifts and tinted atmospheric shadows -- not the "pasted on" drop shadows of early Material Design.

### 5.1 The Shadow Vocabulary

All shadows use `rgba(3, 58, 0, ...)` -- a tint of `--primary` -- to keep elevation anchored to the brand.

| Level        | Value                                        | Use                                |
| ------------ | -------------------------------------------- | ---------------------------------- |
| **Resting**  | none                                         | Default card state                  |
| **Hover**    | `0 12px 32px rgba(3, 58, 0, 0.08)`          | Light card hover lift               |
| **Elevated** | `0 16px 40px rgba(3, 58, 0, 0.10)`          | Card active / expanded state        |
| **Deep**     | `0 16px 40px rgba(3, 58, 0, 0.25)`          | Dark card hover (on primary bg)     |
| **Floating** | `0 20px 60px rgba(0, 0, 0, 0.2)`            | Mockup panels, hero AI card         |
| **Ambient**  | `0 4px 24px rgba(3, 58, 0, 0.06)`           | Accordion containers, spotlight panels |
| **Inset**    | `4px 0 12px -4px rgba(3, 58, 0, 0.06)`      | Active tab side shadow              |

### 5.2 Glassmorphism Specification

Glass effects are used in exactly two contexts:

**Navigation bar:**
```css
background: rgba(255, 255, 255, 0.92);
backdrop-filter: blur(20px);
-webkit-backdrop-filter: blur(20px);
border-bottom: 1px solid transparent;
/* On scroll: border-bottom-color transitions to var(--neutral-100) */
```

**Video dialog backdrop:**
```css
background: rgba(15, 20, 18, 0.7);
backdrop-filter: blur(8px);
```

The nav glass uses 92% white opacity -- enough to read content through, not enough to lose the floating effect. The dialog uses `(15, 20, 18)` -- a tint of `--neutral-900` -- not generic black.

### 5.3 The Border Convention

Borders are used sparingly. When required, they follow these rules:

- **Structural borders** (cards, panels): `1px solid var(--neutral-100)` -- the lightest neutral.
- **Accent borders** (highlighted columns, mockups): `2px solid var(--primary)` -- draws the eye.
- **On dark surfaces** (hero inputs, demo forms): `1px solid rgba(255, 255, 255, 0.2)` -- ghost border. Focus state strengthens to `rgba(255, 255, 255, 0.5)`.
- **Nav scroll border:** Starts transparent, transitions to `var(--neutral-100)` on scroll via `.scrolled` class.

**Rule:** If you can achieve separation through background color shift or spacing alone, do not add a border.

---

## 6. Motion: Deliberate Transitions

Animation in Gintic is restrained and purposeful. Movement communicates state change, not decoration.

### 6.1 The Animation Library

| Name        | Purpose                      | Duration / Timing                           |
| ----------- | ---------------------------- | ------------------------------------------- |
| `fadeUp`    | Hero headline entrance       | Staggered per line, `ease` out              |
| `pulse`     | Status dot glow              | Infinite, indicates "alive" system           |
| `bounce`    | Typing indicator dots        | Infinite, 3 dots staggered by `0.15s`        |
| `marquee`   | Trust logo strip scroll      | `30s linear infinite`, pauses on `:hover`    |
| `ucSpotIn`  | Spotlight card entrance      | `0.4s ease`, opacity + translateY            |
| `spin`      | Gear decoration rotation     | `8s linear infinite`                         |

### 6.2 Scroll Reveal System

Elements with the `.reveal` class enter the viewport with a soft upward fade:

```css
.reveal {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.5s ease, transform 0.5s ease;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

Triggered by `IntersectionObserver` at `threshold: 0.15` -- the element becomes visible when 15% enters the viewport. This prevents "popping" and creates a natural reading rhythm as users scroll.

### 6.3 Interaction Transitions

| Context                | Duration | Curve                           | Property                      |
| ---------------------- | -------- | ------------------------------- | ----------------------------- |
| Button hover           | `0.2s`  | `ease` (default)                 | `background`, `color`          |
| Link hover             | `0.2s`  | `ease`                           | `color`, `border-color`        |
| Card hover lift        | `0.3s`  | `ease`                           | `transform`, `box-shadow`      |
| Accordion expand       | `0.5s`  | `cubic-bezier(0.4, 0, 0.2, 1)` | `flex`, `opacity`, `max-height`|
| Grid layout fade       | `0.4s`  | `ease`                           | `opacity`                      |
| FAQ answer             | `0.3s`  | `ease`                           | `max-height`                   |
| FAQ icon rotation      | `0.3s`  | `ease`                           | `transform` (45deg)            |
| Nav border on scroll   | `0.3s`  | `ease` (default)                 | `border-color`                 |
| SVG connector draw     | `0.8s`  | `ease`                           | `stroke-dashoffset`            |

### 6.4 Hover Motion

Cards and interactive elements lift on hover with `translateY(-4px)`. CTA-level elements use a subtler `translateY(-2px)`. Spotlight list items shift horizontally with `translateX(4px)`.

**Constraint:** No element should move more than 4px on hover. Larger movements feel anxious. All hover transforms pair with the corresponding shadow escalation from the Shadow Vocabulary (Section 5.1).

---

## 7. Components: Refined Primitives

### 7.1 Buttons

#### Primary Button

```css
.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 48px;
  padding: 0 24px;
  background: var(--primary);       /* #033A00 */
  color: var(--white);
  font-family: 'DM Sans', sans-serif;
  font-weight: 500;
  font-size: 14px;
  border-radius: 8px;
  transition: background 0.2s;
}
/* Hover: background shifts to --primary-mid (#597D58) */
```

**On dark surfaces** (hero, final CTA): colors invert. Background becomes `--white`, text becomes `--primary`. Hover lightens to `--neutral-50`.

#### Secondary Button

```css
.btn-secondary {
  /* Same layout as primary */
  min-height: 48px;
  padding: 0 24px;
  background: transparent;
  color: var(--primary);
  border: 1px solid var(--primary);
  border-radius: 8px;
  transition: background 0.2s, color 0.2s;
}
/* Hover: background fills with --primary-dim (#E9EEEA) */
```

**On dark surfaces:** border becomes `rgba(255, 255, 255, 0.4)`, text becomes white. Hover adds `rgba(255, 255, 255, 0.1)` fill.

#### Nav CTA (Compact Variant)

```css
/* Smaller for navigation context */
min-height: 40px;
padding: 0 20px;
border-radius: 8px;
/* Same primary fill + DM Sans 500 14px */
```

#### Newsletter Button

```css
/* Footer compact variant */
min-height: 40px;
padding: 0 16px;
background: var(--primary-mid);    /* #597D58 -- softer than full primary */
border-radius: 8px;
/* Hover: --primary-light (#9DB29C) */
```

### 7.2 Input Fields

#### Demo Form Input (Dark Surface)

```css
.demo-input {
  min-height: 48px;
  padding: 0 16px;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 8px;
  color: var(--white);
  font-family: 'DM Sans', sans-serif;
  font-size: 14px;
}
/* Placeholder: rgba(255, 255, 255, 0.5) */
/* Focus: border-color strengthens to rgba(255, 255, 255, 0.5) */
```

#### Newsletter Input (Dark Surface, Compact)

```css
.newsletter-input {
  min-height: 40px;
  padding: 0 12px;
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 8px;
}
/* Focus: border-color transitions to --primary-light */
```

**Rule:** Inputs on dark surfaces use translucent white backgrounds, never opaque fills. This maintains the depth of the underlying dark surface.

### 7.3 Cards

#### Light Card (Default)

- Background: `--white`
- Border: `1px solid var(--neutral-100)`
- Border radius: `12px`
- Hover: `translateY(-4px)` + shadow escalation to `0 12px 32px rgba(3, 58, 0, 0.08)`

#### Dark Card (On Grid Layouts)

- Background: `--primary` (`#033A00`)
- Text: `--white`
- Number badge: `rgba(255, 255, 255, 0.15)` background
- Hover shadow: `0 16px 40px rgba(3, 58, 0, 0.25)`

#### Accent Bar

Cards in certain layouts receive a top accent via `::before` pseudo-element:

```css
/* 3px gradient bar at top of card */
height: 3px;
background: linear-gradient(90deg, var(--primary) 0%, var(--primary-mid) 100%);
border-radius: 8px 8px 0 0;
```

### 7.4 Badges (Security Section)

- Background: `--white`
- Border: `1px solid var(--neutral-100)`
- Border radius: `12px`
- Accent: `border-top: 2px solid var(--primary)` for emphasis
- Icon container: `48px` square, `--primary-dim` background, `8px` radius
- Hover: `translateY(-4px)` + shadow

### 7.5 Accordion (Use Case Layout C)

- Container: `--white` background, `12px` radius, ambient shadow
- Panels: flex items that expand/collapse via `flex` transition (`0.5s cubic-bezier`)
- Expanded panel: gradient overlay `linear-gradient(135deg, var(--primary) 0%, #0a5a04 100%)` with white text
- Collapsed panel: white background, dark text

### 7.6 Spotlight Tabs (Use Case Layout D)

- Tab list: vertical stack with hover activation
- Active tab: side shadow `4px 0 12px -4px rgba(3, 58, 0, 0.06)`
- Tab content: appears via `ucSpotIn` animation (opacity + translateY)
- Watermark numbers: `160px` Space Grotesk at `4%` opacity for large decorative numbering

### 7.7 Focus States

Global `:focus-visible` applies `2px solid var(--primary)` with `outline-offset: 2px`. This is the only focus style -- keep it consistent across all interactive elements.

---

## 8. Responsive Behavior

Three breakpoints govern the responsive cascade:

### 8.1 Tablet -- `max-width: 1024px`

**What changes:** Typography scales down, grids compress.

| Element            | Desktop | Tablet  |
| ------------------ | ------- | ------- |
| Hero h1            | 60px    | 48px    |
| Section headline   | 40px    | 32px    |
| Final CTA headline | 48px    | 40px    |
| Feature panel      | 48px gap| 32px gap|
| Security badges    | 4-col   | 2-col   |

### 8.2 Mobile -- `max-width: 768px`

**What changes:** Layout collapses to single-column. Navigation switches to hamburger.

- **Nav:** Desktop links and CTA hidden. Hamburger icon + full-screen mobile menu.
- **Hero:** Two-column grid becomes single column with `40px` gap. Headline drops to `40px`, subtitle to `14px`.
- **All grids** (use cases, why, how it works, features, security, pulse): collapse to `1fr`.
- **Section headline:** `24px`. Final CTA headline: `32px`. Quote: `18px`. Stat number: `80px`.
- **Footer:** Collapses from 4-column to 2-column grid with `32px` gap. Bottom bar stacks vertically.
- **Tech pills:** Horizontal scroll with `overflow-x: auto` instead of wrapping.
- **Accordion (Layout C):** Switches from horizontal row to vertical column layout.
- **Spotlight (Layout D):** Tabs become horizontally scrollable row. Active indicator moves to bottom border.

### 8.3 Small Mobile -- `max-width: 480px`

**What changes:** Final compression pass for the smallest viewports.

- **Footer grid:** Collapses from 2-column to single column.
- **Hero CTAs:** Stack vertically with `width: 100%` on both buttons.
- **Demo form:** Row layout stacks to column.

---

## 9. Do's and Don'ts

### Do

- **Do** use `80px` or `120px` margins between major sections. Let the AI "breathe."
- **Do** use `--neutral-900` (`#0F1412`) for all body text. It harmonizes with the green palette.
- **Do** tint shadows with `rgba(3, 58, 0, ...)`. Shadows should feel organic to the brand.
- **Do** use translucent white fills (`rgba(255, 255, 255, 0.1)`) for inputs on dark surfaces.
- **Do** keep all border-radius at `8px` for standard UI and `12px` for cards/panels. Consistency over novelty.
- **Do** use the DM Mono "stamp" style (`uppercase`, `12px`, `2px letter-spacing`) for all metadata labels. This is the system's voice.
- **Do** pair every semantic status color with its `-bg` background token.
- **Do** apply `letter-spacing: -0.01em` to Space Grotesk above 32px.
- **Do** limit body text containers to `480-560px` max-width for comfortable reading.
- **Do** use `IntersectionObserver` for scroll-triggered animations with a `0.15` threshold.

### Don't

- **Don't** use `#000000` for anything. The darkest permissible value is `--neutral-900` (`#0F1412`).
- **Don't** use generic grey shadows (`rgba(0, 0, 0, ...)`). Always tint to the primary palette.
- **Don't** create borders when background color shifts or spacing can define the boundary.
- **Don't** exceed `4px` of movement on hover transforms. Larger movements feel undisciplined.
- **Don't** use transitions faster than `0.2s` or slower than `0.8s`. The sweet spot for interactions is `0.2s-0.3s`; for reveals and layout shifts, `0.4s-0.5s`.
- **Don't** use linear easing for UI interactions. Use `ease` for simple transitions, `cubic-bezier(0.4, 0, 0.2, 1)` for layout changes.
- **Don't** set DM Mono above 12px or in sentence case. It is the machine voice -- keep it small and uppercase.
- **Don't** fill more than 1200px of horizontal content width. If data is dense, use horizontal scroll or a secondary view -- do not compress typography.
- **Don't** add icon fonts or external SVG sprite sheets. All icons are inline SVG for zero-dependency rendering.
- **Don't** use high-intensity animations (scale, rotate, color-flash). The only permitted infinite animations are `pulse` (status dot), `bounce` (typing indicator), `marquee` (logo strip), and `spin` (gear decoration).

---

## Appendix: Token Reference (Quick Copy)

```css
:root {
  /* Primary */
  --primary: #033A00;
  --primary-mid: #597D58;
  --primary-light: #9DB29C;
  --primary-lighter: #CDD7CD;
  --primary-dim: #E9EEEA;

  /* Secondary */
  --secondary: #1F3A5F;
  --secondary-mid: #495F7D;
  --secondary-light: #A7B2BF;
  --secondary-lighter: #D1D7DC;
  --secondary-dim: #EBEEEE;

  /* Neutrals */
  --neutral-900: #0F1412;
  --neutral-500: #707170;
  --neutral-300: #AEB1B0;
  --neutral-100: #DFE1E0;
  --neutral-50: #F3F5F4;
  --white: #FFFFFF;

  /* Semantic */
  --success-bg: #E8F5E9;
  --success: #069A11;
  --pending-bg: #E3F2FD;
  --pending: #0D47A1;
  --error-bg: #FDECEA;
  --error: #D40404;
  --warning-bg: #FFF8E1;
  --warning: #E65100;
}
```

**Fonts:**
```
Space Grotesk 400, 500   — Headlines, data, navigation logo
DM Sans 300, 400, 500    — Body, UI text, buttons
DM Mono 400              — Labels, metadata, machine voice
```

**Spacing scale:**
```
4  8  12  16  20  24  32  40  48  60  80  120
```

**Border radii:**
```
8px  — Buttons, inputs, small UI
12px — Cards, panels, badges
16px — Bento grids, large containers
20px — Pill chips
50%  — Circles, avatars
```

**Breakpoints:**
```
1024px — Tablet (typography + grid compression)
768px  — Mobile (single column, hamburger nav)
480px  — Small mobile (full-width CTAs, stacked forms)
```
