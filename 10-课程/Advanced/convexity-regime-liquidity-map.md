---
title: "凸性环境地图：多头与空头凸性下的流动性差异"
title_en: "The Convexity Regime Map: Liquidity Under Long And Short Convexity"
slug: "convexity-regime-liquidity-map"
type: lesson
level: Advanced
order: 94
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "20 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "凸性环境地图：多头与空头凸性下的流动性差异"
  - "The Convexity Regime Map: Liquidity Under Long And Short Convexity"
  - "convexity-regime-liquidity-map"
source_url: "https://tradinghubs.org/docs/trading-knowledge/convexity-regime-liquidity-map"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 凸性环境地图：多头与空头凸性下的流动性差异

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[zero-gamma-flip-boundary|零 Gamma / Gamma Flip 边界]] ｜ 下一课：[[taker-position-walls-and-squeeze-risk|持仓两侧的不对称性：墙与挤压力]]

**高级 · 做市商定位与期权敞口 · 20 分钟**

> 同一个执行价上的凸性，在不同波动率环境里的表现并不相同。本课不讨论方向，而是讨论地形：先确认各处凸性的符号与规模，再判断当前属于哪一类波动率环境，最后把这些信息转换成「哪里可能减速、哪里可能被快速穿过」的观察顺序。

把净凸性从「方向指标」还原成「地形图」：多头凸性倾向放慢价格，空头凸性在波动率下降环境中更容易被穿越，而在波动率上升环境中角色互换；两端转换处是激励改变的位置。

### 01 / 符号含义

#### 多头凸性想要远离，空头凸性想要停留

把净凸性读成动机而不是信号，会更容易理解。持有多头凸性的一方希望价格尽量离开自己的执行价，这样才能兑现凸性收益；因此当价格靠近时，他们通常没有提供流动性的动机。持有空头凸性的一方则希望价格停留或收敛在自己的执行价附近，因为时间价值与波动率回落会替他们工作；价格靠近时，他们更愿意在两侧提供流动性。

从这个角度看，凸性阶梯更像一张地图而不是一个指标：它告诉你哪一段地形会让价格减速，哪一段地形可能被迅速穿过，以及哪些位置是两地形的分界。读它的主要目的不是判断方向，而是衡量风险集中程度和价格通过的方式。

- 多头凸性区域：价格靠近时提供流动性的动机弱，可能放慢或反复测试。
- 空头凸性区域：价格靠近时倾向提供流动性，但也可能形成拥挤的集中点。
- 两种地形的交界处是激励改变的位置，通常比单条线更值得观察。

- **净凸性（概念式）**

  ```latex
  C_{\text{net}}=\sum_{k}\left(c^{+}_{k}-c^{-}_{k}\right)
  ```
  c⁺ 与 c⁻ 分别代表执行价 k 上多头与空头凸性对应的规模，符号约定表示哪一侧在为主；具体数值由产品模型决定，本课不给出复算方式。

- **到期临近的集中效应**

  ```latex
  T\downarrow\;\Rightarrow\;\Gamma_{\text{near ATM}}\uparrow
  ```
  其他条件不变时，剩余期限缩短会让平值附近的 Gamma 更集中，凸性分布也随之变窄。

### 02 / 波动率环境

#### 波动率下降与上升，会交换这两类地形的作用

在波动率下降的环境中——多数交易日属于这一类——多头凸性区域更容易让价格减速，而空头凸性区域更容易被穿过：因为价格回落使期权价值下降，空头凸性持有者获益、不需要防御，而多头凸性持有者反而受损。波动率上升时情况相反：多头凸性区域变得容易被穿过，价格反而更容易在空头凸性区域停下来，因为此时卖方被支付更多权利金，更愿意继续持有甚至增加空头仓位。

因此判断顺序是：先看当前波动率是在上升还是在下降，再决定把哪一类区域视为减速带。如果跳过这一步而固定地认为空头凸性就是支撑、多头凸性就是压力，就会在环境反转时得到完全相反的结论。

整条阶梯的分布也有信息。分布较广的负凸性通常对应流动性充足、参与者愿意卖出期权的市场；分布较广且规模明显的正凸性，往往出现在市场对波动率有较高且较有共识的预期时，例如事件驱动波动率到来之前。单个执行价上的极端集中则属于例外情况，需要单独对待。

| 波动率环境 | 多头凸性区域 | 空头凸性区域 |
| --- | --- | --- |
| 波动率下降（常见） | 倾向减速，容易反复测试。 | 倾向被穿过，价格容易延续。 |
| 波动率上升 | 倾向被穿过，防御动机弱。 | 倾向减速，卖方被支付更多。 |
| 分布广的负凸性 | 说明市场流动性较好。 | 说明参与者乐于卖出波动率。 |
| 单一执行价极端集中 | 属于例外，需要单独确认。 | 拥挤位置的避险行为可能很快。 |

### 03 / 尾盘加速

#### 时间衰减会让效果非线性地放大

越接近到期，平值附近的 Gamma 越集中，而由时间衰减与波动率回落带来的 Delta 漂移也会加速。其结果是同一套结构在尾盘的影响可以明显大于早盘，尤其是当日到期的合约。这也是为什么当天的凸性地图必须在接近收盘时重新确认一次，而不是沿用早盘的结论。

这种加速有一个可观察的方向：当衰减带来的是被动买盘时，它吸收下行压力；当衰减带来的是被动卖盘时，它压制上行并形成下压。它同时解释了为什么当日到期的空头凸性区域在最后阶段表现得像磁铁——稳定流动性的供给把价格吸引过去，而不是当作支撑压力线使用。

使用边界仍然严格：本条描述的是流动性的倾向与时间结构，不是价格承诺。如果价格已经进入该区域并使其变成平值合约，原本提供流动性的动机就会消失；如果波动率突然上升，前述角色互换也会立即发生。任何读到极端集中位置的结论，都应该同时写下这两项失效条件。

> [!tip] 读地图，不读方向
> 凸性地图回答「哪里可能减速、哪里可能被穿过、哪里是分界」，不回答「应该做多还是做空」。把它当方向指标使用，会同时失去它最有价值的部分。

> [!warning] 极端集中是例外
> 单一执行价的极端空头凸性并不是稳定结构。拥挤位置一旦需要调整，动作往往比正常区域更快，因此不能用「稳定支撑」的方式对待它。

- 第一步：确认当前净凸性的符号与分布，标出集中区与分界位置。
- 第二步：判断波动率处于上升还是下降环境，再决定哪一侧是减速带。
- 第三步：接近尾盘时重新确认一次，比较早盘与当前的结论是否仍然成立。
- 风险边界：价格为平值、波动率跳升或数据刷新都会改变结论，必须写明失效条件。

## 相关概念

- [[gamma-convexity|Gamma 与凸性：为什么买方 Long Gamma]] — 凸性的定义与买方偏好是读地图的前提。
- [[gamma-exposure-gex|GEX / vGEX：Gamma Exposure 怎么看]] — 凸性分布是 Gamma 敞口在行权价上的展开。
- [[realized-vs-implied-volatility|已实现波动率与隐含波动率]] — 波动率上升或下降的环境判断依赖已实现与隐含波动率的比较。
- [[absorption-exhaustion-and-iceberg-orders|吸收、衰竭与冰山单]] — 价格能否穿过某区域，最终要由吸收与成交来确认。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Convexity at a strike does not behave the same way across volatility environments. This lesson is about terrain rather than direction: confirm the sign and size of convexity at each level, decide which volatility environment is in force, and turn that into an observation order for where price may slow and where it may be traversed quickly.

Restore net convexity from a direction indicator to a terrain map: long convexity tends to slow price while short convexity is far easier to traverse in a falling-volatility environment, and the roles swap when volatility rises; the transition between the two marks where incentives change.

### 01 / What The Sign Means

#### Long Convexity Wants Distance, Short Convexity Wants Rest

Reading net convexity as an incentive rather than a signal clarifies it. Those holding long convexity want price to travel away from their strikes so the convex payoff can be realised, so they generally have little reason to supply liquidity when price approaches. Those holding short convexity want price to rest near their strikes because time value and volatility compression work for them, so they are more willing to supply liquidity on both sides as price arrives.

Seen this way, a convexity ladder is closer to a map than an indicator: it shows which terrain slows price, which terrain price may cross quickly, and where the two meet. Its main purpose is not to call direction but to gauge how concentrated the risk is and how price is likely to travel through it.

- Long-convexity zones: weak incentive to supply liquidity on approach, so price may slow or retest repeatedly.
- Short-convexity zones: liquidity tends to be supplied on approach, but a crowded single strike can also build.
- Where the two terrains meet, incentives change; that transition is usually worth more attention than a single line.

- **Net convexity (conceptual)**

  ```latex
  C_{\text{net}}=\sum_{k}\left(c^{+}_{k}-c^{-}_{k}\right)
  ```
  c+ and c- are the long- and short-convexity sizes at strike k, and the sign shows which side dominates; the actual values come from the product model, which this lesson does not ask a reader to reproduce.

- **Concentration into expiry**

  ```latex
  T\downarrow\;\Rightarrow\;\Gamma_{\text{near ATM}}\uparrow
  ```
  Other things equal, shorter time to expiry concentrates gamma near the money and narrows the convexity distribution with it.

### 02 / Volatility Environment

#### Falling And Rising Volatility Swap What Each Terrain Does

In a falling-volatility environment - the common case - long-convexity zones are more likely to slow price while short-convexity zones are more likely to be traversed: falling option values reward those short convexity and need no defence from them, while those long convexity lose. Rising volatility reverses it: long-convexity zones become easier to traverse while price more readily stalls at short-convexity zones, because sellers are paid more to keep or even add to their positions.

The order of judgement therefore runs: first establish whether volatility is rising or falling, then decide which terrain is the speed bump. Skipping that step and permanently treating short convexity as support and long convexity as resistance produces exactly the wrong answer when the environment flips.

The distribution across the ladder also carries information. Broadly spread negative convexity usually corresponds to a liquid market where participants are willing to sell options; broadly spread positive convexity of meaningful size tends to appear when the market holds a well-formed expectation of elevated volatility, such as ahead of event-driven moves. Extreme concentration in one strike is the exception and has to be treated on its own.

| Volatility Environment | Long-Convexity Zone | Short-Convexity Zone |
| --- | --- | --- |
| Falling (common case) | Tends to slow price and invite repeated tests. | Tends to be traversed, letting price continue. |
| Rising | Tends to be traversed because the defence incentive is weak. | Tends to slow price because sellers are paid more. |
| Broad negative convexity | Suggests reasonably liquid markets. | Suggests participants are comfortable selling volatility. |
| Extreme single-strike concentration | An exception that needs its own confirmation. | Crowded positioning can force fast defensive action. |

### 03 / Acceleration Into The Close

#### Time Decay Amplifies The Effect Non-Linearly

Closer to expiry, gamma concentrates near the money and the delta drift generated by time decay and volatility collapse speeds up. The consequence is that the same structure can matter measurably more late in the session than in the morning, especially for same-day expiry. That is why a same-day convexity map has to be re-confirmed into the close instead of carrying a morning conclusion forward.

The acceleration has an observable direction: when decay adds passive bids it absorbs downward pressure, and when decay adds passive offers it caps upside and adds downward drag. It also explains why same-day short-convexity strikes can behave like a magnet late in the session - stabilising liquidity attracts price - rather than functioning as a support or resistance line.

The boundary remains strict: this describes a liquidity tendency and its time structure, not a price promise. If price enters the zone and turns those contracts into at-the-money positions, the incentive to supply liquidity disappears; if volatility jumps, the role swap above takes effect immediately. Any conclusion drawn from an extreme concentration should be written down together with both failure conditions.

> [!tip] Read The Map, Not A Direction
> A convexity map answers where price may slow, where it may pass through, and where the terrain changes; it does not answer whether to be long or short. Using it as a direction indicator discards the part that is actually informative.

> [!warning] Extreme Concentration Is The Exception
> Extreme short convexity at one strike is not a stable structure. When a crowded position has to adjust, the move tends to be faster than in a normal zone, so it cannot be treated as steady support.

- Step one: confirm the sign and distribution of net convexity, marking concentrations and transitions.
- Step two: decide whether volatility is rising or falling, then establish which side is the speed bump.
- Step three: re-confirm into the close and compare the current conclusion with the morning reading.
- Risk boundary: price becoming at-the-money, a volatility jump, or a data refresh can change the conclusion, so the failure conditions must be written down.

## Related Concepts

- [[gamma-convexity|Gamma And Convexity: Why Buyers Are Long Gamma]] — The definition of convexity and the long side's preference are the prerequisite for the map.
- [[gamma-exposure-gex|GEX / vGEX: How To Read Gamma Exposure]] — The convexity distribution is the gamma exposure unfolded across strikes.
- [[realized-vs-implied-volatility|Realized Versus Implied Volatility]] — Deciding whether volatility is rising or falling depends on comparing realised with implied volatility.
- [[absorption-exhaustion-and-iceberg-orders|Absorption, Exhaustion, And Iceberg Orders]] — Whether price can traverse a zone is ultimately confirmed by absorption and trading.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- finra-volatility
- nyu-avellaneda-stoikov
