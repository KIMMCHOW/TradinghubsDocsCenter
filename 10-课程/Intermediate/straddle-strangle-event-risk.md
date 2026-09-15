---
title: "Straddle、Strangle 与事件波动"
title_en: "Straddles, Strangles, And Event Volatility"
slug: "straddle-strangle-event-risk"
type: lesson
level: Intermediate
order: 32
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "20 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "Straddle、Strangle 与事件波动"
  - "Straddles, Strangles, And Event Volatility"
  - "straddle-strangle-event-risk"
source_url: "https://tradinghubs.org/docs/trading-knowledge/straddle-strangle-event-risk"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# Straddle、Strangle 与事件波动

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[vertical-ratio-backspread|垂直价差、Ratio Spread 与 Backspread]] ｜ 下一课：[[greeks-introduction|Greeks 入门]]

**中级 · 结构、定价与波动率 · 20 分钟**

> 双向期权结构把“方向未知”转换成“移动幅度、发生时间和期权价格是否匹配”的问题。猜对有事件并不等于结构盈利，因为市场可能早已把不确定性计入权利金。

比较 Straddle 与 Strangle 的到期几何、Gamma/Theta 权衡、事件总方差和波动率回落风险，避免把 Expected Move 当成价格边界。

### 01 / 到期几何

#### Straddle 集中在同一执行价，Strangle 把两侧起点拉开

Long Straddle 同时买入同执行价、同到期的 Call 与 Put，到期毛价值为标的与执行价距离的绝对值。Long Strangle 买入较低执行价 Put 和较高执行价 Call，初始成本通常较低，但需要更大移动才进入任一腿的内在价值。

Short 版本反转现金流：初始收取权利金，若标的留在中间区域则到期价值较小，但大幅单边移动会带来不对称或开放尾部风险。到期盈亏平衡点只适用于持有到期且忽略费用的简化场景。

- **Long Straddle 到期毛价值**

  ```latex
  \max(S_T-K,0)+\max(K-S_T,0)=|S_T-K|
  ```

- **Long Straddle 简化盈亏平衡**

  ```latex
  K-D\quad\text{and}\quad K+D
  ```

- **Long Strangle 简化盈亏平衡**

  ```latex
  K_P-D\quad\text{and}\quad K_C+D
  ```

| 对比 | Straddle | Strangle |
| --- | --- | --- |
| 执行价 | Call 与 Put 相同。 | Put 较低、Call 较高。 |
| 初始权利金 | 通常更高。 | 通常较低，但依赖 Skew。 |
| 移动要求 | 从中心执行价开始积累毛价值。 | 先跨过两个执行价之间区域。 |

### 02 / 事件定价

#### 事件前 IV 上升不等于事件后期权一定升值

临近已知事件时，覆盖事件的到期可能积累更多总方差。事件结束后，一部分不确定性被解析，IV 可能快速回落；即使方向判断正确，标的移动若小于权利金中已计入的幅度，Long Volatility 结构仍可能亏损。

常见 Expected Move 近似用现货、IV 与时间平方根缩放，但它依赖模型、到期与 IV 选择。它是分布尺度，不是支撑阻力、置信区间保证或最大涨跌幅；偏斜和跳跃分布还会使上下方向并不对称。

- Long Straddle / Strangle 通常 Long Gamma、Long Vega、Short Theta，但符号和大小随状态变化。
- Short 结构收取时间价值，但承担跳空、流动性消失与尾部保证金风险。
- 事件日期变化或结果提前泄露会改变原有期限分解。

- **简化的一标准差尺度**

  ```latex
  \text{Move scale}\approx S_0\sigma\sqrt{T}
  ```

- **期限总方差**

  ```latex
  w(T)=\sigma_{\mathrm{imp}}^2T
  ```

- **Delta 中性 Long Gamma 的局部权衡**

  ```latex
  d\Pi\approx \frac{1}{2}\Gamma(dS)^2+\Theta\,dt+\text{Vega}\,d\sigma
  ```

### 03 / 事件流程

#### 把事件前价格、事件窗口和事件后重估分开

先确认事件是否落在合约期限内，比较事件前后相邻到期的总方差、Skew、Bid / Ask 与近期 RV。再计算结构的净 Debit / Credit、简化到期盈亏平衡和价格 × IV × 时间情景，不把单一 Expected Move 当作终点。

事件后分别归因标的移动、IV 回落、时间流逝和成交成本。若结果与预期不同，要检查市场实际移动路径、偏斜变化与报价深度，而不是只用“IV Crush”解释所有盈亏。

- 第一步：确认事件时间与到期覆盖关系，比较相邻期限总方差。
- 第二步：同时画价格、IV、时间与流动性情景，而非只画到期曲线。
- 第三步：事件后拆分移动、波动率、Theta 和执行成本贡献。
- 事件结构可能快速损失权利金或产生开放尾部风险，本课不建议做多或做空事件。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Two-sided option structures turn unknown direction into questions about move size, timing, and whether option price matches the outcome. Correctly anticipating an event does not guarantee a profitable structure because uncertainty may already be embedded in premium.

Compare straddle and strangle expiry geometry, gamma-theta tradeoffs, event total variance, and post-event volatility compression without treating expected move as a price boundary.

### 01 / Expiry Geometry

#### A Straddle Concentrates At One Strike; A Strangle Separates The Two Wings

A long straddle buys a call and put with the same strike and expiry; gross terminal value is the absolute distance between underlying and strike. A long strangle buys a lower-strike put and a higher-strike call, usually at lower initial cost but requiring a larger move before either leg becomes intrinsic.

Short versions reverse the cash flow: premium is collected initially and terminal value is small if the underlying stays in the middle, but a large directional move creates asymmetric or open-tail risk. Expiry break-evens apply only to a simplified hold-to-expiry case before costs.

- **Long-straddle gross terminal value**

  ```latex
  \max(S_T-K,0)+\max(K-S_T,0)=|S_T-K|
  ```

- **Simplified long-straddle break-evens**

  ```latex
  K-D\quad\text{and}\quad K+D
  ```

- **Simplified long-strangle break-evens**

  ```latex
  K_P-D\quad\text{and}\quad K_C+D
  ```

| Comparison | Straddle | Strangle |
| --- | --- | --- |
| Strikes | Call and put share one strike. | Lower put and higher call strikes. |
| Initial premium | Usually higher. | Usually lower, but skew dependent. |
| Move requirement | Gross value starts building from the center strike. | Must first cross the gap between strikes. |

### 02 / Event Pricing

#### Higher Pre-Event IV Does Not Mean Options Must Gain After The Event

As a known event approaches, an expiry spanning it may accumulate more total variance. Once the event resolves, part of the uncertainty disappears and IV may fall quickly; even with the correct direction, a long-volatility package can lose if the move is smaller than the amount already priced into premium.

A common expected-move approximation scales spot by IV and the square root of time, but depends on model, expiry, and IV selection. It is a distribution scale, not support, resistance, a guaranteed confidence band, or a maximum move; skew and jump distributions can also make the two directions asymmetric.

- Long straddles and strangles are generally long gamma, long vega, and short theta, but magnitudes and even local behavior vary by state.
- Short structures collect time value but bear gap, liquidity-withdrawal, and tail-margin risk.
- A changed event date or early information release can invalidate the original term decomposition.

- **Simplified one-standard-deviation scale**

  ```latex
  \text{Move scale}\approx S_0\sigma\sqrt{T}
  ```

- **Term total variance**

  ```latex
  w(T)=\sigma_{\mathrm{imp}}^2T
  ```

- **Local delta-neutral long-gamma tradeoff**

  ```latex
  d\Pi\approx \frac{1}{2}\Gamma(dS)^2+\Theta\,dt+\text{Vega}\,d\sigma
  ```

### 03 / Event Workflow

#### Separate Pre-Event Price, Event Window, And Post-Event Revaluation

Confirm that the event falls inside the contract horizon, then compare total variance, skew, bid-ask, and recent RV across expiries bracketing it. Calculate package debit or credit, simplified terminal break-evens, and price-by-IV-by-time scenarios rather than treating one expected-move number as the answer.

After the event, attribute underlying movement, IV compression, time passage, and execution cost separately. If results differ from expectation, inspect the realized path, skew changes, and quote depth instead of using IV crush to explain all P&L.

- Step 1: Align event time with expiry coverage and compare neighboring-expiry total variance.
- Step 2: Map price, IV, time, and liquidity scenarios rather than only the terminal curve.
- Step 3: Separate movement, volatility, theta, and execution-cost contributions after the event.
- Event structures can rapidly lose premium or create open-tail risk; this lesson does not recommend buying or selling an event.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

