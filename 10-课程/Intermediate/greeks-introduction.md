---
title: "Greeks 入门"
title_en: "Introduction To Greeks"
slug: "greeks-introduction"
type: lesson
level: Intermediate
order: 33
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "Greeks 入门"
  - "Introduction To Greeks"
  - "greeks-introduction"
source_url: "https://tradinghubs.org/docs/trading-knowledge/greeks-introduction"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# Greeks 入门

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[straddle-strangle-event-risk|Straddle、Strangle 与事件波动]] ｜ 下一课：[[delta-curve|Delta 曲线：从 Buy Call 推导方向敏感度]]

**中级 · Greeks 与敏感度 · 18 分钟**

> Greeks 是连接期权和期货的桥梁。它们不预测行情，而是说明 Spot、DTE、IV、Rate 变化时风险如何变化。

把 Delta、Gamma、Theta、Vega、Rho 看成期权风险暴露语言。

### 01 / 风险地图

#### 每个 Greek 只回答一个维度的问题

Delta 衡量方向敏感度，Gamma 衡量 Delta 的变化速度，Theta 衡量时间衰减，Vega 衡量 IV 敏感度，Rho 衡量利率敏感度。

Greeks 不是固定数值。Spot、Strike、DTE、IV 和 Rate 改变后，同一张期权的 Greeks 也会改变。

| Greek | 回答的问题 | 基础阶段重点 |
| --- | --- | --- |
| Delta | 标的动 1 点，期权大约动多少。 | 方向暴露。 |
| Gamma | Delta 变化有多快。 | 对冲敏感度。 |
| Theta | 时间过去如何影响价格。 | 到期压力。 |
| Vega | IV 变化如何影响价格。 | 波动率重定价。 |
| Rho | 利率变化如何影响价格。 | 短期期权中弱化。 |

### 02 / Gamma 与对冲

#### Gamma 决定 Delta hedge 需要多快调整

Gamma 高的区域，价格接近 Strike 时，Delta 会随 Spot 变化更快。Dealer 如果需要维持风险中性，就会更频繁地调整期货对冲。

- **Delta 更新近似**

  ```latex
  \Delta_{new}\approx\Delta_{old}+\Gamma\times\Delta S
  ```

### 03 / ES / NQ 传导

#### 已知持仓方向时，Gamma 会改变对冲路径

在明确知道某一库存为 Long Gamma 且对冲者维持 Delta 中性时，对冲可表现为低买高卖；明确为 Short Gamma 时，路径可能相反。这是已知持仓的条件式机制，不代表 ODV 暴露正负号揭示 dealer 库存，也不能单独预测盘中波动。

- Delta hedge 把期权仓位和期货成交连接起来。
- Gamma 高的 Strike 附近，价格运动可能更敏感。
- 这说明波动机制，不说明方向胜率。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Greeks connect options and futures. They do not predict direction; they describe how risk changes as spot, DTE, IV, and rates move.

Read Delta, Gamma, Theta, Vega, and Rho as the language of options risk exposure.

### 01 / Risk Map

#### Each Greek Answers One Risk Dimension

Delta measures directional sensitivity, gamma measures how fast delta changes, theta measures time decay, vega measures IV sensitivity, and rho measures rate sensitivity.

Greeks are not fixed values. When spot, strike, DTE, IV, or rate changes, the same option's Greeks change too.

| Greek | Question | Foundation focus |
| --- | --- | --- |
| Delta | How much the option moves for a 1-point spot move. | Directional exposure. |
| Gamma | How quickly delta changes. | Hedging sensitivity. |
| Theta | How passing time affects price. | Expiration pressure. |
| Vega | How IV changes affect price. | Volatility repricing. |
| Rho | How rates affect price. | Lower priority for short-dated options. |

### 02 / Gamma And Hedging

#### Gamma Determines How Fast Delta Hedges Need To Adjust

In high-gamma areas, delta changes faster as spot approaches the strike. Dealers maintaining neutral exposure may need to adjust futures hedges more frequently.

- **Delta update approximation**

  ```latex
  \Delta_{new}\approx\Delta_{old}+\Gamma\times\Delta S
  ```

### 03 / ES / NQ Transmission

#### Gamma Changes Hedge Paths When Position Side Is Known

When an inventory is known to be long gamma and its hedger maintains delta neutrality, rebalancing can buy lower and sell higher; a known short-gamma inventory can produce the opposite path. This is a conditional mechanism for a known position. ODV exposure signs do not reveal dealer inventory or predict intraday volatility by themselves.

- Delta hedging links options positions to futures flow.
- Around high-gamma strikes, price movement can become more sensitive.
- This explains volatility mechanics, not directional win rate.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

