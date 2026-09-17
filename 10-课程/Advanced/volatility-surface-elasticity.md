---
title: "波动率曲面弹性：成交如何变成波动率供给"
title_en: "Volatility Surface Elasticity: How Trading Becomes Volatility Supply"
slug: "volatility-surface-elasticity"
type: lesson
level: Advanced
order: 92
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "22 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "波动率曲面弹性：成交如何变成波动率供给"
  - "Volatility Surface Elasticity: How Trading Becomes Volatility Supply"
  - "volatility-surface-elasticity"
source_url: "https://tradinghubs.org/docs/trading-knowledge/volatility-surface-elasticity"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 波动率曲面弹性：成交如何变成波动率供给

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[futures-flow-from-options-positioning|期权定位如何传导到期货价格]] ｜ 下一课：[[zero-gamma-flip-boundary|零 Gamma / Gamma Flip 边界]]

**高级 · 订单流与市场微观结构 · 22 分钟**

> 本课讨论一个方法论问题：期权市场活动的可观测口径并不只有持仓量。先比较持仓量、成交量与主动方分类三种口径各自回答什么，再说明为什么「谁在承担波动率」比「合约有多少张」更接近可用信息，最后给出这套口径的边界。

从「有多少持仓」转向「哪里风险不足」：把每笔期权成交按主动方分类，理解主动买入对应承接方短波动率库存、主动卖出对应长波动率库存，并用曲面弹性与失效条件区分吸收与重定价。

### 01 / 供给度量

#### 先问「哪里风险不足」，而不是「有多少张合约」

最可靠的「有多少」是未平仓量：清算机构在每个交易日结束后汇总开仓与平仓指令，并在下一个交易日开盘前公布，所以它是隔夜确认过的存量数字。它的优点是权威，缺点是只有日频节奏，且不说明谁持有这些合约。由于期权买卖价差较宽、成交多发生在中间价附近，单看逐笔成交也常常难以判断这一笔究竟是被买入还是被卖出。

成交量可以把画面变细：当某个执行价的成交量明显超过该处未平仓量时，至少说明当天有大量新成交活动，而不只是旧仓位换手。但成交量本身没有方向，它衡量的是参与强度，而不是谁在承担风险。把成交量与未平仓量放在一起，得到的是「今天哪里活跃」，仍然不是「今天谁承担了波动率」。

第三种口径换了一个提问方式。流动性提供方并不关心一笔成交是开仓还是平仓，只关心它如何改变自己的敞口：如果能找到对手方，它赚取价差并把库存配平；找不到对手方时，它必须调整报价来补偿自己承接的风险。按这个逻辑，把每一笔成交相对一个理论估值基准分类为主动买入或主动卖出：主动方愿意多付一点立刻成交，说明该执行价的波动率供给不足，承接方因此在该处持有短波动率库存；主动方愿意让出一点立刻离场，说明波动率供给充足，承接方在该处持有长波动率库存。

这样得到的不是一张持仓归属表，而是一张「风险集中在哪里、并且还在变化中」的地图。它把注意力从静态库存转移到价格与报价如何变化，这也是本课与未平仓量课程的分工：未平仓量回答存量，本课的分类口径回答当天的供给状态。

- 未平仓量是隔夜确认的存量，适合定位结构，不适合描述当天变化。
- 成交量衡量参与强度，没有方向；用它推断买卖方向是常见误用。
- 分类口径给出方向与供给状态，但它的正确性依赖分类规则本身。

- **按执行价累计的分类库存（概念式）**

  ```latex
  I_{k}=\sum_{t}\left(q^{+}_{k,t}-q^{-}_{k,t}\right)
  ```
  I_k 是执行价 k 上的分类净库存，q⁺ 与 q⁻ 分别代表主动买入与主动卖出的成交数量，符号约定代表承接方库存方向，不代表任何账户的持仓归属。

- **三种口径回答不同问题**

  ```latex
  \text{OI}\Rightarrow\text{stock},\quad\text{Volume}\Rightarrow\text{activity},\quad\text{Classified}\Rightarrow\text{supply}
  ```
  三者不可互相替代：它们的时间频率、方向含义与失效原因都不同。

### 02 / 存量质疑

#### 累计库存为什么不能直接当作当前对冲行为

另一种常见做法是按参与者类型与开平方向打标签，把同一合约生命周期内的库存累加起来。它的吸引力在于看起来像一张完整的账面，但累计库存并不等于当前的对冲行为：交易台会吸收、再对冲，或与其他账簿净额抵消旧仓位，于是很久以前建立的持仓仍然被当作活跃风险计入，而它实际上可能早已被覆盖。

这套方法还有若干结构性限制。完整的参与者标签只在单一交易所的品种上成立，而在多个交易场所挂牌的股票与 ETF 没有统一的标签口径；做市方同时在指数期权、ETF 与期货等相关品种上运行多个交易台，中央风险台会在内部互相净额，孤立看待单一品种会漏掉共享的风险预算；参与者也不会按理论希腊字母连续对冲，他们在离散区间里调整、在成交密集时段再平衡，还会依据自身风险敏感度改变行为。

更根本的问题是框架假设：传统模型假定只有做市方对冲，其他参与者保持不变。现实中许多参与者会根据自身激励主动调整仓位，其中一部分还是对价格高度敏感的资金。所以在使用任何库存类指标之前，先问清楚它衡量的是「谁持有」，还是「谁在动」。

| 口径 | 能回答 | 不能回答 |
| --- | --- | --- |
| 未平仓量 | 隔夜确认的存量规模与位置。 | 当天谁在承接、库存是否已经改变。 |
| 成交量 | 参与强度与新旧仓混合程度。 | 方向、库存归属与对冲行为。 |
| 参与者标签累计库存 | 合约生命周期内的累计分类流向。 | 当前仍具约束力的对冲压力。 |
| 主动方分类供给状态 | 当天各执行价的波动率供给与需求失衡。 | 任何账户的身份、意图或最终对冲动作。 |

### 03 / 弹性读法

#### 吸收与重定价，是同一口径下的两种结果

把曲面看成供给曲线，就能区分两种状态。当曲面在不扭曲价格的情况下吸收了成交量，交易是弹性的：有人愿意在那个位置提供风险。当单边成交迫使报价必须调整才能成交，曲面是非弹性的，这种状态本身就是供给与需求已经扭曲了波动率曲面的表现。把它类比为记牌而不是猜牌：关注的不是某一手牌，而是整副牌里各类牌的消耗情况。

实务读法分三步。第一步，确认执行价附近的分类库存是净偏一侧还是两侧接近抵消；两侧接近抵消时，该处不构成集中的调整点。第二步，观察价格进入该区域后的表现：如果成交量放大而报价没有被连续推动，属于吸收；如果价格被持续推向同一侧并且回踩无法收回，属于重定价。第三步，把该区域与邻近执行价一起看：孤立的一个执行价与一片连在一起的区域，含义并不相同。

这套读法的边界必须写清：它描述的是相对强度与关系变化，而不是精确持仓数字。价差与多腿组合会被拆分记账，场外或协商成交可能不进入公开数据，隐藏流动性也会改变主动方的归属。因此最相关的永远是最近被分类、尚未被充分消化的流量，而不是整日累计的总量。

> [!question] 分类不等于持仓归属
> 供给状态描述的是当时承接风险的一侧偏向，不是任何账户的仓位、意图或后续动作。把分类结果直接翻译成「某某在做多或做空」超出了这套口径能支持的范围。

> [!warning] 过期流量会稀释判断
> 把整个交易日的分类流量与最近几分钟的流量同等看待，会让久已消化的成交继续主导结论。记录时必须写明时间窗口。

- 第一步：写下当前观察的是存量、活动量还是供给状态，三者不混用。
- 第二步：对目标执行价记录分类库存的偏向，并检查邻近执行价是否连成一片。
- 第三步：用价格与成交区分吸收和重定价，再写下哪一种结果会推翻当前判断。
- 风险边界：分类流量是相对强度证据，不是持仓数字，也不能单独作为方向依据。

## 相关概念

- [[open-interest-oi|OI 未平仓量：期权仓位账本]] — 未平仓量是本课要区分的那个「有多少」口径，两课必须对照阅读。
- [[options-volume-participation|Volume：期权参与强度怎么读]] — 成交量解释参与强度，是分类口径的对照面。
- [[options-flow-direction|Flow：期权成交分类怎么读]] — 成交分类的读法与边界在本课被进一步扩展到波动率供给。
- [[market-making-inventory-adverse-selection|做市库存与逆向选择：价差收入不是免费收益]] — 承接风险的动机来自库存与逆向选择成本，这是供给侧行为的微观基础。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> This lesson is about one methodological question: standing contracts are not the only observable measure of options activity. It compares what open interest, volume, and aggressor classification each answer, explains why 'who is carrying the volatility' is closer to usable information than 'how many contracts exist', and then marks where that claim stops.

Move from 'how many contracts exist' to 'where is risk under-supplied': classify each option trade by its aggressor, read aggressor buying as short-volatility inventory on the absorbing side and aggressor selling as long-volatility inventory, and separate absorption from repricing with a surface-elasticity reading and its failure conditions.

### 01 / Measuring Supply

#### Ask Where Risk Is Under-Supplied, Not How Many Contracts Exist

The most reliable 'how many' is open interest: a clearing house tallies opening and closing instructions after each session and publishes the result before the next session, so it is a confirmed standing figure at daily frequency. Its strength is authority; its limits are the overnight rhythm and the absence of any statement about who holds those contracts. Because option spreads are wide and most trades print near the midpoint, a raw time-and-sales tape can also be ambiguous about whether a contract was bought or sold.

Volume sharpens the picture: where session volume at a strike clearly exceeds the contracts standing there, the day at least carried substantial new trading rather than only turnover of old positions. Volume itself has no direction; it measures participation, not who ended up carrying risk. Combining volume with open interest therefore answers 'where was today active', still not 'who took on volatility today'.

A third measure changes the question. A liquidity provider does not care whether a trade opens or closes a position; it cares how the trade changes its own exposure. When it can find the other side it captures the spread and stays balanced; when it cannot, it must move its quotes to be paid for the risk it is warehousing. Following that logic, each trade is classified against a theoretical valuation benchmark as aggressor-bought or aggressor-sold: an aggressor willing to concede edge to trade immediately shows that volatility is under-supplied at that strike, leaving the absorbing side short-volatility inventory there, while an aggressor willing to concede edge to leave immediately shows volatility is well supplied, leaving the absorbing side long-volatility inventory.

What comes out is not an ownership register but a map of where risk is concentrated and still changing. It shifts attention from static inventory to how prices and quotes move, which is the division of labour between this lesson and the open-interest lesson: standing contracts describe the stock, classified aggressor flow describes the current state of supply.

- Open interest is a confirmed overnight stock: good for structure, poor for describing today's change.
- Volume measures participation with no direction; reading buying or selling from it is a common misuse.
- Classification supplies direction and a supply state, but its correctness depends on the classification rule itself.

- **Classified inventory accumulated by strike (conceptual)**

  ```latex
  I_{k}=\sum_{t}\left(q^{+}_{k,t}-q^{-}_{k,t}\right)
  ```
  I_k is the classified net inventory at strike k, q+ and q- are the aggressor-bought and aggressor-sold quantities, and the sign convention describes the absorbing side's inventory direction rather than any account's ownership.

- **Three measures answer different questions**

  ```latex
  \text{OI}\Rightarrow\text{stock},\quad\text{Volume}\Rightarrow\text{activity},\quad\text{Classified}\Rightarrow\text{supply}
  ```
  They are not substitutes: their frequency, directional meaning, and failure modes all differ.

### 02 / Why Static Inventory Misleads

#### Why Cumulative Inventory Is Not Current Hedging Behaviour

Another common approach tags volume by participant type and open-versus-close origin, then accumulates inventory across the life of a contract. Its appeal is that it looks like a complete ledger, but cumulative inventory is not current hedging behaviour: desks absorb, re-hedge, or net older positions against other books, so positions built long ago are still counted as active risk that may already be covered.

The approach also carries structural limits. Complete participant tagging is only available for single-venue instruments, while multiply-listed equities and ETFs trade across venues without a unified tag; the dealing side runs several desks across correlated products such as index options, ETFs, and futures, and a central risk desk nets those exposures internally, so reading one product in isolation misses a shared risk budget; and participants do not hedge continuously according to theoretical Greeks - they adjust at discrete intervals, rebalance when volume is high, and change behaviour with their own risk sensitivity.

The deeper problem is the framing assumption: the traditional model assumes only the dealing side hedges while everyone else stays put. In practice many participants reposition in response to their own incentives, and some of that capital is highly price sensitive. Before using any inventory-style metric, establish whether it measures who holds risk or who is moving it.

| Measure | Can Answer | Cannot Answer |
| --- | --- | --- |
| Open interest | Confirmed overnight stock and where it sits. | Who is absorbing today or whether the inventory already changed. |
| Volume | Participation intensity and how much activity is new. | Direction, ownership, or hedging behaviour. |
| Tagged cumulative inventory | Cumulative tagged flow over a contract's life. | The hedging pressure that still binds today. |
| Classified aggressor supply | Same-day imbalance between volatility supply and demand by strike. | Any account's identity, intent, or eventual hedge action. |

### 03 / Reading Elasticity

#### Absorption And Repricing Are The Two Outcomes Of One Reading

Treating the surface as a supply curve separates two states. When the surface absorbs volume without distorting price, trading is elastic: someone was willing to supply risk there. When one-sided flow forces quotes to move before it can be filled, the surface is inelastic, and that state is itself the expression of supply and demand having distorted the volatility surface. The useful analogy is counting cards rather than guessing a hand: the subject is how the deck is being consumed, not what one player holds.

The practical reading has three steps. First, check whether the classified inventory near a strike leans to one side or roughly cancels; a near-cancelling strike is not a concentrated adjustment point. Second, watch what price does on entering the area: expanding volume without quotes being pushed repeatedly is absorption, while price being driven persistently to one side with a failed retest is repricing. Third, read the strike together with its neighbours, because an isolated strike and a connected band do not mean the same thing.

The boundary must be explicit: this reading describes relative intensity and changing relationships, not exact position counts. Spread and multi-leg packages get booked leg by leg, negotiated or off-venue trades may never appear in public data, and hidden liquidity changes who appears to be the aggressor. What matters most is therefore the most recently classified flow that has not yet been digested, not a whole-day total.

> [!question] Classification Is Not Ownership
> A supply state describes which side leaned into the risk at that moment, not any account's position, intent, or later action. Translating classification straight into 'someone is long or short' claims more than the measure supports.

> [!warning] Stale Flow Dilutes The Read
> Treating a whole session of classified flow as equal to the last few minutes lets long-digested trades keep dominating the conclusion. Any record must state its time window.

- Step one: state whether you are reading stock, activity, or supply state, and never mix them.
- Step two: record the classified bias at the target strike and check whether neighbouring strikes form a connected band.
- Step three: use traded price and volume to separate absorption from repricing, then write down which outcome would invalidate the read.
- Risk boundary: classified flow is relative-intensity evidence, not a position count, and cannot stand alone as a directional basis.

## Related Concepts

- [[open-interest-oi|OI Open Interest: The Options Position Ledger]] — Open interest is the 'how many' measure this lesson distinguishes itself from; the two must be read against each other.
- [[options-volume-participation|Volume: How To Read Options Participation Strength]] — Volume explains participation intensity and is the natural contrast to classification.
- [[options-flow-direction|Flow: How To Read Classified Options Trading]] — The reading rules and boundaries of trade classification are extended here into volatility supply.
- [[market-making-inventory-adverse-selection|Market-Making Inventory And Adverse Selection: Spread Capture Is Not Free Return]] — The incentive to absorb risk comes from inventory and adverse-selection cost, the microfoundation of the supplying side.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- glosten-milgrom-original
- nyfed-market-liquidity
- nyu-avellaneda-stoikov
