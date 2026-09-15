---
title: "Sharpe Ratio：单位总波动的超额收益"
title_en: "Sharpe Ratio: Excess Return Per Unit Of Total Volatility"
slug: "sharpe-ratio"
type: lesson
level: Advanced
order: 51
track: risk-performance-and-hedging
track_label: "风险、绩效与对冲"
reading_time: "20 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/风险、绩效与对冲"
  - "权限/需登录"
aliases:
  - "Sharpe Ratio：单位总波动的超额收益"
  - "Sharpe Ratio: Excess Return Per Unit Of Total Volatility"
  - "sharpe-ratio"
source_url: "https://tradinghubs.org/docs/trading-knowledge/sharpe-ratio"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# Sharpe Ratio：单位总波动的超额收益

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[risk-performance-and-hedging|风险、绩效与对冲]]
> 上一课：[[expectations-feedback-path-dependence|预期、反馈与路径依赖]] ｜ 下一课：[[sortino-ratio|Sortino Ratio：只把目标下方偏差计入风险]]

**高级 · 风险、绩效与对冲 · 20 分钟**

> Sharpe Ratio 把平均超额收益与全部收益波动放进同一个比率。它适合回答“承担一单位历史总波动获得了多少超额收益”，却不能单独证明策略稳健、可复制或适合未来市场。

从收益口径、无风险基准、波动率与年化假设四个层面正确计算 Sharpe Ratio，并识别序列相关、尾部风险和样本选择造成的失真。

### 01 / 概念边界

#### 先统一分子、分母和时间尺度

令同一计价货币、同一频率下的组合总收益为 R_{p,t}，同期可获得的现金基准收益为 R_{f,t}，超额收益为 x_t=R_{p,t}-R_{f,t}。分子衡量样本平均超额收益，分母衡量超额收益的样本标准差；二者必须来自完全一致的观测区间。

现金基准不是随手填入的常数。日、周或月收益需要匹配相同持有期的基准，并明确收益是否已扣除费用、融资、借券、滑点和税费。比较两个结果前，还要统一简单收益或对数收益、估值时点以及缺失值处理。

- **总体定义**

  ```latex
  \operatorname{SR}=\frac{\mathbb{E}[R_p-R_f]}{\sigma(R_p-R_f)}
  ```
  分母是总波动，不只统计亏损期。

### 02 / 机制与度量

#### 平方根年化依赖独立且稳定的周期结构

若一年有 m 个等长周期，且超额收益近似独立同分布，常见样本年化写法是周期 Sharpe 乘以 √m。重叠收益、平滑估值、持仓自相关、波动率聚类或变化中的杠杆都会破坏该缩放关系，因此高频结果不能机械放大。

Sharpe 只压缩了均值和二阶离散程度。两个具有相同比率的策略，可以分别表现为接近对称的小波动和长期平稳后偶发巨亏。置信区间、滚动窗口、偏度、尾部损失和最大回撤必须与点估计一起查看。

- **常见样本年化形式**

  ```latex
  \widehat{\operatorname{SR}}_{\mathrm{ann}}=\sqrt{m}\,\frac{\bar{x}}{s_x},\qquad x_t=R_{p,t}-R_{f,t}
  ```

| 检查项 | 正确问题 | 常见误差 |
| --- | --- | --- |
| 收益 | 是否为可实现的净总收益？ | 忽略费用或融资 |
| 基准 | 是否与币种和周期匹配？ | 把年利率直接减去日收益 |
| 年化 | 序列相关是否足够低？ | 对重叠样本机械乘 √m |

### 03 / 阅读流程

#### 从可审计收益序列开始，而不是从最终比率开始

实务中先冻结研究窗口、估值频率和净值口径，再生成每期现金基准与超额收益。随后检查异常值、停牌或缺价、非同步估值和仓位跳变；只有基础序列通过检查后才计算点估计、滚动区间和不确定性。

- 固定币种、频率、起止日、费用与再投资规则，并保留样本数量。
- 逐期匹配现金基准，禁止混用年化利率与周期收益。
- 绘制超额收益、滚动波动率、自相关和回撤，标记数据修订。
- 同时报告周期值、年化值、滚动范围和适合序列相关的置信区间。
- 在相同口径下与替代策略比较，并用未参与调参的样本复核。

### 04 / 风险边界

#### 高 Sharpe 不等于低尾部风险，也不等于未来可复制

卖出凸性、流动性溢价或平滑估值可能在多数时期产生小额正收益，从而抬高历史 Sharpe，却在跳空或流动性收缩时集中暴露损失。短样本还可能遗漏完整市场周期，参数搜索则会把偶然性包装成稳定性。

该指标是描述工具，不是仓位规模、杠杆或交易许可。任何决策还需结合容量、最大回撤、尾部情景、保证金、流动性和模型外风险；历史点估计不能替代前瞻压力测试。

- 只比较同币种、同频率、同成本和同窗口的 Sharpe。
- 若滚动值由少数观测推动，回到原始交易与估值记录核验。
- 把尾部损失、回撤和流动性压力放在同一绩效面板中。
- 本课用于绩效度量教育，不构成收益承诺或交易建议。

## 相关概念

- [[expected-utility-opportunity-cost|期望效用、机会成本与风险收益]] — 把收益与风险压缩为单一比值，本身就是一种效用假设。
- [[risk-free-rate-discounting|无风险利率、贴现与时间价值]] — Sharpe 的超额收益以现金基准利率为参照。
- [[sortino-ratio|Sortino Ratio：只把目标下方偏差计入风险]] — Sortino 只惩罚下行偏离，是该比值的非对称变体。
- [[efficient-market-hypothesis|有效市场假说（EMH）]] — 任何 alpha 声明都必须先说明用哪个风险基准来度量。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> The Sharpe Ratio places average excess return over a cash benchmark above total return volatility. It answers how much historical excess return accompanied one unit of total variability, but it cannot by itself prove robustness, repeatability, or future suitability.

Calculate the Sharpe Ratio with aligned return, cash benchmark, volatility, and annualization conventions, then diagnose distortions from serial dependence, tail risk, and sample selection.

### 01 / Concept Boundary

#### Align The Numerator, Denominator, And Clock

Let portfolio total return be R_{p,t}, the attainable cash benchmark over the same currency and interval be R_{f,t}, and excess return be x_t=R_{p,t}-R_{f,t}. The numerator is the sample mean of excess returns and the denominator is their sample standard deviation, so both must use identical observations.

The cash benchmark is not an arbitrary constant. Daily, weekly, or monthly returns need a matching holding-period benchmark, while fee, financing, borrow, slippage, and tax treatment must be stated. Comparisons also require the same simple-versus-log return convention, valuation timestamp, and missing-data policy.

- **Population Definition**

  ```latex
  \operatorname{SR}=\frac{\mathbb{E}[R_p-R_f]}{\sigma(R_p-R_f)}
  ```
  The denominator is total variability, not only losing periods.

### 02 / Mechanics And Measurement

#### Square-Root Annualization Needs Stable Period Structure

With m equal periods per year and approximately independent, identically distributed excess returns, the usual sample annualization multiplies the periodic Sharpe by the square root of m. Overlapping returns, smoothed marks, autocorrelated positions, volatility clustering, or changing leverage break that scaling, so high-frequency estimates must not be amplified mechanically.

Sharpe compresses the sample into a mean and a second-moment dispersion. Two strategies with the same ratio can represent small symmetric fluctuations or long calm periods interrupted by rare large losses. Confidence intervals, rolling windows, skew, tail loss, and maximum drawdown belong beside the point estimate.

- **Common Sample Annualization**

  ```latex
  \widehat{\operatorname{SR}}_{\mathrm{ann}}=\sqrt{m}\,\frac{\bar{x}}{s_x},\qquad x_t=R_{p,t}-R_{f,t}
  ```

| Check | Question To Ask | Common Error |
| --- | --- | --- |
| Return | Is it realizable net total return? | Ignoring costs or financing |
| Benchmark | Does it match currency and horizon? | Subtracting an annual rate from a daily return |
| Annualization | Is serial dependence sufficiently low? | Applying square-root scaling to overlaps |

### 03 / Reading Workflow

#### Start With An Auditable Return Series, Not The Final Ratio

In practice, freeze the study window, valuation frequency, and net-asset-value convention before building each period's cash benchmark and excess return. Then inspect outliers, stale or missing marks, asynchronous valuation, and position jumps; compute the estimate, rolling ranges, and uncertainty only after the base series passes review.

- Fix currency, frequency, dates, costs, and reinvestment rules, and retain the observation count.
- Match the cash benchmark period by period; never mix an annual rate with a periodic return.
- Plot excess returns, rolling volatility, autocorrelation, and drawdown, with data revisions marked.
- Report periodic and annualized values, rolling ranges, and confidence intervals suited to serial dependence.
- Compare alternatives under identical conventions and recheck on data not used for tuning.

### 04 / Risk Boundary

#### A High Sharpe Is Neither Low Tail Risk Nor Future Repeatability

Short convexity, liquidity premia, or smoothed marks can produce many small gains and elevate historical Sharpe while concentrating losses during gaps or liquidity contraction. Short samples may omit a full regime, and parameter searches can disguise chance as stability.

The metric is descriptive, not a position-size, leverage, or trading authorization rule. Decisions still require capacity, maximum drawdown, tail scenarios, margin, liquidity, and risks outside the model; a historical point estimate cannot replace forward stress testing.

- Compare Sharpe values only across the same currency, frequency, cost, and window conventions.
- If a rolling value is driven by a few observations, inspect the underlying trades and marks.
- Place tail loss, drawdown, and liquidity stress on the same performance panel.
- This lesson teaches performance measurement and is not a return promise or trading recommendation.

## Related Concepts

- [[expected-utility-opportunity-cost|Expected Utility, Opportunity Cost, And Risk-Reward]] — Compressing return and risk into one ratio is itself a utility assumption.
- [[risk-free-rate-discounting|Risk-Free Rates, Discounting, And Time Value]] — The Sharpe ratio references excess return against a cash benchmark rate.
- [[sortino-ratio|Sortino Ratio: Counting Only Deviation Below A Target]] — Sortino penalizes only downside deviation, an asymmetric variant of the same ratio.
- [[efficient-market-hypothesis|Efficient Market Hypothesis (EMH)]] — Any alpha claim must first state which risk benchmark defines it.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cfa-risk-adjusted-performance
- finra-risk
- nist-distributions
