---
title: "期权基础：合约与报价"
title_en: "Options Basics: Contracts And Quotes"
slug: "options-contract-and-quote"
type: lesson
level: Beginner
order: 8
track: options-foundations
track_label: "期权基础与合约"
reading_time: "11 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/期权基础与合约"
  - "权限/需登录"
aliases:
  - "期权基础：合约与报价"
  - "Options Basics: Contracts And Quotes"
  - "options-contract-and-quote"
source_url: "https://tradinghubs.org/docs/trading-knowledge/options-contract-and-quote"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 期权基础：合约与报价

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[options-foundations|期权基础与合约]]
> 上一课：[[sunk-cost-commitment-escalation|沉没成本与承诺升级]] ｜ 下一课：[[option-value-moneyness-put-call-parity|期权价值、价内价外与 Put-Call Parity]]

**初级 · 期权基础与合约 · 11 分钟**

> 本课只处理期权合约语言和报价语言。对冲、OI、GEX、DEX、IV 等结构性知识会作为独立课程学习，避免把多个知识点塞进同一页。

读懂 Call、Put、Strike、Premium、Bid / Ask、价内价外、乘数和基础报价字段，为后续 OI、GEX、DEX 与做市商对冲课程打底。

### 01 / 合约语言

#### Call、Put、Long、Short 先定义权利和义务

Call 给买方按合约规则获得上涨一侧结算价值的权利，Put 给买方获得下跌一侧结算价值的权利。美式合约通常可在到期日或之前行权，欧式合约通常只能在到期日行权；实物结算可能交付标的，现金结算则支付规定差额。Long 表示买入期权、支付 Premium；Short 表示卖出期权、收取 Premium。

Strike 是合约的参考价格，不是自动买卖点。Expiration 决定这份权利还剩多少时间，Multiplier 决定每 1 点价格变化对应多少合约金额；行权风格、结算方式和乘数都必须以当前合约规范为准。

| 字段 | 含义 | 误读边界 |
| --- | --- | --- |
| Strike | 行权参考价，常承载仓位聚集。 | 不是机械支撑或阻力。 |
| Premium | 期权价格，包含内在价值和时间价值。 | 高 Premium 不等于方向更确定。 |
| Open Interest | 未平仓合约数量，描述存量仓位。 | 需要结合 Volume 和价差看活跃度。 |

### 02 / 报价与价值

#### Bid / Ask 说明交易摩擦，Mid 只是中间参考

Bid 是市场愿意买入的价格，Ask 是市场愿意卖出的价格。Spread 越宽，说明进入和退出这份合约的摩擦越大。

Intrinsic Value 来自当前 Spot 与 Strike 的关系；Extrinsic Value 则包含时间、波动率、事件风险和供需溢价。

- **中间价**

  ```latex
  \text{Mid}=\frac{\text{Bid}+\text{Ask}}{2}
  ```

- **价差**

  ```latex
  \text{Spread}=\text{Ask}-\text{Bid}
  ```

- **Call 内在价值**

  ```latex
  \max(\text{Spot}-\text{Strike},0)
  ```

- **Put 内在价值**

  ```latex
  \max(\text{Strike}-\text{Spot},0)
  ```

- **时间价值**

  ```latex
  \text{Extrinsic}=\text{Premium}-\text{Intrinsic}
  ```

### 03 / 下一步学习

#### 报价先回答合约是什么，结构压力要去独立课程里看

一张报价能告诉你权利、义务、价格、价差和乘数，但它还不能单独说明期货价格会不会被吸附、压制或放大。那些问题要分别进入 OI、做市商对冲、GEX、DEX 和 IV 课程。

- 先确认合约和报价字段，再讨论仓位和对冲压力。
- Bid / Ask 与 Volume 共同帮助判断某个价位是否真的有交易活跃度。
- 报价是基础语言，不是开仓建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> This lesson focuses only on option contract language and quote language. Hedging, OI, GEX, DEX, IV, and other structural topics are handled as standalone lessons instead of being folded into one page.

Read calls, puts, strikes, premium, bid / ask, moneyness, multipliers, and basic quote fields before moving into OI, GEX, DEX, and dealer-hedging lessons.

### 01 / Contract Language

#### Calls, Puts, Long, And Short Define Rights And Obligations

A call gives its holder the contract-defined right to the upside settlement value, while a put gives the right to the downside settlement value. American-style contracts are generally exercisable on or before expiry, while European-style contracts are generally exercisable only at expiry; physical settlement may deliver the underlying, whereas cash settlement pays a defined difference. Long means buying the option and paying premium; short means selling it and collecting premium.

The strike is a contract reference price, not an automatic buy or sell point. Expiration defines remaining time, and the multiplier converts one price point into contract value; exercise style, settlement method, and multiplier must all be read from the current contract specification.

| Field | Meaning | Boundary |
| --- | --- | --- |
| Strike | Exercise reference price, often where positioning clusters. | Not mechanical support or resistance. |
| Premium | Option price, including intrinsic and extrinsic value. | High premium does not mean direction is certain. |
| Open Interest | Open contracts, describing standing positioning. | Needs volume and spread context for activity. |

### 02 / Quote And Value

#### Bid / Ask Shows Friction, Mid Is Only A Reference

Bid is where the market is willing to buy, and ask is where it is willing to sell. A wider spread means higher friction to enter or exit the contract.

Intrinsic value comes from the relationship between spot and strike; extrinsic value contains time, volatility, event risk, and supply-demand premium.

- **Mid price**

  ```latex
  \text{Mid}=\frac{\text{Bid}+\text{Ask}}{2}
  ```

- **Spread**

  ```latex
  \text{Spread}=\text{Ask}-\text{Bid}
  ```

- **Call intrinsic value**

  ```latex
  \max(\text{Spot}-\text{Strike},0)
  ```

- **Put intrinsic value**

  ```latex
  \max(\text{Strike}-\text{Spot},0)
  ```

- **Extrinsic value**

  ```latex
  \text{Extrinsic}=\text{Premium}-\text{Intrinsic}
  ```

### 03 / Next Learning Step

#### Quotes Identify The Contract; Structural Pressure Belongs In Separate Lessons

A quote tells you rights, obligations, price, spread, and multiplier, but it does not by itself explain pinning, compression, or volatility expansion in futures. Those questions belong in the standalone OI, dealer-hedging, GEX, DEX, and IV lessons.

- Confirm contract and quote fields before discussing positioning and hedging pressure.
- Bid / ask and volume together help judge whether the level is actually active.
- Quote language is foundation, not an entry recommendation.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

