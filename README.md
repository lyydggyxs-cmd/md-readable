<p align="center">
  <img src="https://img.shields.io/badge/Claude%20Code-Skill-4F46E5?logo=anthropic" alt="Claude Code Skill">
  <img src="https://img.shields.io/badge/license-MIT-green" alt="License: MIT">
  <img src="https://img.shields.io/badge/design%20system-v2.1-4F46E5" alt="Design System v2.1">
  <img src="https://img.shields.io/badge/deps-zero-success" alt="Zero Dependencies">
  <img src="https://img.shields.io/badge/philosophy-don't%20compress%2C%20reorganize-blueviolet" alt="Don't compress, reorganize">
</p>

<h1 align="center">md-to-html</h1>
<p align="center"><strong>Markdown → Human-Friendly HTML Briefings</strong></p>
<p align="center">AI generates in 3 seconds. Humans shouldn't need 30 minutes to read it.</p>

<p align="center">
  <em>English · <a href="#中文">中文</a></em>
</p>

---

## What It Does

**md-to-html** is a [Claude Code](https://claude.ai/code) skill that transforms AI-generated Markdown reports into scannable, human-friendly HTML briefings — **without removing or summarizing any content**.

> **Not a Markdown-to-HTML converter. An analyzer that reorganizes content around how humans actually consume information.**

### See It in Action

<p align="center">
  <em>📸 Before (Markdown wall of text) → After (Spatial briefing you can scan in 3 seconds)</em>
  <br>
  <sub>Open <a href="examples/ai-document-crisis.html"><code>examples/ai-document-crisis.html</code></a> in your browser for the full experience.</sub>
</p>

---

## Why This Exists

**Thariq Shihipar** (Claude Code team, Anthropic) lit a fire under the ecosystem with *"The Unreasonable Effectiveness of HTML"* — arguing that Markdown collapses past 100 lines and AI agents should output HTML instead. 950,000+ views on X. He's right.

But there's a deeper problem Shihipar's argument implies but doesn't solve:

**AI text has three structural defects that HTML alone doesn't fix:**

| AI Text Problem | Cognitive Reason | Our Solution |
|----------------|------------------|--------------|
| **Intention Deficit** — readers assume every sentence has a purpose, but LLM output is statistical prediction without selective intent | Kintsch (1988): reading = building a situation model; cost rises exponentially with length | **SCQA Signal Card + Confidence Markers** — Layer 1 provides the intent signal the LLM couldn't |
| **Predictability Fatigue** — over-smooth text fails to maintain attentional arousal; no surprises, no rhythm | Pirolli & Card (1999): humans are information foragers — we scan for "scent," not read linearly | **Premise-Flip Conditions + Contrast Tables** — Layer 1 & 2 actively expose contradictions, uncertainty, alternatives |
| **Verification Burden** — readers must simultaneously comprehend AND fact-check AI output, competing for the same working memory | Larkin & Simon (1987): diagrams encode relationships spatially, reducing search cost to zero | **Source Tracing + Layer 3 Verification** — every claim tagged with confidence and sources; verify on demand, not in parallel |

HTML gives you a better container. **Three-layer spatial architecture** gives you what the container should hold. That's what this skill does.

---

## The Three-Layer Architecture

| Layer | What It Does | Reader Time |
|-------|-------------|-------------|
| **Signal Card** | SCQA structure, core conclusion, key metrics (≤3), premise-flip conditions, confidence level | 3 seconds |
| **Reasoning Blocks** | Each claim gets its own block: assertion title, visible summary, expandable full reasoning with sources | 2–15 minutes (selective) |
| **Verification** | Sources, limitations, alternatives — collapsed by default | On demand |

> **Core philosophy:** This is NOT a summarization tool. Every word from the original Markdown is preserved. The only thing that changes is the container.

---

## Why This, Not That

| Tool | What It Excels At | When It's Not Enough |
|------|------------------|---------------------|
| **Pandoc** | Syntax-level conversion. Fast, deterministic. | Zero semantic understanding. A `<h2>` stays a `<h2>` — it doesn't know if that heading is a conclusion, a premise, or a topic label. |
| **[md2html](https://github.com/haidang1810/md2html)** | Beautiful document presentation. Mermaid diagrams, timelines, callouts, multi-language. Great for specs and plans. | Designed for *documentation*, not *analysis reports*. No SCQA extraction, no confidence markers, no premise-flip conditions. Content stays linear — it just looks better. |
| **[huashu-md-html](https://github.com/alchaincyf/huashu-md-html)** | Full pipeline: anything→md→html/docx. 4 themes, anti-AI-slop design. Great for publishing workflows. | Heavy external dependencies (pandoc, markitdown, python-docx). Template-driven — doesn't semantically analyze your content. |
| **This skill (md-to-html)** | **Semantic reorganization of analytical content.** SCQA extraction, confidence encoding, premise-flip conditions, source tracing. Three compensation mechanisms for AI text fatigue. | Not for narratives, API docs, or pure data tables (and it'll tell you when not to use it). |

**If you're publishing a book → huashu. If you're documenting a system design → md2html. If you need to actually get people to read and think about your AI's analysis → this skill.**

---

## Installation

### Prerequisites
- [Claude Code](https://claude.ai/code) installed and configured

### Install

```bash
git clone https://github.com/lyydggyxs-cmd/md-to-html.git ~/.claude/skills/md-to-html/
```

**Zero dependencies.** No pip. No brew. No npm. Claude does the work — the skill just tells it what standard to meet.

### Usage

In Claude Code:

```
/md-to-html path/to/report.md    → outputs report.html next to source
"Make this readable"
"生成HTML简报" / "把这个转成HTML"
```

Or point and describe:

```
"Convert this analysis to HTML — I can't read another wall of Markdown"
"Generate a briefing from this research report"
```

The skill outputs `<original-filename>.html` in the same directory.

It also knows when NOT to convert — and will tell you.

---

## Design System

Built on **10 cross-domain first principles** (not aesthetic preference), derived from a cross-domain study of PPT design, web UI, app UI, editorial typography, and Chinese long-form reading:

| # | Principle | System Constraint |
|---|-----------|-------------------|
| P1 | Assertion-First | Every section title is a complete claim — never a topic label |
| P2 | One Container, One Claim | "And" in a heading → split into two blocks |
| P3 | Progressive Disclosure | Non-critical details in expandable `<details>` with "information scent" labels |
| P4 | Spatial Encoding > Visual Marking | 2024 eye-tracking confirms proximity beats similarity. Unrelated = separated |
| P5 | Three-Level Visual Hierarchy | Squint test: the 3 loudest elements ARE the 3 most important |
| P6 | Whitespace as Active Element | If spacing feels adequate — double it. Whitespace isn't empty, it's the container that separates ideas |
| P7 | Monochrome + One Accent | 60% white, 30% structural gray, 10% accent on ≤2 elements |
| P8 | Signal-to-Noise Maximization | Every CSS rule must convey information. No gradients, no decorative elements |
| P9 | Content Rhythm | Max 2 consecutive reasoning blocks at same density → insert visual break (comparison table, inference chain, key quote) |
| P10 | Systematic → Inevitable | Every spacing, font-size, and color value traces to a CSS token. Zero ad-hoc values |

Full design system spec: [`references/design-system.md`](references/design-system.md)

### What's Forbidden (Signal-to-Noise Audit)

These are explicitly **forbidden** to preserve signal-to-noise ratio. Each serves a specific design principle:

- ❌ Gradients of any kind (P8: elements that don't convey information)
- ❌ Border-radius > 12px (P8 + P7: distracts from the single accent color)
- ❌ Emoji as heading/CTA decoration (P8: emoji are emotional markers, not information architecture)
- ❌ External fonts or icon libraries (P10: breaks self-containment)
- ❌ Animations beyond 150ms hover transitions (P8 + accessibility)
- ❌ Decorative borders, dividers, background colors (P8)
- ❌ Ad-hoc spacing or font-size values outside the token scale (P10)
- ❌ Important content in the bottom-right corner (visual dead zone: F-pattern endpoint)
- ❌ `#000000` for body text — use `#333333` (screen readability + Chinese typography)

---

## Project Structure

```
~/.claude/skills/md-to-html/
├── SKILL.md                      # Skill definition (what Claude reads)
├── README.md                     # You are here
├── references/
│   └── design-system.md          # CSS tokens, component templates, full HTML skeleton
└── examples/
    ├── ai-document-crisis.md     # Example input (~3,000 words)
    └── ai-document-crisis.html   # Example output (same words, spatial layout)
```

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Issues and PRs welcome.

If you've built something with this skill — a research briefing, a decision memo, a competitive analysis — share the output. Good examples help more than good code.

---

## License

MIT © 2026

## Credits

Built as a Claude Code skill. Design system informed by Tufte (*Envisioning Information*), Minto (*The Pyramid Principle*), Krug (*Don't Make Me Think*), Nielsen Norman Group research, and Peirce's semiotics.

The three-compensation-mechanism framework is original — derived from cognitive science (Kintsch, Pirolli & Card, Larkin & Simon) applied to the specific problem of AI-generated analytical text.

---

## <a name="中文"></a>中文

## 这是什么

**md-to-html** 是一个 Claude Code 技能，将 AI 生成的 Markdown 分析报告转化为人类可扫读的 HTML 简报——**不删除、不压缩任何内容**。

> 这不是 Markdown-to-HTML 转换器。这是一个分析器——它重新组织内容，让人类真正读完 AI 的分析。

## 为什么需要这个

Anthropic Claude Code 团队的 **Thariq Shihipar** 提出了 *"HTML 的不可理喻的有效性"*——Markdown 超过 100 行就崩溃了，AI 应该输出 HTML。观点在 X 上 95 万阅读。他是对的。

但 HTML 只是容器。AI 文本有三种结构性缺陷——意图缺位、可预测性疲劳、验证负担——HTML 本身解决不了。**三层空间架构**通过 SCQA 信号卡、置信度编码、翻转前提、来源追溯来补偿这三种缺陷。

## 为什么选这个，不是其他

| 工具 | 适合什么 | 不适合什么 |
|------|---------|----------|
| Pandoc | 语法级转换，快且确定 | 零语义理解——它不知道 h2 是结论还是话题标签 |
| md2html | 漂亮的文档展示，Mermaid/时间线/注释 | 文档不是分析报告——没有 SCQA，没有置信度 |
| huashu-md-html | 全流水线出版，万物→md→html/docx | 重依赖（pandoc/markitdown），模板驱动不是语义分析 |
| **这个 skill** | **分析性内容的语义重组**——SCQA 提取、置信度编码、翻转前提、来源追溯 | 不是给叙事，不是给 API 文档（而且会主动告诉你） |

**出书 → huashu。写系统设计文档 → md2html。让人真正读完并思考 AI 的分析 → 这个 skill。**

## 安装

```bash
git clone https://github.com/lyydggyxs-cmd/md-to-html.git ~/.claude/skills/md-to-html/
```

**零依赖。** 不 pip，不 brew，不 npm。Claude 做转换——skill 只告诉它什么标准算好。

## 设计系统

基于 10 条跨领域第一性原则（PPT × Web × App UI × 编辑排版 × 中文长文），不是审美偏好。详见 [`references/design-system.md`](references/design-system.md)。

核心原则：**不压缩信息，重组信息。**

## License

MIT © 2026

---

<p align="center">
  <sub>If this skill saved you from one more dense wall of AI-generated Markdown, ⭐ the repo — it helps others find it too.</sub>
</p>
