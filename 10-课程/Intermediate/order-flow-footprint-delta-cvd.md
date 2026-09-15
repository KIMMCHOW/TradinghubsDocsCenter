---
title: "订单流、Footprint、Delta 与累计 Delta"
title_en: "Order Flow, Footprint, Delta, And Cumulative Delta"
slug: "order-flow-footprint-delta-cvd"
type: lesson
level: Intermediate
order: 26
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "19 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "订单流、Footprint、Delta 与累计 Delta"
  - "Order Flow, Footprint, Delta, And Cumulative Delta"
  - "order-flow-footprint-delta-cvd"
source_url: "https://tradinghubs.org/docs/trading-knowledge/order-flow-footprint-delta-cvd"
source_file: "Tradinghub-Web/components/site/options-knowledge/orderflow-data.ts"
generated: 2026-09-15
---

# 订单流、Footprint、Delta 与累计 Delta

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[auction-market-theory-value-and-imbalance|拍卖市场理论：价值、平衡与失衡]] ｜ 下一课：[[volume-profile-value-area-hvn-lvn|成交量分布：价值区、HVN 与 LVN]]

**中级 · 订单流与市场微观结构 · 19 分钟**

> Delta 类指标不是方向概率，而是对已发生交易的分类汇总。本课重点讲清口径、计算与失效条件，避免把分类结果当作事实。

理解 Footprint 如何在价位上拆分买卖成交、Delta 如何定义、累计 Delta 如何累积，以及为什么这些指标高度依赖主动方分类这一推断过程。

### 01 / Footprint 结构

#### Footprint 把一根 K 线拆成价位上的成交

普通图表只显示一根 K 线的时间与价格范围，Footprint 进一步在同一价位上显示成交量，并按主动买卖分类：成交在 Ask 一侧通常记为买方主动，成交在 Bid 一侧通常记为卖方主动。由此可以看见一根 K 线内部的分布，而不是只看它的开高低收。

典型形状具有可读含义：某一价位的双边成交都很大（成交墙）表示分歧；价位之间成交断层（成交量空档）表示价格快速通过，缺少业务发生；同一方向在连续价位上远超另一方向（不平衡）表示该段由单侧主导。

### 02 / Delta 的口径

#### Delta 是分类后的净成交，不是资金流向

Bar Delta 通常定义为买方主动成交量减卖方主动成交量；Session Delta 是同一天内所有 Bar Delta 的合计；累计 Delta（CVD）把 Session Delta 跨日或跨区间连续累加。三者都建立在同一件事上：每笔成交被归到哪一侧。

分类本身是推断。交易所公开数据通常只给出成交价与数量，必须用成交价位于 Bid 还是 Ask、或用报价变动规则推断主动方；价差内成交、组合与多腿订单、场外转仓、隐藏订单都会使分类出现误差。因此在跨平台比较前，必须确认口径一致：是否包含组合交易、如何处理价差内成交、如何重置累计值。

- **Bar Delta**

  ```latex
  \Delta_{\text{bar}}=V_{\text{buy}}-V_{\text{sell}}
  ```

- **Session Delta**

  ```latex
  \Delta_{\text{session}}=\sum_{i=1}^{n}\Delta_{\text{bar},i}
  ```

- **累计 Delta**

  ```latex
  \text{CVD}_t=\text{CVD}_{t-1}+\Delta_{\text{session},t}
  ```

### 03 / 背离与吸收

#### 价格与 Delta 不一致时，先问谁在承接

价格新高而 Delta 不再新高，或价格新低而 Delta 收敛，称为背离。它至少有两种截然不同的解释：一是主动买盘减少、推动力衰减；二是主动买盘仍然存在，但被足够的被动卖盘吸收，因此价格无法推进。分辨两者需要看该价位的成交是否持续放大以及价格是否真正停滞。

吸收（absorption）描述的是被动方持续承接主动成交，使价格无法继续推进的状态。吸收本身只说明当时存在足够的对手意愿，不说明结果一定是反转：吸收可以在趋势中反复出现并最终被突破，也可能只是把行程拖长。

- 先把口径核对清楚：主动方分类方式、是否含组合交易、累计值如何重置。
- 把 Delta 背离记录为待解释现象，再去找吸收或流动性撤走的证据。
- 同向 Delta 配合价格停滞时，优先考虑吸收而不是继续加仓。
- 任何单一 Bar 的 Delta 都不足以支撑结论，需要连续性与上下文。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Delta-family metrics are classified summaries of trades that already happened, not directional probabilities. This lesson focuses on definitions, calculation, and failure conditions so the output is never mistaken for fact.

Understand how a footprint splits execution by price and side, how delta is defined, how cumulative delta accumulates, and why all of them depend on an inferred aggressor classification.

### 01 / Footprint Structure

#### A Footprint Splits One Bar Into Execution By Price

A standard chart shows only the time and price range of a bar. A footprint adds volume at each price inside that bar and separates it by side: prints at the ask are usually labelled buyer-initiated and prints at the bid seller-initiated. That exposes the internal distribution of the bar instead of only its open, high, low, and close.

Typical shapes carry readable meaning: heavy two-sided volume at one price indicates disagreement; a gap in traded volume between prices shows price travelled without doing business; and one side dominating several consecutive price levels indicates that segment was driven by a single side.

### 02 / Delta And Its Conventions

#### Delta Is Classified Net Volume, Not A Money Flow Reading

Bar delta is commonly defined as buyer-initiated volume minus seller-initiated volume. Session delta is the sum of bar deltas across a session, and cumulative volume delta chains session delta across days or across a selected range. All three rest on one operation: assigning each print to a side.

The classification is an inference. Public data generally provides only price and size, so the aggressive side must be inferred from whether the print occurred at the bid or the ask, or from a quote-rule convention. Inside-spread prints, spread and multi-leg orders, off-exchange transfers, and hidden orders all introduce error. Before comparing two platforms, confirm the conventions match: whether spread trades are included, how inside-spread prints are handled, and how cumulative values reset.

- **Bar delta**

  ```latex
  \Delta_{\text{bar}}=V_{\text{buy}}-V_{\text{sell}}
  ```

- **Session delta**

  ```latex
  \Delta_{\text{session}}=\sum_{i=1}^{n}\Delta_{\text{bar},i}
  ```

- **Cumulative delta**

  ```latex
  \text{CVD}_t=\text{CVD}_{t-1}+\Delta_{\text{session},t}
  ```

### 03 / Divergence And Absorption

#### When Price And Delta Disagree, Ask Who Is Absorbing

A new price high with a delta high that fails to confirm, or a new low with delta converging, is a divergence. It has at least two very different explanations: aggressive buying is fading, or aggressive buying is still present but met by enough passive selling to stop progress. Separating them requires checking whether volume at that level keeps expanding and whether price actually stalls.

Absorption describes a passive side that keeps taking the aggressive flow and prevents price from progressing. It proves that sufficient opposing interest existed at that moment, and nothing more: absorption can occur repeatedly inside a trend and still be overcome, or it can merely slow the travel down.

- Verify conventions first: aggressor classification, spread-trade inclusion, and cumulative reset behaviour.
- Record delta divergence as an unexplained observation, then look for absorption or withdrawn liquidity.
- When delta and a stalled price coexist, consider absorption before adding risk.
- Delta from a single bar cannot support a conclusion; continuity and context are required.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

