---
title: "零 Gamma / Gamma Flip 边界"
title_en: "The Zero-Gamma / Gamma-Flip Boundary"
slug: "zero-gamma-flip-boundary"
type: lesson
level: Advanced
order: 93
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "零 Gamma / Gamma Flip 边界"
  - "The Zero-Gamma / Gamma-Flip Boundary"
  - "zero-gamma-flip-boundary"
source_url: "https://tradinghubs.org/docs/trading-knowledge/zero-gamma-flip-boundary"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 零 Gamma / Gamma Flip 边界

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[volatility-surface-elasticity|波动率曲面弹性：成交如何变成波动率供给]] ｜ 下一课：[[convexity-regime-liquidity-map|凸性环境地图：多头与空头凸性下的流动性差异]]

**高级 · 做市商定位与期权敞口 · 18 分钟**

> 很多图表会画出一条被称为零 Gamma 或 Gamma Flip 的线。本课先把这个概念还原成一个可检验的命题：在某个价格上，整个期权复合体的净 Gamma 敞口为零。然后再讨论为什么围绕它的常见说法超出了这个命题能支持的范围。

把零 Gamma 理解为净 Gamma 敞口改变符号的平衡价格，而不是一条支撑或压力线：本课说明它如何形成、为什么单次穿越不构成结构切换，以及它与上下方关键位聚集、时间衰减和快照迁移的关系。

### 01 / 平衡价格

#### 零 Gamma 是净敞口换号的位置，不是一个价格承诺

Gamma 衡量 Delta 随标的价格变化的速度。把每个执行价的 Gamma 按其有符号的仓位度量加权，再对所有执行价求和，就得到一条随标的价格变化的净 Gamma 曲线。这条曲线穿过零的位置就是零 Gamma：在该价格之上与之下，净敞口的符号不同，因此两个区域内对冲行为的方向性含义也不同。

这条曲线不是常数。它随标的价格移动而重算，随隐含波动率变化而改变形状，并且每个交易日都会因为新公布的未平仓量而整体移动。因此「今天的零 Gamma 在哪里」是一个带时间戳的读数，而不是一个固定的技术位。把它当成静态支撑压力，就等于假设曲线在盘中不会移动。

还要区分两种来源：一种只用隔夜确认的未平仓量计算，一种把当天的成交分类也计入。前者稳定但滞后，后者贴近当天活动但更易变化。两者给出不同数值是正常的，说明的是口径差异，而不是其中一条「算错了」。

- **净 Gamma 敞口曲线（概念式）**

  ```latex
  G(S)=\sum_{k} n_{k}\,M\,\Gamma_{k}(S)
  ```
  n_k 为执行价 k 上的有符号仓位度量，M 为合约乘数，Γ_k(S) 为该执行价的 Gamma 作为标的价格的函数。符号约定决定正负解读，而具体数值由产品模型与其价格缩放决定。

- **平衡条件**

  ```latex
  G(S^{\ast})=0
  ```
  S* 即零 Gamma 价格；在它两侧净敞口符号相反。

### 02 / 穿越与接受

#### 单次穿越不是结构切换，接受才是

零 Gamma 最容易被误用成一句话结论：价格站上它就转多，跌破它就转空。更严格的做法是把穿越与接受分开。穿越只表示价格短暂位于另一侧；接受要求价格在该侧持续成交、经受一次回踩并且回踩没有把它送回原区域。两者在图表上看起来相似，含义完全不同。

判断时至少记录三件事：穿越之后停留了多久、该侧成交量是否真正放大、以及回踩结果。三项同时支持时才值得把零 Gamma 当作已经切换的结构边界。否则它只是一次测试。

如果同一时间还有若干个执行价集中在这一带，判断的重点会从单条线转移到一条价格带：观察价格是逐层穿越、在带内来回成交，还是进入后放慢并离开。聚集越密，把它压成一个精确点位就越容易出错。

| 观察结果 | 可支持的结论 | 不支持的结论 |
| --- | --- | --- |
| 单次穿越后迅速返回原区域 | 该价位被测试且未能维持。 | 结构已经切换方向。 |
| 另一侧持续成交并经回踩保持 | 可以讨论结构边界的迁移。 | 未来方向已被确定。 |
| 多个执行价同时集中在附近 | 该区域值得提高观察优先级。 | 价格一定在此反转。 |
| 读数在盘中多次迁移 | 输入变化导致模型输出变化。 | 较早的读数仍然有效。 |

### 03 / 失效条件

#### 什么时候不该再依赖这条线

零 Gamma 建立在若干前提上：仓位度量与符号约定一致、模型对 Gamma 的估计在近端有效、并且当天的成交已经足以改变结构。当隐含波动率剧烈变化、临近到期使 Gamma 在平值附近快速集中、或数据尚未更新时，这些前提都会被削弱，读数与价格行为脱节的时间也会变长。

因此本课的结论是使用方式而非数值：把零 Gamma 当作观察顺序里的一个坐标，先确认它当前的数值与时间戳，再检查价格相对它的位置，最后用价格与成交决定这次穿越是测试还是接受。若价格与成交没有给出任何一侧的接受证据，正确的动作是把该读数降权，而不是给出方向。

> [!tip] 它是一个平衡读数
> 零 Gamma 描述净敞口换号的价位，不描述接下来的方向。它是一个位置，不是一次预测。

> [!warning] 行情与未平仓量更新不同步
> 价格与波动率是实时变化的，而清算机构的未平仓量隔夜更新。两者不同步时，读数会先动一部分，因此必须记录快照时间。

- 第一步：记录当前零 Gamma 数值、口径与快照时间。
- 第二步：标出现价在它上方还是下方，以及附近是否有多条线聚集。
- 第三步：把穿越归为测试或接受，并写明哪一项证据会推翻该归类。
- 风险边界：读数随输入迁移，较早的快照不能替代当前快照。

## 相关概念

- [[gamma-exposure-gex|GEX / vGEX：Gamma Exposure 怎么看]] — 零 Gamma 是 GEX 结构的一个方向读数，必须先理解 GEX 的边界。
- [[gamma-convexity|Gamma 与凸性：为什么买方 Long Gamma]] — 净敞口换号的机制来自 Gamma 本身的性质。
- [[market-maker-flow|做市商对冲：Delta 中性与 Gamma 再平衡]] — 上下两侧解读不同，是因为对冲方向在对冲框架中不同。
- [[delta-exposure-dex|DEX：Delta Exposure 怎么看]] — 方向暴露与净 Gamma 边界联读，才能区分位置与压力。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Many charts draw a line labelled zero gamma or gamma flip. This lesson first reduces the concept to a testable proposition: at some price, the net gamma exposure of the option complex is zero. It then examines why the common narratives around that line claim more than the proposition supports.

Read zero gamma as the balance price where net gamma exposure changes sign rather than as a support or resistance line: this lesson covers how it forms, why a single cross is not a regime change, and how it relates to level clustering, time decay, and snapshot migration.

### 01 / The Balance Price

#### Zero Gamma Is Where Net Exposure Changes Sign, Not A Price Promise

Gamma measures how quickly delta changes with the underlying. Weight each strike's gamma by its signed position measure, sum across strikes, and the result is a net gamma curve that varies with the underlying price. Where that curve crosses zero sits the zero-gamma price: above and below it the net exposure carries opposite signs, so the directional meaning of hedging behaviour differs across the two regions.

The curve is not a constant. It is recomputed as the underlying moves, it reshapes as implied volatility changes, and it shifts as a whole whenever newly published open interest arrives. 'Where is zero gamma today' is therefore a timestamped reading rather than a fixed technical level. Treating it as static support or resistance assumes the curve does not move during the session.

Two sources must also be distinguished: one computed from overnight-confirmed open interest, and one that also folds in same-day classified trading. The first is stable but lagging; the second tracks today's activity but moves more. Different values from the two are normal and signal a difference in scope, not that one of them is wrong.

- **Net gamma exposure curve (conceptual)**

  ```latex
  G(S)=\sum_{k} n_{k}\,M\,\Gamma_{k}(S)
  ```
  n_k is the signed position measure at strike k, M is the contract multiplier, and Γ_k(S) is that strike's gamma as a function of the underlying. The sign convention sets the reading, while the actual values come from the product's model and price scaling.

- **Balance condition**

  ```latex
  G(S^{\ast})=0
  ```
  S* is the zero-gamma price, and the net exposure carries opposite signs on either side of it.

### 02 / Cross And Acceptance

#### A Single Cross Is Not A Regime Change; Acceptance Is

Zero gamma is most often misused as a one-line conclusion: above it turns bullish, below it turns bearish. The stricter method separates crossing from acceptance. A cross only means price was briefly on the other side; acceptance requires price to keep trading there, survive a retest, and have that retest fail to send it back into the original region. On a chart the two look similar and mean different things.

Record at least three things: how long price stayed after the cross, whether volume actually expanded on that side, and how the retest resolved. Only when all three point the same way is it worth treating zero gamma as a switched structural boundary; otherwise it was one test.

When several strikes also cluster in the same zone, attention moves from one line to one price band: watch whether price traverses it layer by layer, trades two-way inside, or slows and leaves. The tighter the cluster, the more misleading it becomes to compress it into one exact price.

| Observation | Defensible Conclusion | Unsupported Conclusion |
| --- | --- | --- |
| Cross followed by a fast return | The level was tested and did not hold. | The structure has switched direction. |
| Sustained trading on the other side with a held retest | A shift of the structural boundary can be discussed. | The future direction has been settled. |
| Several strikes clustering nearby | The area deserves higher observation priority. | Price will certainly reverse here. |
| The reading migrates during the session | Changing inputs moved the model output. | The earlier reading is still valid. |

### 03 / Failure Conditions

#### When To Stop Relying On The Line

Zero gamma rests on assumptions: a consistent position measure and sign convention, a gamma estimate that remains informative in the near term, and enough same-day trading to have moved the structure. When implied volatility moves sharply, when expiry compresses gamma near the money, or when the data has not yet refreshed, those assumptions weaken and the reading can stay out of step with price behaviour for longer.

The conclusion is therefore about use rather than value: treat zero gamma as one coordinate in a reading order - confirm its current value and timestamp, check where price sits relative to it, then let price and volume decide whether the cross was a test or acceptance. When neither side shows acceptance evidence, the correct action is to reduce the weight of the reading rather than to pick a direction.

> [!tip] It Is A Balance Reading
> Zero gamma describes the price at which net exposure changes sign; it does not describe what follows. It is a location, not a forecast.

> [!warning] Prices And Open Interest Refresh Apart
> Prices and volatility update continuously while clearing-house open interest refreshes overnight. When the two are out of step, part of the reading moves first, so the snapshot time must be recorded.

- Step one: record the current zero-gamma value, its scope, and its snapshot time.
- Step two: mark whether price sits above or below, and whether other levels cluster nearby.
- Step three: classify the cross as a test or acceptance, and state which evidence would overturn that classification.
- Risk boundary: the reading migrates with its inputs, and an older snapshot cannot substitute for the current one.

## Related Concepts

- [[gamma-exposure-gex|GEX / vGEX: How To Read Gamma Exposure]] — Zero gamma is one directional reading of a GEX structure, so the GEX boundary must come first.
- [[gamma-convexity|Gamma And Convexity: Why Buyers Are Long Gamma]] — The mechanism behind a sign change comes from the properties of gamma itself.
- [[market-maker-flow|Market-Maker Hedging: Delta Neutrality And Gamma Rebalancing]] — The two sides read differently because hedging direction differs within the hedging framework.
- [[delta-exposure-dex|DEX: How To Read Delta Exposure]] — Reading directional exposure alongside the net-gamma boundary separates location from pressure.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- black-scholes-original
- nyu-avellaneda-stoikov
