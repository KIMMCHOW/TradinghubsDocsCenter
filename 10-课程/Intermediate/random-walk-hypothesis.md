---
title: "随机游走假说"
title_en: "Random Walk Hypothesis"
slug: "random-walk-hypothesis"
type: lesson
level: Intermediate
order: 23
track: markets-macro-and-behavior
track_label: "市场、宏观与行为"
reading_time: "20 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/市场、宏观与行为"
  - "权限/需登录"
aliases:
  - "随机游走假说"
  - "Random Walk Hypothesis"
  - "random-walk-hypothesis"
source_url: "https://tradinghubs.org/docs/trading-knowledge/random-walk-hypothesis"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 随机游走假说

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[markets-macro-and-behavior|市场、宏观与行为]]
> 上一课：[[efficient-market-hypothesis|有效市场假说（EMH）]] ｜ 下一课：[[market-efficiency-information-signaling|市场效率、信息不对称与信号]]

**中级 · 市场、宏观与行为 · 20 分钟**

> 随机游走最常见的误读是「价格完全无法预测」。它真正主张的是：在给定信息集下，下一期收益的条件期望接近于零，因此方向本身不提供系统性的可交易优势。

学习随机游走的三种强度表述（不相关增量、鞅、独立同分布）、Bachelier–Samuelson–Fama 的思想脉络、方差随时间线性增长的含义，以及它在真实市场中因肥尾、波动率聚集与微观结构噪声而失效的方式。

### 01 / 概念边界

#### 「不可预测」有强弱不同的三种表述

随机游走描述价格序列的一种统计性质：下一期变动与已有历史的关联很弱或不存在。学术与实务经常混用三个强度不同的表述，但它们约束的条件并不相同。

最弱的形式只要求收益序列不相关，也就是线性自相关为零；这仍然允许非线性依赖、波动率聚集与条件异方差。中间的形式要求价格近似为鞅，即给定信息集时下一期价格的条件期望等于当前价格。最强的形式要求增量独立同分布，因而连波动率的可预测性也被排除。

区分这三层很重要：实证研究通常能找到收益不相关的证据，却很难支持独立同分布。波动率聚集与厚尾正是后一层被拒绝的直接证据，而不是对随机游走整体的推翻。

> [!question] 常见误解：随机游走意味着完全没有任何交易机会
> 随机游走约束的是收益方向的条件期望，而不是风险补偿、波动率水平、执行质量或流动性结构。波动率仍然可以聚集并预测，风险溢价仍然可以被收取，做市仍然可以赚取价差。它否定的是「仅凭历史价格形态就能系统性获得方向性优势」这类主张。

| 表述强度 | 数学条件 | 仍然允许 |
| --- | --- | --- |
| 不相关增量 | 线性自相关为零 | 非线性依赖、波动率聚集、条件异方差 |
| 鞅 | 条件期望等于当前值 | 波动率随时间变化，但方向不可预测 |
| 独立同分布 | 增量相互独立且同分布 | 几乎没有；连波动率聚集也被排除 |

### 02 / 机制与度量

#### 为什么它在数学上成立，以及在什么条件下成立

Bachelier（1900）用随机过程描述投机价格，给出了最早的数学处理。Samuelson（1965）证明「被正确预期的价格随机波动」：一旦预期被纳入价格，后续变动就来自新信息，因而不可预测。Fama（1965）随后整理了股价随机游走的经验证据。

随机游走最重要的可检验含义是方差随时间的缩放关系：在独立增量假设下，h 期的方差等于单期方差的 h 倍，因此标准差按时间平方根增长。这一关系同时被用于期权定价的时间缩放，也正是方差比检验所要检验的对象。

方差比偏离 1 的方向给出具体的拒绝信息：显著大于 1 提示趋势或正相关，显著小于 1 提示均值回复或负相关。实务中这类偏离往往来自微观结构噪声、买卖价差跳动、非同步成交与流动性冲击，因此必须先排除数据口径问题，再解释为市场性质。

> [!note] 随机游走不是效率本身
> 随机游走是弱式效率最常见、最易检验的一个特例。效率命题只要求价格反映信息集，并不要求增量独立；因此随机游走被拒绝并不自动意味着市场无效，而随机游走成立也不意味着市场已经完美定价。

- **随机游走的增量形式**

  ```latex
  P_t=P_{t-1}+\varepsilon_t,\quad \varepsilon_t\sim \mathrm{iid}(0,\sigma^2)
  ```
  P_t 为价格，ε_t 为增量。独立性假设是最强的一层；若只要求 ε_t 不相关，则允许波动率聚集。

- **方差随时间线性增长**

  ```latex
  \mathrm{Var}(P_{t+h}-P_t)=h\sigma^2
  ```
  在独立增量下，h 期方差是单期方差的 h 倍，因此标准差按 √h 增长。这正是期权定价时间缩放的来源。

- **方差比统计量**

  ```latex
  VR(q)=\frac{\mathrm{Var}\left(R_t^{(q)}\right)}{q\,\mathrm{Var}\left(R_t\right)}
  ```
  R_t^{(q)} 为 q 期累计收益。VR(q)=1 与随机游走一致；偏离 1 的方向提示趋势或均值回复，但必须先排除微观结构噪声。

### 03 / 阅读流程

#### 把「不可预测」写成可检验的假设与可证伪的条件

在使用随机游走作为基准之前，先说明三件事：使用哪一层强度（不相关、鞅、独立同分布）、检验的是收益还是价格、以及数据是否经过复权与去噪声处理。缺少任何一项，结论都无法比较。

对交易的含义不是「不能做方向」，而是方向优势必须来自方向之外：风险补偿、波动率、流动性与执行。这也是为什么多数被记录的边缘出现在波动率、期限结构、价差与成本端，而不是单纯的方向预测。

> [!tip] 本课的核心结论
> 随机游走检验的是「方向能否被既有信息预测」。它同时允许波动率可预测、风险溢价存在、以及由执行与流动性创造收益。把这三件事分开，本课才有可操作的意义。

- 1. 明确强度：只声明收益不相关，还是同时声明波动率不可预测？两者的证据要求完全不同。
- 2. 选择检验对象：收益自相关、方差比、游程检验还是分布拟合；不同检验拒绝的是不同层次。
- 3. 先排除微观结构噪声：买卖价差跳动、非同步成交与非交易时段会人为制造负自相关。
- 4. 记录样本外与扣除成本后的结果：样本内显著不等于扣除成本后仍然可交易。

### 04 / 风险边界

#### 它在哪些地方失效，以及失效后应当怎样表述

真实收益序列在多个方面偏离独立同分布：尾部比正态更厚，波动率成簇出现，且波动率本身具有可预测性。Engle（1982）的 ARCH 框架正是为刻画条件异方差而提出，这直接否定了「连波动率都不可预测」的最强形式。

Shiller（1981）关于过度波动的论证与后续的动量、漂移研究说明，价格可能在一段时间内偏离基本价值。但这些结果也必须面对同一套约束：它们可能来自风险补偿、度量方法或数据挖掘。Malkiel（2003）因此指出，部分异象在公开后减弱或消失，这并不构成对随机游走的完全否定。

- 厚尾：极端日收益的出现频率明显高于正态假设，尾部风险必须单独建模。
- 波动率聚集：高波动与低波动成簇出现，使波动率可预测而方向仍然难以预测。
- 微观结构噪声：价差跳动与非同步成交会在高频数据中制造虚假的自相关结构。
- 非平稳性：制度变化、波动率水平迁移与参与者结构改变会让「同分布」假设失效。

- 先声明检验的层次，再报告结果；不要把「收益不相关」写成「市场完全不可预测」。
- 在检验高频数据前先处理价差跳动与非同步成交，否则结论可能只是度量产物。
- 把方向、波动率、流动性与执行分开评估，因为它们各自的可预测性并不相同。
- 任何基于「价格可预测」的策略都必须报告扣除成本与滑点后的结果与容量上限。

## 相关概念

- [[efficient-market-hypothesis|有效市场假说（EMH）]] — 随机游走是弱式效率最常见的可检验形式，但效率命题本身比随机游走更宽。
- [[market-efficiency-information-signaling|市场效率、信息不对称与信号]] — 不可预测性如何与信息成本、噪声和信号可信度共存。
- [[price-discovery-market-clearing|价格发现与市场出清]] — 随机性描述统计性质，价格发现解释这些变动由哪些边际订单产生。
- [[normal-lognormal-distributions|正态、对数正态与收益分布]] — 随机游走的分布假设与真实收益的肥尾、波动率聚集之间的差距。
- [[volatility-forecasting|波动率预测：从实现方差到样本外条件预测]] — 方向不可预测不等于波动率不可预测：可预测的是二阶矩而非收益率本身。
- [[time-value-and-theta|时间价值与 Theta]] — 在随机游走下，方向期望为零，期权持仓的确定性损耗来自时间价值。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> The common misreading of a random walk is that prices are completely unpredictable. What it actually claims is that, given an information set, the conditional expectation of the next return is close to zero, so direction alone offers no systematic tradable advantage.

Study the three strengths of the random walk (uncorrelated increments, martingale, i.i.d.), the Bachelier–Samuelson–Fama lineage, what variance scaling with time implies, and how it fails in real markets through fat tails, volatility clustering, and microstructure noise.

### 01 / Concept Boundary

#### Unpredictability Comes In Three Strengths

A random walk describes a statistical property of a price series: the next change has little or no relationship to the past. Academic and practitioner usage often conflates three statements of different strength, and they do not impose the same conditions.

The weakest form requires only that returns be uncorrelated, that is, zero linear autocorrelation; that still permits nonlinear dependence, volatility clustering, and conditional heteroskedasticity. The middle form requires price to be approximately a martingale, meaning the conditional expectation of the next price given the information set equals the current price. The strongest form requires independent and identically distributed increments, which rules out even predictability of volatility.

Keeping these layers apart matters: empirical work can usually find evidence of uncorrelated returns but rarely supports i.i.d. increments. Volatility clustering and fat tails are direct evidence against that stronger layer, not a refutation of the whole idea.

> [!question] Common Misconception: A Random Walk Means There Is No Trading Opportunity
> A random walk constrains the conditional expectation of return direction, not risk compensation, volatility level, execution quality, or liquidity structure. Volatility can still cluster and be forecast, risk premia can still be earned, and market making can still capture spread. What it denies is the claim that historical price patterns alone deliver a systematic directional advantage.

| Strength | Mathematical Condition | Still Permits |
| --- | --- | --- |
| Uncorrelated increments | Zero linear autocorrelation | Nonlinear dependence, volatility clustering, conditional heteroskedasticity |
| Martingale | Conditional expectation equals the current value | Time-varying volatility while direction stays unpredictable |
| Independent and identically distributed | Increments are independent and identically distributed | Almost nothing; even volatility clustering is excluded |

### 02 / Mechanics And Measurement

#### Why It Holds Mathematically, And Under What Conditions

Bachelier (1900) described speculative prices with a random process, the earliest mathematical treatment. Samuelson (1965) proved that properly anticipated prices fluctuate randomly: once expectations are priced, later changes come from new information and are unpredictable. Fama (1965) then organized the empirical evidence on random-walk behaviour in stock prices.

The most important testable implication is variance scaling: under independent increments, the variance over h periods is h times the single-period variance, so standard deviation grows with the square root of time. The same relation underpins time scaling in option pricing and is exactly what a variance-ratio test examines.

The direction of the deviation from a variance ratio of one carries specific information: significantly above one suggests trending or positive autocorrelation, significantly below one suggests mean reversion or negative autocorrelation. In practice such deviations often come from microstructure noise, bid-ask bounce, asynchronous trading, and liquidity shocks, so data conventions must be ruled out before reading them as market behaviour.

> [!note] A Random Walk Is Not Efficiency Itself
> A random walk is the most common and most easily tested special case of weak-form efficiency. The efficiency proposition requires only that prices reflect an information set and does not require independent increments, so rejecting a random walk does not automatically mean inefficiency, and accepting one does not mean prices are perfectly set.

- **Increment form of a random walk**

  ```latex
  P_t=P_{t-1}+\varepsilon_t,\quad \varepsilon_t\sim \mathrm{iid}(0,\sigma^2)
  ```
  P_t is the price and ε_t the increment. Independence is the strongest layer; requiring only uncorrelated ε_t still permits volatility clustering.

- **Variance scales with time**

  ```latex
  \mathrm{Var}(P_{t+h}-P_t)=h\sigma^2
  ```
  Under independent increments the h-period variance is h times the single-period variance, so the standard deviation grows with the square root of h. This is the origin of time scaling in option pricing.

- **Variance-ratio statistic**

  ```latex
  VR(q)=\frac{\mathrm{Var}\left(R_t^{(q)}\right)}{q\,\mathrm{Var}\left(R_t\right)}
  ```
  R_t^{(q)} is the q-period cumulative return. A value of one is consistent with a random walk; deviations indicate trending or mean reversion, but microstructure noise must be excluded first.

### 03 / Reading Workflow

#### Write Unpredictability As A Testable Hypothesis And A Falsifier

Before using a random walk as a baseline, state three things: which layer of strength is meant (uncorrelated, martingale, i.i.d.), whether returns or prices are being tested, and whether the data has been adjusted and cleaned of microstructure noise. Without all three, results cannot be compared.

The trading implication is not that direction is impossible but that a directional edge must come from something other than direction: risk compensation, volatility, liquidity, and execution. That is why most documented edges appear in volatility, term structure, spread, and cost rather than in direction forecasting alone.

> [!tip] The Central Takeaway Of This Lesson
> A random walk tests whether direction can be predicted from existing information. It simultaneously allows forecastable volatility, existing risk premia, and returns created by execution and liquidity provision. Keeping those three apart is what makes the hypothesis usable.

- 1. Fix the strength: only uncorrelated returns, or also unpredictable volatility? The two need very different evidence.
- 2. Choose the test: return autocorrelation, variance ratio, runs test, or distribution fit; each rejects a different layer.
- 3. Rule out microstructure noise first: bid-ask bounce, asynchronous trading, and non-trading hours can manufacture negative autocorrelation.
- 4. Record out-of-sample and after-cost results: in-sample significance is not the same as tradability after cost.

### 04 / Risk Boundary

#### Where It Fails, And How To State The Failure

Real return series depart from i.i.d. in several ways: tails are fatter than normal, volatility clusters, and volatility itself is forecastable. Engle's (1982) ARCH framework was introduced precisely to model conditional heteroskedasticity, which directly rejects the strongest claim that even volatility is unpredictable.

Shiller's (1981) excess-volatility argument and the later momentum and drift literature show that price can depart from fundamental value for a period. Those results still face the same constraints: they may come from risk compensation, measurement choices, or data mining. Malkiel (2003) therefore noted that some anomalies weaken or disappear once public, which is not a complete refutation of the random walk.

- Fat tails: extreme daily returns occur far more often than a normal assumption implies, so tail risk needs its own model.
- Volatility clustering: high- and low-volatility periods come in clusters, making volatility forecastable while direction stays difficult.
- Microstructure noise: bid-ask bounce and asynchronous trading create spurious autocorrelation in high-frequency data.
- Non-stationarity: regime change, volatility-level shifts, and participant-structure change break the identical-distribution assumption.

- State the layer being tested before reporting a result; never turn uncorrelated returns into fully unpredictable markets.
- Clean bid-ask bounce and asynchronous trading before testing high-frequency data, or the conclusion may be a measurement artefact.
- Evaluate direction, volatility, liquidity, and execution separately, because their predictability differs.
- Any strategy based on predictable prices must report results and capacity limits after cost and slippage.

## Related Concepts

- [[efficient-market-hypothesis|Efficient Market Hypothesis (EMH)]] — The random walk is the most common testable form of weak-form efficiency, while the efficiency proposition is broader.
- [[market-efficiency-information-signaling|Market Efficiency, Information Asymmetry, And Signals]] — How unpredictability coexists with information cost, noise, and signal credibility.
- [[price-discovery-market-clearing|Price Discovery And Market Clearing]] — Randomness describes the statistical property; price discovery explains which marginal orders produced the moves.
- [[normal-lognormal-distributions|Normal, Lognormal, And Return Distributions]] — The gap between the random walk's distributional assumption and the fat tails and volatility clustering of real returns.
- [[volatility-forecasting|Volatility Forecasting: From Realized Variance To Out-Of-Sample Conditional Forecasts]] — Unpredictable direction does not mean unpredictable volatility: the second moment is forecastable even when returns are not.
- [[time-value-and-theta|Time Value And Theta]] — Under a random walk the directional expectation is zero, so a long option's deterministic cost is time decay.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- bachelier-1900-theorie-speculation
- samuelson-1965-anticipated-prices
- fama-1965-random-walks
- fama-1970-efficient-capital-markets
- engle-arch-original
- nist-distributions
- shiller-1981-excess-volatility
- malkiel-2003-efficient-market-hypothesis-critics
