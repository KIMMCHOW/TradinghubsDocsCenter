---
title: "期权价值、价内价外与 Put-Call Parity"
title_en: "Option Value, Moneyness, And Put-Call Parity"
slug: "option-value-moneyness-put-call-parity"
type: lesson
level: Beginner
order: 9
track: options-foundations
track_label: "期权基础与合约"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/期权基础与合约"
  - "权限/需登录"
aliases:
  - "期权价值、价内价外与 Put-Call Parity"
  - "Option Value, Moneyness, And Put-Call Parity"
  - "option-value-moneyness-put-call-parity"
source_url: "https://tradinghubs.org/docs/trading-knowledge/option-value-moneyness-put-call-parity"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# 期权价值、价内价外与 Put-Call Parity

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[options-foundations|期权基础与合约]]
> 上一课：[[options-contract-and-quote|期权基础：合约与报价]] ｜ 下一课：[[single-leg-payoff|单腿盈亏结构]]

**初级 · 期权基础与合约 · 18 分钟**

> 权利金不是方向概率，也不是最大可赚金额。它是一组现金流、剩余时间、波动率和交易摩擦共同形成的价格；本课建立一套可重复核对这些组成部分的语言。

把权利金拆成内在价值与时间价值，区分价内、平值、价外，并用 Put-Call Parity 检查同执行价 Call 与 Put 的相对价格。

### 01 / 价值拆分

#### 先分清立即行权价值，再讨论剩余价值

Call 的内在价值来自标的价格高于执行价的部分，Put 的内在价值来自执行价高于标的价格的部分，且两者都不会小于零。权利金扣除内在价值后的余额通常称为时间价值或外在价值。

外在价值补偿的是尚未实现的不确定性，而不是一笔保证返还的存款。剩余期限、隐含波动率、利率、股息或持有收益、供需和报价宽度都可能改变它，因此相同内在价值不代表相同权利金。

- **Call 内在价值**

  ```latex
  \operatorname{IV}_{C}=\max(S-K,0)
  ```

- **Put 内在价值**

  ```latex
  \operatorname{IV}_{P}=\max(K-S,0)
  ```

- **外在价值**

  ```latex
  \operatorname{EV}=\text{Premium}-\operatorname{IV}
  ```

| 观察项 | 能回答的问题 | 不能推出的结论 |
| --- | --- | --- |
| 内在价值 | 现在行权是否有现金价值。 | 未来一定盈利。 |
| 外在价值 | 市场为剩余不确定性支付多少。 | 到期前会完整保留。 |
| 权利金 | 当前合约报价的总价格。 | 上涨或下跌的真实概率。 |

### 02 / 相对价格

#### Moneyness 描述位置，Parity 约束相对价格

对 Call 而言，标的高于执行价通常称为价内；对 Put 则相反。平值不是永远固定在某个现货价上：在有利率、股息或持有成本时，远期价格往往比现货更适合比较同到期合约的相对位置。

对同一标的、执行价和到期日的欧式期权，Call 与 Put 不是两张互不相关的票。在连续收益率 q 的口径下，等式右侧的折现标的项是今天预付、到期交付一单位标的的预付远期价值；它不是今天买入一股实际股票。实际持股支付现货价，并在到期前享有股息现金流；若看似偏离，先核对股息、借券、合约风格和可成交价。

- 所有腿必须使用同一标的、到期日、执行价、乘数和结算口径。
- Parity 是无套利关系，不是忽略交易成本后的自动套利提示。
- 美式提前行权、离散股息和借券约束会使简单等式需要调整。
- 若使用已知离散现金股息，预付远期价值应改为现货价减去这些股息的现值；不要把连续收益率 q 与同一批离散股息重复扣除。

- **无连续收益率时的 Parity**

  ```latex
  C-P=S_0-Ke^{-rT}
  ```

- **连续收益率下的预付远期 Parity**

  ```latex
  C-P=S_0e^{-qT}-Ke^{-rT}
  ```

- **远期形式**

  ```latex
  C-P=e^{-rT}(F_{0,T}-K)
  ```

### 03 / 阅读流程

#### 从合约对齐开始，而不是从“便宜或昂贵”开始

先确认标的、到期、执行价、期权风格、乘数和结算方式；再按可成交 Bid / Ask 而非只按 Mid 拆分内在与外在价值。随后比较相邻执行价和相邻到期，观察价值差异来自方向、时间还是波动率。

最后才使用 Parity 做一致性检查。短暂差值可能只是不同腿报价不同步、价差过宽或无法同时成交；未经成本、保证金、税务和行权流程核验，不应把屏幕差值解释为无风险收益。

- 第一步：对齐同一到期和执行价的 Call、Put 与远期参考。
- 第二步：把权利金拆成内在与外在价值，并标记报价宽度。
- 第三步：用 Parity 检查相对价格，但把股息、借券、风格和执行成本列为边界。
- 本流程用于识别价格组成，不构成对任何合约的交易建议。

## 相关概念

- [[options-contract-and-quote|期权基础：合约与报价]] — 先确认 Strike、Expiration 与乘数，Parity 才有明确定义。
- [[no-arbitrage-and-synthetics|无套利边界与合成头寸]] — 平价关系是第一个可检验的无套利约束，也是合成头寸的基础。
- [[forwards-futures-basis-cost-of-carry|远期、期货、基差与持有成本：从现货到股指公平价值]] — 平价中的远期项由持有成本与分红决定。
- [[time-value-and-theta|时间价值与 Theta]] — 内在价值与时间价值的拆分直接决定 Theta 的行为。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Premium is neither a directional probability nor a maximum-profit forecast. It is a price formed by cash flows, remaining time, volatility, and trading frictions; this lesson builds a repeatable language for checking those components.

Split premium into intrinsic and extrinsic value, distinguish in-, at-, and out-of-the-money contracts, and use put-call parity to check relative call and put prices at the same strike.

### 01 / Value Components

#### Separate Immediate Exercise Value Before Discussing The Remainder

A call's intrinsic value comes from spot being above the strike, while a put's comes from the strike being above spot; neither can be negative. Premium left after subtracting intrinsic value is commonly called time value or extrinsic value.

Extrinsic value compensates for unresolved uncertainty; it is not a refundable deposit. Time to expiry, implied volatility, rates, dividends or carry, supply and demand, and quote width can all change it, so equal intrinsic value does not imply equal premium.

- **Call intrinsic value**

  ```latex
  \operatorname{IV}_{C}=\max(S-K,0)
  ```

- **Put intrinsic value**

  ```latex
  \operatorname{IV}_{P}=\max(K-S,0)
  ```

- **Extrinsic value**

  ```latex
  \operatorname{EV}=\text{Premium}-\operatorname{IV}
  ```

| Observation | Question It Answers | What It Does Not Prove |
| --- | --- | --- |
| Intrinsic value | Whether immediate exercise has cash value. | That the position will be profitable later. |
| Extrinsic value | What the market pays for remaining uncertainty. | That it will survive intact to expiry. |
| Premium | The contract's current total quoted price. | The true probability of an up or down move. |

### 02 / Relative Pricing

#### Moneyness Describes Location; Parity Constrains Relative Price

A call is commonly in the money when spot is above strike; the relationship reverses for a put. At-the-money is not permanently anchored to one spot price: with rates, dividends, or carry, forward price is often the better reference for contracts sharing an expiry.

European calls and puts on the same underlying, strike, and expiry are not unrelated tickets. Under a continuous yield q, the discounted-underlying term is the value paid today for a prepaid forward delivering one unit of the underlying at expiry; it is not one actual share bought today. An actual shareholder pays spot and receives interim dividends. Apparent deviations require checks for dividends, borrow, exercise style, and executable prices.

- Every leg must share the same underlying, expiry, strike, multiplier, and settlement convention.
- Parity is a no-arbitrage relationship, not an automatic arbitrage alert after ignoring costs.
- American exercise, discrete dividends, and borrow constraints require adjustments to the simple equality.
- With known discrete cash dividends, replace the prepaid-forward value by spot less the present value of those dividends; do not subtract both a continuous yield q and the same discrete dividends.

- **Parity without continuous yield**

  ```latex
  C-P=S_0-Ke^{-rT}
  ```

- **Prepaid-forward parity with continuous yield**

  ```latex
  C-P=S_0e^{-qT}-Ke^{-rT}
  ```

- **Forward form**

  ```latex
  C-P=e^{-rT}(F_{0,T}-K)
  ```

### 03 / Reading Workflow

#### Start With Contract Alignment, Not A Cheap-Or-Expensive Label

First confirm underlying, expiry, strike, exercise style, multiplier, and settlement. Then split intrinsic and extrinsic value using executable bid and ask prices rather than mid alone. Compare neighboring strikes and expiries to see whether differences come from direction, time, or volatility.

Use parity only at the end as a consistency check. A temporary gap may reflect asynchronous quotes, wide spreads, or legs that cannot be filled together; without validating costs, margin, tax, and exercise mechanics, a screen difference should not be treated as risk-free profit.

- Step 1: Align the call, put, and forward reference for the same expiry and strike.
- Step 2: Split premium into intrinsic and extrinsic value and mark quote width.
- Step 3: Check relative pricing with parity while treating dividends, borrow, style, and execution costs as boundaries.
- This workflow identifies price components and is not a recommendation for any contract.

## Related Concepts

- [[options-contract-and-quote|Options Basics: Contracts And Quotes]] — Strike, expiration, and multiplier must be fixed before parity has a defined meaning.
- [[no-arbitrage-and-synthetics|No-Arbitrage Bounds And Synthetic Positions]] — Parity is the first testable no-arbitrage constraint and the basis of synthetic positions.
- [[forwards-futures-basis-cost-of-carry|Forwards, Futures, Basis, And Cost Of Carry: From Spot To Equity-Index Fair Value]] — The forward term inside parity is set by cost of carry and dividends.
- [[time-value-and-theta|Time Value And Theta]] — The split between intrinsic and time value directly determines how theta behaves.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

