---
title: "DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选"
title_en: "DTE Windows: How To Choose 0DTE, 1DTE+, And 90D Window"
slug: "dte-window-selection"
type: lesson
level: Intermediate
order: 41
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "12 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选"
  - "DTE Windows: How To Choose 0DTE, 1DTE+, And 90D Window"
  - "dte-window-selection"
source_url: "https://tradinghubs.org/docs/trading-knowledge/dte-window-selection"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[implied-volatility-surface|隐含波动率 IV 与波动率曲面]] ｜ 下一课：[[market-maker-flow|做市商对冲：Delta 中性与 Gamma 再平衡]]

**中级 · Greeks 与敏感度 · 12 分钟**

> 不要把所有到期日混成一个结论。0DTE 的敏感度可能更集中但生命周期短，90D Window 的单位时间变化通常更慢；三个页面窗口都是独立值，90D Window 不等于 0DTE 与 1DTE+ 相加。

把 0DTE、1DTE+ 和 90D Window 分开看，理解这些独立预计算窗口分别回答日内、近端和中期结构问题。

### 01 / DTE 是什么

#### DTE 是距离到期还有多少天

其他输入不变且价格靠近平值时，DTE 缩短常使 Gamma 峰值与日历时间敏感度更集中；深 ITM / OTM 的 Gamma、Theta 或 Charm 则可能收缩或改变符号。DTE 较长时单位时间变化通常更慢，但大 OI 仍可形成重要背景暴露。

在 ODV 里，DTE 不是一个筛选小按钮而已；它决定你正在问的问题属于今天、下一交易日，还是更长周期。

- D 是定价模型声明的年化日计数，不能在 365、252 与产品交易日口径之间静默切换。

- **按模型日计数换算到期时间**

  ```latex
  T=\frac{\mathrm{DTE}}{D}
  ```

- **平值且其他输入不变时的 Gamma 直觉**

  ```latex
  \text{Near ATM:}\quad T\downarrow\;\Rightarrow\;\Gamma_{\mathrm{peak}}\uparrow
  ```

### 02 / 窗口选择

#### 不同 DTE 窗口回答不同问题

同一个行权价，在 0DTE 和 90D Window 里可能代表完全不同的模型风险。前者偏盘中敏感度，后者偏中期背景；只能在各自标的、指标、窗口和数据快照内比较原始数值。

| DTE 窗口 | 适合观察 | 风险边界 |
| --- | --- | --- |
| 0DTE | 日内敏感区与临近收盘的快速变化。 | 生命周期很短；符号不证明 dealer 对冲。 |
| 1DTE+ | 近端到期窗口的结构分布。 | 不要和 0DTE 结论混用。 |
| 90D Window | 中期模型敏感度与背景风险分布。 | 独立窗口，不是 0DTE + 1DTE+，也不适合解释每次日内急动。 |

### 03 / 期货传导

#### 先选周期，再读 GEX / DEX / VEX / CHEX

观察日内 ES / NQ 时，分别在 0DTE 的 GEX、DEX、VEX、CHEX 视图内定位现价附近的相对热点；观察近端或中期背景时，再分别读取 1DTE+ 与 90D Window。只比较热点位置，不跨指标或 DTE 比较原始绝对值。

- DTE 是所有 Greeks Profile 读法的第一层过滤器。
- 不同窗口冲突时，不要强行合并成一个方向结论。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Do not collapse all expirations into one conclusion. Sensitivity can be more concentrated in 0DTE but is short lived, while per-unit-time change is usually slower in 90D Window. All three page windows are independent values; 90D Window is not 0DTE plus 1DTE+.

Separate the independently precomputed 0DTE, 1DTE+, and 90D Window views to answer intraday, near-term, and medium-term structural questions.

### 01 / What DTE Means

#### DTE Is Days To Expiration

With other inputs fixed and price near ATM, shorter DTE often concentrates the gamma peak and calendar-time sensitivity; deep-ITM or deep-OTM gamma, theta, or charm may instead shrink or change sign. Longer DTE usually changes more slowly per unit time, but large OI can still create material background exposure.

In ODV, DTE is not just a small filter button; it defines whether the question you are asking belongs to today, the next session, or a longer horizon.

- D is the pricing model's stated annual day-count basis; do not silently switch among 365, 252, and product trading-day conventions.

- **Time to expiry on the model day-count basis**

  ```latex
  T=\frac{\mathrm{DTE}}{D}
  ```

- **ATM gamma intuition with other inputs fixed**

  ```latex
  \text{Near ATM:}\quad T\downarrow\;\Rightarrow\;\Gamma_{\mathrm{peak}}\uparrow
  ```

### 02 / Window Selection

#### Different DTE Windows Answer Different Questions

The same strike can represent very different modeled risk in 0DTE and 90D Window. The former emphasizes intraday sensitivity and the latter medium-term background. Raw values are comparable only within the same symbol, metric, window, and snapshot.

| DTE Window | Best For | Boundary |
| --- | --- | --- |
| 0DTE | Intraday sensitivity areas and rapid late-session change. | Very short lived; signs do not establish dealer hedging. |
| 1DTE+ | Structural distribution in the near-term expiry window. | Do not mix it with 0DTE conclusions. |
| 90D Window | Medium-term modeled sensitivity and background-risk distribution. | An independent window, not 0DTE plus 1DTE+, and not suited to explain every intraday burst. |

### 03 / Futures Transmission

#### Choose The Window Before Reading GEX / DEX / VEX / CHEX

For intraday ES or NQ, locate relative hotspots near price separately within each 0DTE GEX, DEX, VEX, and CHEX view. For near-term or medium-term context, read 1DTE+ and 90D Window separately. Compare hotspot locations, not raw magnitudes across metrics or DTE windows.

- DTE is the first filter for every Greeks Profile reading.
- When windows conflict, do not force them into one directional conclusion.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

