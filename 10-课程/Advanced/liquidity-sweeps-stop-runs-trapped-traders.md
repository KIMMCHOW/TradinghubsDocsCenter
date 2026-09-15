---
title: "流动性扫荡、止损猎杀与被困交易者"
title_en: "Liquidity Sweeps, Stop Runs, And Trapped Traders"
slug: "liquidity-sweeps-stop-runs-trapped-traders"
type: lesson
level: Advanced
order: 86
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
  - "流动性扫荡、止损猎杀与被困交易者"
  - "Liquidity Sweeps, Stop Runs, And Trapped Traders"
  - "liquidity-sweeps-stop-runs-trapped-traders"
source_url: "https://tradinghubs.org/docs/trading-knowledge/liquidity-sweeps-stop-runs-trapped-traders"
source_file: "Tradinghub-Web/components/site/options-knowledge/orderflow-data.ts"
generated: 2026-09-15
---

# 流动性扫荡、止损猎杀与被困交易者

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[absorption-exhaustion-and-iceberg-orders|吸收、衰竭与冰山单]] ｜ 下一课：[[options-order-flow-dex-gex-convexity|期权订单流：Delta、Gamma 与凸性加权]]

**高级 · 订单流与市场微观结构 · 20 分钟**

> 扫荡不是一个预测规则，而是一类可被记录的事件：某些价位同时聚集了止损单、挂单与将要被强平的仓位。事件之后走哪条路径，取决于承接是否延续。

解释价格快速穿过关键价位、触发集中止损后的几种路径：流动性空洞、被动承接失败、以及被困持仓被迫平仓形成的反馈。

### 01 / 流动性与扫荡

#### 缺少对手意愿时，价格以跳跃方式移动

在流动性充足的市场中，每一档价位都有挂单，价格移动是连续的。当某段价格的挂单被快速消耗或提前撤走时，同一数量成交可以推动价格跨越多档，形成流动性空洞。扫荡与空洞都是流动性结构变化的结果，不是单一参与者发布的消息。

止损单在成交前并不显示在盘口，但它们的分布有规律：常聚集在前高、前低、整数位与近期区间边缘。这意味着这些价位附近同时存在止损触发与被动承接两种力量，二者的相对强弱决定价格穿越后是延续还是回到区间内部。

### 02 / 被困仓位与反馈

#### 被否定的一方必须平仓，平仓又强化原方向

当价格穿越某个被广泛信任的价位时，在该价位附近建立仓位的一方论点被否定，被迫减仓或反向平仓。平仓本身是市价成交，会进一步推动价格朝穿越方向前进，形成短时自我强化。

这种反馈有明确终点：一旦被迫平仓的量耗尽，或价格进入新的密集成交区，推动力就会衰减。观察重点是穿越后成交量是否继续放大、价格是否在新区域形成接受。若成交量迅速回落且价格立即返回原区间，更接近一次失败的试探而不是趋势启动。

- 延续的证据：穿越后成交量持续、回撤在突破位获得承接。
- 失败的证据：穿越成交稀疏、快速返回、原区间重新成交。
- 边界：同一形态在不同流动性环境下会得到相反结果。

### 03 / 角色互换

#### 被接受的穿越会把角色互换

如果价格在突破位之上或之下形成接受，原来的承接方会转为反向参考：支撑变为上方回撤的阻力，阻力变为下方反弹的支撑。角色互换是接受过程的副产品，而不是价格记住某个数字。没有接受，就没有互换。

这类结构对风险管理的要求高于对预测的要求。穿越后的位移可能非常快，因此常见的失败模式不是方向判断错误，而是仓位与止损距离在使用高波动结构时没有相应调整。

- 先确认流动性结构（挂单密度、近期区间边缘），再解释穿越。
- 把穿越后的成交量与接受情况作为主要证据，而非穿越本身。
- 在可能出现快速位移的结构中预先压缩仓位与止损距离。
- 把无法验证的“猎杀意图”说法替换为可观察的流动性与成交记录。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> A sweep is not a prediction rule but a recordable event: some price levels hold clustered stop orders, resting orders, and positions that will be forced to close. Which path follows depends on whether defence persists.

Explain the paths that follow a fast sweep through a key level: liquidity voids, failed passive defence, and the feedback created when trapped positions are forced to close.

### 01 / Liquidity And Sweeps

#### When Opposing Interest Is Missing, Price Moves In Steps

In a liquid market every tick has resting orders, so price moves continuously. When size in a band is consumed quickly or withdrawn in advance, the same order can push price across several ticks and create a liquidity void. Sweeps and voids are consequences of liquidity structure, not messages published by one participant.

Stop orders are not displayed before they execute, but their distribution is patterned: they cluster around prior highs and lows, round numbers, and the edges of recent ranges. That means both stop triggers and passive defence exist near those prices, and which dominates decides whether price continues after the cross or returns inside the range.

### 02 / Trapped Positions And Feedback

#### The Negated Side Must Close, And Closing Reinforces The Move

When price crosses a level that was widely relied on, the participants positioned around it have their premise negated and are forced to reduce or reverse. Those closes execute aggressively and push price further in the direction of the break, producing brief self-reinforcement.

The feedback has an identifiable end: once forced closes are exhausted, or price reaches a new concentration of business, the push decays. The signals to watch are whether volume keeps expanding after the cross and whether price forms acceptance in the new area. If volume collapses and price returns inside the old range quickly, the probe failed rather than starting a trend.

- Evidence of continuation: volume persists after the cross and pullbacks find defence at the broken level.
- Evidence of failure: thin trade through the level, fast return, and business resuming in the old range.
- Boundary: the same shape resolves differently in different liquidity conditions.

### 03 / Role Conversion

#### An Accepted Cross Converts The Level's Role

If price establishes acceptance above or below the broken level, the former defence becomes the opposite reference: support becomes resistance on a pullback and resistance becomes support on a bounce. Role conversion is a by-product of acceptance, not price remembering a number. Without acceptance there is no conversion.

Structures like this demand more from risk management than from forecasting. Displacement after a cross can be very fast, so the common failure is not a wrong direction but a position size and stop distance that were never adjusted for the higher volatility of the structure.

- Confirm the liquidity structure — order density and recent range edges — before interpreting a cross.
- Use post-cross volume and acceptance as the evidence, not the cross itself.
- Reduce size and stop distance in advance when fast displacement is possible.
- Replace unverifiable claims about intent with observable liquidity and execution records.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

