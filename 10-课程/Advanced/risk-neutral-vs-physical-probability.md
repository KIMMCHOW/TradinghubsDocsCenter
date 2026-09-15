---
title: "风险中性概率与现实概率：定价分布不是行情预测"
title_en: "Risk-Neutral Versus Physical Probability: A Pricing Distribution Is Not A Forecast"
slug: "risk-neutral-vs-physical-probability"
type: lesson
level: Advanced
order: 55
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "24 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "风险中性概率与现实概率：定价分布不是行情预测"
  - "Risk-Neutral Versus Physical Probability: A Pricing Distribution Is Not A Forecast"
  - "risk-neutral-vs-physical-probability"
source_url: "https://tradinghubs.org/docs/trading-knowledge/risk-neutral-vs-physical-probability"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# 风险中性概率与现实概率：定价分布不是行情预测

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[forwards-futures-basis-cost-of-carry|远期、期货、基差与持有成本：从现货到股指公平价值]] ｜ 下一课：[[model-assumptions-and-model-risk|模型假设与模型风险：从公式正确到决策可靠]]

**高级 · 结构、定价与波动率 · 24 分钟**

> 期权价格可以反推出市场用于定价的风险中性分布，但它把状态发生概率与投资者对该状态的定价权重混合在一起。风险中性尾部更重，不必意味着市场认为现实尾部概率同样高。

区分现实测度 P 下的预测与风险中性测度 Q 下的无套利定价，理解期权隐含分布、风险溢价和风险中性方差的正确解释。

### 01 / 概念边界

#### P 回答会发生什么，Q 回答无套利价格如何加权

现实测度 P 描述研究者对未来路径的统计信念，包含风险资产的预期风险溢价。对支付股息的资产，无套利风险中性测度 Q 使正确贴现的累计收益（含股息）过程成为鞅；单独把除息价格 e^{-rt}S_t 贴现并不满足这一表述。

两种测度可以使用相同的瞬时波动率，却具有不同漂移与尾部权重。Q 不是“投资者没有风险厌恶”的现实陈述，而是把风险价格吸收到概率权重中的数学表示。

- **现实与风险中性动态的简化对照**

  ```latex
  \frac{dS_t}{S_t}=(\mu-q)dt+\sigma dW_t^{P},\qquad \frac{dS_t}{S_t}=(r-q)dt+\sigma dW_t^{Q}
  ```
  这里 μ 是含连续股息的总预期收益率，q 是连续股息率；因此除息价格在 P 下的资本利得漂移为 μ-q。

- **常数利率与股息率下的贴现累计收益过程**

  ```latex
  \widetilde G_t=e^{-rt}S_t+\int_0^t e^{-ru}qS_u\,du
  ```
  在简化的常数 r、q 框架与相应技术条件下，上式的贴现累计收益过程而不是单独的贴现除息价格是 Q 下的鞅。

### 02 / 机制与度量

#### 衍生品价格是 Q 期望的贴现值，而不是 P 下平均收益

在简化的完备无套利框架中，到期支付 H(S_T) 的价值是 Q 下期望支付的贴现值。现实测度下的期望支付可以不同，因为它没有自动包含状态价格与风险补偿。

期权横截面可用于推断风险中性密度或风险中性方差，但需要无套利插值、远期与贴现输入，并承受报价噪声和尾部外推。风险中性方差反映期权价格中的方差交换水平；它不是对未来实际方差的无偏物理预测。

- **风险中性定价关系**

  ```latex
  V_t=e^{-r\tau}\,\mathbb{E}^{Q}\!\left[H(S_T)\mid\mathcal{F}_t\right]
  ```

- **方差风险溢价的一种研究约定**

  ```latex
  \operatorname{VRP}_{t,T}=\mathbb{E}^{Q}_t[\operatorname{RV}_{t,T}]-\mathbb{E}^{P}_t[\operatorname{RV}_{t,T}]
  ```
  有些资料采用相反符号，比较前必须确认。

| 维度 | 现实测度 P | 风险中性测度 Q |
| --- | --- | --- |
| 主要用途 | 预测、情景频率、资本规划 | 无套利定价与隐含状态价格 |
| 风险溢价 | 进入预期收益与转移动态 | 吸收到定价权重 |
| 校验 | 样本外预测与实现数据 | 期权横截面与无套利约束 |

### 03 / 阅读流程

#### 分别构建定价视图与预测视图，再研究差异

一个稳健流程不会把隐含波动率直接贴成预测标签。先从同步期权、远期、利率与股息构造 Q 下分布或方差，再用独立的时间序列、状态变量和样本外规则构造 P 下预测，最后才计算风险溢价与分歧。

- 写明问题是定价、对冲还是现实概率预测。
- 对 Q 视图同步期权、远期、贴现、股息与到期时间。
- 对 P 视图冻结训练窗口、特征、预测期限和样本外评估。
- 将方差、波动率和百分比单位统一后再计算差异。
- 同时展示 Q、P、实现结果和置信区间，不把差异自动解释成方向信号。

### 04 / 风险边界

#### Q 不是真实概率，P 也不是可直接交易的真相

风险中性分布受流动性、供需、尾部保护需求与模型插值影响。现实预测则受结构变化、有限样本和特征选择影响。两者差异既可能是风险溢价，也可能包含数据、期限和模型误差。

风险中性方差通常高于某些物理预测，并不意味着卖出波动率是无风险收益。实现方差可以跳升，期权组合还承受偏斜、跳跃、流动性、保证金和离散对冲误差。

- 遇到“隐含概率”时先确认它来自 Q 还是 P。
- 比较方差前统一期限、年化、方差与波动率单位。
- 把 Q-P 差异拆成风险溢价、报价噪声与模型误差候选。
- 该框架解释定价与预测差异，不构成波动率交易建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Option prices can imply a risk-neutral distribution used for valuation, but that distribution combines state likelihood with how investors price each state. A heavier risk-neutral tail does not necessarily mean the market assigns the same physical probability to that tail.

Separate forecasting under the physical measure P from no-arbitrage pricing under the risk-neutral measure Q, and interpret option-implied distributions, risk premia, and risk-neutral variance correctly.

### 01 / Concept Boundary

#### P Asks What May Happen; Q Weights No-Arbitrage Prices

The physical measure P describes statistical beliefs about future paths and includes expected risk premia on risky assets. For a dividend-paying asset, a no-arbitrage risk-neutral measure Q makes the properly discounted cumulative-gains process, including dividends, a martingale; the discounted ex-dividend price e^{-rt}S_t alone does not satisfy that statement.

The two measures can share instantaneous volatility while carrying different drift and tail weights. Q is not a real-world claim that investors are risk-neutral; it is a mathematical representation that absorbs the price of risk into probability weights.

- **Simplified Physical And Risk-Neutral Dynamics**

  ```latex
  \frac{dS_t}{S_t}=(\mu-q)dt+\sigma dW_t^{P},\qquad \frac{dS_t}{S_t}=(r-q)dt+\sigma dW_t^{Q}
  ```
  Here mu is the total expected return including continuous dividends and q is the continuous dividend yield, so the ex-dividend capital-gain drift under P is mu minus q.

- **Discounted Cumulative-Gains Process With Constant Rates**

  ```latex
  \widetilde G_t=e^{-rt}S_t+\int_0^t e^{-ru}qS_u\,du
  ```
  In the simplified constant-r and constant-q setting, subject to the usual technical conditions, the discounted cumulative-gains process above, rather than the discounted ex-dividend price alone, is the Q-martingale.

### 02 / Mechanics And Measurement

#### A Derivative Price Is A Discounted Q Expectation, Not A P Forecast

In a simplified complete no-arbitrage setting, the value of terminal payoff H(S_T) is its discounted expectation under Q. The expected payoff under P can differ because it does not automatically include state prices and risk compensation.

An option cross-section can be used to infer a risk-neutral density or risk-neutral variance, subject to no-arbitrage interpolation, forward and discount inputs, quote noise, and tail extrapolation. Risk-neutral variance reflects the variance-exchange level embedded in option prices; it is not an unbiased physical forecast of future realized variance.

- **Risk-Neutral Valuation**

  ```latex
  V_t=e^{-r\tau}\,\mathbb{E}^{Q}\!\left[H(S_T)\mid\mathcal{F}_t\right]
  ```

- **One Research Convention For Variance Risk Premium**

  ```latex
  \operatorname{VRP}_{t,T}=\mathbb{E}^{Q}_t[\operatorname{RV}_{t,T}]-\mathbb{E}^{P}_t[\operatorname{RV}_{t,T}]
  ```
  Some references use the opposite sign; verify before comparing.

| Dimension | Physical Measure P | Risk-Neutral Measure Q |
| --- | --- | --- |
| Primary use | Forecasting, scenario frequency, capital planning | No-arbitrage valuation and implied state prices |
| Risk premium | Appears in expected return and transitions | Absorbed into pricing weights |
| Validation | Out-of-sample forecasts and realizations | Option cross-section and no-arbitrage constraints |

### 03 / Reading Workflow

#### Build Pricing And Forecast Views Separately Before Comparing Them

A robust process does not relabel implied volatility as a forecast. First construct a Q distribution or variance from synchronized options, forward, rates, and dividends; separately build a P forecast from time series, state variables, and out-of-sample rules; only then calculate risk premia and divergence.

- State whether the question concerns valuation, hedging, or physical forecasting.
- Synchronize options, forward, discounting, dividends, and expiry for the Q view.
- Freeze training window, features, forecast horizon, and out-of-sample evaluation for the P view.
- Align variance, volatility, and percentage units before calculating differences.
- Show Q, P, realization, and uncertainty together without turning their difference automatically into a directional signal.

### 04 / Risk Boundary

#### Q Is Not Real-World Probability, And P Is Not A Tradable Truth

The risk-neutral distribution is influenced by liquidity, supply and demand, tail-protection demand, and model interpolation. Physical forecasts face regime change, finite samples, and feature selection. Their difference can contain both risk premium and data, horizon, or model error.

Risk-neutral variance being above a physical forecast does not make short volatility a risk-free return. Realized variance can jump, while an options portfolio also bears skew, jump, liquidity, margin, and discrete-hedging error.

- For any implied probability, first determine whether it belongs to Q or P.
- Align horizon, annualization, variance, and volatility units before comparison.
- Decompose a Q-P gap into risk-premium, quote-noise, and model-error candidates.
- The framework explains valuation-versus-forecast differences and is not volatility-trading advice.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- schweizer-martingale-gains
- black-scholes-original
- occ-options-disclosure
- finra-volatility
- cboe-vix
- nist-distributions
