---
title: "正态、对数正态与收益分布"
title_en: "Normal, Lognormal, And Return Distributions"
slug: "normal-lognormal-distributions"
type: lesson
level: Intermediate
order: 20
track: markets-macro-and-behavior
track_label: "市场、宏观与行为"
reading_time: "17 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/市场、宏观与行为"
  - "权限/需登录"
aliases:
  - "正态、对数正态与收益分布"
  - "Normal, Lognormal, And Return Distributions"
  - "normal-lognormal-distributions"
source_url: "https://tradinghubs.org/docs/trading-knowledge/normal-lognormal-distributions"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-market-data.ts"
generated: 2026-09-15
---

# 正态、对数正态与收益分布

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[markets-macro-and-behavior|市场、宏观与行为]]
> 上一课：[[trade-capital-flows-fx|贸易、资本流动与外汇]] ｜ 下一课：[[skewness-kurtosis-fat-tails|偏度、峰度与肥尾风险]]

**中级 · 市场、宏观与行为 · 17 分钟**

> “价格服从正态分布”和“对数收益近似正态”是完全不同的假设。先确认变量，再谈概率。

区分价格、简单收益与对数收益，理解正态和对数正态模型各自描述的变量、优点与失效边界。

### 01 / 概念边界

#### 正态变量可取任意实数，对数正态变量保持为正

正态分布由均值和标准差定义，形状对称且支持整个实数轴。若某正值变量的自然对数为正态，则原变量为对数正态；它右偏、下界为零，乘法增长可以转化为对数空间的加法。

简单收益直接比较期末与期初价格；对数收益把价格比取对数，并可在连续时间段相加。两者在小变动时接近，在大跌大涨时明显不同。

- **简单收益**

  ```latex
  R_t=\frac{S_t-S_{t-1}}{S_{t-1}}
  ```

- **对数收益**

  ```latex
  r_t=\ln\!\left(\frac{S_t}{S_{t-1}}\right)
  ```

| 对象 | 范围 / 特性 | 用途边界 |
| --- | --- | --- |
| 正态变量 | 对称，支持负无穷到正无穷 | 不适合直接保证正价格 |
| 对数正态变量 | 保持为正，通常右偏 | 仍可能低估现实尾部 |
| 经验收益 | 受状态、跳跃和聚集影响 | 必须用数据检验分布假设 |

### 02 / 机制与度量

#### 模型用可处理的分布换取简洁，但现实收益并不固定同分布

几何布朗运动假设对数价格有连续扩散，带来对数正态终值和易处理的期权公式。现实市场却存在跳跃、交易时段、波动率聚集、结构断点和价格限制；即使均值标准差匹配，尾部概率也可能不同。

正态近似的尺度依赖很强。日收益的分布不能无条件按平方根时间扩展到事件分钟或多年；序列相关、时变方差和非交易时间会破坏简单缩放。

- **几何布朗运动终值**

  ```latex
  S_T=S_0\exp\!\left((\mu-\tfrac12\sigma^2)T+\sigma\sqrt{T}Z\right)
  ```

- **小收益近似**

  ```latex
  \ln(1+R)\approx R\quad\text{when }|R|\text{ is small}
  ```

| 检查 | 目的 | 失败信号 |
| --- | --- | --- |
| 直方图 / Q-Q 图 | 观察主体与尾部 | 尾端系统偏离 |
| 滚动波动率 | 检查方差稳定性 | 明显聚集与状态切换 |
| 事件分组 | 区分普通与事件日 | 条件分布差异巨大 |

### 03 / 阅读流程

#### 从变量定义到样本外尾部逐步检验

选择分布前先写清采样频率、复权方式、交易时段与缺失值处理，否则漂亮拟合也不可复现。

- 1. 明确建模对象是价格、简单收益、对数收益还是波动率。
- 2. 固定频率、时区、复权和异常值规则。
- 3. 比较均值、标准差、偏度、峰度和经验分位，而非只看均值方差。
- 4. 把普通日、事件日和压力期分组，并在样本外检查尾部覆盖。

### 04 / 风险边界

#### 分布是条件模型，不是真实市场的永久定律

同一资产在不同制度、流动性和波动状态下可能表现出不同分布。模型拟合主体良好也不代表尾部可靠，而衍生品损益往往恰好对尾部最敏感。

- 不从“近似正态”推出极端事件可忽略。
- 不混用价格分布与收益分布。
- 不在未检验独立同分布时机械使用平方根时间。

- 分布假设决定概率、风险和理论价值的尾部形状。
- 对数空间有利于处理复利，但不消除跳跃与状态切换。
- 经验分位与压力情景应和参数模型并行使用。
- 本课不承诺任何资产服从特定分布。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Price is normally distributed and log return is approximately normal are entirely different assumptions. Identify the variable before discussing probability.

Separate prices, simple returns, and log returns, then understand which variables normal and lognormal models describe, their benefits, and their failure boundaries.

### 01 / Concept Boundary

#### A Normal Variable Spans The Real Line; A Lognormal Variable Stays Positive

A normal distribution is defined by mean and standard deviation, is symmetric, and spans the real line. If the natural logarithm of a positive variable is normal, the original variable is lognormal; it is right-skewed, bounded below by zero, and turns multiplicative growth into addition in log space.

Simple return compares ending and starting prices directly. Log return takes the log of the price ratio and is additive across consecutive periods. They are close for small moves and diverge for large gains or losses.

- **Simple return**

  ```latex
  R_t=\frac{S_t-S_{t-1}}{S_{t-1}}
  ```

- **Log return**

  ```latex
  r_t=\ln\!\left(\frac{S_t}{S_{t-1}}\right)
  ```

| Object | Range / Property | Use Boundary |
| --- | --- | --- |
| Normal variable | Symmetric over the real line | Does not preserve positive prices |
| Lognormal variable | Positive and typically right-skewed | Can still understate real tails |
| Empirical return | Affected by regimes, jumps, and clustering | Distribution must be tested from data |

### 02 / Mechanics And Measurement

#### Tractable Distributions Buy Simplicity, But Real Returns Are Not Fixed IID Draws

Geometric Brownian motion gives log price a continuous diffusion, producing lognormal terminal prices and tractable option formulas. Real markets have jumps, sessions, volatility clustering, structural breaks, and price limits; tail probabilities can differ even when mean and standard deviation match.

Normal approximation is highly horizon-dependent. A daily-return distribution cannot be unconditionally scaled by square-root time to event minutes or many years; serial dependence, time-varying variance, and nontrading hours can break simple scaling.

- **Geometric-Brownian terminal value**

  ```latex
  S_T=S_0\exp\!\left((\mu-\tfrac12\sigma^2)T+\sigma\sqrt{T}Z\right)
  ```

- **Small-return approximation**

  ```latex
  \ln(1+R)\approx R\quad\text{when }|R|\text{ is small}
  ```

| Check | Purpose | Failure Signal |
| --- | --- | --- |
| Histogram / Q-Q plot | Inspect body and tails | Systematic tail deviation |
| Rolling volatility | Check variance stability | Clustering and regime shifts |
| Event conditioning | Separate normal and event days | Large conditional differences |

### 03 / Reading Workflow

#### Test From Variable Definition To Out-Of-Sample Tails

Before selecting a distribution, document sampling frequency, adjustments, session, and missing-data handling; otherwise even a good-looking fit is not reproducible.

- 1. Specify whether the modeled object is price, simple return, log return, or volatility.
- 2. Fix frequency, timezone, adjustment, and outlier rules.
- 3. Compare mean, standard deviation, skewness, kurtosis, and empirical quantiles rather than only mean-variance.
- 4. Separate ordinary, event, and stress periods and test tail coverage out of sample.

### 04 / Risk Boundary

#### A Distribution Is A Conditional Model, Not A Permanent Market Law

The same asset can exhibit different distributions across policy, liquidity, and volatility regimes. A good fit in the body does not ensure reliable tails, while derivative P&L is often most sensitive precisely there.

- Do not infer from approximately normal that extreme events are negligible.
- Do not mix price and return distributions.
- Do not mechanically use square-root time without testing IID assumptions.

- Distribution assumptions shape tails in probability, risk, and theoretical value.
- Log space helps with compounding but does not remove jumps or regime shifts.
- Empirical quantiles and stress scenarios should accompany parametric models.
- This lesson does not claim any asset follows a particular distribution.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- nist-distributions
