---
title: "组合读法：趋势延续、吸附与波动放大"
title_en: "Combined Reads: Trend Continuation, Pinning, And Volatility Expansion"
slug: "combined-odv-reads"
type: lesson
level: Advanced
order: 62
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "14 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "组合读法：趋势延续、吸附与波动放大"
  - "Combined Reads: Trend Continuation, Pinning, And Volatility Expansion"
  - "combined-odv-reads"
source_url: "https://tradinghubs.org/docs/trading-knowledge/combined-odv-reads"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 组合读法：趋势延续、吸附与波动放大

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[skew-term-structure|Skew / Term Structure]] ｜ 下一课：[[dynamic-delta-hedging|动态 Delta 对冲与路径风险]]

**高级 · 做市商定位与期权敞口 · 14 分钟**

> ODV 的核心不是找一个万能指标，而是把多个结构变量组合起来，判断当前盘面更像哪一种状态。

把 Flow、Volume、GEX、vGEX、OI、IV、VEX、CHEX 组合起来，区分趋势延续、区间吸附、波动放大和信号冲突。

### 01 / 框架

#### 先识别状态，再讨论交易计划

组合读法先问：当前是趋势延续、区间吸附、波动放大，还是信号冲突？不同状态下，同一个 GEX 或 Flow 数字的意义可能完全不同。

| 状态 | 可能特征 | 读法重点 |
| --- | --- | --- |
| 趋势延续 | 分类 Flow 与期货价格同向、成交持续、vGEX 活动靠近被穿越区域。 | 看突破后是否不快速回落。 |
| 区间或吸附 | 价格在同一窗口的 OI / GEX 热点附近反复接受，分类 Flow 不持续单边。 | 把吸附当作待验证假设，看价格是否反复接受该区。 |
| 波动放大 | 价格离开模型热点后持续扩展，分类 Flow、期货成交与 IV 同时增强。 | 由价格与成交确认扩张，不把暴露符号当作 dealer 因果。 |
| 信号冲突 | 最近 OI/GEX 快照与当天分类 Flow 或 vGEX 活动热点不一致。 | 先排除标的、指标、DTE 与数据快照差异，再等待价格与 OI 更新。 |

### 02 / 证据顺序

#### 用三层证据确认，而不是把指标票数相加

第一层是慢变量：OI、主要 GEX 区和 1DTE+ / 90D Window 结构，负责定义盘前地图。第二层是快变量：vGEX、Flow、Volume 与近端 IV，负责判断当天是否正在偏离这张地图。第三层是期货确认：价格是否接受关键位、突破后是否回测、成交是否持续。三个 Exposure 窗口彼此独立，90D Window 不是前两窗之和。

多个指标同向并不自动代表高胜率，因为它们可能来自同一批合约或同一次价格变化。相反，慢结构、当日成交和期货行为来自不同观察层时，才更接近独立确认。

| 层级 | 先问什么 | 失效信号 |
| --- | --- | --- |
| 慢结构 | 每个指标各自视图里的主要热点在哪里？ | 近期热点迁移，或独立 DTE 窗口给出不同地图。 |
| 当日重定价 | 当天活动热点与期货价格是否持续接受原结构内外的新区域？ | Flow 无延续、Volume 收缩或 IV 回吐。 |
| 期货确认 | 价格是否接受关键位外的新区域？ | 突破快速收回，或成交无法跟进。 |

- 先写下慢结构，再观察快变量是否改变地图。
- 只有期货价格与成交确认后，结构判断才进入执行层。

### 03 / 边界

#### 组合读法是状态识别，不是自动策略

组合读法只能提高你对结构状态的判断质量，不能替代期货盘口、成交、宏观事件、仓位管理和止损规则。

- 先识别状态，再匹配自己的交易系统。
- 冲突状态下，少做结论比硬做方向更重要。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> ODV is not about finding one perfect metric. It is about combining structural variables to judge which market state the current tape resembles.

Combine flow, volume, GEX, vGEX, OI, IV, VEX, and CHEX to separate trend continuation, range pinning, volatility expansion, and conflicting signals.

### 01 / Framework

#### Identify The State Before Discussing A Trade Plan

Combined reading first asks whether the current state is trend continuation, range pinning, volatility expansion, or signal conflict. The same GEX or flow number can mean different things in different states.

| State | Possible Features | Reading Focus |
| --- | --- | --- |
| Trend continuation | Classified flow and futures price align, participation persists, and vGEX activity sits near the crossed area. | Watch whether price avoids quickly falling back after the break. |
| Range or pinning | Price repeatedly accepts an OI / GEX hotspot within one window while classified flow lacks persistent one-way pressure. | Treat pinning as a hypothesis and watch whether price repeatedly accepts the area. |
| Volatility expansion | Price continues to expand after leaving a modeled hotspot while classified flow, futures participation, and IV strengthen. | Let price and participation confirm expansion; do not treat exposure sign as dealer causality. |
| Conflicting signals | The latest OI/GEX snapshot differs from same-session classified flow or the vGEX activity hotspot. | First exclude symbol, metric, DTE, and snapshot differences, then wait for price and the OI update. |

### 02 / Evidence Order

#### Confirm With Three Evidence Layers Instead Of Counting Indicator Votes

The first layer contains slower variables: OI, major GEX areas, and 1DTE+ / 90D Window structure define the pre-market map. The second layer contains faster variables: vGEX, flow, volume, and front-end IV show whether the session is departing from that map. The third layer is futures confirmation: whether price accepts a level, retests after a break, and sustains participation. Exposure windows are independent; 90D Window is not the sum of the first two.

Several aligned metrics do not automatically imply high confidence because they may come from the same contracts or the same price move. Confirmation is more meaningful when slow structure, same-day trading, and futures behavior contribute evidence from different layers.

| Layer | Question | Invalidation |
| --- | --- | --- |
| Slow structure | Where are the main hotspots within each metric's own view? | Recent hotspots migrate or independent DTE windows show different maps. |
| Session repricing | Do same-session activity hotspots and futures price persistently accept a new area inside or beyond the prior structure? | Flow loses persistence, volume contracts, or IV retraces. |
| Futures confirmation | Does price accept a new area beyond the key level? | The break is quickly reclaimed or participation fails to follow. |

- Write down the slow structure first, then watch whether fast variables change the map.
- A structural read reaches the execution layer only after futures price and participation confirm it.

### 03 / Boundary

#### Combined Reading Is State Recognition, Not An Automatic Strategy

Combined reading can improve the quality of structural state recognition, but it does not replace futures order flow, volume, macro events, position sizing, or stop rules.

- Identify the state first, then map it to your own trading system.
- In conflict states, avoiding forced conclusions is more important than forcing direction.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

