# 公报.skill · gazette-skill

> 把 Agent 变成一名古典公报编辑 / 老钱金融大报设计师。

---

## 这是什么

`gazette-skill` 是一个符合 [agentskills.io](https://agentskills.io) 开放规范的 AI Agent 技能包。
安装后，你的 Agent 将具备 **"现代古典报纸 + 金融数据密度"** 风格的完整网站设计与 HTML 报告生成能力——
从报头组件到列表页、从排行表到文章页，全流程一体化输出 **FT / Economist / Monocle / WSJ 数字版** 视觉语言的 HTML。

视觉参考：[findmymoat.com](https://www.findmymoat.com)（仅作 reference，不绑品牌）。

---

## 它能做什么

| # | 能力 | 产出 |
|---|---|---|
| 1 | **网站首页设计** | Masthead + 三栏布局 + 城堡线描 + 搜索框 + 迷你排行 |
| 2 | **Curated Directory 列表页** | 两列网格卡片（logo + 名字 + 标签 pills + 投票 + 操作） |
| 3 | **排行榜表格页** | 密集表格（小标大写宽字距 + 衬线数字 + 涨跌色） |
| 4 | **文章页** | 双行超大标题 + 斜体副标 + drop cap 首字下沉 + section divider |
| 5 | **中文化重建** | 中文报纸风（思源宋体 + 宽字距替代大写 + 宣纸米色 + 红涨绿跌） |
| 6 | **起始模板复用** | `assets/starter-template.html` 一键起步，含昼夜主题切换 |

---

## 何时触发

> gazette 风格、大报风格、报纸风格网站、金融数据型网站、古典金融、老钱感、复古衬线网站、投研工具网站、Curated Directory 风格、broadsheet style、editorial finance style、FT style、Economist style、Monocle style、legacy finance style、old money aesthetic、classical gazette、financial broadsheet……

---

## 核心输出风格

输出使用 **古典公报 / 金融大报** 视觉语言：

- 🎨 近单色纪律：纯白 `#FFFFFF` + 纯黑 `#000000` + 中灰 `#6B6B6B`（唯一彩色：浅绿/浅红用于涨跌）
- 📜 Playfair Display 粗衬线大标题 + Source Serif Pro 正文（中文：思源宋体 Heavy + Regular）
- 📋 Masthead 报头：`VOL. XCIV, NO. 247` + 黑色日期横条 + 三等距标签
- 📊 密集表格：小标全大写宽字距 + 衬线粗体数字 + tabular-nums
- ✒️ Drop cap 首字下沉 4.5x（中文 3x）+ ★ 装饰星号 + 黑白线描插画
- 🌗 内置昼夜主题切换按钮（右上角固定定位，localStorage 持久化）

---

## 快速上手

### 在 Claude / WorkBuddy 中使用

1. 下载 `gazette-skill/` 文件夹，放入 `~/.claude/skills/` 或 `~/.workbuddy/skills/`。
2. 重启客户端，向 Agent 说：**"帮我做个投研工具网站"** 或 **"用 gazette 风格生成这份报告的 HTML"**，技能自动触发。

### 在 OpenClaw / Hermes 中使用

1. 将 `gazette-skill/` 放入 `skills/` 目录。
2. 通过 `skill_view` 查看 SKILL.md 加载。

### 在 SkillHub 中使用

1. 打包：`zip -r gazette-skill.zip gazette-skill/`
2. 登录 SkillHub，点击"上传 Skill"，选择 zip 文件。

---

## 目录结构（7 件文件 · 三层架构）

```
gazette-skill/
├── SKILL.md                          # 主路由（必读）
├── CHANGELOG.md                      # 版本日志
├── README.md                         # GitHub 门面
├── LICENSE                           # MIT
├── assets/                           # 🅰️ ASSETS 资产真源
│   ├── starter-template.html         # 可直接复用起始模板（含昼夜切换）
│   ├── screenshot-home.png           # 参考网站首页截图
│   └── screenshot-ranking.png        # 参考网站排行页截图
└── references/                       # 📚 REFERENCES 具体规范
    ├── design-system.md              # 完整设计系统（字体/配色/布局/视觉）
    ├── localization-zh.md            # 中文化重建规则（中文站必读）
    └── components.md                 # HTML/CSS 组件配方（9 个组件）
```

> 三层架构：**META**（SKILL.md frontmatter）· **ASSETS**（assets/ 资产真源）· **REFERENCES**（references/ 具体规范）。
> SKILL.md 只做路由，能力 SOP 拆到 references/ 省 token。

---

## 六条设计哲学

1. **报纸骨架 + 现代数据**：保留古典报头（VOL.NO. / 日期横条 / 三标签），承载密集金融数据表格。
2. **近单色纪律**：不靠颜色制造层次，靠字体重量、字号、留白说话。唯一彩色仅用于涨跌/投票。
3. **衬线至上**：正文必须衬线（Source Serif Pro / 思源宋体），UI 控件才用无衬线（Inter / PingFang）。
4. **报头不可省**：VOL.NO. + 日期横条 + 三标签缺一不可——少了就不是 gazette，只是"普通衬线网站"。
5. **中英分治**：英文用 Playfair Display，中文必须重建为思源宋体 Heavy（Playfair 无 CJK 字形）。版式规则不能直译——大写失效改宽字距、斜体失效改浅灰、drop cap 缩到 3x。
6. **数字不本地化**：阿拉伯数字始终保留西文衬线（Playfair Display），绝不写"一二三"——这是"印刷品质"的灵魂。

---

## 兼容性

| 平台 | 状态 | 备注 |
|---|---|---|
| Claude Skills | ✅ | 遵循 agentskills.io 规范，frontmatter 覆盖触发词 |
| WorkBuddy | ✅ | 原生支持，含 `agent_created: true` 标记 |
| OpenClaw | ✅ | 通过 clawhub 兼容 |
| Hermes Agent | ✅ | 通过 agentskills.io 标准 |
| SkillHub | ✅ | zip 上传 |

---

## 与 OPC-Studio 其他 skill 协同

`gazette-skill` 是 **视觉风格层** skill，与 OPC-Studio 其他 **业务工作流层** skill 互补：

- 业务 skill（[investor-skill](https://github.com/D-kart/investor-skill) / [ma-pitch-skill](https://github.com/D-kart/ma-pitch-skill) / [summary-skill](https://github.com/D-kart/summary-skill)）产出 HTML 报告时，可选用 `gazette-skill` 提供的视觉风格包装——当报告定位是"严肃投研 / 古典金融 / 老钱感"时尤其契合。
- 业务 skill 自带的视觉令牌（如 investor-skill 的"券商研报范"深蓝米白）与 gazette 的"古典公报"黑白衬线是两种独立视觉语言，按报告调性选择。

---

## 中文化特别说明

做中文网站时，**必须先读 `references/localization-zh.md`**。直接套用英文版会失败：

- Playfair Display 无中文字形 → 必须换思源宋体 Heavy + Regular
- `text-transform: uppercase` 在中文上无效 → 改用宽字距 + 加粗
- `font-style: italic` 在中文上极丑 → 改用浅灰 + 字号变化
- Drop cap 4.5x 在汉字上过重 → 缩到 3x
- 金融场景红涨绿跌（与欧美相反）

文化定位两条路：
- **A. 民国大报路线**（《申报》《大公报》风）——金融/投研产品推荐
- **B. 宋韵刻书路线**（清雅留白）——文化/内容产品推荐

---

## 许可证

MIT License · © 2026 OPC-Studio

---

## 反馈与贡献

- Issue / PR：欢迎在本仓库提交
- 兼容问题：请附上平台名与 Agent 版本号
- 风格扩展：期待更多组件配方（如移动端适配、打印样式、邮件模板）的贡献

---

_OPC-Studio 出品 · 让每个 AI Agent 都能成为行业专家。_
