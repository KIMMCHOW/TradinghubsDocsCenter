---
title: "波动率预测：从实现方差到样本外条件预测"
title_en: "Volatility Forecasting: From Realized Variance To Out-Of-Sample Conditional Forecasts"
slug: "volatility-forecasting"
type: lesson
level: Advanced
order: 61
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "25 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "波动率预测：从实现方差到样本外条件预测"
  - "Volatility Forecasting: From Realized Variance To Out-Of-Sample Conditional Forecasts"
  - "volatility-forecasting"
source_url: "https://tradinghubs.org/docs/trading-knowledge/volatility-forecasting"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# 波动率预测：从实现方差到样本外条件预测

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[bsm-pricing-model|Black-Scholes-Merton Pricing Model]] ｜ 下一课：[[variance-swaps-and-vix|方差互换与 VIX：从期权横截面到风险中性方差]]

**高级 · 结构、定价与波动率 · 25 分钟**

> 波动率预测不是选一个历史窗口后开平方。它需要明确收益频率、预测起点、目标期限、信息集、方差代理和样本外损失函数，并承认波动率聚类、跳跃与结构变化会让参数持续漂移。

构建滚动、EWMA 与 GARCH 型物理波动率预测，正确聚合期限、评估样本外误差，并与风险中性隐含方差保持概念分离。

### 01 / 概念边界

#### 预测对象是未来条件方差，而不是一个无期限的波动率数字

对收益 r_t，先定义条件均值 μ_{t+1|t}=E_t^P[r_{t+1}] 与创新 ε_{t+1}=r_{t+1}-μ_{t+1|t}，再把单期条件方差写成 E_t^P[ε_{t+1}²]。物理测度 P 表示基于时点 t 可得信息对未来实现路径的预测；必须说明预测的是下一期、未来 h 期累计方差还是固定日历期限。

实现方差只是潜在方差的有噪声代理。低频平方收益噪声很大，高频数据又受到微观结构、交易时段和跳跃处理影响。训练与评估必须使用一致的实现方差定义。

- **条件均值、创新与单期条件方差**

  ```latex
  \mu_{t+1|t}=\mathbb{E}_t^P[r_{t+1}],\qquad \varepsilon_{t+1}=r_{t+1}-\mu_{t+1|t},\qquad \sigma_{t+1|t}^2=\mathbb{E}_t^P[\varepsilon_{t+1}^2]
  ```

- **年化样本波动率**

  ```latex
  \widehat{\sigma}_{\mathrm{ann}}=\sqrt{m\,\frac{1}{n-1}\sum_{t=1}^{n}(r_t-\bar r)^2}
  ```

### 02 / 机制与度量

#### 滚动、EWMA 与 GARCH 对记忆结构作出不同假设

滚动方差对窗口内观测等权并在越过窗口时突然遗忘；EWMA 用 λ 控制指数衰减，λ 越高记忆越长；GARCH(1,1) 通过常数项、近期冲击与上一期条件方差描述均值回归。参数必须满足非负与稳定性约束，并在样本外冻结。

若条件收益不相关，未来 h 期累计方差可近似为各期条件方差之和；存在可预测相关性时还要加入协方差。累计方差开平方后才是期限波动率，不能把单期波动率直接相加。

- **EWMA 方差更新**

  ```latex
  \widehat{\sigma}_{t+1|t}^{2}=\lambda\widehat{\sigma}_{t|t-1}^{2}+(1-\lambda)\varepsilon_t^2,\qquad 0<\lambda<1
  ```
  ε_t=r_t-μ_{t|t-1}。RiskMetrics 常见的零条件均值特例令 μ_{t|t-1}=0，此时 ε_t²=r_t²。

- **GARCH(1,1) 条件方差**

  ```latex
  \sigma_{t+1}^{2}=\omega+\alpha\varepsilon_t^2+\beta\sigma_t^2,\qquad \omega>0,\ \alpha,\beta\ge0,\ \alpha+\beta<1
  ```

- **多期条件方差聚合**

  ```latex
  \operatorname{Var}_t\!\left(\sum_{j=1}^{h}r_{t+j}\right)=\sum_{j=1}^{h}\operatorname{Var}_t(r_{t+j})+2\sum_{i<j}\operatorname{Cov}_t(r_{t+i},r_{t+j})
  ```

### 03 / 阅读流程

#### 使用滚动预测原点做真正的样本外评估

每个预测原点只能使用当时可获得的数据。训练窗口、重估频率、超参数搜索和实现方差目标应在回测前固定，并与简单基准比较；否则未来信息和重复调参会产生虚假精度。

- 定义收益时段、时区、隔夜处理、预测期限和实现方差目标。
- 建立滚动方差等简单基准，再加入 EWMA 或 GARCH 型模型。
- 在每个预测原点只使用过去数据，并记录参数重估日期。
- 同时评估方差损失、波动率误差、区间覆盖率和压力状态表现。
- 按状态、期限和流动性分组比较，并保留模型组合与降级规则。

- **方差预测的 QLIKE 损失**

  ```latex
  \operatorname{QLIKE}_t=\log(\widehat{\sigma}_t^2)+\frac{\operatorname{RV}_t}{\widehat{\sigma}_t^2}
  ```
  该写法省略了只依赖已实现代理、与候选预测无关的常数项，并要求预测方差严格为正。

### 04 / 风险边界

#### 隐含方差是风险中性价格，不是物理预测的替代品

期权隐含方差来自 Q 下定价，包含方差风险溢价、尾部保护需求和市场摩擦；时间序列模型试图预测 P 下实现方差。两者可以作为不同信息源比较，但不能把隐含波动率直接当作无偏实现波动率预测。

任何平稳模型都可能在制度变化、跳跃和流动性危机中失效。低预测误差也不等于交易获利，因为期权损益还取决于风险溢价、偏斜、路径、对冲和成本。

- 比较预测前统一物理或风险中性测度、期限和单位。
- 模型突然落后时检查状态变化、数据修订和参数漂移。
- 压力期单独报告误差，不让平静期的大样本稀释失败。
- 预测用于风险规划，不保证波动率交易或方向收益。

## 相关概念

- [[realized-vs-implied-volatility|已实现波动率与隐含波动率]] — 预测未来波动是判断隐含波动率是否偏贵的基础。
- [[skewness-kurtosis-fat-tails|偏度、峰度与肥尾风险]] — 波动率聚集与厚尾要求模型刻画二阶矩的时间结构。
- [[model-assumptions-and-model-risk|模型假设与模型风险：从公式正确到决策可靠]] — 波动率模型的参数本身并不稳定，参数风险必须显式处理。
- [[variance-swaps-and-vix|方差互换与 VIX：从期权横截面到风险中性方差]] — 方差互换与 VIX 把波动率预测变成了可交易标的。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Volatility forecasting is not merely choosing a historical window and taking a square root. It requires a return frequency, forecast origin, target horizon, information set, variance proxy, and out-of-sample loss function while recognizing clustering, jumps, and structural change.

Build rolling, EWMA, and GARCH-style physical volatility forecasts, aggregate horizons correctly, evaluate out of sample, and keep them conceptually separate from risk-neutral implied variance.

### 01 / Concept Boundary

#### The Target Is Future Conditional Variance, Not A Horizon-Free Number

For return r_t, first define the conditional mean mu_{t+1|t}=E_t^P[r_{t+1}] and innovation epsilon_{t+1}=r_{t+1}-mu_{t+1|t}, then write one-period conditional variance as E_t^P[epsilon_{t+1} squared]. The physical measure P represents a forecast of future realized paths using information available at t; the target must state next-period, cumulative h-period variance, or a fixed calendar horizon.

Realized variance is a noisy proxy for latent variance. Low-frequency squared returns are noisy, while high-frequency data introduce microstructure, session, and jump-treatment choices. Training and evaluation must use the same realized-variance definition.

- **Conditional Mean, Innovation, And One-Period Variance**

  ```latex
  \mu_{t+1|t}=\mathbb{E}_t^P[r_{t+1}],\qquad \varepsilon_{t+1}=r_{t+1}-\mu_{t+1|t},\qquad \sigma_{t+1|t}^2=\mathbb{E}_t^P[\varepsilon_{t+1}^2]
  ```

- **Annualized Sample Volatility**

  ```latex
  \widehat{\sigma}_{\mathrm{ann}}=\sqrt{m\,\frac{1}{n-1}\sum_{t=1}^{n}(r_t-\bar r)^2}
  ```

### 02 / Mechanics And Measurement

#### Rolling, EWMA, And GARCH Impose Different Memory

Rolling variance equally weights observations inside a window and forgets them abruptly at the edge. EWMA uses lambda for exponential decay, with larger lambda retaining longer memory. GARCH(1,1) combines a constant, recent shock, and prior conditional variance to represent mean reversion. Parameters need nonnegativity and stability constraints and must be frozen out of sample.

If conditional returns are uncorrelated, cumulative h-period variance is approximately the sum of period conditional variances; predictable dependence requires covariance terms as well. Take the square root of cumulative variance to obtain horizon volatility; never add period volatilities directly.

- **EWMA Variance Update**

  ```latex
  \widehat{\sigma}_{t+1|t}^{2}=\lambda\widehat{\sigma}_{t|t-1}^{2}+(1-\lambda)\varepsilon_t^2,\qquad 0<\lambda<1
  ```
  Here epsilon_t=r_t-mu_{t|t-1}. In the common RiskMetrics zero-conditional-mean special case, mu_{t|t-1}=0 and epsilon_t squared equals r_t squared.

- **GARCH(1,1) Conditional Variance**

  ```latex
  \sigma_{t+1}^{2}=\omega+\alpha\varepsilon_t^2+\beta\sigma_t^2,\qquad \omega>0,\ \alpha,\beta\ge0,\ \alpha+\beta<1
  ```

- **Multi-Period Conditional Variance Aggregation**

  ```latex
  \operatorname{Var}_t\!\left(\sum_{j=1}^{h}r_{t+j}\right)=\sum_{j=1}^{h}\operatorname{Var}_t(r_{t+j})+2\sum_{i<j}\operatorname{Cov}_t(r_{t+i},r_{t+j})
  ```

### 03 / Reading Workflow

#### Use Rolling Forecast Origins For Genuine Out-Of-Sample Evaluation

Each forecast origin may use only information available at that time. Training window, refit frequency, hyperparameter search, and realized-variance target should be frozen before backtesting and compared with simple baselines, or future information and repeated tuning will create false accuracy.

- Define return session, timezone, overnight treatment, forecast horizon, and realized-variance target.
- Establish a rolling-variance baseline before adding EWMA or GARCH-style models.
- At each forecast origin, use past data only and record parameter-refit dates.
- Evaluate variance loss, volatility error, interval coverage, and stress-regime behavior together.
- Compare by regime, horizon, and liquidity, retaining model-combination and fallback rules.

- **QLIKE Loss For Variance Forecasts**

  ```latex
  \operatorname{QLIKE}_t=\log(\widehat{\sigma}_t^2)+\frac{\operatorname{RV}_t}{\widehat{\sigma}_t^2}
  ```
  This form omits terms that depend only on the realized proxy and not on the competing forecast, and it requires a strictly positive variance forecast.

### 04 / Risk Boundary

#### Implied Variance Is A Risk-Neutral Price, Not A Substitute For A Physical Forecast

Option-implied variance comes from Q pricing and includes variance risk premia, tail-protection demand, and market frictions; a time-series model seeks realized variance under P. They may be compared as distinct information sources, but implied volatility cannot simply be treated as an unbiased realized-volatility forecast.

Any stationary model can fail during structural change, jumps, or a liquidity crisis. Low forecast error does not imply trading profit because option P&L also depends on risk premia, skew, path, hedging, and costs.

- Before comparing forecasts, align physical-versus-risk-neutral measure, horizon, and units.
- When a model suddenly lags, inspect regime change, data revisions, and parameter drift.
- Report stress-period error separately so calm observations cannot dilute failure.
- Forecasts support risk planning and do not guarantee volatility-trading or directional returns.

## Related Concepts

- [[realized-vs-implied-volatility|Realized Versus Implied Volatility]] — Forecasting future volatility is the basis for judging whether implied volatility is rich.
- [[skewness-kurtosis-fat-tails|Skewness, Kurtosis, And Fat-Tail Risk]] — Volatility clustering and fat tails require modelling the second moment's time structure.
- [[model-assumptions-and-model-risk|Model Assumptions And Model Risk: From Correct Formula To Reliable Decision]] — A volatility model's parameters are themselves unstable, so parameter risk must be handled explicitly.
- [[variance-swaps-and-vix|Variance Swaps And VIX: From Option Cross-Sections To Risk-Neutral Variance]] — Variance swaps and VIX turn a volatility forecast into a tradable instrument.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- msci-riskmetrics-technical
- engle-arch-original
- patton-volatility-proxies
- finra-volatility
- nist-distributions
- cfa-risk-adjusted-performance
