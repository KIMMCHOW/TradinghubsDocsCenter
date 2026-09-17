---
title: "订单流测量的三种类型：累计、净额与速度"
title_en: "Three Measurement Types In Options Flow: Cumulative, Net And Velocity"
slug: "orderflow-velocity-and-thresholds"
type: lesson
level: Advanced
order: 99
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "19 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "订单流测量的三种类型：累计、净额与速度"
  - "Three Measurement Types In Options Flow: Cumulative, Net And Velocity"
  - "orderflow-velocity-and-thresholds"
source_url: "https://tradinghubs.org/docs/trading-knowledge/orderflow-velocity-and-thresholds"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 订单流测量的三种类型：累计、净额与速度

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[index-futures-etf-level-conversion|同一价位在不同市场：指数、ETF 与期货的换算]] ｜ 下一课：[[dealer-hedging-bands-and-discrete-rebalance|对冲区间与离散再平衡：为什么对冲不是连续动作]]

**高级 · 订单流与市场微观结构 · 19 分钟**

> 订单流指标常被当成一类东西使用，但它们测量的对象并不相同。一个指标回答「今天累计买了多少」，另一个回答「现在链条的净敞口是多少」，第三个回答「刚刚一秒里变化了多少」。把它们混在一张图上比较，等于把三个不同问题当成一个问题。

同一张订单流图上混着三种不同的问题：日内累计成交的方向、当前链条的净敞口、以及每秒变化的速度；本课说明三者的定义差异、量级门槛的作用，以及混用会怎样制造错误的结论。

### 01 / 三种测量

#### 先确认你问的是哪一类问题

第一类是日内累计：从开盘起把每笔分类成交按方向累加，得到「今天市场整体买了多少、卖了多少」。它衡量一整段时间的累计方向压力，最适合用来描述全天基调，但对当下的变化反应很慢。它不会因为过去十分钟出现大额反向成交而立刻转向，因为更早的累计部分仍然留在曲线里。

第二类是当前链条净敞口：把每个执行价的有符号敞口加总，得到此刻整条链的净值。它的时间基准是「现在」，不包含历史累计，因此适合判断当前结构偏向哪一侧，但不回答今天是怎么走到这里的。它会在仓位被平掉时回落，这是它与累计口径最直观的区别。

第三类是速度指标：衡量最近一段时间内敞口变化的速率，回答「刚刚发生了什么」以及「变化有多快」。它对大额单笔成交最敏感，也最容易受到噪声影响。速度指标的价值在于捕捉转折的时点，而不是判断结构本身的大小。

- **日内累计（概念式）**

  ```latex
  A_{t}=\sum_{\tau\le t} x_{\tau}
  ```
  从开盘起的分类成交按方向累加，包含整段时间的历史，因此对当下变化反应迟缓。

- **当前净额与速度（概念式）**

  ```latex
  N_{t}=\sum_{k} n_{k,t},\qquad V_{t}=\dfrac{N_{t}-N_{t-\Delta t}}{\Delta t}
  ```
  N_t 为当前链条净额，V_t 为其在 Δt 窗口内的变化率。两者不可互相替代。

### 02 / 量级门槛

#### 过滤门槛把噪声压掉，同时也改变了曲线

订单流图上通常有一个最小量级输入：低于该绝对值的成交不计入，达到或超过才显示，而设为 0 相当于关闭过滤。它的作用是把日常小额成交压掉，让较大的单向成交更容易被看到。这在实际使用中很有价值，但也意味着同一条曲线在不同门槛下是两件不同的东西。

因此比较时必须保持门槛一致。用高门槛的序列与低门槛的序列对比「今天是否更活跃」，得到的差异里包含门槛差异，而不只是市场差异。记录时应把门槛值当作图表配置的一部分，与时间窗口、到期范围一起保存。

门槛还有一个容易被忽略的副作用：它改变了累计与速度两类曲线的形状，却不改变净额的定义。同一时段内，提高门槛会让速度指标出现更少但更陡的峰值，而累计曲线会变得更阶梯化。理解这一点，可以避免把过滤造成的外观误读成市场行为改变。

| 测量类型 | 回答的问题 | 典型误用 |
| --- | --- | --- |
| 日内累计 | 今天整体偏向哪一侧。 | 用它判断当下转折时点。 |
| 当前净额 | 此刻链条的净敞口在哪一侧。 | 把它当作全天累计流量。 |
| 速度 | 最近一段时间变化有多快。 | 用它推断结构规模。 |
| 过滤门槛 | 哪些成交会被计入曲线。 | 跨门槛比较两条曲线的水平。 |

### 03 / 记录纪律

#### 先写类型，再写读数

一个可复核的记录应该先声明测量类型，再写出读数与配置。这样做的原因是三种类型对同一事件的反应完全不同：一笔大额反向成交会让速度指标立刻反向，让当前净额部分回落，却可能完全不动日内累计。若记录中没有类型，事后无法判断当时看到的是什么。

第二个纪律是不要把三者的方向简单相加。它们的时间基准、单位与包含范围都不同，同向不代表互相确认，反向也不代表出现了矛盾。真正需要比较的是各自在自身口径下的变化，以及与价格和成交是否一致。

最后一层限制来自数据本身：分类结果依赖分类规则，价差与多腿组合会被拆分记账，隐藏流动性会改变主动方的判定。这套指标适合描述相对强度与变化关系，不适合当作精确的仓位或资金数字。凡是需要精确数量的判断，都应回到可审计的公开数据源。

> [!tip] 三种类型不可互换
> 累计描述全天基调，净额描述此刻结构，速度描述刚刚的变化。用错类型会让同一个事件的解读完全相反。

> [!note] 门槛是配置，不是结论
> 改变门槛会改变曲线外观，但不会改变市场。记录门槛值，才能在事后区分两者。

- 第一步：先声明正在读的是累计、净额还是速度。
- 第二步：记录时间窗口、到期范围与过滤门槛。
- 第三步：把该口径下的变化与价格、成交量一起核对，再决定是否提高权重。
- 风险边界：分类流量是相对强度证据，不适合当作精确仓位数字。

## 相关概念

- [[options-order-flow-dex-gex-convexity|期权订单流：Delta、Gamma 与凸性加权]] — 该课定义了 Delta、Gamma 与凸性加权序列，本课说明它们的测量类型。
- [[order-flow-footprint-delta-cvd|订单流、Footprint、Delta 与累计 Delta]] — 期货侧的 Delta 与累计 Delta 存在同样的三种测量类型区分。
- [[aggregate-options-data|Aggregate Data：总量结构怎么读]] — 总量页面的口径规则与门槛记录要求完全一致。
- [[absorption-exhaustion-and-iceberg-orders|吸收、衰竭与冰山单]] — 判断吸收需要速度与净额同时对齐，而累计口径无法提供这种时点信息。
- [[net-exposure-balance-metrics|净敞口平衡指标：单值重心与量级门槛]] — 当前净额正是单值平衡指标的一种，其量级门槛逻辑与本课一致。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Options-flow metrics are often used as if they were one thing, but they measure different objects. One answers how much was cumulatively traded today, another answers the chain's current net exposure, and a third answers how much changed in the last second. Comparing them on one chart treats three questions as one.

One options-flow chart mixes three different questions: the direction of cumulated session trading, the current net exposure of the chain, and the per-second rate of change. This lesson separates the three definitions, explains what a magnitude filter does, and shows how mixing them produces wrong conclusions.

### 01 / Three Measurements

#### First Establish Which Question You Are Asking

The first type is session cumulative: from the open, every classified trade is added with its direction, producing how much the market bought and sold overall today. It measures cumulative directional pressure over a stretch of time, which makes it good for the session's tone and slow to react to the present. A large reverse trade ten minutes ago will not flip it, because the earlier accumulated part is still on the curve.

The second type is the current chain net: sum the signed exposure across strikes to get the chain's value right now. Its time basis is the present and it contains no accumulated history, so it describes which way the structure currently leans without saying how the session got there. It can fall back when positions are closed, which is the clearest visible difference from the cumulative measure.

The third type is a velocity indicator: it measures how fast exposure changed over a recent interval, answering what just happened and how quickly. It is the most sensitive to a single large trade and also the most exposed to noise. Its value is timing a turning point, not sizing the structure itself.

- **Session cumulative (conceptual)**

  ```latex
  A_{t}=\sum_{\tau\le t} x_{\tau}
  ```
  Classified trades are accumulated with direction from the open, so the whole earlier history is present and the reaction to the present is slow.

- **Current net and velocity (conceptual)**

  ```latex
  N_{t}=\sum_{k} n_{k,t},\qquad V_{t}=\dfrac{N_{t}-N_{t-\Delta t}}{\Delta t}
  ```
  N_t is the current chain net and V_t is its rate of change over the window Δt. Neither substitutes for the other.

### 02 / Magnitude Filters

#### A Magnitude Filter Removes Noise And Changes The Curve

An options-flow chart usually carries a minimum-magnitude input: trades below that absolute size do not register, trades at or above it render normally, and a value of zero disables filtering. Its purpose is to suppress routine small prints so that larger one-sided trades are easier to see. That is genuinely useful and it also means the same curve under two thresholds is two different objects.

Comparisons must therefore keep the threshold fixed. Contrasting a high-threshold series with a low-threshold one to ask whether today was busier measures the threshold difference as much as the market. When recording, the threshold belongs in the chart configuration alongside the time window and expiry scope.

A less obvious side effect is that the threshold reshapes the cumulative and velocity curves while leaving the definition of net exposure untouched. Over the same period, raising the threshold produces fewer but steeper velocity peaks and a more stepped cumulative curve. Knowing this prevents mistaking a filter artefact for a change in market behaviour.

| Measurement | Question Answered | Typical Misuse |
| --- | --- | --- |
| Session cumulative | Which way the session leaned overall. | Using it to time a current turning point. |
| Current net | Which side the chain's net exposure is on right now. | Treating it as the whole session's accumulated flow. |
| Velocity | How fast exposure changed over a recent interval. | Using it to infer the size of the structure. |
| Magnitude filter | Which trades enter the curve. | Comparing curve levels across two thresholds. |

### 03 / Recording Discipline

#### Write The Type Before The Reading

A reviewable record states the measurement type first and then the reading and its configuration. The reason is that the three types react to the same event completely differently: a large reverse trade flips velocity immediately, pulls the current net back partially, and may not move the cumulative curve at all. Without the type in the record, later review cannot tell what was actually seen.

The second rule is not to add the three directions together. They differ in time basis, unit, and inclusion, so agreement is not confirmation and disagreement is not a contradiction. What should be compared is how each moved within its own definition, and whether price and volume agree.

A final limit comes from the data: classification depends on the classification rule, spreads and multi-leg packages are booked leg by leg, and hidden liquidity changes who appears to be the aggressor. These metrics describe relative intensity and changing relationships well and stand poorly as precise position or flow figures. Any judgement that needs an exact quantity should return to an auditable public source.

> [!tip] The Three Types Are Not Interchangeable
> Cumulative describes the session's tone, net describes the current structure, and velocity describes what just changed. Using the wrong type can invert the reading of one event.

> [!note] The Threshold Is Configuration, Not A Conclusion
> Changing the threshold changes the curve's appearance, not the market. Recording the threshold is what lets later review separate the two.

- Step one: declare whether you are reading cumulative, net, or velocity.
- Step two: record the time window, the expiry scope, and the magnitude filter.
- Step three: check the change in that measure against price and volume before raising its weight.
- Risk boundary: classified flow is relative-intensity evidence and is not a precise position figure.

## Related Concepts

- [[options-order-flow-dex-gex-convexity|Options Order Flow: Delta, Gamma, And Convexity Weighting]] — That lesson defines the delta, gamma, and convexity weighted series; this one explains their measurement types.
- [[order-flow-footprint-delta-cvd|Order Flow, Footprint, Delta, And Cumulative Delta]] — Futures-side delta and cumulative delta carry the same three-way measurement distinction.
- [[aggregate-options-data|Aggregate Data: How To Read The Total Structure]] — The aggregate view's scope rules match the recording requirement for thresholds exactly.
- [[absorption-exhaustion-and-iceberg-orders|Absorption, Exhaustion, And Iceberg Orders]] — Judging absorption needs velocity and net aligned; a cumulative measure cannot supply that timing.
- [[net-exposure-balance-metrics|Net Exposure Balance Metrics: A Single Balance Value And Its Magnitude Thresholds]] — Current net exposure is a balance metric, and its magnitude-threshold logic matches this lesson.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- nyfed-market-liquidity
- glosten-milgrom-original
- cme-volume-open-interest
