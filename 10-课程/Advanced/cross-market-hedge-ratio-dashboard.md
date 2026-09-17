---
title: "跨市场对冲比率面板：把基差、乘数与等值手数放进同一张可核对表"
title_en: "Cross-Market Hedge-Ratio Dashboard: Basis, Multiplier And Equivalent Lots In One Checkable Table"
slug: "cross-market-hedge-ratio-dashboard"
type: lesson
level: Advanced
order: 103
track: futures-and-options-linkage
track_label: "期货与期权衔接"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/期货与期权衔接"
  - "权限/需登录"
aliases:
  - "跨市场对冲比率面板：把基差、乘数与等值手数放进同一张可核对表"
  - "Cross-Market Hedge-Ratio Dashboard: Basis, Multiplier And Equivalent Lots In One Checkable Table"
  - "cross-market-hedge-ratio-dashboard"
source_url: "https://tradinghubs.org/docs/trading-knowledge/cross-market-hedge-ratio-dashboard"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 跨市场对冲比率面板：把基差、乘数与等值手数放进同一张可核对表

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[futures-and-options-linkage|期货与期权衔接]]
> 上一课：[[expiry-week-liquidity-migration|到期周的流动性迁移：0DTE 到 1DTE 的重心转移]]

**高级 · 期货与期权衔接 · 18 分钟**

> 分开记录基差、换算与手数，会让任何一次复核都变成考古。本课把这些字段放进同一张表，并说明每一项在什么情况下会失效。

把期权侧的敞口换算成可执行的期货手数时，基差、乘数与时点必须同框记录：本课给出一份字段固定、可复核、明确失效条件的面板结构。

### 01 / 面板输入

#### 四项输入缺一不可

面板需要四项输入：期权侧的方向敞口（以每点金额表达）、目标期货合约的每点金额、当期基差或缩放关系、以及取数时点。前两项决定手数，第三项决定坐标，第四项决定结论是否还有效。

把四项放在同一行记录，可以在任何时候复核一次换算是否还成立；缺少任意一项，这张表在事后都无法重现。

- **等值期货手数（概念式）**

  ```latex
  n_{f}=\dfrac{E_{o}}{M_{f}}
  ```
  E_o 为期权侧以每点金额表达的方向敞口，M_f 为目标期货合约的每点金额；两者必须取同一时点的数据。

### 02 / 字段结构

#### 一行记录，八列字段

推荐字段：标的与合约月份、期权侧敞口、敞口单位、期货每点金额、基差或缩放、换算后手数、取整方式、取数时间。八列固定，新增行只改数值，不改结构。

这样记录还有额外好处：当基差变化时，只需要重算受影响的那一列，其他列保持可比；如果把基差与手数混在同一栏里，任何一次基差更新都会让历史记录失去可比性。

| 字段 | 为什么必须单列 | 失效条件 |
| --- | --- | --- |
| 合约月份 | 坐标随换月整体改变。 | 主力合约切换后未更新。 |
| 期货每点金额 | 迷你与微型合约只在此列不同。 | 按错误的合约类型换算。 |
| 基差或缩放 | 它随时点漂移。 | 沿用早盘数值。 |
| 取整方式 | 手数必须落到最小变动单位。 | 报告了无法执行的手数。 |

### 03 / 失效与边界

#### 比率面板不能替你决定该不该对冲

面板回答的是「如果要换算，换算成多少手」，不回答「是否应该对冲」。把换算结果当作行动指令，是把算术当成了决策。

边界还包括：期权侧敞口本身是估计值，会随价格与波动率变化；基差在资金紧张或特殊股息处理时会显著偏离简单模型；换月当天的可比性有限。三项同时出现时，应当把面板标记为不可用，而不是勉强给出一个手数。

> [!question] 手数不是指令
> 换算结果只表达等值关系。是否行动取决于风险预算、已有持仓与个人计划，面板不参与这三项。

> [!warning] 过期基差使整张表失效
> 基差漂移会同时改变坐标与手数，因此取数时间是这一行的组成部分，而不是附注。

- 第一步：四项输入必须来自同一时点，缺一即标记不可用。
- 第二步：八列固定，只更新数值，不改结构，保证历史可比。
- 第三步：手数落到最小变动单位后再记录。
- 风险边界：资金紧张、特殊股息或换月日应直接标记不可用。

## 相关概念

- [[index-futures-etf-level-conversion|同一价位在不同市场：指数、ETF 与期货的换算]] — 基差与缩放是本面板的输入之一。
- [[synthetic-futures-and-delta-equivalent-sizing|用期权表达期货敞口：合成结构与等值换算]] — 等值手数换算与本课的比率表是同一套算术。
- [[futures-contract-mechanics-tick-value|期货合约机制：最小变动、点值与展期]] — 每点金额与最小变动单位来自合约规格。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Recording basis, conversion, and lot sizing in separate places turns any review into archaeology. This lesson puts the fields into one table and states when each of them fails.

Converting option-side exposure into executable futures lots requires basis, multiplier, and timestamp to be recorded in one frame: this lesson gives a dashboard structure with fixed fields, checkable arithmetic, and explicit failure conditions.

### 01 / Dashboard Inputs

#### Four Inputs, None Optional

The dashboard needs four inputs: the option-side directional exposure expressed as money per point, the target futures contract's currency per point, the current basis or scaling relation, and the timestamp of the reading. The first two determine the lot size, the third determines the coordinate, and the fourth determines whether the conclusion is still valid.

Recording all four on one row makes it possible to re-check at any time whether a conversion still holds; omit any one and the table cannot be reproduced afterwards.

- **Equivalent futures lots (conceptual)**

  ```latex
  n_{f}=\dfrac{E_{o}}{M_{f}}
  ```
  E_o is the option-side directional exposure expressed as money per point and M_f is the target futures contract's currency per point; both must come from the same timestamp.

### 02 / Field Structure

#### One Row, Eight Columns

Recommended fields: symbol and contract month, option-side exposure, exposure unit, futures currency per point, basis or scaling, converted lots, rounding rule, and timestamp. Keep the eight columns fixed; new rows change values, not structure.

The structure has a further benefit: when the basis changes only the affected column is recomputed and the rest stay comparable; mixing basis and lots in one field destroys the comparability of history on every basis update.

| Field | Why it needs its own column | Failure condition |
| --- | --- | --- |
| Contract month | The coordinate shifts as a whole on a roll. | Not updated after the front month rolls. |
| Currency per point | Mini and micro contracts differ only here. | Converted against the wrong contract type. |
| Basis or scaling | It drifts with the timestamp. | Reusing a morning value. |
| Rounding rule | Lot size must land on the minimum increment. | Reporting a lot size that cannot be traded. |

### 03 / Failure And Boundaries

#### The Dashboard Does Not Decide Whether To Hedge

The dashboard answers how many lots a conversion implies, not whether hedging should happen. Treating the converted number as an instruction mistakes arithmetic for a decision.

The boundaries also include: the option-side exposure is itself an estimate that moves with price and volatility; the basis departs materially from a simple model under funding stress or special dividend treatment; comparability on a roll day is limited. When all three appear together the dashboard should be marked unusable rather than squeezing out a lot count.

> [!question] A Lot Count Is Not An Instruction
> A converted result expresses an equivalence only. Whether to act depends on risk budget, existing positions, and a personal plan, none of which the dashboard knows.

> [!warning] A Stale Basis Invalidates The Whole Table
> A drifting basis changes both the coordinate and the lot size, which makes the timestamp part of the row rather than a footnote.

- Step one: all four inputs must share one timestamp; missing any marks the row unusable.
- Step two: keep the eight columns fixed and update values only, so history stays comparable.
- Step three: record the lot size only after rounding to the minimum increment.
- Risk boundary: funding stress, special dividends, or a roll day should be marked unusable outright.

## Related Concepts

- [[index-futures-etf-level-conversion|One Level, Three Markets: Converting Between Cash Index, ETF And Futures]] — Basis and scaling are one of the dashboard's inputs.
- [[synthetic-futures-and-delta-equivalent-sizing|Expressing Futures Exposure With Options: Synthetics And Equivalent Sizing]] — Equivalent lot sizing and this lesson's ratio table share one arithmetic.
- [[futures-contract-mechanics-tick-value|Futures Contract Mechanics: Tick Size, Tick Value, And Rolls]] — Currency per point and minimum increment come from the contract specification.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-equity-index-basis
- cftc-futures-basics
- cme-volume-open-interest
