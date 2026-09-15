---
title: "价差与组合结构"
title_en: "Spread And Multi-Leg Structures"
slug: "option-spread-structures"
type: lesson
level: Intermediate
order: 30
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "16 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "价差与组合结构"
  - "Spread And Multi-Leg Structures"
  - "option-spread-structures"
source_url: "https://tradinghubs.org/docs/trading-knowledge/option-spread-structures"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 价差与组合结构

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[volume-profile-value-area-hvn-lvn|成交量分布：价值区、HVN 与 LVN]] ｜ 下一课：[[no-arbitrage-and-synthetics|无套利边界与合成头寸]]

**中级 · 结构、定价与波动率 · 16 分钟**

> Vertical Spread、Straddle、Strangle、Butterfly 和 Iron Condor 在这里都是结构样本，用来观察风险如何叠加。

理解多条期权腿如何叠加成一个风险结构，而不是学习开仓策略。

### 01 / 叠加逻辑

#### 组合盈亏来自每条腿的 payoff 相加

多腿结构不是魔法。每一条腿都有自己的方向、Strike、Premium、数量和乘数，组合后的 Net Payoff 就是这些腿的盈亏相加。

- **组合盈亏**

  ```latex
  \text{Net Payoff}=\text{Leg}_1+\text{Leg}_2+\text{Leg}_3+\text{Leg}_4
  ```

### 02 / 常见结构

#### 名称只是标签，核心是风险边界

Vertical Spread 用两个不同行权价限制一侧风险。Straddle / Strangle 把上行和下行风险同时纳入。Butterfly 与 Iron Condor 则把多条腿叠加成范围型风险形状。

不要把这些结构写成“适合震荡”或“适合突破”的操作建议。这里关心的是风险有限、风险无限、收益有限、收益非线性这些结构特征。

- Vertical Spread：两条腿限制一侧尾部。
- Straddle / Strangle：围绕波动范围形成双侧暴露。
- Butterfly / Iron Condor：多腿叠加形成范围型结构。

### 03 / 对冲密集区

#### 大型组合仓位可能把价格区间变成对冲密集区

机构组合仓位可能在某些 Strike 区间形成集中的 Gamma / Vega 暴露。当 ES / NQ 接近这些区间时，期权风险管理可能改变期货盘面的流动性。

- 对冲密集区可能表现为吸附、压制或突破后的加速。
- 组合名称本身不重要，仓位方向和风险暴露才重要。

## 相关概念

- [[single-leg-payoff|单腿盈亏结构]] — 多腿结构的风险形状由各单腿盈亏相加而成。
- [[vertical-ratio-backspread|垂直价差、Ratio Spread 与 Backspread]] — 垂直与比率结构是同一族结构的数量与方向变体。
- [[no-arbitrage-and-synthetics|无套利边界与合成头寸]] — 结构定价必须满足相同的无套利约束，否则可被拆解套利。
- [[portfolio-greeks-node-aggregation|组合 Greeks 与节点聚合：先统一单位，再讨论净敞口]] — 结构的组合 Greeks 由各腿按数量与到期汇总得到。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Vertical spreads, straddles, strangles, butterflies, and iron condors are structural examples here for reading how risk layers together.

Understand how multiple option legs combine into one risk structure, not how to enter a strategy.

### 01 / Additive Logic

#### A Structure's Payoff Is The Sum Of Its Legs

Multi-leg structures are not magic. Each leg has direction, strike, premium, quantity, and multiplier; net payoff is the sum of those leg payoffs.

- **Net payoff**

  ```latex
  \text{Net Payoff}=\text{Leg}_1+\text{Leg}_2+\text{Leg}_3+\text{Leg}_4
  ```

### 02 / Common Structures

#### Names Are Labels; Risk Boundaries Matter

A vertical spread uses two strikes to bound one side of risk. Straddles and strangles include both upside and downside exposure. Butterflies and iron condors layer legs into range-shaped risk.

Do not turn these into 'good for range' or 'good for breakout' trade advice. The point is whether risk is limited, unlimited, capped, or nonlinear.

- Vertical spread: two legs bound one tail.
- Straddle / strangle: two-sided exposure around realized range.
- Butterfly / iron condor: several legs create range-shaped exposure.

### 03 / Hedging Zones

#### Large Structures Can Turn Price Areas Into Hedging Zones

Institutional structures can concentrate gamma / vega exposure around strike ranges. When ES / NQ approaches those ranges, options risk management can change futures liquidity.

- Hedging zones may appear as pinning, compression, or acceleration after a break.
- The structure name matters less than positioning direction and exposure.

## Related Concepts

- [[single-leg-payoff|Single-Leg Payoff Structure]] — A multi-leg structure's risk shape is the sum of its single-leg payoffs.
- [[vertical-ratio-backspread|Vertical Spreads, Ratio Spreads, And Backspreads]] — Vertical and ratio structures are quantity and direction variants of the same family.
- [[no-arbitrage-and-synthetics|No-Arbitrage Bounds And Synthetic Positions]] — A structure must satisfy the same no-arbitrage constraint or it can be taken apart and arbitraged.
- [[portfolio-greeks-node-aggregation|Portfolio Greeks And Node Aggregation: Align Units Before Net Exposure]] — A structure's portfolio Greeks aggregate from its legs by quantity and expiry.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

