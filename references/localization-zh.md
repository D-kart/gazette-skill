# Localization — Chinese (中文网站必读)

When building a Chinese-language site in gazette style, the EN defaults fail. This file contains the rebuild rules. **Read this entire file before writing any code for a ZH site.**

## 1. Why direct translation fails

| EN mechanism | Why it fails on ZH |
|---|---|
| `Playfair Display` font | No CJK glyphs — falls back to system default, "printed quality" lost |
| `text-transform: uppercase` | Chinese has no case distinction — no effect |
| `font-style: italic` | Italic CJK is ugly and unreadable |
| `letter-spacing: 2-3px` | Sufficient for Latin, too tight for CJK |
| Drop cap at 4-5x | CJK strokes are dense — looks heavy and unbalanced |
| `VOL. XCIV` Roman numerals | Foreign-feeling, breaks ZH immersion |
| Body at 14-15px | CJK strokes blur at small sizes — unreadable |
| Line-height 1.5 | CJK needs more vertical breathing room |

## 2. Font system rebuild

### CJK serif fonts (replaces Playfair + Source Serif)

| Role | Family | Weight | Notes |
|---|---|---|---|
| Display title (ZH) | `Source Han Serif SC` (思源宋体) / `方正悠宋` / `汉仪文宋` | Heavy (700) | The CJK equivalent of Playfair Display |
| Body (ZH) | `Source Han Serif SC` Regular | 400 | The CJK equivalent of Source Serif Pro |
| UI controls (ZH) | `PingFang SC` / `Source Han Sans SC` (思源黑体) | 400-500 | Same role as Inter |
| Numerals | `Playfair Display` | 700 | **Keep Western serif — do NOT localize digits to 一二三** |

### Font stack (with fallback)

```css
:root {
  --font-display: 'Playfair Display', 'Source Han Serif SC', 'Noto Serif SC', 'Songti SC', 'STSong', serif;
  --font-body: 'Source Serif Pro', 'Source Han Serif SC', 'Noto Serif SC', 'Songti SC', serif;
  --font-ui: -apple-system, 'PingFang SC', 'Source Han Sans SC', 'Inter', sans-serif;
}
```

### Google Fonts CDN for CJK

```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;700;900&family=Playfair+Display:wght@700;900&family=Source+Serif+Pro:wght@400;600&display=swap" rel="stylesheet">
```

Note: `Noto Serif SC` is the Google-hosted equivalent of Source Han Serif SC. Full CJK fonts are large (~5-30MB); use `unicode-range` or `font-display: swap` to mitigate.

### Technical pitfalls

- `Source Han Serif Heavy` at small sizes (<14px) becomes muddy. Use Heavy only for 24px+ titles.
- For mixed CJK+Latin text, the Latin glyphs often need `font-size` +1px to optically center against CJK. Test and adjust.
- `font-feature-settings` (ligatures, kerning) has minimal effect on CJK — don't waste time tuning.
- For production: subset CJK fonts by page (use `font-subset` or `cn-font-split`) to avoid the 30MB download.

## 3. Layout rules remapping

### All-caps → wide tracking + bold

EN:
```css
.eyebrow { text-transform: uppercase; letter-spacing: 0.2em; font-size: 11px; }
```

ZH equivalent:
```css
.eyebrow {
  font-family: var(--font-ui);
  font-weight: 500;
  letter-spacing: 0.25em;   /* wider than EN, since CJK has no caps to provide visual weight */
  font-size: 12px;
}
```

### Italic subtitle → muted gray + serif + size shift

EN:
```css
.subtitle { font-style: italic; color: var(--color-muted); }
```

ZH equivalent:
```css
.subtitle {
  font-family: var(--font-body);
  font-style: normal;          /* no italic on CJK */
  color: var(--color-muted);
  font-size: 0.9em;
}
```

### Drop cap → scaled down

EN: 4.5x font size.
ZH: **3x**. CJK characters are visually heavier; 4.5x looks aggressive.

```css
.drop-cap-zh::first-letter {
  font-family: var(--font-display);
  font-weight: 900;
  font-size: 3em;
  float: left;
  line-height: 0.95;
  margin: 0.05em 0.12em 0 0;
}
```

### Roman numeral masthead → Chinese period numbering

EN: `VOL. XCIV, NO. 247`
ZH options:
- **Modern**: `第 二 四 七 期` (with wide tracking, spaces between digits)
- **Republican-era**: `卷廿四 · 第七期` (more "old newspaper" feel)
- **Bilingual**: `第 247 期 · ISSUE NO. 247` (works for mixed audiences)

Pick based on cultural positioning (see section 5 below).

### Date bar

EN: `SUNDAY, JULY 19, 2026`
ZH: `二〇二六年七月十九日 · 星期日` (formal) or `2026 年 7 月 19 日 · 星期日` (modern)

Keep the solid black bar + white text + wide tracking. The structure is identical; only the text changes.

## 4. Reading experience adjustments

CJK stroke density makes EN defaults feel cramped:

| Property | EN default | ZH recommended |
|---|---|---|
| Body font-size | 16px | **17-18px** (never below 16px) |
| Body line-height | 1.6 | **1.7-1.8** |
| Paragraph margin | 1em | 1.2em |
| Max line length | 65-75 chars | 35-45 chars (CJK is wider per char) |
| Elements per screen | EN baseline | **-20%** (less per screen) |

## 5. Color & cultural adaptation

### Palette

- Black + white + rice-paper base still works perfectly for ZH
- Use `--color-bg-rice: #F8F4ED` instead of `--color-bg-paper: #FBFAF5` for "宣纸感" (rice-paper feel)
- Otherwise palette unchanged

### Finance-specific (China)

**Red = up, green = down** — opposite of US/EU. This is non-negotiable for any China-facing finance product.

```css
:root {
  --color-up: #B23A3A;   /* red — price increase / bullish */
  --color-down: #2E7D5B; /* green — price decrease / bearish */
}
```

For non-finance ZH sites, this swap does not apply.

### Illustrations

Replace European line engravings with Chinese equivalents:
- **山海经木刻** (Shan Hai Jing woodcuts) — mythical creatures, classical
- **宋画白描** (Song dynasty plant/animal line drawings) — elegant, scholarly
- **明清小说绣像** (Ming-Qing novel illustrations) — narrative, dense
- **版画** (woodblock prints) — Hokusai-style if East Asian flavor wanted

All still black-and-white only.

### Decorative symbols

`★` (U+2605) works in ZH. Also consider:
- `※` (U+203B) — Japanese/Korean origin, common in ZH typography for "note"
- `◇` `◆` (U+25C7 / U+25C6) — diamond, classic Chinese decorative
- `❖` (U+2756) — fancier diamond
- `—` em dash as separator (very common in ZH newspapers)

Mix sparingly — pick one or two and use consistently.

## 6. Cultural positioning — pick a route

Two valid directions for ZH gazette-style sites:

### Route A: 民国大报 (Republican-era broadsheet)

Reference: 《申报》《大公报》1930s layouts.

- Use `卷廿四 · 第七期` style period numbering
- Mix `方正仿宋` for subheads with `思源宋体` for body (mimics lead-type mixed fonts)
- Heavier stroke contrast, denser composition
- Pair with 明清绣像 illustrations
- **Recommended for: finance, investment-research, data-tool products** — authority + density match

### Route B: 宋韵刻书 (Song-dynasty block-print)

Reference: 宋代刻书风, clean and elegant.

- Use `第二四七期` modern numbering with wide tracking
- Pure `思源宋体` throughout, no font mixing
- More whitespace, sparser composition
- Pair with 宋画白描 illustrations
- **Recommended for: cultural, content, editorial products** — elegance + restraint match

Default to Route A for finance products unless the user specifies otherwise.

## 7. Mixed CJK+Latin rendering tips

When the page mixes ZH body with EN terms (stock tickers, company names, technical terms):

```css
body {
  font-family: var(--font-body);
  font-feature-settings: "halt" 1;        /* half-width Latin in CJK context */
  text-spacing: ideograph-alpha;           /* auto-spacing between CJK and Latin */
}
```

For specific Latin runs that need optical centering:
```css
.en-run {
  font-family: 'Playfair Display', serif;
  font-size: 1.06em;       /* +1px equivalent */
  vertical-align: baseline;
}
```

## 8. Validation checklist for ZH sites

Before delivering a ZH site, verify:

- [ ] Body font is `Source Han Serif SC` / `Noto Serif SC` (NOT PingFang or system sans)
- [ ] Display title uses Source Han Serif Heavy at 24px+ (not at small sizes)
- [ ] No `text-transform: uppercase` on CJK text (replaced with wide tracking + bold)
- [ ] No `font-style: italic` on CJK text (replaced with muted color + size shift)
- [ ] Drop cap scaled to 3x (not 4.5x)
- [ ] Body font-size >= 17px, line-height >= 1.7
- [ ] Numerals still in `Playfair Display` (not 一二三)
- [ ] If finance: red=up, green=down
- [ ] Illustrations are CJK-style line art (not European woodcuts)
- [ ] Period numbering uses 卷/期 or 第N期 (not VOL. XCIV)
- [ ] CJK fonts subset or CDN-loaded to avoid 30MB payload
