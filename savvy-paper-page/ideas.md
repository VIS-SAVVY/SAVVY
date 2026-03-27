# SAVVY Paper Page — Design Ideas

<response>
<text>
**Design Movement:** Deep Space Academic — 受深色学术出版物与太空科幻美学影响

**Core Principles:**
1. 深色背景为主，强调内容可读性，绿色作为唯一高亮色
2. 各 section 通过明暗交替（深色 / 浅灰白）形成节奏感
3. 代码块与数据展示区采用终端风格，强化技术感
4. 所有占位区域用虚线框清晰标注，方便后续替换

**Color Philosophy:**
- 背景：#0f0f1a（极深蓝黑）
- 卡片：#1c1c2e
- 强调绿：oklch(0.75 0.18 145)（鲜亮绿）
- 文字：oklch(0.88 0.005 285)
- 静默文字：oklch(0.60 0.01 285)

**Layout Paradigm:**
- 单列居中，最大宽度 860px，左右留白充足
- Hero 区用白色卡片浮于深色渐变背景之上
- 各 section 交替深色/浅色背景，形成视觉分层

**Signature Elements:**
1. 绿色短横线作为 section 标题下方的装饰分隔线
2. 虚线边框的占位框（dashed border）
3. 代码块使用深色终端背景 + 等宽字体

**Interaction Philosophy:**
- 导航链接 hover 时绿色高亮 + 轻微上移
- 按钮 hover 时背景填充绿色
- 滚动进入视口时 fade-in + slide-up 动画

**Animation:**
- 使用 framer-motion 的 `whileInView` 实现 section 入场
- 导航链接 hover 使用 CSS transition
- 代码块无动画，保持静态可读性

**Typography System:**
- 标题：Space Grotesk（700/800），大号，紧凑行高
- 正文：DM Sans（400），宽松行高 1.7
- 代码：JetBrains Mono（400/500）
</text>
<probability>0.07</probability>
</response>

<response>
<text>
**Design Movement:** Brutalist Academic — 粗犷边框 + 高对比度，反精致美学

**Core Principles:**
1. 粗黑边框替代阴影，强调结构感
2. 黄色 + 黑色高对比配色
3. 不规则网格布局，打破对称

**Color Philosophy:** 黑底黄字，极高对比度

**Layout Paradigm:** 不规则网格，故意不对齐

**Signature Elements:** 粗边框、手写风格字体、斜切角

**Interaction Philosophy:** 点击时边框颜色变化

**Animation:** 无动画，强调静态力量感

**Typography System:** Bebas Neue + IBM Plex Mono
</text>
<probability>0.03</probability>
</response>

<response>
<text>
**Design Movement:** Glassmorphism Academic — 毛玻璃 + 渐变背景

**Core Principles:**
1. 半透明卡片叠加在渐变背景上
2. 柔和蓝紫渐变背景
3. 轻盈感，大量空白

**Color Philosophy:** 蓝紫渐变背景，白色半透明卡片

**Layout Paradigm:** 居中卡片堆叠

**Signature Elements:** backdrop-blur、渐变边框、浮动粒子

**Interaction Philosophy:** hover 时卡片上浮

**Animation:** 粒子背景动画

**Typography System:** Outfit + Fira Code
</text>
<probability>0.04</probability>
</response>

---

**Selected:** Response 1 — Deep Space Academic
理由：与 HyperMOOC 风格最接近，深色背景 + 绿色强调 + 代码块终端风格，符合学术论文介绍页的专业气质。
