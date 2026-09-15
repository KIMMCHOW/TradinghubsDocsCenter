---
title: "OI 未平仓量：期权仓位账本"
title_en: "OI Open Interest: The Options Position Ledger"
slug: "open-interest-oi"
type: lesson
level: Beginner
order: 13
track: options-foundations
track_label: "期权基础与合约"
reading_time: "13 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/期权基础与合约"
  - "权限/需登录"
aliases:
  - "OI 未平仓量：期权仓位账本"
  - "OI Open Interest: The Options Position Ledger"
  - "open-interest-oi"
source_url: "https://tradinghubs.org/docs/trading-knowledge/open-interest-oi"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# OI 未平仓量：期权仓位账本

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[options-foundations|期权基础与合约]]
> 上一课：[[liquidity-slippage-execution|流动性、滑点与期权执行]] ｜ 下一课：[[options-volume-participation|Volume：期权参与强度怎么读]]

**初级 · 期权基础与合约 · 13 分钟**

> OI 不告诉你今天谁在主动买卖，也不直接给方向。它回答的是：市场上还有多少合约没有平掉，以及这些合约集中在哪些行权价。

把 OI 读成未平仓合约的存量账本，区分它和 Volume，并理解为什么大 OI 行权价会成为期货观察区。

### 01 / OI 是什么

#### OI 是未平仓合约数量，不是当天成交量

Open Interest 统计的是还没有被平仓、行权或到期消失的合约数量。它是存量，不是流量；Volume 是当天成交了多少，OI 则按交易场所或清算发布节奏更新，许多期权链在盘中显示的是上一结算周期快照。

如果一笔新买方和新卖方成交，OI 可能增加；如果双方都在平旧仓，OI 可能减少；如果一方开仓、一方平仓，OI 可能基本不变。

- **分行权价 OI**

  ```latex
  \text{Per-Strike OI}=\text{Call OI}+\text{Put OI}
  ```

- **OI 比例**

  ```latex
  \text{OI Ratio}=\frac{\text{Total Call OI}}{\text{Total Call OI}+\text{Total Put OI}}
  ```

### 02 / OI 与 Volume

#### OI 看仓位留存，Volume 看当日参与强度

大 OI 说明某个 Strike 在最近已发布快照中有大量合约仍在场内，但不说明今天有没有人正在推动它。Volume 放大只说明当天参与增加；在下一次 OI 更新前，不能据此区分新开仓、平仓、换手或多腿交易。

Options Data Viewer 中应先把最近发布的 OI 当作结构底图，再用成交分类、Volume、绝对 GEX / DEX 与期货价格观察当天活动是否集中在相同区域。只有下一次 OI 更新后，才能判断底图是否真的迁移。

| 观察 | 更像什么 | 下一步 |
| --- | --- | --- |
| OI 高，Volume 低 | 历史仓位集中，但当天不一定活跃。 | 等待价格接近或 Flow 放大再确认。 |
| OI 高，Volume 高 | 结构位置正在被交易。 | 去 Greeks Profile 看 GEX / DEX 是否同区集中。 |
| Volume 高，OI 低 | 当天活动高于最近 OI 快照，但开平仓尚未知。 | 等待下一次 OI 更新；不要直接当成稳定墙位。 |

### 03 / 为什么重要

#### 大 OI 行权价可能成为期货盘面的观察区

当大量合约集中在一个行权价附近，价格接近该区域时，做市商对冲、客户止盈止损、换仓和到期处理都可能更密集。OI 本身不是支撑阻力，但它能告诉你哪里值得额外观察。

- OI 是 ODV 读图的底层账本。
- 大 OI 与 GEX 峰值重合时，结构意义通常更强。
- OI 不说明方向，必须结合 Flow、GEX、DEX、IV 和价格行为。

## 相关概念

- [[options-volume-participation|Volume：期权参与强度怎么读]] — OI 是存量，Volume 是当日活动，两者必须联合解读。
- [[gamma-exposure-gex|GEX / vGEX：Gamma Exposure 怎么看]] — 敞口指标以 OI 为权重基础，理解存量才能理解敞口。
- [[delta-exposure-dex|DEX：Delta Exposure 怎么看]] — DEX 把 OI 与 Delta 结合，形成方向性存量敞口。
- [[options-flow-direction|Flow：期权成交分类怎么读]] — OI 变化是判断成交属于开仓还是平仓的关键证据。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> OI does not tell you who is aggressively trading today and it does not directly give direction. It answers how many contracts remain open and where they are concentrated by strike.

Read OI as the standing contract ledger, separate it from volume, and understand why high-OI strikes can become futures observation zones.

### 01 / What OI Is

#### OI Is Open Contracts, Not Today's Volume

Open interest counts contracts that have not been closed, exercised, or expired. It is stock, not flow; volume is what traded today, while OI updates on the venue or clearing publication schedule, and many option chains show the prior clearing snapshot intraday.

If a new buyer trades with a new seller, OI can rise. If both sides close existing positions, OI can fall. If one side opens and the other closes, OI may stay roughly unchanged.

- **Per-strike OI**

  ```latex
  \text{Per-Strike OI}=\text{Call OI}+\text{Put OI}
  ```

- **OI ratio**

  ```latex
  \text{OI Ratio}=\frac{\text{Total Call OI}}{\text{Total Call OI}+\text{Total Put OI}}
  ```

### 02 / OI Versus Volume

#### OI Reads Standing Positioning; Volume Reads Participation

Large OI means many contracts remained at a strike in the latest published snapshot, but it does not prove someone is pushing it today. Rising volume only shows more same-session participation; until the next OI update, it cannot distinguish new opening, closing, turnover, or multi-leg activity.

In Options Data Viewer, use the latest published OI as the structural base map, then compare classified trades, volume, magnitude GEX and DEX, and futures price to see whether same-session activity clusters in the same areas. Structural migration can be assessed only after the next OI update.

| Observation | Likely Meaning | Next Step |
| --- | --- | --- |
| High OI, low volume | Standing positioning is concentrated, but today may be quiet. | Wait for price proximity or stronger flow confirmation. |
| High OI, high volume | A structural area is actively trading. | Check Greeks Profile for nearby GEX / DEX concentration. |
| High volume, low OI | Same-session activity is high versus the latest OI snapshot, but opening versus closing is unknown. | Wait for the next OI update; do not read it as a durable wall by itself. |

### 03 / Why It Matters

#### High-OI Strikes Can Become Futures Observation Zones

When many contracts cluster around a strike, dealer hedging, customer exits, rolls, and expiry handling can become denser as price approaches. OI is not support or resistance by itself, but it shows where extra attention is warranted.

- OI is the base ledger for ODV reading.
- High OI overlapping with a GEX peak usually carries stronger structural relevance.
- OI does not define direction; combine it with flow, GEX, DEX, IV, and price behavior.

## Related Concepts

- [[options-volume-participation|Volume: How To Read Options Participation Strength]] — OI is a stock and volume is daily activity, so the two must be read together.
- [[gamma-exposure-gex|GEX / vGEX: How To Read Gamma Exposure]] — Exposure metrics are weighted by OI, so standing positioning must be understood first.
- [[delta-exposure-dex|DEX: How To Read Delta Exposure]] — DEX combines OI with delta into a directional standing exposure.
- [[options-flow-direction|Flow: How To Read Classified Options Trading]] — A change in OI is the key evidence for whether a trade opened or closed a position.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

