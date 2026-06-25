<p align="center">
  <img src="https://img.shields.io/badge/Claude%20Code-Skill-4F46E5?logo=anthropic" alt="Claude Code Skill">
  <img src="https://img.shields.io/badge/license-MIT-green" alt="License: MIT">
  <img src="https://img.shields.io/badge/design%20system-v2.1-4F46E5" alt="Design System v2.1">
  <img src="https://img.shields.io/badge/deps-zero-success" alt="Zero Dependencies">
  <img src="https://img.shields.io/badge/philosophy-don't%20compress%2C%20reorganize-blueviolet" alt="Don't compress, reorganize">
</p>

<h1 align="center">md-readable</h1>
<p align="center"><strong>Not a converter. A readability layer.</strong> It reads your agent's argument, then rebuilds it spatially.</p>

<p align="center">
  <em>English · <a href="#中文">中文</a></em>
</p>

---

## The Problem

You're discussing something with an AI agent. It responds with 3,000 words of Markdown. You stare at the wall of text. You don't know where the conclusion is. You can't tell what's a key premise and what's a footnote. You can't follow its thinking. So you can't give good feedback. The conversation degrades. The task suffers.

**The bottleneck in human-agent collaboration isn't the agent's intelligence — it's the interface.** Agent outputs are linear. Human reading is spatial. `md-readable` bridges that gap.

---

## The Trend

In 2025, [Thariq Shihipar](https://x.com/thariqshihipar) (Claude Code team, Anthropic) published *"The Unreasonable Effectiveness of HTML"* — arguing that Markdown collapses past 100 lines and AI agents should output HTML instead. 950,000+ views. The ecosystem took notice.

**He's right.** But he left a question open: **what kind of HTML?**

Wrapping linear Markdown in `<h2>` tags doesn't make it readable. It's the same wall of text — now with angle brackets. Real readability needs three things no syntax converter provides:

1. **Semantic reorganization** — knowing whether a heading is a conclusion, a premise, or a topic label
2. **Compensation mechanisms** — for the specific cognitive defects of AI-generated text
3. **A design system built on first principles** — not someone's aesthetic preference

`md-readable` is the answer to "what kind of HTML." It picks up where Shihipar's argument ends.

> **The md-to-html movement needs a standard. This is it.**

## What It Does

`md-readable` is a [Claude Code](https://claude.ai/code) skill that unpacks agent-generated Markdown into a scannable, three-layer spatial HTML view. **Every word preserved. Nothing compressed.** The only thing that changes is the container.

> **Not a Markdown-to-HTML converter. A readability layer that reorganizes content around how humans actually consume information — so you can follow the agent's thinking and keep the conversation productive.**

---

## Why Agent Output Is Hard to Read

AI-generated text has three structural defects that make it exhausting:

| Problem | Cognitive Reason | What md-readable does |
|---------|------------------|----------------------|
| **Intention Deficit** — is this a conclusion, a premise, or speculation? The agent didn't make that choice consciously | Kintsch (1988): reading = building a situation model; cost rises exponentially with length | **SCQA Signal Card + Confidence Markers** — Layer 1 provides the intent signal the agent couldn't |
| **Predictability Fatigue** — agent text is over-smooth; no surprises, no rhythm, attention collapses | Pirolli & Card (1999): humans forage for "information scent" — we don't read linearly | **Premise-Flip Conditions + Contrast Tables** — Layers 1 & 2 surface contradictions, uncertainty, alternatives |
| **Verification Burden** — you're simultaneously trying to understand AND fact-check, competing for the same working memory | Larkin & Simon (1987): spatial encoding reduces search cost to zero | **Source Tracing + Layer 3** — every claim tagged with confidence and sources; verify on demand |

---

## The Three-Layer Architecture

| Layer | What It Does | Reader Time |
|-------|-------------|-------------|
| **Signal Card** | SCQA structure, core conclusion, key metrics (≤3), premise-flip conditions, confidence level | 3 seconds |
| **Reasoning Blocks** | Each claim gets its own block: assertion title, visible summary, expandable full reasoning with sources | 2–15 minutes (selective) |
| **Verification** | Sources, limitations, alternatives — collapsed by default | On demand |

---

## Installation

### Prerequisites
- [Claude Code](https://claude.ai/code) installed and configured

### Install

```bash
git clone https://github.com/lyydggyxs-cmd/md-readable.git ~/.claude/skills/md-readable/
```

**Zero dependencies.** No pip. No brew. No npm. The agent does the work — the skill just tells it what standard to meet.

### Usage

In Claude Code:

```
/md-readable path/to/report.md    → outputs report.html next to source
"This is too dense, make it readable"
"Agent又输出了一大段MD，帮我看看"
```

Or describe what you're facing:

```
"I can't read this wall of text from the agent — make it readable"
"Unpack this analysis so I can actually follow what it's saying"
"Agent说的太密了，帮我拆开看看"
```

The skill outputs `<original-filename>.html` in the same directory.

It also knows when NOT to convert — and will tell you.

---

## Why This, Not That

The md-to-html movement is having its moment. But not all HTML is created equal. Here's where you go for what:

| Tool | What It Excels At | What's Missing |
|------|------------------|----------------|
| **Pandoc** | Syntax-level conversion. Fast, deterministic. | Zero semantic understanding. An `<h2>` stays an `<h2>` — it doesn't know if that heading is a conclusion, a premise, or a topic label. Pandoc makes valid HTML. It doesn't make readable HTML. |
| **[md2html](https://github.com/haidang1810/md2html)** | Beautiful document presentation. Mermaid diagrams, timelines, callouts, multi-language. Great for specs and plans. | Designed for *documentation*, not *reading agent output*. No SCQA extraction, no confidence markers, no premise-flip conditions. Content stays linear — it just looks better. |
| **[huashu-md-html](https://github.com/alchaincyf/huashu-md-html)** | Full pipeline: anything→md→html/docx. 4 themes, anti-AI-slop design. Great for publishing workflows. | Heavy external dependencies (pandoc, markitdown, python-docx). Template-driven — doesn't semantically analyze your content. |
| **This skill (md-readable)** | **The standard for what md-to-html should be.** SCQA extraction, confidence encoding, premise-flip conditions, source tracing. Three compensation mechanisms for AI text fatigue — so you can follow the thinking and respond usefully. | Not for narratives, API docs, or pure data tables (and it'll tell you when not to use it). |

**Publishing a book → huashu. Documenting a system design → md2html. Trying to understand what your agent is actually saying so you can give it good feedback → md-readable.**

---

## Design System

Built on **10 cross-domain first principles** (not aesthetic preference), derived from PPT design, web UI, app UI, editorial typography, and Chinese long-form reading:

| # | Principle | System Constraint |
|---|-----------|-------------------|
| P1 | Assertion-First | Every section title is a complete claim — never a topic label |
| P2 | One Container, One Claim | "And" in a heading → split into two blocks |
| P3 | Progressive Disclosure | Non-critical details in expandable `<details>` with "information scent" labels |
| P4 | Spatial Encoding > Visual Marking | Proximity beats similarity. Unrelated = separated |
| P5 | Three-Level Visual Hierarchy | Squint test: the 3 loudest elements ARE the 3 most important |
| P6 | Whitespace as Active Element | If spacing feels adequate — double it |
| P7 | Monochrome + One Accent | 60% white, 30% structural gray, 10% accent on ≤2 elements |
| P8 | Signal-to-Noise Maximization | Every CSS rule must convey information. No gradients, no decoration |
| P9 | Content Rhythm | Max 2 consecutive reasoning blocks at same density → insert visual break |
| P10 | Systematic → Inevitable | Every value traces to a CSS token. Zero ad-hoc values |

Full design system spec: [`references/design-system.md`](references/design-system.md)

---

## Project Structure

```
~/.claude/skills/md-readable/
├── SKILL.md                      # Skill definition (what the agent reads)
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

If this skill saved you from staring at another wall of agent output — share what you built with it. Good examples help more than good code.

---

## License

MIT © 2026

## Credits

Built as a Claude Code skill. Design system informed by Tufte (*Envisioning Information*), Minto (*The Pyramid Principle*), Krug (*Don't Make Me Think*), Nielsen Norman Group research, and Peirce's semiotics.

The three-compensation-mechanism framework is original — derived from cognitive science (Kintsch, Pirolli & Card, Larkin & Simon) applied to the specific problem of AI-generated agent output.

---

## <a name="中文"></a>中文

## 问题

你跟 agent 讨论一件事。它回了 3000 字 Markdown。你对着文本墙发呆。找不到结论在哪。分不清哪个是关键前提、哪个是注释。跟不上它在想什么。所以给不出好反馈。对话质量下降。任务受影响。

**人机协作的瓶颈不是 agent 的智能——是信息呈现。** Agent 产出是线性的，人阅读是空间化的。`md-readable` 搭了这座桥。

---

## 行业正在觉醒

2025 年，Anthropic Claude Code 团队的 Thariq Shihipar 发表了 [《HTML 的不合理有效性》](https://x.com/thariqshihipar)，论证 Markdown 超过 100 行就崩了，AI agent 应该直接输出 HTML。95 万次观看，整个生态在跟进。

**他说得对。**但他留下了一个问题没人回答：**什么样的 HTML？**

把线性 Markdown 包上 `<h2>` 标签不解决可读性。只是同一堵文本墙——多了角标。真正的可读性需要三个东西，纯语法转换工具一个都没有：

1. **语义重组**——知道一个标题是结论、前提、还是话题标签
2. **补偿机制**——针对 AI 文本三种结构性缺陷的专门设计
3. **第一性原则驱动的设计系统**——不是谁的审美偏好

`md-readable` 回答了这个"什么样的 HTML"的问题。

> **md-to-html 运动需要标准。我们就是。**

## 这是什么

`md-readable` 是一个 Claude Code 技能，把 agent 生成的 Markdown 展开成可扫读的三层空间 HTML——**不删除、不压缩任何内容**，只改变组织方式。让你能跟得上 agent 的思考，让对话继续推进。

> 这不是 Markdown-到-HTML 转换器。这是一个可读层——重新组织信息，让人真正能读下去、理解、给 feedback。

## 为什么 agent 输出难读

AI 文本有三种结构性缺陷：

| 问题 | 认知原因 | 怎么补偿 |
|------|---------|---------|
| **意图缺位** — 这段话是结论、前提、还是推测？agent 没有在结构上区分 | 人脑默认每一句话都有选择意图 | SCQA 信号卡 + 置信度标记 |
| **可预测性疲劳** — agent 文本太"顺"了，没有节奏，看几段就走神 | 人是信息觅食者，靠"气味"扫描 | 翻转前提 + 对比表，制造认知张力 |
| **验证负担** — 你一边想理解、一边还要判断 agent 说得对不对，工作记忆不够用 | 信息搜索成本和理解成本争夺同一认知资源 | 来源追溯 + Layer 3 折叠，验证变按需 |

## 安装

```bash
git clone https://github.com/lyydggyxs-cmd/md-readable.git ~/.claude/skills/md-readable/
```

**零依赖。** 不 pip，不 brew，不 npm。Agent 做转换——skill 只告诉它什么标准算好。

## 用法

在 Claude Code 里：

```
/md-readable report.md
"Agent 这输出太密了，让我能看进去"
"帮我 unpack 一下这个分析"
```

输出 `<原文件名>.html`，放回原 MD 目录。

不合适的内容会主动告知不转——这是 skill 的一部分，不是 bug。

## 设计系统

基于 10 条跨领域第一性原则（PPT × Web × App UI × 编辑排版 × 中文长文），不是审美偏好。详见 [`references/design-system.md`](references/design-system.md)。

核心原则：**不压缩信息，重组信息。**

## License

MIT © 2026

---

<p align="center">
  <sub>If this skill made one wall of agent text readable, ⭐ the repo — it helps others escape the wall too.</sub>
</p>
