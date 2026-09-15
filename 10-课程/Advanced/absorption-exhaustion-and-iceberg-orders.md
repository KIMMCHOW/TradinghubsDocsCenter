---
title: "吸收、衰竭与冰山单"
title_en: "Absorption, Exhaustion, And Iceberg Orders"
slug: "absorption-exhaustion-and-iceberg-orders"
type: lesson
level: Advanced
order: 87
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "20 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "吸收、衰竭与冰山单"
  - "Absorption, Exhaustion, And Iceberg Orders"
  - "absorption-exhaustion-and-iceberg-orders"
source_url: "https://tradinghubs.org/docs/trading-knowledge/absorption-exhaustion-and-iceberg-orders"
source_file: "Tradinghub-Web/components/site/options-knowledge/orderflow-data.ts"
generated: 2026-09-15
---

# 吸收、衰竭与冰山单

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[avellaneda-stoikov-market-making|Avellaneda–Stoikov 做市模型：库存偏移、价差与校准]] ｜ 下一课：[[liquidity-sweeps-stop-runs-trapped-traders|流动性扫荡、止损猎杀与被困交易者]]

**高级 · 订单流与市场微观结构 · 20 分钟**

> 吸收不是反转信号，而是“此处对手意愿充足”的记录。是否改变方向，取决于后续成交与流动性是否继续存在。

分辨被动承接、主动衰竭与隐藏流动性：三种状态在成交量、Delta 与价格反应上各自留下什么证据，以及它们何时不成立。

### 01 / 吸收机制

#### 成交放大而价格不再推进

吸收发生在被动方持续以限价承接主动成交时。可观察的特征是：该价位成交量显著放大、主动方向的一侧持续占优、但价格位移越来越小。市场含义是每一次推进都被同等或更强的对手意愿抵消。

吸收的强度由持续时间与价格反应共同衡量，而不是由单次大额成交衡量。一笔巨量成交之后价格立即向原方向继续前进，说明对手意愿已被消耗完；只有价格反复停滞，才说明承接具有持续性。

- 证据：同价位成交连续放大、位移缩小、回撤被迅速买回或卖回。
- 反证：成交量放大后价格迅速穿越该价位，说明承接被吸收完。
- 边界：吸收可以在趋势内反复出现，并不自动指向反转。

### 02 / 衰竭机制

#### 主动方仍在，但边际效果下降

衰竭描述的是主动方数量或质量下降：成交仍然同向，但每一单位成交带来的价格位移递减。它与吸收的区别在于对手盘的角色——吸收是新增被动意愿，衰竭是主动意愿消耗。实务上两者常常同时出现，需要成交量、Delta 斜率与价格斜率三者一起判断。

成交量的相对变化比绝对水平更有信息。把当日成交量按活跃度分层，观察大额成交是否在关键价位集中出现，可以区分持续的机构式参与与零星的大单；但任何分层都依赖阈值选择，阈值改动会改变结论。

### 03 / 隐藏流动性

#### 冰山单只显示一部分，补量会重复出现

冰山单在盘口只展示申报量的一部分，成交后自动补足剩余数量。其可观察痕迹不是静态挂单，而是同一价位被反复吃掉后重新出现等量规模，且价格反复无法穿透。补量的节奏与规模在不同市场与经纪商规则下不同。

需要区分隐藏流动性与虚假挂单：前者在被成交时提供真实数量，后者只试图影响他人判断并在触及前消失。外部无法直接读取意图，因此唯一可靠的判据是“这个价位是否真的成交、成交后价格是否反应”。

| 状态 | 观察证据 | 失效条件 |
| --- | --- | --- |
| 吸收 | 成交放大、位移递减、反复停滞。 | 该价位被迅速穿透。 |
| 衰竭 | 同向成交持续但单位效果下降。 | 新信息带来新的参与度。 |
| 冰山单 | 同价位被吃掉后等量补回。 | 补量停止或价格直接穿透。 |

### 04 / 市场影响

#### 把状态记录成假设，而不是结论

吸收、衰竭与隐藏流动性都是对当时流动性状况的描述。它们可以在很长时间内维持，也可能在一次新闻或一次大额风险调整后立即失效。任何基于它们的判断都需要明确的失效条件。

- 用位移衰减而不是成交额大小判断吸收。
- 把成交量按活跃度分层时固定阈值，并说明阈值敏感度。
- 用“是否真的成交”区分隐藏流动性与虚假挂单。
- 为每一种状态预设明确的失效条件，再讨论如何利用。

## 相关概念

- [[order-flow-footprint-delta-cvd|订单流、Footprint、Delta 与累计 Delta]] — 吸收必须用主动成交量与价格位移的背离来识别。
- [[order-book-depth-and-resting-liquidity|订单簿、深度与挂单流动性]] — 冰山与隐藏单解释了可见深度为何低估真实承接意愿。
- [[auction-market-theory-value-and-imbalance|拍卖市场理论：价值、平衡与失衡]] — 吸收成功或失败决定失衡区是否被价值区重新接受。
- [[liquidity-sweeps-stop-runs-trapped-traders|流动性扫荡、止损猎杀与被困交易者]] — 吸收失败后的价格位移常表现为扫荡与被困仓位。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Absorption is not a reversal signal; it records that opposing interest was sufficient at that moment. Whether direction changes depends on what the following business and liquidity do.

Separate passive absorption, aggressive exhaustion, and hidden liquidity: the evidence each leaves in volume, delta, and price response, and the conditions under which each read fails.

### 01 / Absorption Mechanism

#### Volume Expands While Price Stops Progressing

Absorption occurs when a passive side keeps meeting aggressive flow with resting orders. The observable pattern is expanding volume at the level, a persistent aggressive side, and progressively smaller price displacement. The market meaning is that each push is being met by equal or greater opposing interest.

The strength of absorption is measured by how long it lasts together with the price response, not by any single large print. If price resumes its original direction immediately after a huge print, the opposing interest was simply consumed; only repeated stalling indicates a persistent counterparty.

- Evidence: repeated heavy volume at one level, shrinking displacement, pullbacks quickly bought or sold back.
- Counter-evidence: price crosses the level quickly after the volume spike, meaning absorption was exhausted.
- Boundary: absorption can recur inside a trend and does not automatically imply reversal.

### 02 / Exhaustion Mechanism

#### The Aggressive Side Is Still There, But Its Marginal Effect Falls

Exhaustion describes a decline in the size or quality of the aggressive side: flow continues in the same direction, but each unit of volume produces less displacement. It differs from absorption in who is acting — absorption adds passive interest, exhaustion consumes aggressive interest. In practice both can appear together, so volume, delta slope, and price slope must be read jointly.

Relative changes in volume carry more information than absolute levels. Layering the session by participation and checking whether large prints cluster at key prices separates sustained participation from isolated orders; every such layer depends on a chosen threshold, and moving the threshold changes the conclusion.

### 03 / Hidden Liquidity

#### An Iceberg Displays A Fraction And Replenishes Repeatedly

An iceberg order displays only a fraction of its size in the book and replenishes after each fill. Its observable footprint is not static displayed size but the repeated reappearance of similar size at the same price after it is consumed, paired with repeated failure of price to trade through. Replenishment behaviour differs across venues and broker rules.

Hidden liquidity must be separated from spoofing: the former supplies real size when it trades, the latter only tries to influence others and disappears before the touch. Intent cannot be read directly from outside, so the reliable test is whether the level actually trades and how price responds afterwards.

| State | Observable evidence | Failure condition |
| --- | --- | --- |
| Absorption | Volume expands, displacement shrinks, price stalls repeatedly. | The level gets crossed quickly. |
| Exhaustion | Same-side flow persists while marginal effect falls. | New information brings fresh participation. |
| Iceberg | Equal size returns after repeated consumption. | Replenishment stops or price trades straight through. |

### 04 / Market Impact

#### Record The State As A Hypothesis, Not A Conclusion

Absorption, exhaustion, and hidden liquidity all describe the liquidity state at a moment. They can persist for a long time and can also fail immediately on news or a single large risk adjustment. Any judgement built on them needs an explicit invalidation condition.

- Judge absorption by decaying displacement rather than by the size of a print.
- Fix the layering threshold and state how sensitive the conclusion is to it.
- Separate hidden liquidity from spoofing by whether the level actually trades.
- Define an explicit invalidation for each state before discussing how to use it.

## Related Concepts

- [[order-flow-footprint-delta-cvd|Order Flow, Footprint, Delta, And Cumulative Delta]] — Absorption must be identified through divergence between aggressive volume and price displacement.
- [[order-book-depth-and-resting-liquidity|Order Book Depth And Resting Liquidity]] — Iceberg and hidden orders explain why visible depth understates real willingness to absorb.
- [[auction-market-theory-value-and-imbalance|Auction Market Theory: Value, Balance, And Imbalance]] — Whether absorption succeeds decides if an imbalance zone is re-accepted by the value area.
- [[liquidity-sweeps-stop-runs-trapped-traders|Liquidity Sweeps, Stop Runs, And Trapped Traders]] — A failed absorption usually shows up as a sweep and trapped positions.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

