---
title: "Aggregate Data：总量结构怎么读"
title_en: "Aggregate Data: How To Read The Total Structure"
slug: "aggregate-options-data"
type: lesson
level: Intermediate
order: 48
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "12 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "Aggregate Data：总量结构怎么读"
  - "Aggregate Data: How To Read The Total Structure"
  - "aggregate-options-data"
source_url: "https://tradinghubs.org/docs/trading-knowledge/aggregate-options-data"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# Aggregate Data：总量结构怎么读

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[delta-exposure-dex|DEX：Delta Exposure 怎么看]] ｜ 下一课：[[odv-10-minute-reading-routine|ODV 10 分钟读盘流程]]

**中级 · 做市商定位与期权敞口 · 12 分钟**

> Aggregate Data 是第一眼的结构背景，不是开仓面板。ODV 直接展示各窗口的预计算结果；当前页面没有统一 multiplier、逐 Strike Call / Put 分解或 dealer ownership，因此不要从通用公式重建总量或把符号翻译成持仓归属。

先核对 Total GEX、Flow Ratio、IV Ratio 与 Max OI 的窗口、时间、符号和权重，再把总量作为进入具体行权价的背景。

### 01 / 总量视角

#### 总量先判断环境，不先判断点位

在本课的产品读法里，正负号、OI 与 Volume 都不能单独证明做市商库存、持仓归属或对冲方向；K / M / B 仅为紧凑显示缩写，不是美元、股数、合约数或每点冲击的经济单位。只可在同一标的、同一指标、同一 DTE 窗口和同一数据快照内比较分布。0DTE、1DTE+ 与 90D Window 均为独立预计算值，90D Window 不等于前两者相加；同一视图中的累计线是页面有符号值的代数累计，不是 Call − Put。

读完总量以后，才切到 Greeks Profile 找具体行权价和 DTE 窗口。

- C_n 只在同一标的、指标、DTE 窗口和数据快照内有意义，不能跨视图相加或比较绝对值。
- IV Ratio 必须声明权重、DTE、Delta / Moneyness 范围与缺失报价处理；否则不同页面或时点不可比较。
- Max OI 使用最近发布的 OI 快照，不是当天新仓证明。

- **同一视图的有符号累计**

  ```latex
  C_n=\sum_{i=1}^{n}x_i
  ```

- **同一视图的相对条宽**

  ```latex
  w_i=\frac{|x_i|}{\max_j|x_j|},\quad \max_j|x_j|>0
  ```

### 02 / 指标组合

#### 先看整体，再看冲突

总量指标最有价值的地方，是快速发现不同观察层是否一致。出现差异时，先检查更新时间、DTE、符号、权重和单位；只有这些口径一致后，差异才可能表示市场活动变化，而不是数据定义差异。

| 观察 | 常见含义 | 下一步 |
| --- | --- | --- |
| 同一视图内出现突出 GEX 区 | 该行权价相对本视图其他位置更突出。 | 用价格接受与期货成交验证，不从符号推 dealer 对冲。 |
| 不同 DTE 的热点位置不同 | 各独立窗口描述不同期限的模型分布。 | 分别记录，不比较原始绝对值，也不把 90D Window 当作前两窗之和。 |
| 分类 Flow 与 GEX 快照不同 | 当天活动与最近仓位观察层不一致。 | 等待价格接受和下一次 OI 更新，不提前称为结构迁移。 |

### 03 / 期货传导

#### Aggregate Data 提出环境假设，期货盘面负责确认

当多个指标各自的热点位置重合时，观察期货是否真的在该区域反复接受；当热点错位或价格穿越时，观察是否出现持续成交和新的价格接受。总量只决定要验证的问题，不决定答案。

- Aggregate Data 不替代具体行权价分析。
- 总量读法和 Greeks Profile 必须闭环。

## 相关概念

- [[gamma-exposure-gex|GEX / vGEX：Gamma Exposure 怎么看]] — 聚合视图是单节点敞口在更大范围内的汇总。
- [[delta-exposure-dex|DEX：Delta Exposure 怎么看]] — 总量与方向必须一起看，否则会掩盖内部冲突。
- [[options-volume-participation|Volume：期权参与强度怎么读]] — 聚合读数需要活动量作为可信度参考。
- [[combined-odv-reads|组合读法：趋势延续、吸附与波动放大]] — 聚合数据是组合读法的第一层，而不是结论本身。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Aggregate Data provides initial structural context, not an entry panel. ODV directly displays precomputed results for each window. The current view has no universal multiplier, per-strike call-put decomposition, or dealer ownership, so do not rebuild totals from a generic formula or translate signs into ownership.

Check the window, timestamp, sign, and weighting behind total GEX, flow ratio, IV ratio, and max OI before using aggregates as context for strike-level analysis.

### 01 / Aggregate View

#### Aggregate Metrics Read The Environment Before Levels

In this product reading, signs, OI, and volume do not establish dealer inventory, ownership, or hedge direction. K / M / B are compact display suffixes, not economic units such as dollars, shares, contracts, or a per-point shock. Compare distributions only within the same symbol, metric, DTE window, and snapshot. 0DTE, 1DTE+, and 90D Window are independent precomputed values; 90D Window is not the sum of the first two. A cumulative line within one view is the algebraic accumulation of displayed signed values, not call minus put.

After reading the aggregate view, move to Greeks Profile to locate specific strikes and DTE windows.

- C_n is meaningful only within the same symbol, metric, DTE window, and snapshot; do not add or compare raw values across views.
- IV ratio must declare weighting, DTE, delta or moneyness range, and missing-quote handling; otherwise pages and timestamps are not comparable.
- Max OI uses the latest published OI snapshot and does not prove same-session new positioning.

- **Signed cumulative line within one view**

  ```latex
  C_n=\sum_{i=1}^{n}x_i
  ```

- **Relative bar width within one view**

  ```latex
  w_i=\frac{|x_i|}{\max_j|x_j|},\quad \max_j|x_j|>0
  ```

### 02 / Metric Combinations

#### Read The Whole First, Then The Conflicts

Aggregate metrics are most useful for checking agreement across observation layers. When they differ, inspect timestamp, DTE, sign, weights, and units first; only after conventions align can disagreement indicate changing market activity rather than different definitions.

| Observation | Common Meaning | Next Step |
| --- | --- | --- |
| A prominent GEX area within one view | That strike is more prominent relative to others in the same view. | Validate with price acceptance and futures participation; do not infer dealer hedging from sign. |
| Hotspot locations differ across DTE windows | Each independent window describes a different-horizon modeled distribution. | Record them separately; do not compare raw magnitudes or treat 90D Window as the sum of the first two. |
| Classified flow differs from the GEX snapshot | Same-session activity differs from the latest positioning layer. | Wait for price acceptance and the next OI update before calling structural migration. |

### 03 / Futures Transmission

#### Aggregate Data Proposes A Regime Hypothesis; Futures Confirm It

When hotspot locations from several metrics overlap, observe whether futures repeatedly accept that area. When hotspots differ or price crosses one, watch for sustained participation and new price acceptance. Aggregates choose the question to test; they do not decide the answer.

- Aggregate Data does not replace strike-level analysis.
- Aggregate reading must close the loop with Greeks Profile.

## Related Concepts

- [[gamma-exposure-gex|GEX / vGEX: How To Read Gamma Exposure]] — The aggregate view is single-node exposure summarized over a wider scope.
- [[delta-exposure-dex|DEX: How To Read Delta Exposure]] — Totals and direction must be read together or internal conflict is hidden.
- [[options-volume-participation|Volume: How To Read Options Participation Strength]] — An aggregate reading needs activity level as a credibility reference.
- [[combined-odv-reads|Combined Reads: Trend Continuation, Pinning, And Volatility Expansion]] — Aggregate data is the first layer of a combined read rather than the conclusion itself.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

