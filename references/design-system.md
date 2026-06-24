# HTML 简报 Design System v2.0

> 完整 CSS Token 系统、组件模板、HTML 骨架。给 md-to-html skill 使用。

---

## 一、CSS 变量系统（复制到 `<style>` 中）

```css
:root {
  /* ═══════════════ Spacing Scale (4px base) ═══════════════ */
  --space-xs:   4px;    /* 极紧密：图标-标签、同组内紧邻元素 */
  --space-sm:   8px;    /* 紧密：按钮间、标签间、列表项间 */
  --space-md:  16px;    /* 标准：段落间距、卡片内 padding */
  --space-lg:  24px;    /* 宽松：块内段落组间 */
  --space-xl:  32px;    /* 大分隔：推理块之间 */
  --space-2xl: 48px;    /* 超宽：章节间 */
  --space-3xl: 64px;    /* 页面级：信号卡与正文之间 */
  --space-4xl: 96px;    /* 极端：仅用于页面级主要部分间的巨大呼吸 */

  /* ═══════════════ Modular Type Scale (Major Third 1.25) ═══════════════ */
  --text-xs:  0.64rem;   /* ~10px — 源引用、注释 */
  --text-sm:  0.8rem;    /* ~13px — 摘要、标签、meta */
  --text-md:  1rem;      /* 16px — 正文 */
  --text-lg:  1.25rem;   /* 20px — 推理块标题、章节标题 */
  --text-xl:  1.563rem;  /* 25px — 信号卡要点 */
  --text-2xl: 1.953rem;  /* ~31px — 信号卡主标题 */
  --text-3xl: 2.441rem;  /* ~39px — 仅极端强调场景 */

  --leading-tight:  1.25;   /* 标题 */
  --leading-normal: 1.6;    /* 正文 */
  --leading-relaxed: 1.75;  /* 长段落、关键陈述 */
  --measure: 65ch;          /* 最优阅读行宽 */

  /* ═══════════════ Monochrome + One Accent ═══════════════ */
  --color-bg:          #FAFAFA;
  --color-card:         #FFFFFF;
  --color-text:         #333333;  /* 不用纯黑 #000 —— 发光屏上刺眼 */
  --color-text-dim:     #666666;
  --color-text-faint:   #999999;
  --color-border:       #E5E5E5;
  --color-bg-subtle:    #F5F5F5;
  --color-accent:        #4F46E5;
  --color-accent-light:  #EEF2FF;
  --color-accent-hover:  #4338CA;

  /* ═══════════════ Confidence Colors ═══════════════ */
  --confidence-high:    #059669;
  --confidence-mid:     #D97706;
  --confidence-low:     #DC2626;
  --confidence-high-bg: #ECFDF5;
  --confidence-mid-bg:  #FFFBEB;
  --confidence-low-bg:  #FEF2F2;

  /* ═══════════════ Borders & Shadows ═══════════════ */
  --radius-sm: 4px;
  --radius:    8px;
  --radius-lg: 12px;
  --shadow-card:    0 1px 3px rgba(0,0,0,0.06);
  --shadow-elevated: 0 4px 12px rgba(0,0,0,0.08);
}
```

### 60-30-10 色彩分布
- 60% 背景白（`--color-bg` / `--color-card`）
- 30% 结构灰（`--color-border` / `--color-bg-subtle`）
- 10% 强调色（`--color-accent` —— 仅在 ≤ 2 个关键元素上）

### 字体层级映射

| 用途 | Font Size | Line Height | Font Weight |
|------|-----------|-------------|-------------|
| 信号卡主标题 | --text-2xl | --leading-tight | 800 |
| 信号卡要点/章节标题 | --text-lg | --leading-tight | 700 |
| 推理块标题 | --text-lg | --leading-tight | 700 |
| 推理块正文 | --text-md | --leading-normal | 400 |
| 推理块摘要 | --text-sm | --leading-normal | 400 |
| 源引用/注释 | --text-xs | --leading-normal | 400 |
| 表格/数据 | --text-sm | --leading-tight | 400 |

---

## 二、全局 Reset & Body

```css
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "PingFang SC", "Microsoft YaHei", sans-serif;
  font-size: var(--text-md);
  line-height: var(--leading-normal);
  color: var(--color-text);
  background: var(--color-bg);
  max-width: 860px;
  margin: 0 auto;
  padding: var(--space-2xl) var(--space-lg);
  -webkit-font-smoothing: antialiased;
}
```

- 系统字体栈，零外部加载
- 中文优先 PingFang SC（Mac）/ Microsoft YaHei（Win）
- 不要加载 Google Fonts 或任何外部字体

---

## 三、Layer 1：信号卡（SCQA 结构）

### HTML 模板

```html
<header class="signal-card">
  <!-- S: Situation — 共识背景 -->
  <div class="signal-context">
    [1-2 句，建立共识背景]
  </div>

  <!-- C: Complication — 矛盾/变化 -->
  <div class="signal-complication">
    [1-2 句，发生了什么变化或存在什么矛盾]
  </div>

  <!-- Q → A: Question → Answer -->
  <div class="signal-answer">
    <span class="signal-answer-label">结论方向</span>
    <h1>[完整断言句，≤28 字]</h1>
  </div>

  <!-- 关键指标（3 个，最多） -->
  <div class="signal-metrics">
    <div class="signal-metric">
      <span class="metric-value accent">[关键数字]</span>
      <span class="metric-label">[数字含义]</span>
    </div>
    <div class="signal-metric">
      <span class="metric-value">[关键数字]</span>
      <span class="metric-label">[数字含义]</span>
    </div>
    <div class="signal-metric">
      <span class="metric-value">[关键数字]</span>
      <span class="metric-label">[数字含义]</span>
    </div>
  </div>

  <!-- 关键前提与翻转条件（最多 3 条） -->
  <div class="signal-premises">
    <h3>如果以下前提错了，结论会翻转</h3>
    <ul>
      <li><strong>[前提 1]</strong> — 如果错了：[后果]</li>
      <li><strong>[前提 2]</strong> — 如果错了：[后果]</li>
    </ul>
  </div>
</header>
```

### 信号卡 CSS

```css
.signal-card {
  background: var(--color-card);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  padding: var(--space-2xl) var(--space-xl);
  margin-bottom: var(--space-3xl);
  box-shadow: var(--shadow-card);
}
.signal-context {
  font-size: var(--text-sm);
  color: var(--color-text-dim);
  margin-bottom: var(--space-sm);
}
.signal-complication {
  font-size: var(--text-md);
  color: var(--color-text);
  margin-bottom: var(--space-xl);
  line-height: var(--leading-relaxed);
  max-width: var(--measure);
}
.signal-answer {
  margin-bottom: var(--space-xl);
}
.signal-answer-label {
  display: inline-block;
  font-size: 11px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--color-accent);
  background: var(--color-accent-light);
  padding: 2px 10px;
  border-radius: var(--radius-sm);
  margin-bottom: var(--space-sm);
}
.signal-answer h1 {
  font-size: var(--text-2xl);
  font-weight: 800;
  line-height: 1.2;
  letter-spacing: -0.02em;
  max-width: 28ch;
}
.signal-metrics {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--space-lg);
  margin-bottom: var(--space-xl);
  padding: var(--space-lg);
  background: var(--color-bg-subtle);
  border-radius: var(--radius);
}
.signal-metric {
  text-align: center;
}
.metric-value {
  display: block;
  font-size: var(--text-xl);
  font-weight: 800;
  line-height: 1.2;
  letter-spacing: -0.02em;
}
.metric-value.accent {
  color: var(--color-accent);
}
.metric-label {
  display: block;
  font-size: var(--text-xs);
  color: var(--color-text-faint);
  margin-top: var(--space-xs);
}
.signal-premises {
  padding-top: var(--space-lg);
  border-top: 1px solid var(--color-border);
}
.signal-premises h3 {
  font-size: var(--text-sm);
  font-weight: 600;
  color: var(--color-text-dim);
  margin-bottom: var(--space-sm);
}
.signal-premises ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: var(--space-sm);
}
.signal-premises li {
  font-size: var(--text-sm);
  color: var(--color-text-dim);
  line-height: var(--leading-normal);
  padding-left: var(--space-md);
  position: relative;
}
.signal-premises li::before {
  content: "⚠";
  position: absolute;
  left: 0;
  font-size: var(--text-sm);
}

@media (max-width: 600px) {
  .signal-metrics { grid-template-columns: 1fr; gap: var(--space-md); }
  .signal-card { padding: var(--space-lg); }
}
```

---

## 四、阅读导航

```html
<nav class="reading-nav">
  <span class="nav-hint">跳转：</span>
  <a href="#section-1">[章节名]</a>
  <a href="#section-2">[章节名]</a>
  <a href="#section-3">[章节名]</a>
  <a href="#section-4">[章节名]</a>
</nav>
```

```css
.reading-nav {
  display: flex;
  gap: var(--space-sm);
  flex-wrap: wrap;
  margin-bottom: var(--space-3xl);
  padding: 0 var(--space-sm);
}
.reading-nav a {
  font-size: var(--text-sm);
  color: var(--color-accent);
  text-decoration: none;
  padding: var(--space-xs) var(--space-md);
  background: var(--color-accent-light);
  border-radius: 20px;
  transition: background 0.15s ease;
}
.reading-nav a:hover { background: #E0E7FF; }
.reading-nav .nav-hint {
  font-size: var(--text-xs);
  color: var(--color-text-faint);
  padding: var(--space-xs) 0;
  margin-right: var(--space-sm);
}
```

---

## 五、Layer 2：推理块

### HTML 模板

```html
<section class="section" id="section-X">
  <h2 class="section-title">[章节标题]</h2>

  <article class="reasoning-block border-high">
    <div class="reasoning-meta">
      <span class="source-count">[N 个来源/支撑]</span>
      <span class="confidence-badge confidence-high-badge">高置信度</span>
    </div>

    <!-- 断言标题：完整句子 -->
    <h3 class="reasoning-assertion">
      [完整断言句——前提 + 推理 → 结论。这是核心主张]
    </h3>

    <!-- 摘要：1-2 句，始终可见。给扫描者"信息气味" -->
    <p class="reasoning-summary">
      [核心逻辑摘要。让读者在展开前就知道里面有什么]
    </p>

    <!-- 详细推理：默认折叠 -->
    <details class="reasoning-details">
      <summary>展开完整推理（[N] 个步骤 · 预计阅读 [M] 分钟）</summary>

      <div class="reasoning-step">
        <h4>步骤 1：[步骤标题]</h4>
        <p>[详细推理内容]</p>
      </div>

      <div class="reasoning-step">
        <h4>步骤 2：[步骤标题]</h4>
        <p>[详细推理内容]</p>
      </div>

      <div class="reasoning-step">
        <h4>步骤 3：[边界条件 —— 在什么情况下不成立]</h4>
        <p>[边界条件说明]</p>
      </div>

      <!-- 源引用：折叠在推理详情内部 -->
      <details class="source-details" style="margin-top: var(--space-md);">
        <summary>查看依据（[N] 个来源）</summary>
        <ul class="source-list">
          <li>[来源描述] <a href="#ref-1">[编号]</a></li>
        </ul>
      </details>
    </details>
  </article>
</section>
```

### 推理块 CSS

```css
.section {
  margin-bottom: var(--space-3xl);
}
.section-title {
  font-size: var(--text-lg);
  font-weight: 700;
  color: var(--color-text);
  margin-bottom: var(--space-lg);
  padding-bottom: var(--space-sm);
  border-bottom: 2px solid var(--color-border);
  letter-spacing: -0.01em;
}
.reasoning-block {
  background: var(--color-card);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  padding: var(--space-lg);
  margin-bottom: var(--space-xl);
  box-shadow: var(--shadow-card);
  transition: box-shadow 0.15s ease;
}
.reasoning-block:hover {
  box-shadow: var(--shadow-elevated);
}
.reasoning-block.border-high { border-left: 3px solid var(--confidence-high); }
.reasoning-block.border-mid  { border-left: 3px solid var(--confidence-mid); }
.reasoning-block.border-low  { border-left: 3px solid var(--confidence-low); }

.reasoning-meta {
  display: flex;
  align-items: center;
  gap: var(--space-md);
  margin-bottom: var(--space-md);
  font-size: var(--text-xs);
  color: var(--color-text-faint);
}
.reasoning-meta .source-count {
  font-weight: 600;
  color: var(--color-text-dim);
}

.reasoning-assertion {
  font-size: var(--text-lg);
  font-weight: 700;
  line-height: var(--leading-tight);
  color: var(--color-text);
  margin-bottom: var(--space-sm);
  letter-spacing: -0.01em;
}

.reasoning-summary {
  font-size: var(--text-sm);
  color: var(--color-text-dim);
  line-height: var(--leading-normal);
  margin-bottom: var(--space-md);
}

.reasoning-details {
  border-top: 1px solid var(--color-border);
  padding-top: var(--space-md);
}
.reasoning-details > summary {
  font-size: var(--text-sm);
  font-weight: 600;
  color: var(--color-accent);
  cursor: pointer;
  list-style: none;
  display: flex;
  align-items: center;
  gap: var(--space-xs);
}
.reasoning-details > summary::-webkit-details-marker { display: none; }
.reasoning-details > summary::before {
  content: "▸";
  display: inline-block;
  font-size: 10px;
  transition: transform 0.2s ease;
}
details[open] > summary::before { transform: rotate(90deg); }

.reasoning-step {
  margin-top: var(--space-md);
  padding-left: var(--space-md);
  border-left: 2px solid var(--color-bg-subtle);
}
.reasoning-step h4 {
  font-size: var(--text-sm);
  font-weight: 700;
  color: var(--color-text);
  margin-bottom: var(--space-xs);
}
.reasoning-step p, .reasoning-step li {
  font-size: var(--text-sm);
  color: var(--color-text-dim);
  line-height: var(--leading-relaxed);
  max-width: var(--measure);
}
.reasoning-step ul { padding-left: var(--space-lg); }
.reasoning-step li { margin-bottom: var(--space-xs); }
```

---

## 六、组件库

### 组件 1：对比表

```html
<table class="comparison-table">
  <thead>
    <tr>
      <th>维度</th>
      <th class="option-a">方案 A</th>
      <th class="option-b">方案 B</th>
      <th>判断</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="dim-label">[维度名称]</td>
      <td class="option-a">[A 的情况]</td>
      <td class="option-b">[B 的情况]</td>
      <td class="judgment judgment-a">← 优</td>
    </tr>
  </tbody>
</table>
```

```css
.comparison-table {
  width: 100%;
  border-collapse: collapse;
  font-size: var(--text-sm);
}
.comparison-table thead th {
  text-align: left;
  font-size: var(--text-xs);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--color-text-faint);
  padding: var(--space-sm) var(--space-md);
  border-bottom: 2px solid var(--color-border);
}
.comparison-table tbody td {
  padding: var(--space-sm) var(--space-md);
  border-bottom: 1px solid var(--color-border);
  vertical-align: top;
  line-height: var(--leading-normal);
}
.comparison-table tbody tr:last-child td { border-bottom: none; }
.comparison-table tbody tr:hover td { background: var(--color-bg-subtle); }
.comparison-table .dim-label {
  font-weight: 600;
  color: var(--color-text);
  white-space: nowrap;
}
.comparison-table .cell-highlight {
  font-weight: 600;
  color: var(--color-accent);
}
```

### 组件 2：推理链可视化

```html
<div class="inference-chain">
  <div class="chain-node premise">前提 A：<br>[前提描述]</div>
  <div class="chain-arrow">→</div>
  <div class="chain-node inference">推理：<br>[推理描述]</div>
  <div class="chain-arrow">→</div>
  <div class="chain-node conclusion">结论：<br>[结论描述]</div>
  <div class="chain-confidence confidence-high-badge">高置信度</div>
</div>
```

```css
.inference-chain {
  display: flex;
  align-items: flex-start;
  gap: var(--space-sm);
  flex-wrap: wrap;
  padding: var(--space-lg);
  background: var(--color-bg-subtle);
  border-radius: var(--radius);
}
.chain-node {
  padding: var(--space-sm) var(--space-md);
  border-radius: var(--radius-sm);
  font-size: var(--text-sm);
  font-weight: 600;
  text-align: center;
  min-width: 120px;
  line-height: var(--leading-tight);
}
.chain-node.premise    { background: #FFF7ED; color: #9A3412; }
.chain-node.inference  { background: #F5F3FF; color: #4C1D95; }
.chain-node.conclusion { background: #ECFDF5; color: #065F46; }
.chain-arrow {
  font-size: var(--text-lg);
  color: var(--color-text-faint);
  display: flex;
  align-items: center;
  padding-top: var(--space-xs);
}
.chain-confidence {
  font-size: var(--text-xs);
  margin-left: auto;
  align-self: center;
}
```

### 组件 3：假设条件卡

```html
<div class="assumption-card">
  <div class="assumption-header">⚠ 此结论依赖 [N] 个关键假设</div>
  <div class="assumption-list">
    <div class="assumption-item">
      <span>[假设陈述]</span>
      <span class="assumption-risk risk-high">若违反 → 结论翻转</span>
    </div>
    <div class="assumption-item">
      <span>[假设陈述]</span>
      <span class="assumption-risk risk-medium">若违反 → 结论弱化</span>
    </div>
    <div class="assumption-item">
      <span>[假设陈述]</span>
      <span class="assumption-risk risk-low">已验证 → 低风险</span>
    </div>
  </div>
</div>
```

```css
.assumption-card {
  background: #FFFBEB;
  border: 1px solid #FDE68A;
  border-radius: var(--radius);
  padding: var(--space-md) var(--space-lg);
  margin: var(--space-xl) 0;
}
.assumption-header {
  font-size: var(--text-sm);
  font-weight: 700;
  color: #92400E;
  margin-bottom: var(--space-sm);
}
.assumption-list {
  display: flex;
  flex-direction: column;
  gap: var(--space-sm);
}
.assumption-item {
  font-size: var(--text-sm);
  color: var(--color-text-dim);
  line-height: var(--leading-normal);
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: var(--space-md);
  flex-wrap: wrap;
}
.assumption-risk {
  font-size: var(--text-xs);
  padding: 1px 8px;
  border-radius: 10px;
  white-space: nowrap;
  font-weight: 600;
}
.risk-high   { background: #FEF2F2; color: #DC2626; }
.risk-medium { background: #FFFBEB; color: #D97706; }
.risk-low    { background: #ECFDF5; color: #059669; }
```

### 组件 4：置信度指示器

```html
<!-- 信号卡级别 -->
<span class="confidence-badge confidence-high-badge">高置信度</span>

<!-- 推理步骤级别 -->
<span class="confidence-badge confidence-mid-badge">中置信度</span>
```

```css
.confidence-badge {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  font-size: var(--text-xs);
  font-weight: 600;
  padding: 3px 10px;
  border-radius: 12px;
}
.confidence-high-badge { background: var(--confidence-high-bg); color: var(--confidence-high); }
.confidence-mid-badge  { background: var(--confidence-mid-bg);  color: var(--confidence-mid); }
.confidence-low-badge  { background: var(--confidence-low-bg);  color: var(--confidence-low); }
```

### 组件 5：视觉断点

```html
<div class="visual-break">
  <div class="visual-break-label">[断点标题 —— 图表、对比表、推理链或关键引语]</div>
  <!-- 断点内容 -->
</div>
```

```css
.visual-break {
  margin: var(--space-3xl) 0;
  padding: var(--space-2xl) var(--space-xl);
  background: var(--color-card);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  box-shadow: var(--shadow-card);
}
.visual-break-label {
  font-size: var(--text-xs);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--color-text-faint);
  margin-bottom: var(--space-lg);
}
```

### 组件 6：关键引语

```html
<blockquote class="insight-quote">
  [引语内容]
  <span class="quote-source">— [来源]</span>
</blockquote>
```

```css
.insight-quote {
  margin: var(--space-xl) 0;
  padding: var(--space-lg) var(--space-xl);
  background: var(--color-card);
  border-left: 3px solid var(--color-accent);
  border-radius: 0 var(--radius) var(--radius) 0;
  font-size: var(--text-md);
  color: var(--color-text);
  font-style: italic;
  line-height: var(--leading-relaxed);
  max-width: var(--measure);
}
.insight-quote .quote-source {
  display: block;
  margin-top: var(--space-sm);
  font-size: var(--text-xs);
  font-style: normal;
  color: var(--color-text-faint);
}
```

---

## 七、Footer

```html
<footer class="briefing-footer">
  <span>由 [Agent 名] 生成 · [日期]</span>
  <span><a href="[MD 产出路径]">查看完整 MD 产出</a></span>
</footer>
```

```css
.briefing-footer {
  margin-top: var(--space-4xl);
  padding-top: var(--space-xl);
  border-top: 2px solid var(--color-border);
  font-size: var(--text-xs);
  color: var(--color-text-faint);
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: var(--space-md);
}
.briefing-footer a {
  color: var(--color-accent);
  text-decoration: none;
}
```

---

## 八、源引用（Layer 3）

```html
<details class="source-details">
  <summary>查看依据（[N] 个来源）</summary>
  <ul class="source-list">
    <li>[来源名] — <a href="#ref-1">[E01]</a></li>
  </ul>
</details>
```

```css
.source-list {
  list-style: none;
  font-size: var(--text-xs);
  color: var(--color-text-dim);
}
.source-list li {
  padding: var(--space-xs) 0;
  border-bottom: 1px solid var(--color-border);
}
.source-list li:last-child { border-bottom: none; }
.source-list a {
  color: var(--color-text-faint);
  text-decoration: underline;
  text-underline-offset: 2px;
}
```

---

## 九、响应式与打印

```css
@media (max-width: 600px) {
  body { padding: var(--space-lg) var(--space-md); }
  .signal-card { padding: var(--space-lg); }
  .signal-metrics { grid-template-columns: 1fr; gap: var(--space-md); }
  .inference-chain { flex-direction: column; align-items: stretch; }
  .chain-arrow { transform: rotate(90deg); justify-content: center; padding: 0; }
  .chain-node { min-width: unset; }
}

@media print {
  body { max-width: 100%; padding: 0; font-size: 11pt; }
  .signal-card, .reasoning-block, .visual-break { break-inside: avoid; box-shadow: none; }
  .reasoning-details { display: block; }
  .reading-nav { display: none; }
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
}
```

---

## 十、完整 HTML 骨架（直接复制使用）

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>[标题]</title>
<style>
  /* ═══════════════════════════════════════════════════════════════
     HTML 简报 Design System v2.0
     基于 10 条跨领域第一性原则
     ═══════════════════════════════════════════════════════════════ */

  :root {
    --space-xs:   4px;
    --space-sm:   8px;
    --space-md:  16px;
    --space-lg:  24px;
    --space-xl:  32px;
    --space-2xl: 48px;
    --space-3xl: 64px;
    --space-4xl: 96px;

    --text-xs:  0.64rem;
    --text-sm:  0.8rem;
    --text-md:  1rem;
    --text-lg:  1.25rem;
    --text-xl:  1.563rem;
    --text-2xl: 1.953rem;
    --text-3xl: 2.441rem;

    --leading-tight:  1.25;
    --leading-normal: 1.6;
    --leading-relaxed: 1.75;
    --measure: 65ch;

    --color-bg:          #FAFAFA;
    --color-card:         #FFFFFF;
    --color-text:         #333333;
    --color-text-dim:     #666666;
    --color-text-faint:   #999999;
    --color-border:       #E5E5E5;
    --color-bg-subtle:    #F5F5F5;
    --color-accent:        #4F46E5;
    --color-accent-light:  #EEF2FF;

    --confidence-high:    #059669;
    --confidence-mid:     #D97706;
    --confidence-low:     #DC2626;
    --confidence-high-bg: #ECFDF5;
    --confidence-mid-bg:  #FFFBEB;
    --confidence-low-bg:  #FEF2F2;

    --radius-sm: 4px;
    --radius:    8px;
    --shadow-card:    0 1px 3px rgba(0,0,0,0.06);
    --shadow-elevated: 0 4px 12px rgba(0,0,0,0.08);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "PingFang SC", "Microsoft YaHei", sans-serif;
    font-size: var(--text-md);
    line-height: var(--leading-normal);
    color: var(--color-text);
    background: var(--color-bg);
    max-width: 860px;
    margin: 0 auto;
    padding: var(--space-2xl) var(--space-lg);
    -webkit-font-smoothing: antialiased;
  }

  /* Layer 1: Signal Card */
  .signal-card { background: var(--color-card); border: 1px solid var(--color-border); border-radius: var(--radius); padding: var(--space-2xl) var(--space-xl); margin-bottom: var(--space-3xl); box-shadow: var(--shadow-card); }
  .signal-context { font-size: var(--text-sm); color: var(--color-text-dim); margin-bottom: var(--space-sm); }
  .signal-complication { font-size: var(--text-md); color: var(--color-text); margin-bottom: var(--space-xl); line-height: var(--leading-relaxed); max-width: var(--measure); }
  .signal-answer { margin-bottom: var(--space-xl); }
  .signal-answer-label { display: inline-block; font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.08em; color: var(--color-accent); background: var(--color-accent-light); padding: 2px 10px; border-radius: var(--radius-sm); margin-bottom: var(--space-sm); }
  .signal-answer h1 { font-size: var(--text-2xl); font-weight: 800; line-height: 1.2; letter-spacing: -0.02em; max-width: 28ch; }
  .signal-metrics { display: grid; grid-template-columns: repeat(3, 1fr); gap: var(--space-lg); margin-bottom: var(--space-xl); padding: var(--space-lg); background: var(--color-bg-subtle); border-radius: var(--radius); }
  .signal-metric { text-align: center; }
  .metric-value { display: block; font-size: var(--text-xl); font-weight: 800; line-height: 1.2; letter-spacing: -0.02em; }
  .metric-value.accent { color: var(--color-accent); }
  .metric-label { display: block; font-size: var(--text-xs); color: var(--color-text-faint); margin-top: var(--space-xs); }
  .signal-premises { padding-top: var(--space-lg); border-top: 1px solid var(--color-border); }
  .signal-premises h3 { font-size: var(--text-sm); font-weight: 600; color: var(--color-text-dim); margin-bottom: var(--space-sm); }
  .signal-premises ul { list-style: none; display: flex; flex-direction: column; gap: var(--space-sm); }
  .signal-premises li { font-size: var(--text-sm); color: var(--color-text-dim); line-height: var(--leading-normal); padding-left: var(--space-md); position: relative; }
  .signal-premises li::before { content: "⚠"; position: absolute; left: 0; font-size: var(--text-sm); }

  /* Reading Nav */
  .reading-nav { display: flex; gap: var(--space-sm); flex-wrap: wrap; margin-bottom: var(--space-3xl); padding: 0 var(--space-sm); }
  .reading-nav a { font-size: var(--text-sm); color: var(--color-accent); text-decoration: none; padding: var(--space-xs) var(--space-md); background: var(--color-accent-light); border-radius: 20px; transition: background 0.15s ease; }
  .reading-nav a:hover { background: #E0E7FF; }
  .reading-nav .nav-hint { font-size: var(--text-xs); color: var(--color-text-faint); padding: var(--space-xs) 0; margin-right: var(--space-sm); }

  /* Layer 2: Reasoning */
  .section { margin-bottom: var(--space-3xl); }
  .section-title { font-size: var(--text-lg); font-weight: 700; color: var(--color-text); margin-bottom: var(--space-lg); padding-bottom: var(--space-sm); border-bottom: 2px solid var(--color-border); letter-spacing: -0.01em; }

  .reasoning-block { background: var(--color-card); border: 1px solid var(--color-border); border-radius: var(--radius); padding: var(--space-lg); margin-bottom: var(--space-xl); box-shadow: var(--shadow-card); transition: box-shadow 0.15s ease; }
  .reasoning-block:hover { box-shadow: var(--shadow-elevated); }
  .reasoning-block.border-high { border-left: 3px solid var(--confidence-high); }
  .reasoning-block.border-mid  { border-left: 3px solid var(--confidence-mid); }
  .reasoning-block.border-low  { border-left: 3px solid var(--confidence-low); }

  .reasoning-meta { display: flex; align-items: center; gap: var(--space-md); margin-bottom: var(--space-md); font-size: var(--text-xs); color: var(--color-text-faint); }
  .reasoning-meta .source-count { font-weight: 600; color: var(--color-text-dim); }
  .reasoning-assertion { font-size: var(--text-lg); font-weight: 700; line-height: var(--leading-tight); color: var(--color-text); margin-bottom: var(--space-sm); letter-spacing: -0.01em; }
  .reasoning-summary { font-size: var(--text-sm); color: var(--color-text-dim); line-height: var(--leading-normal); margin-bottom: var(--space-md); }

  .reasoning-details { border-top: 1px solid var(--color-border); padding-top: var(--space-md); }
  .reasoning-details > summary { font-size: var(--text-sm); font-weight: 600; color: var(--color-accent); cursor: pointer; list-style: none; display: flex; align-items: center; gap: var(--space-xs); }
  .reasoning-details > summary::-webkit-details-marker { display: none; }
  .reasoning-details > summary::before { content: "▸"; display: inline-block; font-size: 10px; transition: transform 0.2s ease; }
  details[open] > summary::before { transform: rotate(90deg); }

  .reasoning-step { margin-top: var(--space-md); padding-left: var(--space-md); border-left: 2px solid var(--color-bg-subtle); }
  .reasoning-step h4 { font-size: var(--text-sm); font-weight: 700; color: var(--color-text); margin-bottom: var(--space-xs); }
  .reasoning-step p, .reasoning-step li { font-size: var(--text-sm); color: var(--color-text-dim); line-height: var(--leading-relaxed); max-width: var(--measure); }
  .reasoning-step ul { padding-left: var(--space-lg); }
  .reasoning-step li { margin-bottom: var(--space-xs); }

  /* Visual Break */
  .visual-break { margin: var(--space-3xl) 0; padding: var(--space-2xl) var(--space-xl); background: var(--color-card); border: 1px solid var(--color-border); border-radius: var(--radius); box-shadow: var(--shadow-card); }
  .visual-break-label { font-size: var(--text-xs); font-weight: 700; text-transform: uppercase; letter-spacing: 0.08em; color: var(--color-text-faint); margin-bottom: var(--space-lg); }

  /* Components */
  .comparison-table { width: 100%; border-collapse: collapse; font-size: var(--text-sm); }
  .comparison-table thead th { text-align: left; font-size: var(--text-xs); font-weight: 700; text-transform: uppercase; letter-spacing: 0.05em; color: var(--color-text-faint); padding: var(--space-sm) var(--space-md); border-bottom: 2px solid var(--color-border); }
  .comparison-table tbody td { padding: var(--space-sm) var(--space-md); border-bottom: 1px solid var(--color-border); vertical-align: top; line-height: var(--leading-normal); }
  .comparison-table tbody tr:last-child td { border-bottom: none; }
  .comparison-table tbody tr:hover td { background: var(--color-bg-subtle); }
  .comparison-table .dim-label { font-weight: 600; color: var(--color-text); white-space: nowrap; }
  .comparison-table .cell-highlight { font-weight: 600; color: var(--color-accent); }

  .inference-chain { display: flex; align-items: flex-start; gap: var(--space-sm); flex-wrap: wrap; padding: var(--space-lg); background: var(--color-bg-subtle); border-radius: var(--radius); }
  .chain-node { padding: var(--space-sm) var(--space-md); border-radius: var(--radius-sm); font-size: var(--text-sm); font-weight: 600; text-align: center; min-width: 120px; line-height: var(--leading-tight); }
  .chain-node.premise    { background: #FFF7ED; color: #9A3412; }
  .chain-node.inference  { background: #F5F3FF; color: #4C1D95; }
  .chain-node.conclusion { background: #ECFDF5; color: #065F46; }
  .chain-arrow { font-size: var(--text-lg); color: var(--color-text-faint); display: flex; align-items: center; padding-top: var(--space-xs); }
  .chain-confidence { font-size: var(--text-xs); margin-left: auto; align-self: center; }

  .assumption-card { background: #FFFBEB; border: 1px solid #FDE68A; border-radius: var(--radius); padding: var(--space-md) var(--space-lg); margin: var(--space-xl) 0; }
  .assumption-header { font-size: var(--text-sm); font-weight: 700; color: #92400E; margin-bottom: var(--space-sm); }
  .assumption-list { display: flex; flex-direction: column; gap: var(--space-sm); }
  .assumption-item { font-size: var(--text-sm); color: var(--color-text-dim); line-height: var(--leading-normal); display: flex; justify-content: space-between; align-items: baseline; gap: var(--space-md); flex-wrap: wrap; }
  .assumption-risk { font-size: var(--text-xs); padding: 1px 8px; border-radius: 10px; white-space: nowrap; font-weight: 600; }
  .risk-high   { background: #FEF2F2; color: #DC2626; }
  .risk-medium { background: #FFFBEB; color: #D97706; }
  .risk-low    { background: #ECFDF5; color: #059669; }

  .confidence-badge { display: inline-flex; align-items: center; gap: 4px; font-size: var(--text-xs); font-weight: 600; padding: 3px 10px; border-radius: 12px; }
  .confidence-high-badge { background: var(--confidence-high-bg); color: var(--confidence-high); }
  .confidence-mid-badge  { background: var(--confidence-mid-bg);  color: var(--confidence-mid); }
  .confidence-low-badge  { background: var(--confidence-low-bg);  color: var(--confidence-low); }

  .insight-quote { margin: var(--space-xl) 0; padding: var(--space-lg) var(--space-xl); background: var(--color-card); border-left: 3px solid var(--color-accent); border-radius: 0 var(--radius) var(--radius) 0; font-size: var(--text-md); color: var(--color-text); font-style: italic; line-height: var(--leading-relaxed); max-width: var(--measure); }
  .insight-quote .quote-source { display: block; margin-top: var(--space-sm); font-size: var(--text-xs); font-style: normal; color: var(--color-text-faint); }

  .source-list { list-style: none; font-size: var(--text-xs); color: var(--color-text-dim); }
  .source-list li { padding: var(--space-xs) 0; border-bottom: 1px solid var(--color-border); }
  .source-list li:last-child { border-bottom: none; }
  .source-list a { color: var(--color-text-faint); text-decoration: underline; text-underline-offset: 2px; }

  /* Footer */
  .briefing-footer { margin-top: var(--space-4xl); padding-top: var(--space-xl); border-top: 2px solid var(--color-border); font-size: var(--text-xs); color: var(--color-text-faint); display: flex; justify-content: space-between; flex-wrap: wrap; gap: var(--space-md); }
  .briefing-footer a { color: var(--color-accent); text-decoration: none; }

  /* Responsive */
  @media (max-width: 600px) {
    body { padding: var(--space-lg) var(--space-md); }
    .signal-card { padding: var(--space-lg); }
    .signal-metrics { grid-template-columns: 1fr; gap: var(--space-md); }
    .inference-chain { flex-direction: column; align-items: stretch; }
    .chain-arrow { transform: rotate(90deg); justify-content: center; padding: 0; }
    .chain-node { min-width: unset; }
  }

  @media print {
    body { max-width: 100%; padding: 0; font-size: 11pt; }
    .signal-card, .reasoning-block, .visual-break { break-inside: avoid; box-shadow: none; }
    .reasoning-details { display: block; }
    .reading-nav { display: none; }
  }

  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
  }
</style>
</head>
<body>

<!-- Layer 1: Signal Card (SCQA) -->
<header class="signal-card">
  <div class="signal-context">S · [共识背景 — 1-2 句]</div>
  <div class="signal-complication">C · [矛盾/变化 — 1-2 句]</div>
  <div class="signal-answer">
    <span class="signal-answer-label">结论方向</span>
    <h1>[核心结论 —— 完整断言句]</h1>
  </div>
  <div class="signal-metrics">
    <div class="signal-metric">
      <span class="metric-value accent">[N]</span>
      <span class="metric-label">[含义]</span>
    </div>
    <div class="signal-metric">
      <span class="metric-value">[N]</span>
      <span class="metric-label">[含义]</span>
    </div>
    <div class="signal-metric">
      <span class="metric-value">[N]</span>
      <span class="metric-label">[含义]</span>
    </div>
  </div>
  <div class="signal-premises">
    <h3>如果以下前提错了，结论会翻转</h3>
    <ul>
      <li><strong>[前提 1]</strong> — 如果错了：[后果]</li>
    </ul>
  </div>
</header>

<!-- Reading Nav -->
<nav class="reading-nav">
  <span class="nav-hint">跳转：</span>
  <a href="#section-1">[章节]</a>
  <a href="#section-2">[章节]</a>
  <a href="#section-3">[章节]</a>
</nav>

<!-- Layer 2: Reasoning Sections -->
<section class="section" id="section-1">
  <h2 class="section-title">[章节标题]</h2>

  <article class="reasoning-block border-high">
    <div class="reasoning-meta">
      <span class="source-count">[N 个来源]</span>
      <span class="confidence-badge confidence-high-badge">高置信度</span>
    </div>
    <h3 class="reasoning-assertion">[完整断言句 —— 前提 + 推理 → 结论]</h3>
    <p class="reasoning-summary">[摘要 —— 1-2 句，给扫描者"信息气味"]</p>
    <details class="reasoning-details">
      <summary>展开完整推理（[N] 个步骤 · 预计阅读 [M] 分钟）</summary>
      <div class="reasoning-step">
        <h4>步骤 1：[步骤标题]</h4>
        <p>[内容]</p>
      </div>
    </details>
  </article>
</section>

<footer class="briefing-footer">
  <span>由 [Agent 名] 生成 · [日期]</span>
  <span><a href="[MD 产出路径]">查看完整 MD 产出</a></span>
</footer>

</body>
</html>
```
