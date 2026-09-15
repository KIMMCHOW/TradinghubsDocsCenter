---
title: "订单簿、深度与挂单流动性"
title_en: "Order Book Depth And Resting Liquidity"
slug: "order-book-depth-and-resting-liquidity"
type: lesson
level: Beginner
order: 16
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "16 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "订单簿、深度与挂单流动性"
  - "Order Book Depth And Resting Liquidity"
  - "order-book-depth-and-resting-liquidity"
source_url: "https://tradinghubs.org/docs/trading-knowledge/order-book-depth-and-resting-liquidity"
source_file: "Tradinghub-Web/components/site/options-knowledge/orderflow-data.ts"
generated: 2026-09-15
---

# 订单簿、深度与挂单流动性

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[market-orders-limit-orders-bid-ask|市价单、限价单与买卖报价]] ｜ 下一课：[[rates-treasuries-central-bank-transmission|利率、国债与央行传导]]

**初级 · 订单流与市场微观结构 · 16 分钟**

> 盘口不是一张静态地图，而是一份随时可撤销的意图清单。本课帮助您判断哪些流动性值得依赖，哪些只是展示。

理解撮合、价格优先与时间优先、可见深度与隐藏流动性，以及撤单、叠加、冰山单为什么会让盘口看起来比实际更厚或更薄。

### 01 / 撮合规则

#### 价格优先、时间优先决定谁先成交

撮合引擎持续把新到达的订单与簿内最优价位的挂单配对：买价大于等于卖价时成交，成交价通常取先挂单的价格。同一价位上，先到者先成交，这就是排队位置（queue position）的价值。

因此同一价位的限价单并非等价：排在队首的订单更容易在价格短暂触及该位时成交，排在队尾的订单可能需要价格穿越该位才能成交，而穿越往往同时意味着逆向选择。

### 02 / 深度结构

#### 可见深度只是流动性的一部分

深度按价位累积，离中间价越远的价位通常挂单越多，因为远离市价的报价更不容易被逆向选择。深度的形状（近端薄、远端厚，或相反）描述的是提供流动性的意愿分布，而不是价格目标。

隐藏流动性包括冰山单（只显示一部分，成交后自动补量）与其他非公开指示。隐藏挂单不会出现在盘口深度里，却会在被吃掉时留下成交量与价格反应，因此“深度为零”不等于“没有流动性”。

- 近端深度被快速吃完但价格几乎不动：可能有隐藏流动性在承接。
- 某价位挂单持续增大且价格始终无法接近：该价位正在被主动维护。
- 挂单在价格接近前突然消失：这是撤单行为，不是被成交。

### 03 / 盘口行为

#### 撤单、叠加与虚假挂单的区别在于是否意图成交

撤单（pulling）是流动性提供者在风险变化时收回报价，属于正常风险管理；叠加（stacking）是同一侧持续加厚，通常反映真实的承接或压制意愿；虚假挂单（spoofing）是挂出并不打算成交的巨量订单以影响他人判断，在多數司法辖区属于违法操纵行为。

从外部只能观察行为，无法直接读出意图。实务上更有意义的问题不是“这是不是幌骗”，而是“当价格真正到达该价位时，这些流动性是否仍然存在，是否真的成交”。成交与价格反应才是证据。

| 行为 | 盘口表现 | 合理解释 |
| --- | --- | --- |
| 撤单 Pulling | 价格接近时挂单量快速减少。 | 流动性提供者降低风险敞口，仓位不会留下成交。 |
| 叠加 Stacking | 同一侧价位持续增厚。 | 存在真实的承接或压制意愿，仍需成交验证。 |
| 虚假挂单 Spoofing | 巨量挂单在触及前消失，随后反向成交。 | 操纵行为；作为信号极不可靠且违法。 |

### 04 / 市场影响

#### 薄盘口放大价格反应，但不创造方向

同样的成交量在薄盘口中会造成更大的价格位移，在厚盘口中可能几乎不留痕迹。这就是为什么“成交量很大”与“价格大幅波动”并不等价，也是为什么低流动性时段的成交需要更谨慎地解读。

- 先看盘口深度与价差，再判断成交量是否异常。
- 把撤单与成交分开统计：只有成交才改变持仓。
- 隐藏流动性只能用成交与价格反应推断，不能从盘口读出。
- 薄盘口中的一次大成交不能单独证明趋势。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> The book is not a static map; it is a continuously cancellable list of intentions. This lesson separates liquidity that can be relied on from liquidity that is only being displayed.

Understand matching, price and time priority, visible versus hidden liquidity, and how cancellations, stacking, and iceberg orders can make the book look thicker or thinner than it really is.

### 01 / Matching Rules

#### Price Then Time Priority Decides Who Fills First

The matching engine continuously pairs incoming orders with the best resting orders: a trade occurs when the best bid is at or above the best ask, and the resting order's price typically sets the fill price. Within one price level, earlier orders fill first, which is why queue position has value.

Two limit orders at the same price are therefore not equivalent. The front of the queue fills when price merely touches the level; the back of the queue may need price to trade through the level, and that usually means adverse selection came with the fill.

### 02 / Depth Structure

#### Visible Depth Is Only Part Of Available Liquidity

Depth accumulates by price level, and levels farther from the mid usually hold more size because a distant quote is less exposed to adverse selection. The shape of that depth — thin near the touch, thick farther out, or the reverse — describes the distribution of willingness to supply liquidity, not a price target.

Hidden liquidity includes iceberg orders, which display only a fraction of their size and replenish after each fill, plus other undisclosed indications. Hidden orders never appear in displayed depth, yet they leave evidence in traded volume and price response, so zero displayed depth does not mean zero liquidity.

- Near-touch depth is consumed quickly while price barely moves: hidden liquidity may be absorbing it.
- Size at one level keeps growing while price cannot reach it: that level is being actively defended.
- Size disappears before price arrives: that is a cancellation, not a fill.

### 03 / Book Behaviour

#### Pulling, Stacking, And Spoofing Differ By Whether Execution Is Intended

Pulling is a liquidity provider withdrawing a quote as risk changes, which is normal risk management. Stacking is repeatedly thickening one side, which usually reflects real willingness to buy or sell. Spoofing is displaying size that the sender never intends to trade in order to distort other participants' decisions, and in most jurisdictions it is illegal manipulation.

From outside the book you can observe behaviour but not intent. The more useful question is not whether something is spoofing but whether that liquidity is still present, and actually trades, when price arrives. Fills and price response are the evidence; displayed size is not.

| Behaviour | What you see | Reasonable read |
| --- | --- | --- |
| Pulling | Displayed size shrinks as price approaches. | The provider cuts risk; no fill is created. |
| Stacking | One side thickens repeatedly. | Genuine absorption or supply interest, still needing fill confirmation. |
| Spoofing | Large size vanishes before the touch, then trades the other way. | Manipulative; unusable as a signal and illegal. |

### 04 / Market Impact

#### A Thin Book Amplifies Price Response Without Creating Direction

The same traded volume produces a larger price displacement in a thin book and may leave almost no trace in a deep one. That is why large volume does not equal a large move, and why prints in low-liquidity sessions deserve extra caution.

- Read depth and spread before judging whether volume is unusual.
- Separate cancellations from fills; only fills change positioning.
- Hidden liquidity can only be inferred from fills and price response, never read from the book.
- One large print in a thin book cannot establish a trend by itself.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

