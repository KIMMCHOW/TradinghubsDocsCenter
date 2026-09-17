---
title: "同一价位在不同市场：指数、ETF 与期货的换算"
title_en: "One Level, Three Markets: Converting Between Cash Index, ETF And Futures"
slug: "index-futures-etf-level-conversion"
type: lesson
level: Advanced
order: 98
track: futures-and-options-linkage
track_label: "期货与期权衔接"
reading_time: "19 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/期货与期权衔接"
  - "权限/需登录"
aliases:
  - "同一价位在不同市场：指数、ETF 与期货的换算"
  - "One Level, Three Markets: Converting Between Cash Index, ETF And Futures"
  - "index-futures-etf-level-conversion"
source_url: "https://tradinghubs.org/docs/trading-knowledge/index-futures-etf-level-conversion"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 同一价位在不同市场：指数、ETF 与期货的换算

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[futures-and-options-linkage|期货与期权衔接]]
> 上一课：[[expected-move-intraday-sigma|盘中预期波动区间（±1σ）]] ｜ 下一课：[[orderflow-velocity-and-thresholds|订单流测量的三种类型：累计、净额与速度]]

**高级 · 期货与期权衔接 · 19 分钟**

> 分析师给出一个指数层面的关键位，交易者下单的却是期货合约。两者之间的差距不是噪声，而是一个有定义、可计算、同时也会随时间漂移的量。本课把换算拆成两种模型，并说明各自会在什么时候失效。

期权关键位来自指数期权，而交易发生在期货或 ETF 上：本课说明加法基差与仿射缩放两类换算、微型合约的对应关系，以及为什么换算结果必须连同基差时点与合约月份一起记录。

### 01 / 加法基差

#### 同一资产的现金指数与期货之间是基差关系

现金指数不可直接交易，而期货在到期前按市场对资金成本与股息的预期定价，因此两者之间存在一个差值：期货价格约等于现金指数加上基差点数。基差由短期利率、成分股股息与到期时间共同决定，并在交易时段内随利率预期与股息预测变化。所以在把指数关键位搬到期货币种时，必须使用当下的基差，而不是某个固定常数。

这也意味着关键位在期货图表上不是一个静止的价位数：随着到期临近，基差会自然收敛到零，所以同一水平在远月与近月的表示并不相同。记录换算结果时，合约月份与基差时点与价格本身同等重要。

- **加法基差模型**

  ```latex
  F_{\text{futures}}\approx I_{\text{cash}}+B
  ```
  B 为当期基差点数，随利率、股息与到期时间变化，并随到期临近收敛。

- **基差收敛**

  ```latex
  B\rightarrow 0\quad\text{as}\quad T\rightarrow 0
  ```
  到期时期货价格与最终结算价一致，因此基差必然消失。

### 02 / 仿射缩放

#### ETF 与商品期货需要乘数加偏移

当来源是 ETF 或另一种计价单位时，单一偏移不足以完成换算，还需要一个乘数。典型形式是「目标价格 = 来源价格 × 乘数 + 偏移」。这一形式既覆盖了 ETF 份额与指数点位之间的倍数关系，也覆盖了不同商品合约的报价单位差异。它同样适用于微型合约：迷你合约与微型合约通常只改变每点金额，不改变价格坐标，因此价位可以直接沿用。

换算时最容易出错的地方是把两种模型混用：对指数与期货之间套用乘数，或对 ETF 与期货之间只用偏移。判断依据不是习惯，而是来源与目标的计价单位是否同尺度。若两者同尺度，只需偏移；若不同尺度，则必须先缩放再偏移。

还有两个工程细节会直接影响下单：一是关键位换算后的取整，必须取到目标合约最小变动价位的整数倍；二是换算不会改变该水平相对当前价格的位置，它只是坐标变换。

| 来源 | 目标 | 使用的模型 |
| --- | --- | --- |
| 现金指数 | 对应的股指期货 | 加法基差：期货 ≈ 指数 + 基差点数。 |
| ETF 价格 | 对应的指数期货 | 仿射：乘数与偏移同时使用。 |
| 迷你合约 | 微型合约 | 价格坐标不变，仅每点金额不同。 |
| 任一来源 | 下单价格 | 取整到目标合约最小变动价位。 |

### 03 / 失效与记录

#### 基差会漂移，参考合约会换月

基差不是常数。短期利率预期的变化、股息季节性与到期时间的缩短都会让它在盘中移动，因此早盘换算出来的期货币种价位，到下午可能已经偏了几个最小变动价位。把换算结果当作静态值并长期沿用，是这一类误差最常见的来源。

第二类风险来自合约本身：主力合约会在某个时点切换到下一月份，而参考坐标随之改变。若只记录了价位而没有记录适用的合约，事后无法还原当时的关键位落在哪里。第三类风险来自模型边界——当市场出现明显的资金紧张、特殊股息处理或流动性断裂时，简单的基差模型会显著偏离，此时应当降低对该换算值的依赖，而不是继续精算。

因此换算的正确交付形式是一组字段：来源市场与计价单位、目标合约与月份、所用乘数与偏移、基差时点、以及取整后的目标价位。缺少其中任意一项，这个数字在事后都不再可用。

> [!tip] 换算只是换坐标
> 换算不会创造新的信息，也不会改变该水平相对当前价格的位置。它只是把同一个水平用另一种计价单位表达出来。

> [!warning] 过期的换算是错的
> 基差在盘中会漂移，换月会改变参考合约。沿用未经更新的换算值下单，等同于使用一个已经失效的价格。

- 第一步：确认来源市场的计价单位与目标合约，判断该用加法还是仿射模型。
- 第二步：记录基差或乘数与偏移的取值，以及取数时点。
- 第三步：把结果取整到目标合约最小变动价位，并确认合约月份仍为主力。
- 风险边界：资金紧张、特殊股息或流动性断裂时，简单换算模型会明显偏离。

## 相关概念

- [[futures-contract-mechanics-tick-value|期货合约机制：最小变动、点值与展期]] — 换算后的取整与每点金额由合约规格决定。
- [[forwards-futures-basis-cost-of-carry|远期、期货、基差与持有成本：从现货到股指公平价值]] — 基差的理论来源是持有成本关系。
- [[synthetic-futures-and-delta-equivalent-sizing|用期权表达期货敞口：合成结构与等值换算]] — 等值手数换算与价位换算是同一套跨市场算术的两个部分。
- [[futures-flow-from-options-positioning|期权定位如何传导到期货价格]] — 期权定位传导到期货价格时，必须先完成坐标换算。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> An analyst quotes a key level on the index while the trader executes in a futures contract. The gap between them is not noise: it is a defined, computable quantity that also drifts over time. This lesson splits the conversion into two models and states when each stops working.

Option key levels come from index options while trading happens in futures or ETFs: this lesson covers additive basis and affine scaling conversions, the micro-contract mapping, and why a converted level must be recorded with its basis timestamp and contract month.

### 01 / Additive Basis

#### Cash Index And Its Future Differ By A Basis

A cash index cannot be traded directly, and a future is priced to expiry by the market's expectation of financing cost and dividends, so a difference sits between them: the futures price is approximately the cash index plus a basis in index points. That basis is set by short rates, index dividends, and time to expiry, and it moves during the session with rate expectations and dividend forecasts. Converting an index level into a futures level therefore requires the basis of the moment rather than a fixed constant.

It also means a key level is not a stationary price on a futures chart: the basis converges toward zero as expiry approaches, so the same level maps differently in a far month than in the front month. When a converted level is recorded, the contract month and the basis timestamp matter as much as the price itself.

- **Additive basis model**

  ```latex
  F_{\text{futures}}\approx I_{\text{cash}}+B
  ```
  B is the current basis in index points, driven by rates, dividends, and time to expiry, and it converges as expiry approaches.

- **Basis convergence**

  ```latex
  B\rightarrow 0\quad\text{as}\quad T\rightarrow 0
  ```
  At expiry the futures price equals final settlement, so the basis must disappear.

### 02 / Affine Scaling

#### ETFs And Commodity Futures Need A Multiplier Plus An Offset

When the source is an ETF or a different unit of quotation, an offset alone will not convert it: a multiplier is also required. The typical form is target price = source price × multiplier + offset. That form covers both the multiple between an ETF share and index points and the unit differences between commodity contracts. It also covers micro contracts: mini and micro variants normally change the currency per point only, not the price coordinate, so the level itself carries over unchanged.

The most common conversion error is mixing the two models: applying a multiplier between an index and its future, or using only an offset between an ETF and a future. The test is not habit but whether the source and target quote in the same unit. Same unit means an offset suffices; different units mean scaling must come before the offset.

Two implementation details directly affect execution: a converted level must be rounded to a whole multiple of the target contract's minimum tick, and the conversion does not change the level's position relative to current price because it is only a coordinate change.

| Source | Target | Model Used |
| --- | --- | --- |
| Cash index | Its equity-index future | Additive: futures ≈ index + basis points. |
| ETF price | The matching index future | Affine: multiplier and offset together. |
| Mini contract | Micro contract | The price coordinate is unchanged; only currency per point differs. |
| Any source | Order price | Rounded to the target contract's minimum tick. |

### 03 / Drift And Recording

#### The Basis Drifts And The Reference Contract Rolls

The basis is not constant. Shifting short-rate expectations, dividend seasonality, and a shorter time to expiry all move it during the session, so a futures-level conversion done in the morning can be off by several ticks by the afternoon. Treating a conversion as a static value and reusing it is the most common source of this error.

The second risk is the contract itself: the front month rolls to the next month at some point and the reference coordinate changes with it. A record that stores only the price and not the applicable contract cannot be reconstructed later. The third risk is the model boundary - when funding is stressed, a dividend is treated specially, or liquidity breaks, a simple basis model departs materially, and the response is to lean less on the converted value rather than to compute it harder.

The correct deliverable for a conversion is therefore a set of fields: the source market and its unit, the target contract and month, the multiplier and offset applied, the basis timestamp, and the rounded target price. Missing any one of them leaves the number unusable afterwards.

> [!tip] Conversion Only Changes Coordinates
> A conversion creates no new information and does not change where the level sits relative to price. It only expresses the same level in another unit.

> [!warning] A Stale Conversion Is Wrong, Not Approximate
> The basis drifts during the session and a roll changes the reference contract. Ordering from an unrefreshed conversion means using a price that has already expired.

- Step one: confirm the source unit and target contract, then decide between the additive and affine models.
- Step two: record the basis or the multiplier and offset along with the timestamp they came from.
- Step three: round the result to the target contract's tick and confirm the contract month is still the front month.
- Risk boundary: stressed funding, special dividends, or a liquidity break make a simple conversion depart materially.

## Related Concepts

- [[futures-contract-mechanics-tick-value|Futures Contract Mechanics: Tick Size, Tick Value, And Rolls]] — The rounding and currency per point after conversion come from the contract specification.
- [[forwards-futures-basis-cost-of-carry|Forwards, Futures, Basis, And Cost Of Carry: From Spot To Equity-Index Fair Value]] — The theoretical source of the basis is the cost-of-carry relation.
- [[synthetic-futures-and-delta-equivalent-sizing|Expressing Futures Exposure With Options: Synthetics And Equivalent Sizing]] — Lot-equivalent sizing and level conversion are two halves of the same cross-market arithmetic.
- [[futures-flow-from-options-positioning|How Options Positioning Transmits Into Futures Prices]] — When options positioning transmits into futures prices, the coordinate conversion has to happen first.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-equity-index-basis
- cftc-futures-basics
- cme-volume-open-interest
