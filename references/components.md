# Components — HTML/CSS Recipes

Ready-to-copy component snippets for gazette-style pages. Each snippet assumes the CSS variables from `design-system.md` are defined on `:root`.

## 1. Masthead

The signature component. Place at the top of the homepage and section pages.

```html
<header class="masthead">
  <div class="masthead-rule"></div>
  <div class="masthead-eyebrow">VOL. XCIV, NO. 247</div>
  <h1 class="masthead-title">Find My Moat</h1>
  <div class="masthead-subtitle">★ A CURATED DIRECTORY OF INVESTMENT RESEARCH TOOLS ★</div>
  <div class="masthead-rule"></div>
  <div class="masthead-datebar">SUNDAY, JULY 19, 2026</div>
  <div class="masthead-tags">
    <span>HUMAN-VETTED</span>
    <span class="sep">·</span>
    <span>READ BY 20,000+</span>
    <span class="sep">·</span>
    <span>UPDATED DAILY</span>
  </div>
</header>
```

```css
.masthead {
  text-align: center;
  padding: 32px 24px 24px;
}
.masthead-rule {
  height: 0.5px;
  background: var(--color-rule);
  margin: 0 auto;
  max-width: 720px;
}
.masthead-eyebrow {
  font-family: var(--font-ui);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.25em;
  color: var(--color-muted);
  margin: 16px 0;
}
.masthead-title {
  font-family: var(--font-display);
  font-size: clamp(40px, 7vw, 72px);
  font-weight: 900;
  line-height: 1.05;
  letter-spacing: -0.02em;
  margin: 8px 0;
  color: var(--color-fg);
}
.masthead-subtitle {
  font-family: var(--font-display);
  font-size: 12px;
  font-weight: 400;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-fg);
  margin: 12px 0 16px;
}
.masthead-datebar {
  background: var(--color-accent);
  color: var(--color-on-accent);
  font-family: var(--font-ui);
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  padding: 8px 0;
  margin: 16px -24px 16px;
}
.masthead-tags {
  font-family: var(--font-ui);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--color-fg);
  display: flex;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
}
.masthead-tags .sep { color: var(--color-muted); }
```

### ZH variant

Replace text content:
- `VOL. XCIV, NO. 247` → `第 二 四 七 期` (modern) or `卷廿四 · 第七期` (Republican)
- Title → `觅护城河` (or actual site name)
- Subtitle → `★ 投研工具精选指南 ★` (drop `text-transform: uppercase`, increase `letter-spacing` to 0.3em)
- Date bar → `二〇二六年七月十九日 · 星期日`
- Tags → `人工筛选  ·  两万余投资者订阅  ·  每日更新`

Remove `text-transform: uppercase` from `.masthead-subtitle`, `.masthead-datebar`, `.masthead-tags` for ZH (no effect anyway, but cleaner CSS).

## 2. Top nav

```html
<nav class="topnav">
  <a href="/" class="brand">FMM</a>
  <ul class="nav-links">
    <li><a href="/directory">Tool Directory</a></li>
    <li><a href="/rankings">Top Tools</a></li>
    <li><a href="/screeners">Screeners</a></li>
    <li><a href="/moat">Moat Stocks</a></li>
    <li><a href="/collections">Collections</a></li>
  </ul>
  <div class="nav-actions">
    <a href="/login" class="btn-secondary">Log in</a>
    <a href="/signup" class="btn-primary">Create account</a>
  </div>
</nav>
```

```css
.topnav {
  display: flex;
  align-items: center;
  gap: 32px;
  padding: 16px 32px;
  border-bottom: 0.5px solid var(--color-rule);
  font-family: var(--font-ui);
}
.topnav .brand {
  font-family: var(--font-display);
  font-weight: 900;
  font-size: 18px;
  letter-spacing: -0.01em;
}
.nav-links {
  display: flex;
  gap: 20px;
  list-style: none;
  margin: 0;
  padding: 0;
  flex: 1;
}
.nav-links a {
  font-size: 13px;
  color: var(--color-fg);
  text-decoration: none;
}
.nav-links a:hover { text-decoration: underline; text-underline-offset: 4px; }
.nav-actions { display: flex; gap: 8px; }
```

## 3. Buttons

```css
.btn-primary, .btn-secondary {
  font-family: var(--font-ui);
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 8px 18px;
  text-decoration: none;
  display: inline-block;
  border: 1px solid var(--color-fg);
  cursor: pointer;
  transition: background 0.15s, color 0.15s;
}
.btn-primary {
  background: var(--color-accent);
  color: var(--color-on-accent);
}
.btn-primary:hover { background: var(--color-fg); }
.btn-secondary {
  background: transparent;
  color: var(--color-fg);
}
.btn-secondary:hover {
  background: var(--color-fg);
  color: var(--color-bg);
}
```

## 4. Directory list card

```html
<article class="tool-card">
  <div class="tool-logo"><img src="logo.svg" alt="Tool"></div>
  <div class="tool-info">
    <h3 class="tool-name">CapEdge <span class="star-badge">★</span></h3>
    <div class="tool-tags">
      <span class="tag">FREE</span>
      <span class="tag">PORTFOLIO</span>
      <span class="tag">USA</span>
    </div>
  </div>
  <div class="tool-meta">
    <span class="vote-count">+142</span>
    <div class="vote-buttons">
      <button class="vote-up" aria-label="Upvote">↑</button>
      <button class="vote-down" aria-label="Downvote">↓</button>
    </div>
  </div>
  <a class="tool-link" href="https://capedge.com" target="_blank" rel="noopener">↗</a>
</article>
```

```css
.tool-card {
  display: grid;
  grid-template-columns: 40px 1fr auto 24px;
  gap: 16px;
  align-items: center;
  padding: 16px;
  background: var(--color-bg);
  border: 0.5px solid var(--color-rule-soft);
  transition: background 0.15s;
}
.tool-card:hover { background: var(--color-bg-paper); }
.tool-logo img { width: 32px; height: 32px; display: block; }
.tool-name {
  font-family: var(--font-display);
  font-size: 17px;
  font-weight: 700;
  margin: 0 0 4px;
}
.star-badge { color: var(--color-fg); font-size: 12px; }
.tool-tags { display: flex; gap: 6px; flex-wrap: wrap; }
.tag {
  font-family: var(--font-ui);
  font-size: 10px;
  font-weight: 500;
  letter-spacing: 0.1em;
  padding: 2px 8px;
  border: 0.5px solid var(--color-rule);
  color: var(--color-fg);
}
.tool-meta { display: flex; align-items: center; gap: 12px; }
.vote-count {
  font-family: var(--font-display);
  font-weight: 700;
  font-size: 16px;
  color: var(--color-fg);
  font-variant-numeric: tabular-nums;
}
.vote-buttons { display: flex; gap: 4px; }
.vote-buttons button {
  width: 24px; height: 24px;
  border: 0.5px solid var(--color-rule);
  background: transparent;
  cursor: pointer;
  font-size: 12px;
  color: var(--color-fg);
  font-family: var(--font-ui);
}
.vote-buttons button:hover { background: var(--color-fg); color: var(--color-bg); }
.tool-link {
  font-family: var(--font-ui);
  font-size: 16px;
  color: var(--color-fg);
  text-decoration: none;
}
```

## 5. Ranking table

```html
<table class="ranking-table">
  <thead>
    <tr>
      <th>#</th>
      <th>Ticker</th>
      <th>Company</th>
      <th class="num">Price</th>
      <th class="num">1Y Return</th>
      <th class="num">Quality Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>MSFT</td>
      <td>Microsoft Corp.</td>
      <td class="num">$412.65</td>
      <td class="num up">+24.83%</td>
      <td class="num">9.4</td>
    </tr>
    <tr>
      <td>2</td>
      <td>NOW</td>
      <td>ServiceNow</td>
      <td class="num">$745.20</td>
      <td class="num up">+31.45%</td>
      <td class="num">9.2</td>
    </tr>
  </tbody>
</table>
```

```css
.ranking-table {
  width: 100%;
  border-collapse: collapse;
  font-family: var(--font-body);
  font-size: 15px;
}
.ranking-table th {
  font-family: var(--font-ui);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--color-muted);
  text-align: left;
  padding: 12px 8px;
  border-bottom: 1px solid var(--color-rule);
}
.ranking-table th.num, .ranking-table td.num {
  text-align: right;
  font-variant-numeric: tabular-nums;
}
.ranking-table td {
  padding: 14px 8px;
  border-bottom: 0.5px solid var(--color-rule-soft);
  color: var(--color-fg);
}
.ranking-table td.num {
  font-family: var(--font-display);
  font-weight: 700;
  font-size: 16px;
}
.ranking-table tr:hover td { background: var(--color-bg-paper); }
.ranking-table .up { color: var(--color-up); }
.ranking-table .down { color: var(--color-down); }
/* For China finance: swap .up and .down colors in CSS */
```

## 6. Article hero with drop cap

```html
<article class="article">
  <header class="article-hero">
    <h1>Best Quality Stocks 2026,<br>Ranked for Business Strength</h1>
    <p class="article-subtitle">A human-vetted list of high-quality compounders, updated quarterly.</p>
    <div class="article-meta">UPDATED JULY 2026  ·  TOP 50 QUALITY STOCKS</div>
  </header>
  <div class="article-body">
    <p class="drop-cap">Quality stocks are companies with durable competitive advantages — the economic moats that protect profits from competitors. This ranking combines return on invested capital, free cash flow consistency, and balance sheet strength to surface businesses built to compound over decades.</p>
    <p>The methodology favors businesses with...</p>
  </div>
</article>
```

```css
.article-hero { margin-bottom: 48px; }
.article-hero h1 {
  font-family: var(--font-display);
  font-size: clamp(32px, 5vw, 48px);
  font-weight: 900;
  line-height: 1.1;
  letter-spacing: -0.015em;
  margin: 0 0 16px;
  color: var(--color-fg);
}
.article-subtitle {
  font-family: var(--font-body);
  font-style: italic;
  font-size: 18px;
  color: var(--color-muted);
  margin: 0 0 16px;
}
/* For ZH: remove font-style: italic, see localization-zh.md */
.article-meta {
  font-family: var(--font-ui);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--color-muted);
}
.article-body {
  font-family: var(--font-body);
  font-size: 17px;
  line-height: 1.65;
  color: var(--color-fg);
  max-width: 680px;
}
.article-body p { margin: 0 0 1.2em; }
.drop-cap::first-letter {
  font-family: var(--font-display);
  font-weight: 900;
  font-size: 4.5em;
  float: left;
  line-height: 0.85;
  margin: 0.05em 0.08em 0 0;
  color: var(--color-fg);
}
```

## 7. Three-column homepage body

```html
<section class="home-grid">
  <div class="col-intro">
    <h2>What is Find My Moat?</h2>
    <p>A curated hub for investing tools, ranked lists, and stock research...</p>
  </div>
  <div class="col-feature">
    <img src="/castle-engraving.svg" alt="">
    <div class="search">
      <input type="search" placeholder="Search tools, stocks, rankings...">
    </div>
  </div>
  <div class="col-ranking">
    <h3>Best Investing Tools</h3>
    <ol class="mini-ranking">
      <li>CapEdge <span>+142</span></li>
      <li>GeminIQ <span>+98</span></li>
      <li>TipRanks <span>+87</span></li>
    </ol>
  </div>
</section>
```

```css
.home-grid {
  display: grid;
  grid-template-columns: 1fr 1.4fr 1fr;
  gap: 32px;
  padding: 32px;
  max-width: 1280px;
  margin: 0 auto;
}
@media (max-width: 900px) {
  .home-grid { grid-template-columns: 1fr; }
}
.col-feature img { width: 100%; display: block; margin-bottom: 24px; }
.col-feature input[type="search"] {
  width: 100%;
  padding: 12px 16px;
  border: 0.5px solid var(--color-rule);
  background: var(--color-bg);
  font-family: var(--font-body);
  font-size: 15px;
}
.mini-ranking {
  list-style: none;
  padding: 0;
  font-family: var(--font-body);
}
.mini-ranking li {
  display: flex;
  justify-content: space-between;
  padding: 8px 0;
  border-bottom: 0.5px solid var(--color-rule-soft);
  font-size: 15px;
}
.mini-ranking li span {
  font-family: var(--font-display);
  font-weight: 700;
  color: var(--color-fg);
  font-variant-numeric: tabular-nums;
}
```

## 8. Footer

```html
<footer class="footer">
  <div class="footer-rule"></div>
  <div class="footer-inner">
    <div class="footer-section">
      <div class="footer-label">CURATION & ACCURACY</div>
      <p>Human-vetted since 2024. Rankings updated daily. No paid placements.</p>
    </div>
    <div class="footer-section">
      <div class="footer-label">CATEGORIES</div>
      <a href="/screeners">Screeners</a>
      <a href="/moat">Moat Stocks</a>
      <a href="/collections">Collections</a>
    </div>
    <div class="footer-section">
      <a class="btn-secondary" href="/suggest">Suggest a tool ↗</a>
    </div>
  </div>
  <div class="footer-bottom">© 2026 Find My Moat</div>
</footer>
```

```css
.footer { padding: 64px 32px 24px; }
.footer-rule { height: 0.5px; background: var(--color-rule); margin-bottom: 32px; }
.footer-inner {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 48px;
  max-width: 1280px;
  margin: 0 auto 48px;
}
.footer-label {
  font-family: var(--font-ui);
  font-size: 10px;
  font-weight: 500;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: var(--color-muted);
  margin-bottom: 12px;
}
.footer-section p { font-family: var(--font-body); font-size: 14px; color: var(--color-fg); margin: 0; }
.footer-section a {
  display: block;
  font-family: var(--font-body);
  font-size: 14px;
  color: var(--color-fg);
  text-decoration: none;
  padding: 4px 0;
}
.footer-bottom {
  text-align: center;
  font-family: var(--font-ui);
  font-size: 11px;
  letter-spacing: 0.15em;
  color: var(--color-muted);
}
```

## 9. Line engraving SVG (castle, inline)

A small inline SVG used as decorative illustration. Black-and-white only.

```html
<svg viewBox="0 0 200 160" xmlns="http://www.w3.org/2000/svg" class="engraving">
  <g fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round">
    <path d="M20 140 L20 80 L40 80 L40 60 L60 60 L60 80 L80 80 L80 40 L100 40 L100 60 L120 60 L120 30 L140 30 L140 60 L160 60 L160 80 L180 80 L180 140 Z"/>
    <path d="M40 100 L60 100 M80 100 L100 100 M120 100 L140 100 M80 120 L100 120 M120 120 L140 120"/>
    <path d="M0 140 L200 140"/>
    <path d="M100 30 L100 20 L105 20 L105 30"/>
  </g>
</svg>
```

```css
.engraving { color: var(--color-fg); width: 100%; max-width: 240px; }
```

Replace with proper line-engraving assets for production. For ZH, swap to Shan Hai Jing or Song-dynasty plant motifs.

## 10. Sticky sidebar + scrollspy (long documents)

For long-form documents (curriculum, table of contents, research reports, tool directories), a sticky left sidebar keeps navigation always in view while the reader scrolls. Inspired by findmymoat.com's layout.

```html
<div class="layout">
  <aside class="sidebar">
    <div class="brand">MAOSHU</div>
    <div class="brand-sub">AI NATIVE INVESTMENT</div>
    <div class="vol">VOL. NO. 01 · EDITION</div>

    <div class="group-label">目录 · INDEX</div>
    <ul class="nav">
      <li><a href="#top"><span class="num">▸</span>课程首页</a></li>
      <li><a href="#gains"><span class="num">▸</span>课程收获</a></li>
    </ul>

    <div class="group-label">模块一 · MINDSET</div>
    <ul class="nav">
      <li><a class="sub" href="#c01"><span class="num">01</span>AI 能力边界</a></li>
      <li><a class="sub" href="#c02"><span class="num">02</span>工具矩阵</a></li>
    </ul>

    <div class="actions">
      <a class="btn btn-primary" href="#top" onclick="event.preventDefault(); window.print();">下载</a>
      <button class="btn btn-secondary" id="contactBtn" type="button">联系</button>
    </div>
  </aside>

  <main class="page" id="top">
    <!-- masthead + content sections, each with id="c01", "c02", ... -->
  </main>
</div>
```

```css
.layout {
  display: flex; gap: 32px;
  max-width: 1320px; margin: 0 auto;
  padding: 40px 32px 64px;
  align-items: flex-start;
}
.sidebar {
  width: 220px; flex-shrink: 0;
  position: sticky; top: 24px;
  align-self: flex-start;
  max-height: calc(100vh - 48px); overflow-y: auto;
  font-family: var(--font-ui);
  scrollbar-width: thin;
  scrollbar-color: var(--color-rule-soft) transparent;
}
.sidebar .brand {
  font-family: var(--font-display); font-weight: 900; font-size: 22px;
  letter-spacing: 0.02em; padding-bottom: 4px;
  border-bottom: 2px solid var(--color-fg);
}
.sidebar .brand-sub {
  font-family: var(--font-ui); font-size: 10.5px; font-weight: 600;
  letter-spacing: 0.22em; color: var(--color-muted); margin-top: 6px;
}
.sidebar .vol {
  margin-top: 14px; font-family: var(--font-ui); font-size: 10.5px;
  letter-spacing: 0.18em; color: var(--color-muted);
  padding-bottom: 12px; border-bottom: 1px solid var(--color-rule-soft);
}
.sidebar .group-label {
  font-family: var(--font-ui); font-size: 10.5px; font-weight: 600;
  letter-spacing: 0.24em; color: var(--color-muted);
  margin: 18px 0 8px;
}
.sidebar ul.nav { list-style: none; }
.sidebar ul.nav li { margin-bottom: 2px; }
.sidebar ul.nav a {
  display: flex; align-items: baseline; gap: 8px;
  padding: 6px 8px; color: var(--color-fg); text-decoration: none;
  font-size: 12.5px; line-height: 1.5;
  transition: background 0.2s, color 0.2s;
  border-left: 2px solid transparent;
}
.sidebar ul.nav a:hover {
  background: var(--color-bg-card);
  border-left-color: var(--color-fg);
}
.sidebar ul.nav a.active {
  background: var(--color-bg-card);
  border-left-color: var(--color-fg);
  font-weight: 600;
}
.sidebar ul.nav a .num {
  font-family: var(--font-display); font-weight: 700; color: var(--color-muted);
  font-size: 11px; min-width: 22px;
}
.sidebar ul.nav a.sub { padding-left: 28px; font-size: 12px; color: var(--color-muted); }
.sidebar .actions {
  margin-top: 24px; padding-top: 18px;
  border-top: 1px solid var(--color-rule-soft);
  display: flex; flex-direction: column; gap: 8px;
}
.sidebar .actions .btn {
  display: block; padding: 9px 14px; text-align: center;
  font-family: var(--font-ui); font-size: 11px; font-weight: 600;
  letter-spacing: 0.2em; text-decoration: none;
  border-radius: 2px; transition: background 0.2s, color 0.2s;
}
.sidebar .actions .btn-primary {
  background: var(--color-accent); color: var(--color-on-accent);
}
.sidebar .actions .btn-secondary {
  background: transparent; color: var(--color-fg); border: 1px solid var(--color-fg);
  cursor: pointer;
}
.page { flex: 1; min-width: 0; max-width: 1020px; }

/* mobile: sidebar collapses to top of page */
@media (max-width: 980px) {
  .layout { flex-direction: column; padding: 28px 20px 48px; }
  .sidebar { position: relative; top: 0; width: 100%; max-height: none; margin-bottom: 16px; }
}
@media print {
  .sidebar { display: none; }
  .layout { display: block; }
  .page { max-width: 100%; }
}
```

```js
/* smooth scroll + scrollspy highlight */
(function() {
  var sidebarLinks = document.querySelectorAll('.sidebar a[href^="#"]');
  sidebarLinks.forEach(function(a) {
    a.addEventListener('click', function(e) {
      var href = a.getAttribute('href');
      if (href === '#top') { e.preventDefault(); window.scrollTo({top: 0, behavior: 'smooth'}); return; }
      var target = document.querySelector(href);
      if (target) { e.preventDefault(); target.scrollIntoView({behavior: 'smooth', block: 'start'}); }
    });
  });
  var sections = document.querySelectorAll('main .section-divider[id], main [id^="c"]');
  var linkMap = {};
  sidebarLinks.forEach(function(a) {
    var h = a.getAttribute('href');
    if (h && h.length > 1) linkMap[h] = a;
  });
  function clearActive() {
    sidebarLinks.forEach(function(a) { a.classList.remove('active'); });
  }
  function setActive(id) {
    clearActive();
    var link = linkMap['#' + id];
    if (link) link.classList.add('active');
  }
  if ('IntersectionObserver' in window) {
    var io = new IntersectionObserver(function(entries) {
      entries.forEach(function(en) {
        if (en.isIntersecting && en.intersectionRatio > 0.15) setActive(en.target.id);
      });
    }, {rootMargin: '-20% 0px -60% 0px', threshold: [0, 0.15, 0.5, 1]});
    sections.forEach(function(s) { if (s.id) io.observe(s); });
  }
})();
```

Notes:
- Add `[id] { scroll-margin-top: 16px; }` and `html { scroll-behavior: smooth; }` globally so anchor jumps land with breathing room.
- The `.sub` class indents sub-entries (per-module lessons); remove it for flat nav.
- The bottom `.actions` pair (primary + secondary button) works for any CTA: print/save, contact, sign in, etc.
- This component pairs with #1 Masthead and #8 Footer to form a complete long-document template.
