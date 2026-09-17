---
title: "到期周的流动性迁移：0DTE 到 1DTE 的重心转移"
title_en: "Expiry-Week Liquidity Migration: How Weight Shifts From 0DTE To 1DTE"
slug: "expiry-week-liquidity-migration"
type: lesson
level: Advanced
order: 102
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "19 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "到期周的流动性迁移：0DTE 到 1DTE 的重心转移"
  - "Expiry-Week Liquidity Migration: How Weight Shifts From 0DTE To 1DTE"
  - "expiry-week-liquidity-migration"
source_url: "https://tradinghubs.org/docs/trading-knowledge/expiry-week-liquidity-migration"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 到期周的流动性迁移：0DTE 到 1DTE 的重心转移

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[intraday-surface-elasticity-session-log|盘中曲面弹性复盘：把吸收与重定价记录成可核对的时间线]] ｜ 下一课：[[cross-market-hedge-ratio-dashboard|跨市场对冲比率面板：把基差、乘数与等值手数放进同一张可核对表]]

**高级 · 结构、定价与波动率 · 19 分钟**

> 近端结构不会一直主导。随着时间推进，近端的敏感度与可用流动性都会变化，观察重心自然移动到下一个到期窗口。本课讨论这个迁移过程及其对读图顺序的影响。

到期周期内，观察重心会从近端逐步迁移到下一个到期日：本课说明迁移的驱动、如何在图上识别迁移已经发生，以及迁移过程中哪些读法会失效。

### 01 / 窗口迁移

#### 剩余时间缩短会先放大、后抽走近端的影响

其他条件不变时，剩余期限缩短会让平值附近的敏感度更集中，所以近端在当天早些时候往往显得更有影响。但同一个过程也意味着合约更快接近失去时间价值：当价格远离执行价时，近端的敏感度会迅速衰减。

于是观察重心会迁移到下一个到期窗口。迁移不是一次事件，而是一个过程：先是两个窗口同时重要，随后近端退居次要，最后大部分可用结构都在下一个窗口里。

| 阶段 | 近端窗口 | 下一窗口 | 读图重点 |
| --- | --- | --- | --- |
| 早期 | 敏感度集中且仍有效。 | 背景结构。 | 以近端为主，下一窗口作对照。 |
| 中期 | 有效性开始随价格距离分化。 | 开始出现可用的集中区。 | 两个窗口并列比较，不做合并。 |
| 后期 | 影响快速衰减，仅近距离有效。 | 承担主要结构。 | 以下一窗口为主，近端仅作即时参考。 |

### 02 / 识别迁移

#### 迁移的三种可观察迹象

第一，同一个价位在近端窗口里反复被测试，但在价格离开后不再对后续走势产生可见影响。第二，下一窗口开始出现与近端无关的独立集中区，且这些集中区在价格到达时的反应更稳定。第三，同样幅度的事件对近端窗口的影响越来越小。

识别出迁移之后，读法要跟着改：不要再假设近端的集中区一定会主导，也不要把两个窗口的数值相加或直接比较大小。两个窗口回答的是两个不同时间范围的问题。

> [!note] 迁移不是新闻事件
> 迁移由时间推进驱动，即使当天没有消息也会发生。把迁移误读成消息驱动，会让人去寻找不存在的新闻原因。

> [!warning] 两个窗口不可相加
> 把近端与下一窗口的读数相加会制造出一个不存在的时间范围，得到的数字无法解释。

### 03 / 风险边界

#### 迁移期间最容易犯的三个错误

一是用旧窗口的结论继续解释新价格行为；二是把两个窗口的集中区强行叠加成一个看上去更强的价位；三是在迁移明显的时段提高对历史结论的信任度，而不是降低。

正确的处理反而是降低确定性：迁移期间结构本身在变，任何基于单一窗口的结论都应当被标记为待下一个快照确认，并把失效条件写在前面。

- 第一步：先确认当前处于迁移的哪个阶段，再决定以哪个窗口为主。
- 第二步：用三种迹象逐一核对迁移是否真的发生，而不是凭感觉。
- 第三步：迁移期间降低结论权重，并写明等待哪一个快照确认。
- 风险边界：两个窗口不可相加，也不可跨窗口比较绝对大小。

## 相关概念

- [[dte-window-selection|DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选]] — 窗口选择是判断迁移阶段的前提。
- [[charm-exposure-chex|CHEX：Charm Exposure 怎么看]] — 时间衰减是近端影响被抽走的直接原因。
- [[convexity-regime-liquidity-map|凸性环境地图：多头与空头凸性下的流动性差异]] — 迁移会改变各窗口的流动性地形。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> The nearest structure does not dominate forever. As time passes, both its sensitivity and its available liquidity change, and the centre of attention moves to the next expiry window. This lesson covers that migration and what it does to the reading order.

Within an expiry cycle the centre of attention migrates from the nearest expiry to the next one: this lesson covers the drivers, how to identify that migration on a chart, and which readings stop working while it happens.

### 01 / The Window Shifts

#### Shorter Time First Amplifies Then Drains The Near Window

Other things equal, a shorter remaining life concentrates sensitivity near the money, so the nearest window often looks more influential earlier in the day. The same process also means those contracts lose time value faster: once price moves away from the strike, near-window sensitivity decays quickly.

The centre of attention therefore migrates to the next expiry window. The migration is a process rather than an event: at first both windows matter, then the near window becomes secondary, and finally most usable structure sits in the next window.

| Stage | Near window | Next window | Reading focus |
| --- | --- | --- | --- |
| Early | Concentrated and still effective. | Background structure. | Lead with the near window and use the next as contrast. |
| Middle | Effectiveness starts to diverge with price distance. | Usable concentrations begin to appear. | Compare the two windows side by side without merging them. |
| Late | Influence decays quickly and only works nearby. | Carries the main structure. | Lead with the next window and keep the near one as an immediate reference. |

### 02 / Identifying The Migration

#### Three Observable Signs Of Migration

First, one price is repeatedly tested in the near window but stops having any visible effect on subsequent price once left behind. Second, the next window starts to show independent concentrations unrelated to the near window, and those react more reliably when price arrives. Third, events of the same size have progressively less effect on the near window.

Once migration is identified the reading must change with it: stop assuming the near window's concentrations must dominate, and never add the two windows together or compare their magnitudes directly. The two windows answer questions about two different time horizons.

> [!note] Migration Is Not A News Event
> Migration is driven by the passage of time and happens even on days with no news. Mistaking it for a news-driven move sends a reader looking for a cause that does not exist.

> [!warning] The Two Windows Are Not Additive
> Adding the near and next window readings manufactures a time horizon that does not exist, and the result cannot be explained.

### 03 / Risk Boundaries

#### Three Mistakes During Migration

First, continuing to explain new price behaviour with the old window's conclusion. Second, forcing the two windows' concentrations into one supposedly stronger price. Third, raising confidence in earlier conclusions during a clearly migrating period instead of lowering it.

The correct handling is the opposite: reduce certainty. The structure itself is changing during migration, so any conclusion drawn from a single window should be marked as awaiting the next snapshot, with the failure condition written first.

- Step one: establish which migration stage you are in before choosing the leading window.
- Step two: check the three migration signs one by one instead of relying on impression.
- Step three: lower the weight of conclusions during migration and state which snapshot will confirm them.
- Risk boundary: the two windows are neither additive nor comparable in absolute magnitude.

## Related Concepts

- [[dte-window-selection|DTE Windows: How To Choose 0DTE, 1DTE+, And 90D Window]] — Window selection is the precondition for judging the migration stage.
- [[charm-exposure-chex|CHEX: How To Read Charm Exposure]] — Time decay is the direct reason near-window influence drains away.
- [[convexity-regime-liquidity-map|The Convexity Regime Map: Liquidity Under Long And Short Convexity]] — Migration changes the liquidity terrain in each window.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- cme-volume-open-interest
- finra-volatility
