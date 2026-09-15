---
title: "方差互换与 VIX：从期权横截面到风险中性方差"
title_en: "Variance Swaps And VIX: From Option Cross-Sections To Risk-Neutral Variance"
slug: "variance-swaps-and-vix"
type: lesson
level: Advanced
order: 62
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "26 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "方差互换与 VIX：从期权横截面到风险中性方差"
  - "Variance Swaps And VIX: From Option Cross-Sections To Risk-Neutral Variance"
  - "variance-swaps-and-vix"
source_url: "https://tradinghubs.org/docs/trading-knowledge/variance-swaps-and-vix"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# 方差互换与 VIX：从期权横截面到风险中性方差

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[volatility-forecasting|波动率预测：从实现方差到样本外条件预测]] ｜ 下一课：[[skew-term-structure|Skew / Term Structure]]

**高级 · 结构、定价与波动率 · 26 分钟**

> 方差互换直接交换实现方差与固定方差执行价的差额，VIX 则从一组指数期权价格计算恒定三十个日历日风险中性方差的年化平方根。二者关联紧密，却不是同一个可交割资产。

理解方差互换的实现方差支付、期权复制思想和 VIX 型常到期计算，并严格区分指数、其衍生品和现实波动率预测。

### 01 / 概念边界

#### 方差名义本金对方差点敏感，不是对波动率点线性敏感

本课采用市场方差点口径：RV_pt 与 K_pt 均等于小数方差乘 10,000，N_pt 的单位是报告货币/方差点。因而波动率从 20% 到 21% 时，方差从 400 点变为 441 点，支付差额是 41 个方差点，而不是一个线性波动率点。

离散采样的实现方差通常由对数收益平方和构造，但开收盘、节假日、缺价、跳跃和最终年化因子都由具体条款决定。若系统改用小数方差口径，则同一经济支付要求 N_dec=10,000N_pt；研究结果必须沿用同一口径，不能混合两套名义本金。

- **方差点口径下的支付与实现方差**

  ```latex
  \operatorname{Payoff}=N_{\mathrm{pt}}(\operatorname{RV}_{\mathrm{pt}}-K_{\mathrm{pt}}),\qquad \operatorname{RV}_{\mathrm{pt}}=10^4\frac{A}{n}\sum_{i=1}^{n}\left(\log\frac{S_i}{S_{i-1}}\right)^2
  ```
  N_pt 为报告货币/方差点，A 为与采样频率一致的年化因子；K_pt 与 RV_pt 必须使用同一合约定义。

### 02 / 机制与度量

#### VIX 型公式用跨执行价期权近似复制方差

单一期限风险中性方差把价外期权报价按 ΔK/K² 加权，并用远期 F、贴现率 R 与参考执行价 K_0 做修正。VIX 的常到期步骤先在线性权重下插值近、次期限的累计总方差 T_iσ_i²，再除以三十个日历日目标期限 T_M 年化；不是直接插值两个年化方差。

该结果是从期权价格提取的 Q 下方差交换水平，包含风险溢价与供需，并非 P 下未来实现方差的无偏预测。期权报价筛选、尾部执行价覆盖、远期估计和插值都会影响指数。

- **单一期限风险中性方差的离散形式**

  ```latex
  \sigma^2=\frac{2}{T}\sum_i\frac{\Delta K_i}{K_i^2}e^{RT}Q(K_i)-\frac{1}{T}\left(\frac{F}{K_0}-1\right)^2
  ```

- **累计总方差的恒定期限插值**

  ```latex
  \sigma_M^2=\frac{T_2-T_M}{T_2-T_1}\frac{T_1}{T_M}\sigma_1^2+\frac{T_M-T_1}{T_2-T_1}\frac{T_2}{T_M}\sigma_2^2,\qquad T_M=\frac{30}{365}
  ```
  T_1、T_M、T_2 必须使用同一年单位并满足 T_1≤T_M≤T_2；被加权的是 T_iσ_i²。

- **三十日波动率指数缩放**

  ```latex
  \operatorname{VolIndex}=100\sqrt{\sigma_M^2}
  ```

### 03 / 阅读流程

#### 从合约条款和指数方法分别重建

分析方差互换先锁定采样与支付条款；分析 VIX 先锁定指数目标期限、期权筛选、远期、利率、执行价间距和插值。两条链路完成后，才能比较风险中性执行价、后续实现方差与风险溢价。

- 记录实现方差的采样时点、年化、异常事件和名义本金单位。
- 同步期权报价，按方法筛选执行价并验证看涨看跌远期关系。
- 逐期限计算累计总方差 T_iσ_i²，再插值到固定三十个日历日目标期限。
- 将指数值、风险中性方差、物理预测和最终实现值分栏展示。
- 对缺失尾部报价、宽价差、跳跃和滚动期限做敏感性分析。

### 04 / 风险边界

#### VIX 指数本身不是可直接买入持有的现货资产

VIX 是按规则计算的指数，不是可直接交割的一篮子现货。VIX 期货和期权是独立衍生品，其价格由自身到期、结算预期和期限结构决定，因此不会与当前指数一比一同步。

方差互换与波动率衍生品具有凸性、跳跃、流动性、保证金和模型风险。风险中性方差高于物理预测可能补偿尾部风险，并不等于可无风险收取的溢价。

- 引用 VIX 时明确是现值指数、期货、期权还是相关产品。
- 比较实现波动率前先平方或开方并统一期限与年化单位。
- 指数跳升时同时检查近远期结构和期权报价质量。
- 本课解释方差定价，不构成买卖波动率衍生品的建议。

## 相关概念

- [[volatility-forecasting|波动率预测：从实现方差到样本外条件预测]] — 方差敞口的盈亏取决于已实现方差与约定方差之差。
- [[implied-volatility-surface|隐含波动率 IV 与波动率曲面]] — 方差互换的公平水平由整条曲面上的期权组合决定。
- [[vega-exposure-vol-hedging|Vega Exposure 与 Vol Hedging]] — 方差敞口是 Vega 敞口在期限与执行价上的积分形式。
- [[expected-shortfall-cvar|CVaR / Expected Shortfall：越过分位点后的平均损失]] — 卖出方差在极端行情下的损失远超线性估计。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> A variance swap exchanges realized variance against a fixed variance strike, while VIX derives the annualized square root of constant 30-calendar-day risk-neutral variance from a strip of index option prices. They are closely related but are not the same deliverable asset.

Understand variance-swap realized-variance payoff, option-replication intuition, and VIX-style constant-maturity calculation while separating the index, its derivatives, and physical volatility forecasts.

### 01 / Concept Boundary

#### Variance Notional Is Linear In Variance Points, Not Volatility Points

This lesson uses market variance points: RV_pt and K_pt equal decimal variance times 10,000, and N_pt is denominated in reporting currency per variance point. A volatility move from 20% to 21% therefore changes variance from 400 to 441 points, a 41-variance-point payoff difference rather than one linear volatility point.

Discretely sampled realized variance is often built from squared log returns, but opens and closes, holidays, missing prices, jumps, and the final annualization factor are contract-specific. If a system instead uses decimal variance, the same economic payoff requires N_dec=10,000 N_pt; research must keep one convention and never mix the two notionals.

- **Payoff And Realized Variance In Variance Points**

  ```latex
  \operatorname{Payoff}=N_{\mathrm{pt}}(\operatorname{RV}_{\mathrm{pt}}-K_{\mathrm{pt}}),\qquad \operatorname{RV}_{\mathrm{pt}}=10^4\frac{A}{n}\sum_{i=1}^{n}\left(\log\frac{S_i}{S_{i-1}}\right)^2
  ```
  N_pt is reporting currency per variance point and A is the annualization factor consistent with the sampling frequency; K_pt and RV_pt must share the same contractual definition.

### 02 / Mechanics And Measurement

#### A VIX-Style Formula Uses Options Across Strikes To Approximate Variance

Single-term risk-neutral variance weights out-of-the-money option quotes by delta-K over K squared and adjusts with forward F, discount rate R, and reference strike K_0. The VIX constant-maturity step linearly interpolates cumulative total variance T_i sigma_i squared across near and next terms, then divides by the 30-calendar-day target T_M to annualize; it does not directly interpolate the two annualized variances.

The result is a Q-measure variance-exchange level extracted from option prices, including risk premia and supply-demand effects, not an unbiased P-measure forecast of future realized variance. Quote filtering, tail-strike coverage, forward estimation, and interpolation all affect the index.

- **Discrete Single-Term Risk-Neutral Variance**

  ```latex
  \sigma^2=\frac{2}{T}\sum_i\frac{\Delta K_i}{K_i^2}e^{RT}Q(K_i)-\frac{1}{T}\left(\frac{F}{K_0}-1\right)^2
  ```

- **Constant-Maturity Interpolation Of Cumulative Total Variance**

  ```latex
  \sigma_M^2=\frac{T_2-T_M}{T_2-T_1}\frac{T_1}{T_M}\sigma_1^2+\frac{T_M-T_1}{T_2-T_1}\frac{T_2}{T_M}\sigma_2^2,\qquad T_M=\frac{30}{365}
  ```
  T_1, T_M, and T_2 must use the same year unit with T_1 less than or equal to T_M less than or equal to T_2; the weighted quantities are T_i sigma_i squared.

- **Thirty-Day Volatility-Index Scaling**

  ```latex
  \operatorname{VolIndex}=100\sqrt{\sigma_M^2}
  ```

### 03 / Reading Workflow

#### Reconstruct Contract Terms And Index Methodology Separately

For a variance swap, start with sampling and payoff terms. For VIX, start with target maturity, option filters, forward, rates, strike spacing, and interpolation. Only after rebuilding each chain should risk-neutral strike, subsequent realized variance, and risk premium be compared.

- Record realized-variance sampling, annualization, disruption rules, and notional units.
- Synchronize option quotes, filter strikes by methodology, and validate the call-put forward relation.
- Calculate cumulative total variance T_i sigma_i squared term by term before interpolating to the fixed 30-calendar-day target.
- Display index level, risk-neutral variance, physical forecast, and eventual realization in separate columns.
- Stress missing tail quotes, wide spreads, jumps, and rolling maturity.

### 04 / Risk Boundary

#### The VIX Index Is Not A Spot Asset That Can Be Bought And Held Directly

VIX is a rules-based index, not a directly deliverable spot basket. VIX futures and options are separate derivatives priced by their own expiries, settlement expectations, and term structure, so they do not track the current index one for one.

Variance swaps and volatility derivatives carry convexity, jump, liquidity, margin, and model risk. Risk-neutral variance above a physical forecast may compensate tail risk and is not a premium that can be collected without risk.

- When citing VIX, identify the current index, future, option, or related product.
- Before comparing with realized volatility, square or take roots as needed and align horizon and annualization.
- When the index jumps, inspect term structure and option-quote quality together.
- This lesson explains variance pricing and is not advice to trade volatility derivatives.

## Related Concepts

- [[volatility-forecasting|Volatility Forecasting: From Realized Variance To Out-Of-Sample Conditional Forecasts]] — Variance exposure pays the difference between realized and contracted variance.
- [[implied-volatility-surface|Implied Volatility And Volatility Surface]] — A variance swap's fair level is set by an option strip across the whole surface.
- [[vega-exposure-vol-hedging|Vega Exposure And Vol Hedging]] — Variance exposure is vega exposure integrated across expiry and strike.
- [[expected-shortfall-cvar|CVaR / Expected Shortfall: Average Loss Beyond A Quantile]] — Short variance loses far more than a linear estimate in extreme markets.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cboe-vix-methodology
- isda-variance-swap-definitions
- cboe-vix
- finra-volatility
- occ-options-disclosure
