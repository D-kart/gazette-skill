# Design System — Gazette Style

Complete spec for the "classical gazette + financial broadsheet" web style. Original visual reference: https://www.findmymoat.com

## 1. Positioning

A hybrid aesthetic that fuses:
- **Traditional newspaper gravitas** (Financial Times, The Economist, Monocle digital editions) — heavy serifs, masthead elements, line engravings, drop caps
- **Modern data-driven finance tool density** — dense tables, multi-column layouts, vote/ranking UI, compact nav

The result feels authoritative, trustworthy, and "printed". Not flashy. Not playful.

## 2. Typography

### Font stack (English)

| Role | Family | Weight | Notes |
|---|---|---|---|
| Display title | `Playfair Display` | 700-900 | The signature. Oversized, often two lines. |
| Subtitle / section divider | `Source Serif Pro` or `Playfair Display` | 400-500 + uppercase + wide tracking | All-caps with `letter-spacing: 0.15-0.3em` |
| Body | `Source Serif Pro`, `Georgia` fallback | 400 | Never sans-serif for body. |
| Numerals | `Playfair Display` | 700 | Always serif, never localize to CJK digits. |
| UI controls (buttons, tags, tabs, nav) | `Inter`, `system-ui` | 400-500 | The only place sans-serif appears. |

### Google Fonts CDN snippet

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=Source+Serif+Pro:ital,wght@0,400;0,600;1,400&family=Inter:wght@400;500&display=swap" rel="stylesheet">
```

### Type scale (desktop)

| Element | Size | Line height | Tracking |
|---|---|---|---|
| H1 (page title) | 56-72px | 1.05 | -0.02em |
| H2 (section title) | 28-32px | 1.2 | -0.01em |
| Masthead small caps | 11-12px | 1.4 | 0.2em uppercase |
| Body | 16-18px | 1.6 | 0 |
| Caption / metadata | 12-13px | 1.4 | 0.05em |
| Date bar text | 11-12px | 1 | 0.25em uppercase |
| Numerals (data) | 18-24px | 1 | -0.01em |

## 3. Palette

Near-monochrome. Color hierarchy is built from typography weight and value contrast, not hue.

```css
:root {
  --color-bg: #FFFFFF;           /* pure white, or warm paper #FBFAF5 */
  --color-bg-paper: #FBFAF5;     /* subtle paper warmth */
  --color-bg-rice: #F8F4ED;      /* "rice paper" for ZH variant */
  --color-fg: #000000;           /* primary text */
  --color-muted: #6B6B6B;        /* secondary text */
  --color-rule: #000000;         /* horizontal rules, 0.5-1px */
  --color-rule-soft: #D9D5C8;    /* soft dividers on paper bg */
  --color-accent: #000000;       /* buttons: solid black + white text */
  --color-on-accent: #FFFFFF;
  --color-up: #2E7D5B;           /* muted green — sentiment/vote only */
  --color-down: #B23A3A;         /* muted red — sentiment/vote only */
  /* For China finance: swap --color-up and --color-down (red=up, green=down) */
}
```

**Rules:**
- Background and text are always one of `--color-bg` / `--color-bg-paper` / `--color-fg`.
- The only solid fill color is `--color-accent` (black) for primary buttons and the date bar.
- `--color-up` / `--color-down` appear ONLY in vote buttons, sentiment indicators, and price ticks. Never as decoration.
- No gradients. No pastels. No accent hues.

## 4. Layout

### Page grid

- Max content width: 1200-1280px, centered
- Outer padding: 24-40px (responsive)
- Column gap: 24-32px
- Body uses 2-3 column grid on desktop, collapsing to 1 column on mobile

### Top nav

- Single horizontal row, 56-64px tall
- Icon + text links, compact spacing (16-20px between items)
- Background transparent or `--color-bg`
- Bottom border: 0.5px `--color-rule`
- No dropdowns on desktop; hamburger menu on mobile

### Masthead (the signature)

Anatomy, top to bottom:
1. Thin horizontal rule
2. Small-caps eyebrow text: `VOL. XCIV, NO. 247` (centered, muted)
3. Oversized display title (centered, 56-72px, serif 700+)
4. Subtitle line: `★ A CURATED DIRECTORY OF INVESTMENT RESEARCH TOOLS ★` (centered, small caps, wide tracking)
5. Thin horizontal rule
6. Black date bar (26-32px tall, solid black bg, white text, small caps, wide tracking): `SUNDAY, JULY 19, 2026`
7. Three evenly spaced tag labels (small caps, muted or black): `HUMAN-VETTED  ·  READ BY 20,000+  ·  UPDATED DAILY`

### List card anatomy

For directory / ranking list items:
- Two-column grid (mobile: single column)
- Each card: white bg, 0.5px border `--color-rule-soft`, 12-16px padding
- Layout: `[logo 40px] [name + star badge] [tag pills] [+N vote count] [↑↓ vote buttons] [⋯ menu] [↗ external link]`
- Hover: subtle bg shift to `--color-bg-paper`, no shadow

### Article page

- Two-line oversized title (H1)
- Italic serif subtitle
- Metadata row: `UPDATED JULY 2026  ·  TOP 50 QUALITY STOCKS` (small caps, wide tracking, muted)
- Body paragraph with drop cap on first letter (4-5x size, serif 700, float left)
- Section dividers: small-caps centered text with `★` or `—` flanking

### Ranking table

- Dense tabular layout
- Header row: small caps, wide tracking, muted
- Body: serif for names and numerals, sans-serif for action buttons
- Row hover: bg shift to `--color-bg-paper`
- No zebra striping
- Right-align numerals; use tabular-nums

## 5. Spacing scale

Use a 4px base:

`4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 120, 160`

Vertical rhythm between sections: 64-96px. Between elements in a card: 8-16px.

## 6. Signature visuals

### Drop cap

```css
.drop-cap::first-letter {
  font-family: 'Playfair Display', serif;
  font-weight: 900;
  font-size: 4.5em;
  float: left;
  line-height: 0.85;
  margin: 0.05em 0.08em 0 0;
  color: var(--color-fg);
}
```

For Chinese: scale to 3x (not 4.5x) — see `localization-zh.md`.

### Line engraving illustrations

- Black-and-white only
- Style: woodcut / copperplate / encyclopedia plate
- Subjects: castles, heraldic beasts, antique instruments, classical architecture
- Sources: public-domain woodcuts (Project Gutenberg RIP), or generate with line-engraving prompts
- For Chinese variant: Shan Hai Jing woodcuts, Song dynasty plant paintings, Ming-Qing novel illustrations

### Decorative asterisks

Use `★` (U+2605) sparingly:
- Flanking subtitle text
- As section divider accent
- As "featured" badge in list cards

Do not scatter randomly — place intentionally at structural points.

### Small-caps section dividers

```html
<div class="section-divider">
  <span class="rule"></span>
  <span class="label">SECTION TITLE</span>
  <span class="rule"></span>
</div>
```

```css
.section-divider { display: flex; align-items: center; gap: 16px; margin: 64px 0; }
.section-divider .rule { flex: 1; height: 1px; background: var(--color-rule); }
.section-divider .label {
  font-family: 'Inter', sans-serif;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--color-fg);
}
```

## 7. Button system

| Variant | Style | Use |
|---|---|---|
| Primary | Solid black bg, white text, no radius, 12px 24px padding | "LOG IN", "CREATE ACCOUNT", "SEE FULL ANALYTICS" |
| Secondary | Transparent bg, 1px black border, black text | Filter chips, secondary actions |
| Tertiary | Text only, underline on hover | Inline links in body |

No rounded corners (or 2px max). No shadows. No hover color shift — only bg invert.

## 8. Iconography

- Use thin-stroke (1-1.5px) geometric icons only
- Prefer custom SVG over icon libraries
- Avoid emoji entirely
- For directory list logos: monochrome treatment, 32-40px square

## 9. Dark mode

Per user preference, all HTML output includes a day/night toggle.

Dark mode mapping:
```css
@media (prefers-color-scheme: dark), [data-theme="dark"] {
  :root {
    --color-bg: #0F0F0F;
    --color-bg-paper: #161616;
    --color-fg: #F5F2EB;
    --color-muted: #9C998F;
    --color-rule: #F5F2EB;
    --color-rule-soft: #2E2E2E;
    --color-accent: #F5F2EB;
    --color-on-accent: #0F0F0F;
  }
}
```

In dark mode the date bar inverts: cream bg + black text. Otherwise the structure is identical.

## 10. What makes it "gazette" vs generic serif site

The combination of all of:
1. Masthead with `VOL. NO.` + black date bar + 3 tag row
2. Near-monochrome palette (no decorative color)
3. Drop cap on article body
4. Line-engraving illustration (not photo, not flat icon)
5. Small-caps wide-tracking section dividers
6. Dense tabular data presented in serif numerals

Drop any two and the style drifts to "generic serif blog". Keep all six for the gazette feel.
