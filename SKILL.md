---
name: gazette-skill
description: 把 Agent 变成一名古典公报编辑 / 老钱金融大报设计师。当用户需要做网站开发、Landing Page、Dashboard、HTML 报告且希望呈现"现代古典报纸 + 金融数据密度"风格时启用本技能——粗衬线大标题、近单色黑白配色、报头元素（VOL. NO. / 日期横条 / drop cap 首字下沉）、黑白线描插画、密集表格数据。视觉参考：Financial Times / The Economist / Monocle / Wall Street Journal 数字版。涵盖：网站设计（web design、landing page、homepage）、HTML 报告生成（HTML report、数据报告、研究报告排版）、金融数据型 Dashboard（finance dashboard、stock screener、rankings page）、Curated Directory 风格列表页、报纸风文章页（editorial article、drop cap）、中文化重建规则（中文衬线字体、宽字距替代大写、宣纸米色背景、红涨绿跌金融色）。触发词：gazette 风格、大报风格、报纸风格网站、金融数据型网站、古典金融、老钱感、复古衬线网站、投研工具网站、Curated Directory 风格、broadsheet style、editorial finance style、FT style、Economist style、Monocle style、legacy finance style、old money aesthetic、classical gazette、financial broadsheet。
license: MIT
compatibility: 纯 HTML/CSS 技能，无运行时依赖；可选 CDN 字体（Google Fonts: Playfair Display / Source Serif Pro / Noto Serif SC）；兼容 Claude Skills / WorkBuddy / OpenClaw / Hermes / SkillHub。
metadata:
  chinese-name: 公报.skill
  author: OPC-Studio
  version: 1.0.0
  category: web-design
  reference_site: https://www.findmymoat.com
  style_positioning: "Classical gazette + financial broadsheet"
  language_support: "EN + ZH (with rebuild rules)"
  target-platforms:
    - claude-skills
    - workbuddy
    - openclaw
    - hermes
    - skillhub
  mcp-server: none
  tags:
    - gazette
    - broadsheet
    - web-design
    - editorial
    - finance
    - serif
    - newspaper
    - old-money
    - html
    - css
agent_created: true
---

# gazette-skill · 公报

A web design style skill: **"classical gazette + financial broadsheet"**. Combines the gravitas of traditional newspaper layout (Financial Times / The Economist / Monocle / WSJ digital editions) with the dense information of modern data-driven finance tools. Visual reference: findmymoat.com.

## When to Use

Activate this skill when the user requests any of the following, AND the desired aesthetic matches the description above:

- Build / scaffold / restyle a website, landing page, dashboard, or HTML report
- Design a "curated directory", "rankings page", "tool listing", "stock screener" UI
- Create a finance / investment-research / data-tool product website
- Convert existing web output to a "newspaper feel", "editorial style", "老钱感", "古典金融感", "gazette feel"
- The user explicitly references findmymoat.com, FT, The Economist, WSJ, or Monocle as a design reference

**Do not activate** for: consumer / entertainment / children / strong-emotional-brand products. The style is wrong for those.

## Style Snapshot (load before designing)

**Positioning.** Classical gazette + financial broadsheet. Authoritative, information-dense, "printed quality". Almost no color — hierarchy comes from typography and whitespace.

**Typography stack.**
- Display / titles: bold serif (Playfair Display weight 700+). EN only — for ZH see `references/localization-zh.md`.
- Body: regular serif (Source Serif Pro / Georgia). Never sans-serif for body.
- UI controls (buttons, tags, tabs): sans-serif (Inter / system-ui).
- Numerals: bold serif (Playfair Display). Do not localize digits.

**Palette (near-monochrome).**
- Background: `#FFFFFF` (or warm paper `#FBFAF5` / `#F8F4ED` for "rice paper" feel)
- Primary text: `#000000`
- Secondary text: `#6B6B6B`
- Accent button: solid black bg + white text
- Only color permitted: muted green / muted red for sentiment votes or up/down indicators

**Layout.**
- Compact horizontal top nav (icon + text links)
- Centered oversized display title (often two lines)
- Masthead elements: `VOL. XCIV, NO. 247` / `★ A CURATED DIRECTORY... ★` / black date bar with white text / three evenly spaced tag labels
- 2-3 column body (left: intro/list, middle: illustration or search, right: ranking)
- List pages: 2-column grid; each item = logo + name + tag pills + vote buttons + actions

**Signature visuals.**
- Black-and-white line engraving illustrations (castle, heraldic, encyclopedia-plate style)
- Scattered ★ decorative asterisks
- Drop cap on article body (first letter enlarged 4-5x)
- All-caps wide-tracking small caps as section dividers
- Monochrome + whitespace + typography as the primary decorative language

## Workflow

### 1. Confirm language

Determine output language before any code:

- **English site** → use the typography stack above directly. Proceed to step 2.
- **Chinese site (中文网站)** → **MUST read `references/localization-zh.md` first**. The default EN stack fails on Chinese (Playfair Display has no CJK glyphs; uppercase / italic / drop cap rules do not translate). The reference contains the full rebuild rules.

### 2. Load full design system

Read `references/design-system.md` for the complete spec: font weights, exact hex values, spacing scale, masthead component anatomy, list-card anatomy, article-page anatomy, table styling, button system, iconography notes.

### 3. Load component recipes (if building real pages)

Read `references/components.md` for ready-to-copy HTML/CSS snippets of the most common patterns:
- Masthead (VOL.NO. + title + subtitle + date bar + tag row)
- Directory list card (logo + name + tags + votes + actions)
- Ranking table (dense tabular data)
- Article hero (two-line title + italic subtitle + drop cap body)
- Search input + filter bar
- Footer

### 4. Use the starter template

For new projects, copy `assets/starter-template.html` as the starting point. It already contains:
- Complete CSS variables (palette, fonts, spacing, radius)
- Font stack with Google Fonts CDN links (Playfair Display, Source Serif Pro, Noto Serif SC)
- Masthead component
- Sample 3-column layout
- Sample list card
- Light/dark theme toggle hook (per user preference: all generated HTML must include day/night toggle)

Customize from there. Do not start from a blank HTML file when this template exists.

### 5. Visual reference

If unsure about the look, open `assets/screenshot-home.png` and `assets/screenshot-ranking.png` — actual screenshots of the reference site (findmymoat.com) homepage and a ranking page. Match the visual density and hierarchy.

### 6. Validate output

Before delivering, self-check against this list:

- [ ] Body text uses serif, not sans-serif
- [ ] Palette stays near-monochrome; no decorative color
- [ ] Masthead has VOL.NO. or equivalent + date bar + tag row
- [ ] At least one signature visual (drop cap, ★, line illustration)
- [ ] Numerals in serif, not localized to CJK digits
- [ ] For Chinese: followed `references/localization-zh.md` (Source Han Serif, wide-tracking instead of uppercase, drop cap scaled to 3x, red-up-green-down for finance)
- [ ] Includes day/night theme toggle button (top-right fixed position)

## Key Anti-Patterns (do not do)

- Using sans-serif for body text — kills the "printed quality" instantly
- Adding decorative color (gradients, accent hues, pastels) — breaks the monochrome discipline
- Localizing digits to Chinese numerals (一二三) — keep Arabic numerals in serif
- Skipping masthead elements — without VOL.NO. / date bar / tag row it is just "a serif site", not the gazette style
- Using emoji or modern flat icons — use line engravings or simple geometric marks only
- Tight line-height on Chinese body — minimum 1.7

## File References

- `references/design-system.md` — full design system spec (fonts, colors, layout, components)
- `references/localization-zh.md` — Chinese rebuild rules (mandatory read for ZH sites)
- `references/components.md` — HTML/CSS component recipes
- `assets/starter-template.html` — copy-and-customize HTML starter
- `assets/screenshot-home.png` — reference site homepage
- `assets/screenshot-ranking.png` — reference site ranking page

## Adaptation Notes

- For finance products in China: red = up, green = down (opposite of US/EU). This is non-negotiable.
- For non-finance use (e.g., serious content platform, curated directory): keep everything, drop the finance-specific data styling.
- The style works best on desktop-first layouts. Mobile requires condensing to single column while preserving masthead hierarchy.

## Naming Note

This skill was originally named `findmymoat-style` after its visual reference site. It was renamed to `gazette` to make the style identity stand on its own — the aesthetic is a general "classical gazette / financial broadsheet" style, not specific to any one site. findmymoat.com remains the original visual reference and is credited in `metadata.reference_site`.
