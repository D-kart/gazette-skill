# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/), and this project adheres to [Semantic Versioning](https://semver.org/).

## [1.1.0] - 2026-08-03

### Added
- references/components.md #10：**Sticky sidebar + scrollspy**（长文档侧边栏导航组件）
  - 左侧 sticky sidebar：品牌 + VOL.NO. + 分组目录（INDEX / 模块分组）+ 底部 CTA 按钮（下载/联系）
  - 平滑滚动锚点跳转：`scrollIntoView({behavior:'smooth'})`，顶部链接平滑回滚
  - IntersectionObserver 滚动高亮：当前章节对应导航项 `.active`（左侧黑色边条）
  - 移动端折叠（<980px 侧栏折回页面顶部）、打印隐藏侧栏
- 全局辅助 CSS：`[id] { scroll-margin-top: 16px }` + `html { scroll-behavior: smooth }`
- SKILL.md 工作流 step 3 注册新组件；Version History 补充 v1.1.0

### Use Cases
- 课程表 / 目录 / 研究报告 / 工具目录等长文档——导航与阅读同步进行
- 与 Masthead（#1）+ Footer（#8）组合构成完整长文档模板

## [1.0.0] - 2026-07-19

### Added
- 首次公开发布
- SKILL.md 主路由（含中英双语触发关键词、OPC-Studio 标准 frontmatter）
- references/design-system.md — 完整设计系统规范（字体/配色/布局/视觉元素/暗色模式）
- references/localization-zh.md — 中文化重建规则（字体重建 / 版式规则映射 / 阅读体验 / 文化定位两条路）
- references/components.md — HTML/CSS 组件配方（9 个组件：Masthead / Topnav / Buttons / Tool Card / Ranking Table / Article Hero / Three-column Grid / Footer / Line Engraving SVG）
- assets/starter-template.html — 可直接复用起始模板（含完整 CSS 变量、Google Fonts CDN、昼夜主题切换、三栏布局、城堡线描）
- assets/screenshot-home.png — 参考网站首页截图
- assets/screenshot-ranking.png — 参考网站排行页截图
- README.md / CHANGELOG.md / LICENSE (MIT) / .gitignore

### Style Positioning
- "Classical gazette + financial broadsheet" — 现代古典报纸 + 金融数据密度
- 视觉参考：findmymoat.com（仅作 reference_site 元数据，不绑品牌）
- 中英双语支持，含完整中文化重建规则

### Compatibility
- Claude Skills / WorkBuddy / OpenClaw / Hermes / SkillHub 五平台兼容
- 遵循 agentskills.io 开放规范
- 纯 HTML/CSS 输出，无运行时依赖
