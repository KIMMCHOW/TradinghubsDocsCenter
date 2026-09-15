---
title: "DEX：Delta Exposure 怎么看"
title_en: "DEX: How To Read Delta Exposure"
slug: "delta-exposure-dex"
type: lesson
level: Intermediate
order: 45
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "14 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "DEX：Delta Exposure 怎么看"
  - "DEX: How To Read Delta Exposure"
  - "delta-exposure-dex"
source_url: "https://tradinghubs.org/docs/trading-knowledge/delta-exposure-dex"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# DEX：Delta Exposure 怎么看

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[gamma-exposure-gex|GEX / vGEX：Gamma Exposure 怎么看]] ｜ 下一课：[[aggregate-options-data|Aggregate Data：总量结构怎么读]]

**中级 · 做市商定位与期权敞口 · 14 分钟**

> DEX 描述当前模型的 Delta 加权分布，GEX 描述 Gamma 加权分布。两者可用来比较热点位置，但页面符号不揭示 dealer ownership，也不能把不同指标的原始绝对值直接相比。

理解 ODV 预计算 DEX 如何显示 Delta 加权分布，并学会在不反推 dealer 库存的前提下与 GEX 联读。

### 01 / 定义

#### 先分清 Delta 概念与页面预计算 DEX

Delta 衡量参考价格小幅变化时的期权价值敏感度。一般概念里，Delta 暴露与 Delta、某种仓位度量和合约乘数成比例；但 ODV 已把具体缩放、符号和聚合纳入预计算值，当前页面没有统一 multiplier 或逐 Strike Call / Put 分解，因此不能从 OI 复算 DEX。

在本课的产品读法里，正负号、OI 与 Volume 都不能单独证明做市商库存、持仓归属或对冲方向；K / M / B 仅为紧凑显示缩写，不是美元、股数、合约数或每点冲击的经济单位。只可在同一标的、同一指标、同一 DTE 窗口和同一数据快照内比较分布。0DTE、1DTE+ 与 90D Window 均为独立预计算值，90D Window 不等于前两者相加。

- C_n 只在同一标的、DEX、DTE 窗口和数据快照内按行权价顺序累加页面值，不是 Call − Put。
- 正负号沿用模型口径，不能单独证明 Long / Short dealer Delta 或未来期货对冲方向。

- **Delta 定义**

  ```latex
  \Delta=\frac{\partial V}{\partial S}
  ```

- **一般概念关系，不能复算页面**

  ```latex
  \text{Delta exposure}\;\propto\;\Delta\times\text{position measure}\times\text{contract multiplier}
  ```

- **同一视图的有符号累计**

  ```latex
  C_n=\sum_{i=1}^{n}x_i
  ```

### 02 / DEX 与 GEX

#### DEX 读方向暴露，GEX 读方向变化速度

先在 DEX 与 GEX 各自的同一标的、DTE 和数据快照视图内定位相对突出区，再比较这些区的行权价是否重合。这里比较的是空间位置，不是跨指标比较绝对数值，也不是判断做市商暴露偏向哪一边。

| 组合观察 | 常见含义 | 读法边界 |
| --- | --- | --- |
| DEX 与 GEX 热点同区 | 方向暴露和对冲敏感度在同一位置。 | 观察价格靠近后的成交吸收或加速。 |
| DEX 热点、GEX 不重合 | Delta 与 Gamma 加权分布的突出位置不同。 | 不要从跨指标数值差推断对冲强弱。 |
| GEX 热点、DEX 不重合 | Gamma 与 Delta 加权分布的突出位置不同。 | 记录位置差异，再用价格与成交验证。 |

### 03 / ODV 读法

#### 在 Greeks Profile 中用 DEX 确认方向暴露区域

先确认标的、DEX、DTE 窗口和更新时间，再进入 Greeks Profile 查看同一视图内的相对集中区。K / M / B 只是显示缩写；不要跨标的、指标、DTE 或数据快照比较绝对值，也不要把 DEX 正负号与 Flow 分类拼成做市商方向。

- DEX 不等于期货必然走向某边。
- DEX 更适合回答“同一视图里哪里更突出”，不是“现在能不能进场”。
- 和 GEX、OI、Flow、IV 一起看，才能判断暴露是否可能影响期货盘面。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> DEX describes the current model's delta-weighted distribution, while GEX describes a gamma-weighted distribution. Their hotspot locations can be compared, but displayed signs do not reveal dealer ownership and raw magnitudes cannot be compared directly across metrics.

Understand how ODV's precomputed DEX displays a delta-weighted distribution, then read it with GEX without inferring dealer inventory.

### 01 / Definition

#### Separate Delta Theory From Precomputed DEX

Delta measures option-value sensitivity to a small move in the reference instrument. Conceptually, delta exposure is proportional to delta, a position measure, and a contract multiplier. ODV already embeds its scaling, signs, and aggregation in precomputed values, and the current view has neither a universal multiplier nor per-strike call-put decomposition, so OI cannot be used to reproduce DEX.

In this product reading, signs, OI, and volume do not establish dealer inventory, ownership, or hedge direction. K / M / B are compact display suffixes, not economic units such as dollars, shares, contracts, or a per-point shock. Compare distributions only within the same symbol, metric, DTE window, and snapshot. 0DTE, 1DTE+, and 90D Window are independent precomputed values; 90D Window is not the sum of the first two.

- C_n accumulates displayed values by strike only within the same symbol, DEX view, DTE window, and snapshot; it is not call minus put.
- Signs follow the model convention and do not establish long or short dealer delta or future futures-hedge direction.

- **Delta definition**

  ```latex
  \Delta=\frac{\partial V}{\partial S}
  ```

- **General concept; not a page-reproduction formula**

  ```latex
  \text{Delta exposure}\;\propto\;\Delta\times\text{position measure}\times\text{contract multiplier}
  ```

- **Signed cumulative line within one view**

  ```latex
  C_n=\sum_{i=1}^{n}x_i
  ```

### 02 / DEX Versus GEX

#### DEX Reads Directional Exposure; GEX Reads How Fast Directional Exposure Changes

First locate relative hotspots within each DEX and GEX view for the same symbol, DTE, and snapshot, then compare whether their strike locations overlap. This compares spatial location, not raw magnitude across metrics, and it does not determine dealer exposure direction.

| Combined Observation | Common Meaning | Reading Boundary |
| --- | --- | --- |
| DEX and GEX hotspots overlap | Directional exposure and hedge sensitivity sit in the same area. | Watch absorption or acceleration as price approaches. |
| DEX hotspot without GEX overlap | The prominent locations of delta- and gamma-weighted distributions differ. | Do not infer hedge intensity from cross-metric magnitude differences. |
| GEX hotspot without DEX overlap | The prominent locations of gamma- and delta-weighted distributions differ. | Record the location difference, then test it with price and participation. |

### 03 / ODV Reading

#### Use DEX In Greeks Profile To Confirm Directional Exposure Areas

First confirm symbol, DEX, DTE window, and timestamp, then use Greeks Profile to locate relative clusters within that view. K, M, and B are display suffixes only. Do not compare raw values across symbols, metrics, DTE windows, or snapshots, and do not combine DEX signs with flow classes to infer dealer direction.

- DEX does not mean futures must move one way.
- DEX is better for answering what is prominent within one view, not whether to enter now.
- Read it with GEX, OI, flow, and IV to judge whether exposure may affect futures behavior.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

