---
title: "用期权表达期货敞口：合成结构与等值换算"
title_en: "Expressing Futures Exposure With Options: Synthetics And Equivalent Sizing"
slug: "synthetic-futures-and-delta-equivalent-sizing"
type: lesson
level: Advanced
order: 90
track: futures-and-options-linkage
track_label: "期货与期权衔接"
reading_time: "22 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/期货与期权衔接"
  - "权限/需登录"
aliases:
  - "用期权表达期货敞口：合成结构与等值换算"
  - "Expressing Futures Exposure With Options: Synthetics And Equivalent Sizing"
  - "synthetic-futures-and-delta-equivalent-sizing"
source_url: "https://tradinghubs.org/docs/trading-knowledge/synthetic-futures-and-delta-equivalent-sizing"
source_file: "Tradinghub-Web/components/site/options-knowledge/futures-linkage-data.ts"
generated: 2026-09-15
---

# 用期权表达期货敞口：合成结构与等值换算

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[futures-and-options-linkage|期货与期权衔接]]
> 上一课：[[options-order-flow-dex-gex-convexity|期权订单流：Delta、Gamma 与凸性加权]] ｜ 下一课：[[futures-flow-from-options-positioning|期权定位如何传导到期货价格]]

**高级 · 期货与期权衔接 · 22 分钟**

> 本课回答一个具体问题：想表达期货观点，但不愿承担期货账户与保证金机制时，期权能否替代、如何换算、代价是什么。所有换算都必须回到合约规范与当时报价。

用同一执行价的 Call 与 Put 合成期货方向敞口，把期权 Delta 换算成期货手数，并说清期权替代期货在保证金、时间价值、到期与行权规则上的全部代价。

### 01 / 合成结构

#### 同一执行价的 Long Call 加 Short Put 就是合成多头

把同一标的、同一执行价、同一到期日的 Call 与 Put 组合在一起，两者的时间价值在执行价处相互抵消：价格高于执行价时只有 Call 有价值，价格低于执行价时只有 Put 有价值，于是组合的到期收益曲线变成一条斜率固定的直线，与期货或远期的到期损益同形。买入 Call 并卖出 Put 得到合成多头，买入 Put 并卖出 Call 得到合成空头。

这不是巧合，而是 Put-Call Parity 的直接结果：同执行价的 Call 减 Put 等于现货减执行价的现值。因此合成头寸的盈亏平衡点是执行价加上（或减去）建立组合时净支付的权利金，而期货的盈亏平衡点由成交价决定。两者形状相同，定价基准与结算机制不同，这正是后面所有代价的来源。

- **Put-Call Parity**

  ```latex
  C-P=S-\text{PV}(K)
  ```
  PV(K) 为执行价的现值；股息或持有收益会改变等式右侧。

- **合成多头**

  ```latex
  \text{Long Call}+\text{Short Put}\approx\text{Long Forward}
  ```

- **合成空头**

  ```latex
  \text{Long Put}+\text{Short Call}\approx\text{Short Forward}
  ```

- **合成多头盈亏平衡**

  ```latex
  \text{Break-even}=K+\text{Net premium paid}
  ```
  净权利金为收到的 Put 权利金减去支付的 Call 权利金。

### 02 / 等值换算

#### 手数由金额对齐，而不是张数对齐

期权与期货的每一跳价值不同，因此不能按张数一比一换算。先把期权换算成“每 1 点标的价格变动对应的金额”：期权 Delta 乘以该合约的乘数，再乘以张数。再把它除以期货合约的每点金额，得到等效期货手数。同一单位下，期权的方向暴露可以用期货张数表达。

举例：某指数期权每 1.00 Delta 对应每点固定金额，10 张、每张 Delta 为 0.30 的合约合计为 3.00 个“期权 Delta 单位”；若一份指数期货每点为该金额的一半，则等效手数为 6 手。方向相反时符号相反：空头合成对应卖出等值期货手数。

Delta 会随价格移动而改变，所以等值手数是一个瞬时值而不是固定值。价格远离执行价时，深度价内的 Call 向 1 靠近、深度价外的 Put 趋近于 0，合成结构的净 Delta 会变化，期权端与期货端的实际暴露随之发散。这一点在滚动检查时最容易被忽略。

- **期权每点金额暴露**

  ```latex
  \text{Exposure}=n_{o}\times\Delta\times M_{o}
  ```
  n_o 为期权张数，Δ 为每张 Delta，M_o 为每 1.00 Delta 对应的每点金额。

- **等效期货手数**

  ```latex
  n_{f}=\frac{n_{o}\times\Delta\times M_{o}}{M_{f}}
  ```
  M_f 为期货合约的每点金额；符号按多空方向取正负。

- **组合的净 Delta 暴露**

  ```latex
  \text{Net exposure}=\sum_{i} n_{i}\Delta_{i}M_{i}
  ```
  多腿组合必须先按同一乘数口径求和，再比较期货手数。

### 03 / 替代品的代价

#### 期权替代期货改变的是现金流与约束，不是方向

买入期权替代多头期货时，资金占用从保证金变为权利金，风险在到期前被锁定为已支付金额；代价是时间价值随时间流失，并且价格不动时也会亏钱。卖出期权替代期货方向时，收到的权利金是收益上限，但价格朝不利方向运行会带来扩张中的亏损，这与期货的线性亏损在形状上相似、在路径上不同。

三类约束必须先核对。第一是到期：期货可以按需展期并保持敞口，期权到期即消失，合成结构必须主动滚动，滚动时重新支付价差与时间价值。第二是行权规则：指数期权通常为欧式、现金结算，而期货期权通常为美式、行权后交割为期货合约，提前行权与指派会提前改变敞口。第三是流动性：宽价差与薄盘口会放大建立与退出成本，并使等值换算的价格失真。

波动率是第四项代价，也是最容易被忽略的一项。买入期权时同时买入波动率：如果方向判断正确但隐含波动率回落，期权端的收益可能小于期货端的等值收益；反过来，卖出期权时承担波动率上升的风险。因此“用期权替代期货”的真实比较对象不是期货价格，而是期货价格加波动率与时间这两个维度。

| 维度 | 期货 | 期权合成 |
| --- | --- | --- |
| 资金占用 | 按保证金要求，逐日结算。 | 买方为权利金；卖出腿仍需相应保证金。 |
| 时间影响 | 无时间价值，只有基差与融资。 | 时间价值持续流失，需滚动重建。 |
| 风险形状 | 线性，两端无限。 | 买腿有限、卖腿扩张；组合近似线性。 |
| 行权风险 | 不适用，但有交割与展期规则。 | 美式期货期权可能提前指派，敞口提前改变。 |

### 04 / 应用与失效

#### 什么时候值得用，什么时候必须放弃

常见的合理用途有三类：以有限风险表达方向观点；用期权端对冲既有期货仓位而不改变名义规模；以及在波动率本身成为判断对象时，用期权而不是期货表达。共同前提是：换算口径明确、到期时间与持有周期匹配、退出成本可接受。

失效情形同样明确：持有周期长于期权到期而没有滚动计划；方向正确但时间价值与波动率回落抵消了收益；卖出腿在流动性不足的合约上被提前指派；把瞬时 Delta 等值当成固定手数使用；以及忽略指数与期货之间的基差与结算差异，直接把两个市场的同一价格水平当作同一件事。

- 先确定换算口径与乘数，再讨论用期权还是期货表达观点。
- 把到期时间与持有周期对齐，并预先写出滚动规则。
- 把时间价值与波动率变化计入对比，不要只看方向是否正确。
- 核对行权风格与结算方式，美式期货期权存在提前指派风险。
- 等值手数随价格变动，必须在过程里重新计算而不是一次设定。

## 相关概念

- [[no-arbitrage-and-synthetics|无套利边界与合成头寸]] — 合成期货是看涨看跌平价与无套利约束的直接应用。
- [[futures-contract-mechanics-tick-value|期货合约机制：最小变动、点值与展期]] — 等值手数必须使用目标合约的真实点值。
- [[delta-curve|Delta 曲线：从 Buy Call 推导方向敏感度]] — 合成敞口随标的变化，因为其 Delta 不是常数。
- [[futures-flow-from-options-positioning|期权定位如何传导到期货价格]] — 等值换算是把期权仓位转化为期货对冲需求的算术桥梁。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> This lesson answers a concrete question: if you want futures exposure without futures margin mechanics, can options substitute, how do you size it, and what does the substitution cost. Every conversion must return to the contract specification and the live quote.

Build a futures-equivalent directional exposure from a call and a put at the same strike, convert option delta into futures lots, and account for every cost the substitute introduces: margin, time value, expiry, and exercise rules.

### 01 / Synthetic Construction

#### A Long Call Plus A Short Put At One Strike Is A Synthetic Long

Combine a call and a put on the same underlying, at the same strike and expiry, and their extrinsic values offset at the strike: above the strike only the call carries value, below it only the put does, so the combined expiration payoff becomes a straight line with a fixed slope — the same shape as a future or forward. Buying the call and selling the put creates a synthetic long; buying the put and selling the call creates a synthetic short.

This is not a coincidence but a direct consequence of put-call parity: at one strike, the call minus the put equals spot minus the present value of the strike. The synthetic's break-even is therefore the strike adjusted by the net premium paid or received when it was opened, while a futures break-even is set by the traded price. The shapes match; the pricing basis and settlement mechanics do not, and that difference is the source of every cost discussed below.

- **Put-call parity**

  ```latex
  C-P=S-\text{PV}(K)
  ```
  PV(K) is the present value of the strike; dividends or carry change the right-hand side.

- **Synthetic long**

  ```latex
  \text{Long Call}+\text{Short Put}\approx\text{Long Forward}
  ```

- **Synthetic short**

  ```latex
  \text{Long Put}+\text{Short Call}\approx\text{Short Forward}
  ```

- **Synthetic long break-even**

  ```latex
  \text{Break-even}=K+\text{Net premium paid}
  ```
  Net premium is the put premium received minus the call premium paid.

### 02 / Equivalent Sizing

#### Lots Come From Equal Money Risk, Not Equal Counts

Options and futures do not carry the same value per price point, so a one-to-one contract conversion is wrong. First express the option position as money per point of underlying movement: option delta times the contract multiplier times the number of contracts. Then divide by the futures contract's currency amount per point to obtain the equivalent number of futures lots.

An example: if one index-option delta corresponds to a fixed currency amount per point, ten contracts at 0.30 delta each total 3.00 option-delta units; if one index futures contract is worth half that amount per point, the equivalent size is six lots. The sign follows the direction: a synthetic short corresponds to selling the equivalent futures lots.

Delta changes as price moves, so the equivalent size is an instantaneous value, not a constant. Farther from the strike, a deep in-the-money call approaches one while a far out-of-the-money put approaches zero, the synthetic's net delta shifts, and the option and futures exposures diverge. This is the step most often missed when the position is reviewed.

- **Option money risk per point**

  ```latex
  \text{Exposure}=n_{o}\times\Delta\times M_{o}
  ```
  n_o is the number of option contracts, delta is the per-contract delta, and M_o is the currency amount per point per unit of delta.

- **Equivalent futures lots**

  ```latex
  n_{f}=\frac{n_{o}\times\Delta\times M_{o}}{M_{f}}
  ```
  M_f is the futures contract's currency amount per point, and the sign follows the position direction.

- **Net book delta exposure**

  ```latex
  \text{Net exposure}=\sum_{i} n_{i}\Delta_{i}M_{i}
  ```
  A multi-leg book must be summed in one multiplier convention before it is compared with futures lots.

### 03 / Costs Of The Substitute

#### The Substitution Changes Cash Flow And Constraints, Not Direction

Replacing long futures with long options converts capital use from margin into premium and caps the loss at the amount paid before expiry; the cost is time decay, which loses money even when price does nothing. Replacing futures direction with sold options caps the gain at the premium received, while adverse movement creates an expanding loss — similar in shape to a futures loss, different in path.

Three constraints must be checked first. Expiry: futures exposure can be rolled and held, while options expire and a synthetic must be actively rolled, paying the spread and new time value each time. Exercise rules: index options are generally European and cash-settled, while options on futures are generally American and exercise into a futures contract, so early exercise and assignment can change the exposure earlier than expected. Liquidity: wide spreads and thin books inflate entry and exit cost and distort the equivalency arithmetic.

Volatility is the fourth cost and the easiest to overlook. Buying an option also buys volatility: if direction is right but implied volatility falls, the option leg can earn less than the equivalent futures position. Selling an option takes the opposite exposure. The honest comparison for 'options instead of futures' is therefore not the futures price alone but the futures price plus a volatility and time dimension.

| Dimension | Futures | Options synthetic |
| --- | --- | --- |
| Capital use | Margin requirement, settled daily. | Premium for the long leg; the short leg still carries margin. |
| Time effect | No time value; only basis and financing. | Time value decays and must be rolled and rebuilt. |
| Risk shape | Linear and unbounded both ways. | Long leg bounded, short leg expanding; the pair approximates a linear payoff. |
| Exercise risk | Not applicable, but delivery and roll rules apply. | American-style futures options can be assigned early, changing exposure sooner. |

### 04 / Application And Failure

#### When The Substitution Helps And When It Must Be Abandoned

Three reasonable uses recur: expressing a directional view with capped risk, hedging an existing futures position without changing its notional size, and expressing a view when volatility itself is the object. All three require an explicit conversion convention, an expiry that matches the holding period, and an acceptable exit cost.

The failure list is equally clear: a holding period longer than the option expiry with no roll plan; correct direction offset by time decay and falling volatility; a short leg assigned early in an illiquid contract; treating an instantaneous delta equivalence as a fixed lot size; and ignoring basis and settlement differences between an index and a futures market by treating the same price level as the same thing.

- Fix the conversion convention and multiplier before choosing between options and futures.
- Align expiry with the holding period and write the roll rule in advance.
- Include time decay and volatility change in the comparison, not only direction.
- Verify exercise style and settlement; American-style futures options carry early-assignment risk.
- Equivalent lots change with price and must be recomputed during the trade, not set once.

## Related Concepts

- [[no-arbitrage-and-synthetics|No-Arbitrage Bounds And Synthetic Positions]] — A synthetic future is a direct application of put-call parity and the no-arbitrage constraint.
- [[futures-contract-mechanics-tick-value|Futures Contract Mechanics: Tick Size, Tick Value, And Rolls]] — Equivalent sizing must use the real tick value of the target contract.
- [[delta-curve|Delta Curve: Deriving Directional Sensitivity From A Buy Call]] — A synthetic exposure drifts with the underlying because its delta is not constant.
- [[futures-flow-from-options-positioning|How Options Positioning Transmits Into Futures Prices]] — Equivalent sizing is the arithmetic bridge from option positioning to futures hedge demand.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

