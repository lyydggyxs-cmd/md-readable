<p align="center">
  <img src="https://img.shields.io/badge/Claude%20Code-Skill-4F46E5?logo=anthropic" alt="Claude Code Skill">
  <img src="https://img.shields.io/badge/license-MIT-green" alt="License: MIT">
  <img src="https://img.shields.io/badge/design%20system-v2.0-4F46E5" alt="Design System v2.0">
</p>

<h1 align="center">md-to-html</h1>
<p align="center"><strong>Markdown → Human-Friendly HTML Briefings</strong></p>
<p align="center">AI generates in seconds. Humans shouldn't need 30 minutes to read it.</p>

<p align="center"><em>English · <a href="#中文">中文</a></em></p>

---

## What It Does

**md-to-html** is a [Claude Code](https://claude.ai/code) skill that transforms AI-generated Markdown reports into scannable, human-friendly HTML briefings — **without removing or summarizing any content**.

### The Problem

AI produces a 3,000-word analysis in 3 seconds. A human needs 15–30 minutes to read it. That's **6 orders of magnitude** of encoding-cost asymmetry. Most AI output gets skimmed, misread, or ignored — not because it's low quality, but because linear Markdown forces a single reading path that nobody follows.

### The Solution

A **three-layer spatial architecture** that reorganizes — but doesn't compress — analytical content:

| Layer | What It Does | Reader Time |
|-------|-------------|-------------|
| **Signal Card** | SCQA structure, core conclusion, key metrics, premise-flip conditions | 3 seconds |
| **Reasoning Blocks** | Each claim gets its own block: assertion title, visible summary, expandable full reasoning | 2–15 minutes (selective) |
| **Verification** | Sources, limitations, alternatives — collapsed by default | On demand |

> **Key philosophy:** This is NOT a summarization tool. Every word from the original Markdown is preserved. The only thing that changes is the container.

## Quick Demo

Open [`examples/ai-document-crisis.html`](examples/ai-document-crisis.html) in your browser to see the output.

| Before (Markdown) | After (HTML Briefing) |
|---|---|
| [`ai-document-crisis.md`](examples/ai-document-crisis.md) — 3,000 words, linear, single reading path | [`ai-document-crisis.html`](examples/ai-document-crisis.html) — Same 3,000 words, spatial, multi-entry-point |

The HTML file opens with a signal card that tells you the conclusion in 3 seconds. You can scan, jump to sections, and drill into details on demand. All content is there — just organized for how humans actually read.

## Installation

### Prerequisites
- [Claude Code](https://claude.ai/code) installed and configured

### Install via GitHub

```bash
# Clone this repo into your Claude Code skills directory
git clone https://github.com/lyydggyxs-cmd/md-to-html.git ~/.claude/skills/md-to-html/
```

### Or: add as a project skill

```bash
git clone https://github.com/lyydggyxs-cmd/md-to-html.git .claude/skills/md-to-html/
```

### Usage

In Claude Code, just point to a Markdown file:

```
/md-to-html path/to/report.md
```

Or describe what you want:

```
"Convert this analysis to HTML" / "生成HTML简报"
"Make this readable" / "让这个可读"
"Generate a briefing from this report"
```

The skill outputs `<original-filename>.html` in the same directory.

## Design System

The skill uses a **v2.0 design system** built on 10 cross-domain first principles (not aesthetic preference):

| # | Principle | System Constraint |
|---|-----------|-------------------|
| 1 | Assertion-First | Every section title is a complete claim — never a topic label |
| 2 | One Container, One Claim | "And" in a heading → split into two blocks |
| 3 | Progressive Disclosure | Non-critical details in expandable `<details>` sections |
| 4 | Spatial Encoding | Related elements physically close; unrelated separated |
| 5 | Visual Hierarchy | Squint test: loudest 3 elements = most important 3 |
| 6 | Whitespace as Active Element | All spacing values from a 4px-base token scale |
| 7 | Monochrome + One Accent | 60% white, 30% gray, 10% accent on ≤2 elements |
| 8 | Signal-to-Noise | No gradients, no animations, no decorative elements |
| 9 | Content Rhythm | Max 2 consecutive reasoning blocks → insert visual break |
| 10 | Systematic | Every value is a CSS variable; zero ad-hoc values |

Full design system spec: [`references/design-system.md`](references/design-system.md)

## What's Forbidden (By Design)

These are explicitly **forbidden** to preserve signal-to-noise ratio:

- ❌ Gradients of any kind
- ❌ Border-radius > 12px
- ❌ Emoji as heading/CTA decoration
- ❌ External fonts or icon libraries
- ❌ Animations (except 150ms hover transitions)
- ❌ Decorative borders, dividers, or background colors
- ❌ Ad-hoc spacing or font-size values outside the token scale
- ❌ Important content in the bottom-right corner (visual dead zone)

## Why This Matters

Most "markdown to HTML" tools are template engines — they wrap your content in a pretty layout but keep the linear structure. **md-to-html** is different: it *reorganizes* content around how humans actually consume information, not how AI generates it.

If you use Claude Code to produce analysis — research reports, market scans, decision memos, competitive analysis — this skill makes that analysis actually get read.

---

## <a name="中文"></a>中文

## 这是什么

**md-to-html** 是一个 Claude Code 技能，将 AI 生成的 Markdown 报告转化为人类友好的、可扫读的 HTML 简报——**不删除、不压缩任何内容**。

### 解决的问题

AI 用 3 秒生成 3000 字分析。人类需要 15-30 分钟阅读。这就是 **6 个数量级**的编码成本不对称。大多数 AI 产出被略过、误读或忽略——不是因为质量差，而是因为线性 Markdown 强制单一阅读路径，而没有人会那样读。

### 核心架构：三层信息模型

| 层 | 功能 | 阅读时间 |
|---|------|---------|
| **信号卡** | SCQA 结构、核心结论、关键指标、翻转前提 | 3 秒定位 |
| **推理块** | 每个主张独立容器：断言标题、可见摘要、可展开的完整推理 | 选择性深入 |
| **验证层** | 来源引用、局限性、替代方案——默认折叠 | 按需查阅 |

> **核心理念：** 这不是摘要工具。源 Markdown 的每个字都保留。唯一改变的是容器。

## 快速演示

在浏览器中打开 [`examples/ai-document-crisis.html`](examples/ai-document-crisis.html) 查看输出效果。

## 安装

```bash
git clone https://github.com/lyydggyxs-cmd/md-to-html.git ~/.claude/skills/md-to-html/
```

## 使用

```
/md-to-html path/to/report.md
"生成HTML简报"
"把这个转成HTML"
```

## 设计与原则

基于 10 条跨领域第一性原则（非审美偏好）的设计系统。详见 [`references/design-system.md`](references/design-system.md)。

---

## License

MIT © 2026

## Credits

Built as a Claude Code skill. Design system heavily informed by Tufte, Minto (Pyramid Principle), Krug (Don't Make Me Think), and Nielsen Norman Group research.

---

<p align="center">
  <sub>If this skill saved you from reading one more dense wall of Markdown text, consider giving it a ⭐</sub>
</p>
