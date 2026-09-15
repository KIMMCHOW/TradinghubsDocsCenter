---
title: "ODV 10 分钟读盘流程"
title_en: "ODV 10-Minute Reading Routine"
slug: "odv-10-minute-reading-routine"
type: lesson
level: Intermediate
order: 49
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "10 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "ODV 10 分钟读盘流程"
  - "ODV 10-Minute Reading Routine"
  - "odv-10-minute-reading-routine"
source_url: "https://tradinghubs.org/docs/trading-knowledge/odv-10-minute-reading-routine"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# ODV 10 分钟读盘流程

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[aggregate-options-data|Aggregate Data：总量结构怎么读]] ｜ 下一课：[[expectations-feedback-path-dependence|预期、反馈与路径依赖]]

**中级 · 做市商定位与期权敞口 · 10 分钟**

> 这不是新的指标，而是一套防止漏看的读盘流程。每次按同样顺序走，才能减少只盯一个数字的错误。

把 Data Dashboard、Greeks Profile、DTE、Flow、Volume、IV 和风险边界串成一个固定读盘顺序。

### 01 / 十步流程

#### 先总量，后行权价，最后回到期货图

10 分钟流程的目标是快速建立结构地图，而不是在 ODV 内直接做交易决策。

- 1. 确认 ticker、参考价格和数据更新时间。
- 2. 标出当前价格上下方最近的 Key Levels。
- 3. 核对 Total GEX 的标的、指标、DTE、时间与模型符号；符号只作当前口径读数，不推断做市商库存或对冲。
- 4. 看 OI 和 Max OI 的最近发布时间，定位快照中的合约集中区。
- 5. 看 Classified Flow Ratio、Net Classified Flow 和 Volume，记录成交分类与参与度，不推断开仓或 dealer 库存。
- 6. 看 IV 与 VEX，记录 IV 变化是否与 VEX 热点重合；不从 VEX 符号推断 dealer 对冲方向。
- 7. 切到 Greeks Profile，先在每个指标自己的视图内找热点，再比较行权价位置是否重合；不跨指标比绝对值。
- 8. 分开读取 0DTE、1DTE+ 与 90D Window；三者是独立值，90D Window 不是前两窗之和。
- 9. 写下两个上方结构位和两个下方结构位。
- 10. 回到期货计划，定义入场、止损、仓位和失效条件。

### 02 / 输出模板

#### 十分钟结束时，必须留下可复核的四行摘要

流程的产物不是一句“偏多”或“偏空”，而是一张可以在盘中复核的结构卡。它必须记录数据时间、上方与下方结构、当前环境，以及什么变化会推翻判断。

如果无法把结论压缩到这四行，通常说明观察项仍然冲突，或者把不同 DTE 混在了一起。此时应回到数据窗口与行权价分布，而不是增加更多指标。

| 记录项 | 示例格式 |
| --- | --- |
| 数据状态 | 品种、更新时间、主观察 DTE。 |
| 结构地图 | 上方两区、下方两区、当前价所在区间。 |
| 环境判断 | 稳定、趋势、波动放大或冲突，并列出依据。 |
| 失效条件 | 哪一项价格接受或数据迁移会改变原判断。 |

- 盘中只更新发生变化的字段，不事后改写盘前地图。
- 结论与证据分开记录，便于复盘判断错误来自数据、解释还是执行。

### 03 / 风险规则

#### 任何 ODV 读法都不能替代风险控制

不要只因为某个指标极端就交易。不要忽略数据更新时间。不要混淆 0DTE 与中期结构。不要用期权结构替代期货盘口、成交量、宏观事件和交易时段背景。

ODV 的正确位置，是期货交易系统里的结构阅读层。最终决策必须回到你的策略、执行和风险管理。

- 流程能减少漏看，但不能消除交易风险。
- 没有止损、仓位和失效条件时，不应使用任何结构判断开仓。

## 相关概念

- [[aggregate-options-data|Aggregate Data：总量结构怎么读]] — 固定流程从总量环境开始，再进入节点细节。
- [[dte-window-selection|DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选]] — 按到期窗口拆分读数，避免把不同期限混为一谈。
- [[combined-odv-reads|组合读法：趋势延续、吸附与波动放大]] — 流程的终点是组合读法，而不是单张图的结论。
- [[options-pnl-attribution|期权 P&L 归因：从起止重估到 Greek 解释残差]] — 读图结论最终必须能对应到可解释的损益来源。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> This is not a new metric. It is a routine that prevents missed context. Walking through the same order reduces the mistake of staring at one number.

Turn Data Dashboard, Greeks Profile, DTE, flow, volume, IV, and risk boundaries into a fixed reading sequence.

### 01 / Ten Steps

#### Aggregate First, Strikes Second, Futures Chart Last

The goal of the 10-minute routine is to build a quick structural map, not to make a trade decision inside ODV.

- 1. Confirm ticker, reference price, and data freshness.
- 2. Mark the nearest key levels above and below current price.
- 3. Check total GEX symbol, metric, DTE, timestamp, and model sign; treat sign as a value under the current convention, not dealer inventory or hedging.
- 4. Read the latest OI and Max OI publication time and locate contract concentration in that snapshot.
- 5. Read classified flow ratio, net classified flow, and volume for classification and participation without inferring opening or dealer inventory.
- 6. Read IV and VEX, noting whether IV changes overlap VEX hotspots; do not infer dealer hedge direction from VEX sign.
- 7. Open Greeks Profile, locate hotspots within each metric's own view, then compare strike locations; do not compare raw magnitudes across metrics.
- 8. Read 0DTE, 1DTE+, and 90D Window separately; they are independent values and 90D Window is not the sum of the first two.
- 9. Write down two upper and two lower structural areas.
- 10. Return to the futures plan and define entry, stop, size, and invalidation.

### 02 / Output Template

#### Finish The Ten Minutes With A Four-Line Reviewable Summary

The output is not a one-line bullish or bearish label. It is a structural card that can be reviewed during the session. Record data time, upper and lower structures, the current regime, and the change that would invalidate the read.

If the conclusion cannot be reduced to these four lines, the observations are usually still in conflict or different DTE windows have been mixed. Return to the data window and strike distribution instead of adding more indicators.

| Field | Example Format |
| --- | --- |
| Data state | Symbol, update time, and primary DTE window. |
| Structure map | Two upper areas, two lower areas, and the current-price range. |
| Regime read | Stable, trending, expanding volatility, or conflict, with supporting evidence. |
| Invalidation | Which price acceptance or data migration would change the original read. |

- Update only the fields that change intraday; do not rewrite the pre-market map after the fact.
- Record conclusions separately from evidence so reviews can isolate data, interpretation, and execution errors.

### 03 / Risk Rules

#### No ODV Reading Replaces Risk Control

Do not trade only because one metric is extreme. Do not ignore data freshness. Do not confuse 0DTE with medium-term structure. Do not use options structure as a replacement for futures order flow, volume, macro events, or session context.

ODV's proper place is the structure-reading layer inside a futures trading system. Final decisions must return to your strategy, execution, and risk management.

- A routine can reduce missed context, but it cannot remove trading risk.
- Without stop, sizing, and invalidation rules, no structural read should be used as an entry.

## Related Concepts

- [[aggregate-options-data|Aggregate Data: How To Read The Total Structure]] — A fixed routine starts from the aggregate regime before moving into node detail.
- [[dte-window-selection|DTE Windows: How To Choose 0DTE, 1DTE+, And 90D Window]] — Reading by expiry window avoids conflating different horizons.
- [[combined-odv-reads|Combined Reads: Trend Continuation, Pinning, And Volatility Expansion]] — The routine ends in a combined read rather than a single-chart conclusion.
- [[options-pnl-attribution|Options P&L Attribution: From Endpoint Revaluation To Greek Explanations]] — A chart conclusion must ultimately map onto an explainable source of P&L.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

