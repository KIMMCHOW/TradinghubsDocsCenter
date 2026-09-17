---
title: "盘中曲面弹性复盘：把吸收与重定价记录成可核对的时间线"
title_en: "Intraday Surface-Elasticity Log: Recording Absorption And Repricing As A Checkable Timeline"
slug: "intraday-surface-elasticity-session-log"
type: lesson
level: Advanced
order: 101
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "盘中曲面弹性复盘：把吸收与重定价记录成可核对的时间线"
  - "Intraday Surface-Elasticity Log: Recording Absorption And Repricing As A Checkable Timeline"
  - "intraday-surface-elasticity-session-log"
source_url: "https://tradinghubs.org/docs/trading-knowledge/intraday-surface-elasticity-session-log"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 盘中曲面弹性复盘：把吸收与重定价记录成可核对的时间线

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[dealer-hedging-bands-and-discrete-rebalance|对冲区间与离散再平衡：为什么对冲不是连续动作]] ｜ 下一课：[[expiry-week-liquidity-migration|到期周的流动性迁移：0DTE 到 1DTE 的重心转移]]

**高级 · 订单流与市场微观结构 · 18 分钟**

> 同一段行情，两个人常常得出相反结论，原因往往不是判断力差异，而是记录的字段、时间切分与失效判定不同。本课给出一份最小可用的复盘模板。

把「吸收还是重定价」从形容词变成可复核记录：固定字段、固定时间切分、固定失效判定，让同一段行情可以被不同人一致地复盘。

### 01 / 记录字段

#### 每一段只记六项

字段过多会让记录本身变成负担，字段过少会让事后无法判断。最小可用集合是六项：时间戳、当时价格、目标价位、到达方式（速度与方向）、成交反应（放量或缩量、是否出现吸收）、以及结论标签（吸收 / 重定价 / 无反应）。

结论标签只能在这六项都填完之后给出。先给标签再补证据，是最常见的自我欺骗方式。

| 字段 | 记录要求 | 常见错误 |
| --- | --- | --- |
| 时间戳 | 精确到分钟，并注明时区。 | 事后凭印象补时间。 |
| 价格与目标价位 | 写明价位来源属于哪类关键位。 | 只记价格不记依据。 |
| 到达方式 | 记录速度变化与接近方向。 | 只写价格到达。 |
| 成交反应 | 记录放量或缩量、是否出现吸收。 | 用印象代替成交证据。 |
| 结论标签 | 只能在其余字段填完后给出。 | 先下结论再找证据。 |

### 02 / 时间切分

#### 固定切分，才能比较不同日子

如果每天按感觉重要的时刻记录，记录本身就不可比较。可行做法是固定切分：例如按开盘后每三十分钟一段，或按每次触线事件切一段，并在所有日子使用同一规则。

切分规则一旦固定，就能做两个有用的比较：同一时段在不同日子的差异，以及同一日子不同时段的差异。前者回答这个时段是否天然更容易吸收，后者回答环境是否在盘中切换。

记录时不要合并切分。把两段合成一段看起来更整洁，却会让结论无法归因到具体时段，等于丢掉最有价值的信息。

### 03 / 失效判定

#### 先写失效，再写结论

给每段记录配一个可执行的失效条件：例如价格在设定时间内没有回到该区域内，则本段归为无反应。这样复盘时不需要重新争论当时的判断，只需要核对条件是否成立。

边界必须写清：这份记录只描述已经发生的成交与价格行为，不含任何未来信息，也不得用事后价格回填当时的结论。复盘的目的是让判断过程可核查，而不是把每一天都解释成有故事。

> [!tip] 日志不是叙事
> 记录的价值来自字段一致与可核对，而不是文字精彩。字段缺失的记录无法比较，也无法验证。

> [!warning] 禁止事后回填
> 用后来的价格去改写当时的标签，会让记录永远正确，也永远无用。

- 第一步：先固定切分规则，并固定六项字段。
- 第二步：每段只在实际发生当下填写，结论标签最后填。
- 第三步：为每段写一个可执行的失效条件。
- 风险边界：记录只含已发生数据，不得用未来价格回填结论。

## 相关概念

- [[volatility-surface-elasticity|波动率曲面弹性：成交如何变成波动率供给]] — 本课把该课的吸收与重定价判断变成可核对记录。
- [[absorption-exhaustion-and-iceberg-orders|吸收、衰竭与冰山单]] — 吸收是记录中最重要的成交证据之一。
- [[odv-10-minute-reading-routine|ODV 10 分钟读盘流程]] — 固定顺序的读盘流程与固定字段的复盘互为依据。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Two people often reach opposite conclusions about the same session, and the reason is usually not judgement but differences in recorded fields, time slicing, and failure tests. This lesson gives a minimum viable review template.

Turn absorption versus repricing from an adjective into a checkable record: fixed fields, fixed time slices, and a fixed failure test so the same session can be reviewed consistently by different people.

### 01 / Fields To Record

#### Six Fields Per Slice

Too many fields make recording a burden; too few make retrospection impossible. The minimum viable set is six: timestamp, price at the time, the target level, how price arrived in terms of speed and direction, the trading response including whether absorption appeared, and a conclusion label of absorption, repricing, or no reaction.

The conclusion label may only be assigned once the other five fields are filled. Assigning the label first and backfilling evidence is the most common form of self-deception.

| Field | Recording requirement | Common mistake |
| --- | --- | --- |
| Timestamp | To the minute, with the time zone stated. | Reconstructing the time from memory afterwards. |
| Price and target level | State which kind of key level the price came from. | Recording the price without its basis. |
| Arrival mode | Note the change of speed and the approach side. | Writing only that price arrived. |
| Trading response | Record volume expansion or contraction and whether absorption appeared. | Substituting impression for trading evidence. |
| Conclusion label | Only after the other fields are complete. | Concluding first and hunting evidence after. |

### 02 / Time Slicing

#### Fixed Slices Are What Make Days Comparable

If each day is recorded at whichever moments felt important, the records are not comparable. A workable method is a fixed slice, for example one slice per thirty minutes after the open, or one slice per level-touch event, applied identically on every day.

Once the slicing rule is fixed, two useful comparisons become possible: the same slice across different days, and different slices within one day. The first answers whether that time of day absorbs more readily; the second answers whether the environment switched during the session.

Do not merge slices while recording. Combining two slices looks tidier but makes the conclusion impossible to attribute to a time of day, discarding the most valuable part of the record.

### 03 / The Failure Test

#### Write The Failure Condition Before The Conclusion

Give every slice an executable failure condition: for example, if price did not return inside the area within the stated time, the slice is classified as no reaction. Review then needs no re-argument about the original judgement, only a check of whether the condition held.

The boundary must be explicit: the record describes only trading and price behaviour that already happened and contains no future information, and later prices must never be used to backfill an earlier conclusion. The purpose is to make the reasoning checkable, not to give every day a story.

> [!tip] A Log Is Not A Narrative
> The value of a log comes from consistent, checkable fields rather than elegant prose. A record with missing fields cannot be compared or verified.

> [!warning] No Backfilling
> Rewriting an earlier label using later prices makes the record always right and therefore useless.

- Step one: fix the slicing rule and the six fields before recording.
- Step two: fill each slice as it happens, with the conclusion label last.
- Step three: give every slice an executable failure condition.
- Risk boundary: the record holds only realised data and must never backfill conclusions from future prices.

## Related Concepts

- [[volatility-surface-elasticity|Volatility Surface Elasticity: How Trading Becomes Volatility Supply]] — This lesson turns that lesson's absorption and repricing judgement into a checkable record.
- [[absorption-exhaustion-and-iceberg-orders|Absorption, Exhaustion, And Iceberg Orders]] — Absorption is one of the key trading evidences recorded.
- [[odv-10-minute-reading-routine|ODV 10-Minute Reading Routine]] — A fixed reading routine and a fixed set of log fields support each other.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- nyfed-market-liquidity
- glosten-milgrom-original
- finra-volatility
