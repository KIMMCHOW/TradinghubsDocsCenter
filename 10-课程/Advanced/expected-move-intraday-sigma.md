---
title: "盘中预期波动区间（±1σ）"
title_en: "The Intraday Expected Move (±1σ)"
slug: "expected-move-intraday-sigma"
type: lesson
level: Advanced
order: 97
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "盘中预期波动区间（±1σ）"
  - "The Intraday Expected Move (±1σ)"
  - "expected-move-intraday-sigma"
source_url: "https://tradinghubs.org/docs/trading-knowledge/expected-move-intraday-sigma"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 盘中预期波动区间（±1σ）

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[net-exposure-balance-metrics|净敞口平衡指标：单值重心与量级门槛]] ｜ 下一课：[[index-futures-etf-level-conversion|同一价位在不同市场：指数、ETF 与期货的换算]]

**高级 · 结构、定价与波动率 · 18 分钟**

> 「今天的预期波动区间是多少」是期权交易里最常见的问题之一。它可以被定义得非常清楚：一个由隐含波动率与剩余时间决定的标准差区间。本课把定义、计算中必要的平滑处理，以及这个区间不能回答的问题一次说清。

用平值隐含波动率与剩余时间构造 ±1 个标准差的统计区间：本课说明它的定义、平值平滑与盘中分数化时间的作用，以及为什么它既不是价格目标也不是概率承诺。

### 01 / 定义

#### 它是标准差区间，不是预测

隐含波动率以年化的一个标准差移动来表达。平值的一个 20% 隐含波动率意味着期权价格对应的年化标准差约为标的现价的 20%。把它换算到更短的剩余时间上，就是把年化标准差乘以剩余时间占一年的比例的平方根——这是标准差随时间的标准缩放关系，也是任何波动区间构造的基础。

这样得到的区间有两个边界，分别位于现价上下各一个标准差处。它描述的是「在当前波动率不变、且价格按扩散过程运动的假设下，统计上的常见范围」。它不描述方向，也不包含任何对事件的判断；价格突破边界本身不是异常，而是该分布尾部的一部分。

- **预期波动区间**

  ```latex
  \text{EM}=S\cdot\sigma_{\text{ATM}}\cdot\sqrt{\dfrac{T_{\text{frac}}}{365}}
  ```
  S 为现价，σ_ATM 为平值隐含波动率（小数形式），T_frac 为剩余时间以天计的比例部分。上下边界为 S±EM。

- **平方根时间缩放**

  ```latex
  \sigma_{T}=\sigma_{\text{annual}}\sqrt{T}
  ```
  这正是为什么缩短四分之三的剩余时间只会把区间缩小一半，而不是缩小到四分之一。

### 02 / 平滑与分数化时间

#### 平值数据需要平滑，盘中时间必须分数化

直接取单一平值执行价的隐含波动率会带来问题：报价可能尚未更新、可能停留在异常档位、也可能因为买卖价差过宽而失真。常见处理是对平值附近的三个执行价加权平均，例如平值权重最高、上下各一个执行价各占较小权重。这样做的目的是抹掉单点异常，代价是把不同执行价的偏斜结构混合了一部分，因此必须把它记录为近似而非精确。

第二个必要的处理是时间。盘中剩余时间不是整天，而是距离收盘的剩余交易时间。把它按一天的比例换算成分数化天数，可以让区间在交易时段内连续收缩，而不是整天固定不变。若不这样做，早盘与尾盘会用同一个时间输入，区间就会明显失真。

两项处理合在一起，得到的是「随行情更新、随剩余时间收缩」的动态边界。它更适合用来回答「今天相对平静还是相对剧烈」，而不是「今天会不会到某个价位」。

| 输入 | 处理方式 | 为什么必要 |
| --- | --- | --- |
| 平值隐含波动率 | 对邻近三个执行价加权平均。 | 抹掉单点报价异常，代价是混合部分偏斜。 |
| 剩余时间 | 按剩余交易时间换算为分数化天数。 | 区间在盘中连续收缩而非整天不变。 |
| 年化换算基数 | 明确写出所用天数基数。 | 不同基数会给出不同区间，必须可追溯。 |

### 03 / 失效条件

#### 它假设了什么，就会在哪里失效

这个区间建立在扩散假设上：价格连续变动、波动率在剩余时间内保持稳定、并且没有跳跃。事件驱动的跳空、突发新闻或流动性断裂都会同时违反这几条假设，此时区间的边界不再是有意义的参照。它的第二个假设是波动率不重定价：一旦市场重新定价波动率，整个区间会在价格没有移动的情况下改变宽度。

第三项限制来自分布形状本身。实际的收益分布具有肥尾，极端日出现的频率高于正态假设，因此「突破区间」在真实市场中并不罕见，也不构成对模型的反驳。把区间当作「价格应该待在里面」的规则，是把一个描述性统计量误用成约束条件。

正确的使用方式是把它当作当天的尺度参照：如果实际波幅明显小于区间，说明当天相对定价而言偏安静；如果明显大于区间，说明当天相对定价而言偏剧烈，并值得检查原因是否来自波动率重定价或事件。把它与已实现波动率、偏斜结构和事件日历一起记录，才是完整的用法。

> [!question] 不是价格目标
> 区间边界是统计量，不是订单会聚集的地方，也不是止盈位置。把它当目标价使用，等于给一个描述性数字赋予了它没有的含义。

> [!warning] 波动率重定价会直接改变区间
> 价格不动而区间变宽是正常的，因为输入是隐含波动率而不是历史波幅。记录时必须同时记录隐含波动率的取值。

- 第一步：记录现价、平值隐含波动率、剩余时间与所用年化基数。
- 第二步：标出上下边界，并确认是否使用了平值平滑与分数化时间。
- 第三步：把当日实际波幅与区间比较，并检查差异是否来自波动率重定价或事件。
- 风险边界：肥尾与跳空使突破区间正常，区间本身不构成方向或概率承诺。

## 相关概念

- [[implied-volatility-surface|隐含波动率 IV 与波动率曲面]] — 区间只取平值一点，曲面说明被省略的偏斜与期限信息。
- [[realized-vs-implied-volatility|已实现波动率与隐含波动率]] — 把区间与实际波幅比较，本质上就是已实现与隐含波动率的比较。
- [[normal-lognormal-distributions|正态、对数正态与收益分布]] — 平方根时间缩放与标准差语言来自分布假设。
- [[straddle-strangle-event-risk|Straddle、Strangle 与事件波动]] — 事件前后的波动率重定价会直接改变区间宽度。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> 'What is today's expected move' is one of the most common questions in options trading, and it can be defined precisely: a one-standard-deviation range set by implied volatility and remaining time. This lesson covers the definition, the smoothing the calculation requires, and what the range cannot answer.

Build a ±1 standard deviation statistical range from at-the-money implied volatility and remaining time: this lesson covers the definition, the role of at-the-money smoothing and fractional intraday time, and why the range is neither a price target nor a probability promise.

### 01 / Definition

#### A Standard-Deviation Range, Not A Prediction

Implied volatility is quoted as an annualised one-standard-deviation move. An at-the-money implied volatility of 20% means the option price corresponds to an annualised standard deviation of about 20% of spot. Converting that to a shorter remaining period means multiplying by the square root of the fraction of a year left - the standard square-root-of-time scaling that underlies any volatility range.

The result is a band whose edges sit one standard deviation above and below spot. It describes the statistically usual range under the assumption that current volatility persists and price follows a diffusion. It carries no direction and no view on events, and price leaving the band is not an anomaly but part of the distribution's tail.

- **Expected move**

  ```latex
  \text{EM}=S\cdot\sigma_{\text{ATM}}\cdot\sqrt{\dfrac{T_{\text{frac}}}{365}}
  ```
  S is spot, σ_ATM is at-the-money implied volatility as a decimal, and T_frac is the remaining time expressed as a fractional number of days. The band edges are S ± EM.

- **Square-root-of-time scaling**

  ```latex
  \sigma_{T}=\sigma_{\text{annual}}\sqrt{T}
  ```
  This is why cutting three quarters of the remaining time only halves the band rather than quartering it.

### 02 / Smoothing And Fractional Time

#### At-The-Money Inputs Need Smoothing And Intraday Time Must Be Fractional

Taking implied volatility from a single at-the-money strike creates problems: a quote may be stale, may sit at an anomalous level, or may be distorted by a wide spread. The usual treatment is a weighted average across the three strikes around the money, with the highest weight on the at-the-money strike and smaller weights on the strike either side. The purpose is to erase single-point anomalies; the cost is blending some of the skew structure, so the result must be recorded as an approximation rather than an exact value.

The second necessary treatment is time. Remaining intraday time is not a whole day but the trading time left until the close. Expressing it as a fractional number of days lets the band contract continuously through the session instead of staying fixed all day. Without it, the morning and the close would use the same time input and the band would be visibly wrong at both ends.

Together the two treatments produce a dynamic boundary that updates with the market and contracts as time runs out. That makes it better suited to answering 'is today calm or violent relative to what was priced' than 'will today reach a particular price'.

| Input | Treatment | Why It Is Necessary |
| --- | --- | --- |
| At-the-money implied volatility | Weighted average across three neighbouring strikes. | Removes single-point anomalies at the cost of blending some skew. |
| Remaining time | Convert remaining trading time into fractional days. | Lets the band contract during the session instead of staying fixed. |
| Annualisation base | State the day-count basis explicitly. | Different bases give different bands, so the basis must be traceable. |

### 03 / Failure Conditions

#### What It Assumes Is Where It Fails

The band rests on a diffusion assumption: continuous price movement, stable volatility over the remaining period, and no jumps. Event-driven gaps, sudden news, or a liquidity break violate several of those at once, and the band edges stop being a meaningful reference. Its second assumption is that volatility does not reprice: once the market reprices volatility, the band changes width even if price has not moved.

A third limit comes from the shape of the distribution itself. Real return distributions have fat tails, so extreme days occur more often than a normal assumption implies; price leaving the band is therefore not rare in practice and does not refute the model. Treating the band as a rule that price should stay inside mistakes a descriptive statistic for a constraint.

The right use is as a scale reference for the day: if the realised range is clearly smaller than the band, the session was quiet relative to what was priced; if clearly larger, the session was violent relative to what was priced, and it is worth checking whether volatility repricing or an event explains it. Recording it alongside realised volatility, skew, and the event calendar is the complete use.

> [!question] Not A Price Target
> The band edges are statistics, not places where orders must gather and not take-profit levels. Using them as targets gives a descriptive number a meaning it does not have.

> [!warning] Volatility Repricing Changes The Band Directly
> A band that widens while price is unchanged is normal because the input is implied volatility rather than realised range. The implied-volatility value must be recorded with it.

- Step one: record spot, at-the-money implied volatility, remaining time, and the annualisation basis used.
- Step two: mark both edges and confirm that at-the-money smoothing and fractional time were applied.
- Step three: compare the day's realised range with the band and check whether any gap comes from volatility repricing or an event.
- Risk boundary: fat tails and gaps make a break normal, and the band is neither a direction nor a probability promise.

## Related Concepts

- [[implied-volatility-surface|Implied Volatility And Volatility Surface]] — The band uses one point at the money while the surface explains the skew and term information left out.
- [[realized-vs-implied-volatility|Realized Versus Implied Volatility]] — Comparing the band with the realised range is essentially comparing realised with implied volatility.
- [[normal-lognormal-distributions|Normal, Lognormal, And Return Distributions]] — Square-root-of-time scaling and standard-deviation language come from the distributional assumptions.
- [[straddle-strangle-event-risk|Straddles, Strangles, And Event Volatility]] — Volatility repricing around events changes the band width directly.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cboe-vix-methodology
- black-scholes-original
- oic-options-basics
