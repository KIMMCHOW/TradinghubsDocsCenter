---
title: "市价单、限价单与买卖报价"
title_en: "Market Orders, Limit Orders, And The Bid-Ask Spread"
slug: "market-orders-limit-orders-bid-ask"
type: lesson
level: Beginner
order: 15
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "15 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "市价单、限价单与买卖报价"
  - "Market Orders, Limit Orders, And The Bid-Ask Spread"
  - "market-orders-limit-orders-bid-ask"
source_url: "https://tradinghubs.org/docs/trading-knowledge/market-orders-limit-orders-bid-ask"
source_file: "Tradinghub-Web/components/site/options-knowledge/orderflow-data.ts"
generated: 2026-09-15
---

# 市价单、限价单与买卖报价

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[options-volume-participation|Volume：期权参与强度怎么读]] ｜ 下一课：[[order-book-depth-and-resting-liquidity|订单簿、深度与挂单流动性]]

**初级 · 订单流与市场微观结构 · 15 分钟**

> 订单流分析的前提不是指标，而是订单本身：谁必须成交、谁可以选择等待。本课只建立这套语言，不涉及任何入场规则。

区分主动方与被动方、市价单与限价单，理解买卖报价、价差与成交代价如何决定一次交易是否真的“成交在你看到的价格上”。

### 01 / 主动与被动

#### 每笔成交都有一个必须成交的人

成交数量永远相等：有人买 10 手，就有人卖 10 手。真正不对称的是意愿——主动方用市价单穿过价差换取确定性，被动方把限价单挂在盘口等待成交。所谓“卖方主导”或“买方主导”，描述的正是这次成交由哪一方让步。

被动方提供流动性，主动方消耗流动性。被动方获得价差补偿，同时承担逆向选择风险：如果成交后价格立刻朝不利方向走，说明对手方可能知道得更多。主动方放弃价差，换取立刻成交和更低的不成交风险。

### 02 / 报价语言

#### Bid、Ask、Mid 与 Spread 描述的是代价，不是方向

Bid 是最优买单价格，Ask 是最优卖单价格。买方的市价单成交在 Ask，卖方的市价单成交在 Bid，因此刚成交就按对手价平仓会立刻损失一个价差。Mid 只是中间参考，不代表任何人都愿意在中间价与您成交。

价差宽度由竞争、库存风险、波动率、合约流动性以及事件不确定性共同决定。价差扩大通常意味着提供流动性的意愿下降，而不代表价格方向已经确定。同样可见的“深度”也可能被快速撤单，看到的挂单不等于承诺的流动性。

- **中间价**

  ```latex
  \text{Mid}=\frac{\text{Bid}+\text{Ask}}{2}
  ```

- **绝对价差**

  ```latex
  \text{Spread}=\text{Ask}-\text{Bid}
  ```

- **相对价差**

  ```latex
  \text{Relative spread}=\frac{\text{Ask}-\text{Bid}}{\text{Mid}}
  ```
  同一价差在低价合约上更昂贵；跨品种、跨价位比较时必须用相对价差。

### 03 / 订单类型

#### 市价单换确定性，限价单换价格

市价单保证成交（在有对手盘的前提下），但不保证价格；订单越大，越可能吃穿多个价位，实际成交均价偏离最优报价越远。限价单保证价格上限或下限，但不保证成交：可能完全未成交，也可能在价格短暂经过时部分成交。

限价单还有一层代价：它只有在对自己不利时更容易成交。价格快速穿过您的挂单价，往往意味着市场正在朝反方向走，这被称为逆向选择。因此“挂单等回踩”的期望成本不是零，而是成交概率乘以不利程度。

| 维度 | 市价单 | 限价单 |
| --- | --- | --- |
| 角色 | 主动方，消耗流动性。 | 被动方，提供流动性。 |
| 主要风险 | 滑点与冲击成本随规模上升。 | 不成交风险与逆向选择。 |
| 信息含量 | 立刻反映在成交价与成交量上。 | 只有被吃掉时才成为成交证据。 |

### 04 / 市场影响

#### 执行质量决定观察到的价格是否可信

同一时刻的成交价可以同时包含三种成分：真实的重定价、大单造成的临时冲击、以及流动性提供者要求的补偿。把三者混在一起，就会把执行成本误读成市场观点。

- 先确认价差与深度，再判断一笔大成交是否代表观点。
- 比较不同持仓、不同价位时使用相对价差，而不是绝对价差。
- 把未成交的挂单视为意图而非承诺，撤单可以让盘口在瞬间改变。
- 执行成本是概率加权的结果，单看一次成交无法证明方向。

## 相关概念

- [[order-book-depth-and-resting-liquidity|订单簿、深度与挂单流动性]] — 订单类型决定成交方式，盘口深度决定成交代价。
- [[liquidity-slippage-execution|流动性、滑点与期权执行]] — 主动与被动选择的差别最终体现为价差与滑点。
- [[price-discovery-market-clearing|价格发现与市场出清]] — 限价单与市场单的交互就是价格发现的过程。
- [[order-flow-footprint-delta-cvd|订单流、Footprint、Delta 与累计 Delta]] — 订单类型分类是解读主动成交与 Delta 的前提。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Order-flow analysis starts with orders, not indicators: who must trade now and who can afford to wait. This lesson builds only that language and contains no entry rules.

Separate aggressive from passive participants, distinguish market from limit orders, and understand how the bid, the ask, the spread, and order size determine the price a trade actually receives.

### 01 / Aggressor And Passive Side

#### Every Trade Has One Side That Had To Trade

Quantity always matches: someone buys ten lots because someone sells ten lots. What is asymmetric is willingness. The aggressive side crosses the spread with a market order to buy certainty now; the passive side rests a limit order and waits. When traders say a print was buyer- or seller-initiated, they are describing which side conceded on price.

The passive side supplies liquidity and the aggressive side consumes it. The supplier is paid the spread and carries adverse-selection risk: if price immediately moves against the fill, the counterparty may simply have known more. The aggressor gives up the spread in exchange for immediate execution and no fill risk.

### 02 / Quote Language

#### Bid, Ask, Mid, And Spread Describe Cost, Not Direction

The bid is the best resting buy price and the ask is the best resting sell price. A market buy fills at the ask and a market sell fills at the bid, so a position opened and immediately closed at the opposing quotes loses roughly one spread. The mid is a reference only; it is not a promise that anyone will trade there.

Spread width is set by competition, inventory risk, volatility, contract liquidity, and event uncertainty. A wider spread usually means less willingness to provide liquidity, not that direction has been decided. The same caution applies to visible depth: displayed size can be pulled, so displayed liquidity is not committed liquidity.

- **Mid price**

  ```latex
  \text{Mid}=\frac{\text{Bid}+\text{Ask}}{2}
  ```

- **Absolute spread**

  ```latex
  \text{Spread}=\text{Ask}-\text{Bid}
  ```

- **Relative spread**

  ```latex
  \text{Relative spread}=\frac{\text{Ask}-\text{Bid}}{\text{Mid}}
  ```
  The same absolute spread is more expensive on a lower-priced contract, so cross-instrument and cross-strike comparisons need the relative measure.

### 03 / Order Types

#### A Market Order Buys Certainty, A Limit Order Buys Price

A market order prioritises execution over price: it fills as long as a counterparty exists, but a larger order can sweep several levels, so the average fill drifts away from the best quote. A limit order prioritises price over execution: it may not fill at all, or it may fill partially while price briefly touches the level.

Limit orders carry a hidden cost: they tend to fill precisely when the market is moving through them. A fast sweep through a resting order is often evidence that flow is going the other way, which is adverse selection. The expected cost of waiting is therefore not zero; it is the probability of a fill multiplied by how unfavourable that fill is.

| Dimension | Market order | Limit order |
| --- | --- | --- |
| Role | Aggressive; consumes liquidity. | Passive; supplies liquidity. |
| Primary risk | Slippage and impact rise with size. | No-fill risk and adverse selection. |
| Information content | Immediately visible in prints and volume. | Becomes evidence only when it is hit. |

### 04 / Market Impact

#### Execution Quality Decides Whether An Observed Price Is Real

A single print can simultaneously contain real repricing, temporary impact from a large order, and compensation demanded by liquidity providers. Treating those as one thing turns an execution cost into a false market opinion.

- Check the spread and depth before treating a large print as a view.
- Compare relative spread rather than absolute spread across instruments and price levels.
- Read resting orders as intent, not commitment; cancellation can change the book instantly.
- Execution cost is probability-weighted; one print cannot establish direction.

## Related Concepts

- [[order-book-depth-and-resting-liquidity|Order Book Depth And Resting Liquidity]] — Order type decides how you trade; book depth decides what it costs.
- [[liquidity-slippage-execution|Liquidity, Slippage, And Option Execution]] — The choice between aggressive and passive shows up as spread and slippage.
- [[price-discovery-market-clearing|Price Discovery And Market Clearing]] — The interaction of limit and market orders is the price-discovery process itself.
- [[order-flow-footprint-delta-cvd|Order Flow, Footprint, Delta, And Cumulative Delta]] — Order-type classification is the precondition for reading aggressive volume and delta.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

