---
title: "成交量分布：价值区、HVN 与 LVN"
title_en: "Volume Profile: Value Area, HVN, And LVN"
slug: "volume-profile-value-area-hvn-lvn"
type: lesson
level: Intermediate
order: 29
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "成交量分布：价值区、HVN 与 LVN"
  - "Volume Profile: Value Area, HVN, And LVN"
  - "volume-profile-value-area-hvn-lvn"
source_url: "https://tradinghubs.org/docs/trading-knowledge/volume-profile-value-area-hvn-lvn"
source_file: "Tradinghub-Web/components/site/options-knowledge/orderflow-data.ts"
generated: 2026-09-15
---

# 成交量分布：价值区、HVN 与 LVN

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[order-flow-footprint-delta-cvd|订单流、Footprint、Delta 与累计 Delta]] ｜ 下一课：[[option-spread-structures|价差与组合结构]]

**中级 · 订单流与市场微观结构 · 18 分钟**

> 成交量分布回答的是“成交发生在哪里”，不回答“谁还持有”。把这两类信息混用，是读分布图时最典型的错误。

按价格而不是按时间统计成交量：POC、价值区上下沿、高成交量节点与低成交量空档如何形成，以及它们与持仓分布类工具的差别。

### 01 / 构造方式

#### 把时间轴折叠掉，只保留价格与数量

成交量分布把每笔成交分配到其成交价所属的价格区间，累加后得到按价格排列的直方图。时间被折叠，因此它描述的是“哪些价格被交易过”，而不是“什么时候被交易”。选择的时间范围（当日、数日、可见区间、合约全周期）会显著改变形状，比较不同分布前必须确认区间一致。

同一区间内还可以区分总成交量与分侧成交量：相对成交价与买卖报价的关系可以把成交拆成主动买与主动卖。这样拆分的分布与只看总量的分布含义不同，前者包含方向分类误差，后者不包含。

### 02 / 节点与价值区

#### POC、价值区、HVN、LVN 描述形状而非承诺

成交最集中的价位称为控制点（POC）；包含选定比例（常见为约七成）成交量的价格带称为价值区，其上沿与下沿分别为 VAH 与 VAL。成交密集的价位区间称为高成交量节点，成交稀薄的区间称为低成交量空档。

形状给出的是相对信息：价格进入高成交量区间时通常需要更多成交才能离开，进入低成交量空档时位移可能更快。这些是参与度差异的结果，而不是价格必须遵守的边界；新的信息流可以让原本稀薄的价格区间迅速变成新的密集区。

| 概念 | 定义 | 常见误读 |
| --- | --- | --- |
| POC | 区间内成交量最高的价位。 | 把它当作必然的回归目标。 |
| 价值区 VAH / VAL | 包含选定比例成交量的上下沿。 | 忽略比例与区间口径，跨图直接比较。 |
| HVN | 成交密集的价格带。 | 把它等同于支撑或阻力位。 |
| LVN | 成交稀薄的价格空档。 | 认为价格必然快速穿越。 |

### 03 / 活动与持仓

#### 成交量分布是活动记录，期权与持仓分布是存量记录

成交量分布在时间上是历史记录：它说明过去谁在这里成交。期权或持仓分布类工具描述的是尚未平仓的存量仓位，其口径通常从零开始、按日累加，或按当前未平仓合约构造。两者都可能呈钟形，但一个问“发生过什么”，另一个问“还留着什么”。

实务上最有价值的做法是把两类信息并列而不是混用：活动分布给出价格经过的成本，持仓分布给出尚未释放的意愿。任何一类的形状变化都需要另一类来确认，否则很容易把一次历史成交堆积解释成当前仓位。

- 记录分布的时间区间与价值区比例，再做任何跨图比较。
- 把节点与空档作为相对参与度信息，而不是既定支撑阻力。
- 区分活动型分布与存量型分布，避免把过去成交当当前仓位。
- 在低成交量空档中仍要求成交确认，因为稀薄不等于无阻力。

## 相关概念

- [[auction-market-theory-value-and-imbalance|拍卖市场理论：价值、平衡与失衡]] — 价值区与 HVN／LVN 是拍卖结果在成交量分布上的投影。
- [[order-flow-footprint-delta-cvd|订单流、Footprint、Delta 与累计 Delta]] — 成交量分布给出位置，Delta 给出该位置的多空主动性。
- [[order-book-depth-and-resting-liquidity|订单簿、深度与挂单流动性]] — LVN 区域通常对应较薄的历史成交与较弱的价格接受度。
- [[absorption-exhaustion-and-iceberg-orders|吸收、衰竭与冰山单]] — 节点处的吸收与分布在同一张图上互相验证。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> A volume profile answers where business happened, not who still holds it. Blending those two questions is the most common mistake when reading a distribution chart.

Aggregate volume by price instead of by time: how the point of control, value-area edges, high-volume nodes, and low-volume gaps form, and how they differ from position-based distribution tools.

### 01 / Construction

#### Collapse The Time Axis And Keep Price With Quantity

A volume profile assigns every trade to the price bucket it executed at and accumulates the result into a histogram ordered by price. Time is collapsed, so the profile describes which prices traded rather than when. The chosen range — one session, several sessions, the visible window, or the contract's life — changes the shape materially, so ranges must match before profiles are compared.

Within one range, total volume can also be split by side: comparing the print price with the prevailing quotes separates buyer-initiated from seller-initiated volume. A split profile means something different from a total-volume profile, because the split version carries the classification error and the total version does not.

### 02 / Nodes And Value Area

#### POC, Value Area, HVN, And LVN Describe Shape, Not Promises

The price with the most traded volume is the point of control. The price band containing a chosen share of volume — commonly around seventy percent — is the value area, bounded by the value-area high and low. Dense price bands are high-volume nodes and sparse bands are low-volume nodes.

The shape provides relative information: more business is typically required to leave a high-volume band, while travel through a low-volume band can be faster. Those are consequences of participation differences, not boundaries price must obey; new information can turn a previously thin band into a new concentration.

| Concept | Definition | Common misread |
| --- | --- | --- |
| POC | Highest-volume price in the range. | Treating it as a guaranteed reversion target. |
| Value area high and low | Edges of the chosen volume share. | Comparing across charts without matching band and range. |
| High-volume node | A dense price band. | Equating it with support or resistance. |
| Low-volume node | A sparse price gap. | Assuming price must cross it quickly. |

### 03 / Activity Versus Positioning

#### A Volume Profile Records Activity; Position Distributions Record Stock

A volume profile is a historical record: it shows where business happened in the past. Option or positioning distributions describe standing exposure that has not been closed, usually accumulated from zero each day or built from current open contracts. Both can look bell-shaped, yet one asks what already happened and the other asks what is still held.

The most useful practice is to place the two side by side instead of blending them: the activity distribution shows where trade occurred and the positioning distribution shows unexercised intent. A change in one needs confirmation from the other, otherwise historical concentration is easily mistaken for current positioning.

- Record the range and value-area share before comparing profiles.
- Treat nodes and gaps as relative participation, not fixed support or resistance.
- Separate activity profiles from position profiles so past trade is not read as current exposure.
- Require trade confirmation inside low-volume gaps; thin does not mean unrestricted.

## Related Concepts

- [[auction-market-theory-value-and-imbalance|Auction Market Theory: Value, Balance, And Imbalance]] — Value area and HVN/LVN are the projection of an auction result onto the volume distribution.
- [[order-flow-footprint-delta-cvd|Order Flow, Footprint, Delta, And Cumulative Delta]] — The volume distribution gives the location, and delta gives the aggressiveness at that location.
- [[order-book-depth-and-resting-liquidity|Order Book Depth And Resting Liquidity]] — An LVN area usually maps to thin historical trade and weak price acceptance.
- [[absorption-exhaustion-and-iceberg-orders|Absorption, Exhaustion, And Iceberg Orders]] — Absorption at a node and the distribution validate each other on the same chart.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

