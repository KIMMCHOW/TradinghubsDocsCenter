---
title: "CVaR / Expected Shortfall：越过分位点后的平均损失"
title_en: "CVaR / Expected Shortfall: Average Loss Beyond A Quantile"
slug: "expected-shortfall-cvar"
type: lesson
level: Advanced
order: 54
track: risk-performance-and-hedging
track_label: "风险、绩效与对冲"
reading_time: "22 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/风险、绩效与对冲"
  - "权限/需登录"
aliases:
  - "CVaR / Expected Shortfall：越过分位点后的平均损失"
  - "CVaR / Expected Shortfall: Average Loss Beyond A Quantile"
  - "expected-shortfall-cvar"
source_url: "https://tradinghubs.org/docs/trading-knowledge/expected-shortfall-cvar"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# CVaR / Expected Shortfall：越过分位点后的平均损失

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[risk-performance-and-hedging|风险、绩效与对冲]]
> 上一课：[[calmar-ratio-maximum-drawdown|Calmar Ratio 与最大回撤：把复合增长放回路径中]] ｜ 下一课：[[multi-metric-risk-dashboard|多指标风险面板：把收益、尾部、路径、敏感度与流动性对齐]]

**高级 · 风险、绩效与对冲 · 22 分钟**

> VaR 给出损失分布的一个分位点，却不说明越过该点后会损失多少。Expected Shortfall 继续观察最差尾部并取平均，因此提供更丰富的尾部严重度信息，但仍然受样本、模型、估值与流动性假设约束。

以正值损失变量统一 VaR 与 Expected Shortfall 的符号，掌握历史、参数和情景估计，并识别有限尾部样本与模型外事件。

### 01 / 概念边界

#### 先把损失定义为正值，再讨论置信水平

令 L=-R_p 或直接用货币损失表示风险，较大的 L 代表更差结果。置信水平 α 下的 VaR 是损失分布达到 α 的最小分位点；Expected Shortfall 则是从 α 到 1 的 VaR 分位函数平均值。

当损失分布连续时，Expected Shortfall 常写成条件平均 E[L | L≥VaR_α]。若分布在 VaR 点有离散质量，简单条件平均可能给出错误权重，因此分位积分定义更稳健。

- **VaR 与一般形式的 Expected Shortfall**

  ```latex
  \operatorname{VaR}_{\alpha}(L)=\inf\{\ell:F_L(\ell)\ge\alpha\},\qquad \operatorname{ES}_{\alpha}(L)=\frac{1}{1-\alpha}\int_{\alpha}^{1}\operatorname{VaR}_{u}(L)\,du
  ```

### 02 / 机制与度量

#### 尾部估计方法不同，回答的问题也不同

历史法对重估后的历史损失排序，透明但默认过去状态覆盖未来；参数法用选定分布与相关结构外推，样本效率更高却承受分布误设；蒙特卡洛与压力情景可以重估非线性组合，但依赖情景生成、依赖结构和定价模型。

α 越高，落入尾部的有效观测越少。百分之九十九 ES 在一千个近似独立样本中只由大约十个最差观测主导；置信区间、重采样方式和压力情景的重要性会迅速上升。重叠收益与波动状态变化还会进一步减少有效样本量。

| 方法 | 优势 | 主要模型风险 |
| --- | --- | --- |
| 历史重估 | 路径直观、非线性可重估 | 历史状态覆盖不足 |
| 参数估计 | 平滑且样本效率较高 | 尾部分布与相关性误设 |
| 蒙特卡洛 | 可构造联合风险因子情景 | 生成过程与定价模型双重误差 |
| 确定性压力 | 覆盖可解释的极端事件 | 不提供自然概率权重 |

### 03 / 阅读流程

#### 从持仓冻结到尾部归因的完整链路

ES 计算必须绑定估值时点、持有期和持仓快照。对期权组合，应在每个情景下完整重估价格、波动率曲面、利率、股息和时间推进，而不是只用线性 Delta 近似尾部损失。

- 定义损失正负号、货币或收益单位、持有期、α 与持仓快照。
- 建立完整重估函数，并用基准情景验证零冲击时损益接近零。
- 分别运行历史、统计模拟与确定性压力，保留情景权重。
- 输出 VaR、ES、尾部样本数、置信区间和最差情景贡献。
- 用后续实现损益做例外回测，并审查模型与市场状态变化。

### 04 / 风险边界

#### ES 不是最坏损失，也不覆盖不可交易状态

Expected Shortfall 是选定分布尾部的平均值，而不是最大可能损失。比样本更极端的跳空、交易暂停、波动率曲面断裂、保证金上调和对手方事件可能完全不在估计分布内。

期限缩放不能把一日 ES 机械乘以平方根得到多日 ES，尤其在仓位动态、流动性衰减和收益相关时。风险限额应配合压力损失、现金需求、集中度和可退出性，而不是只依赖一个置信水平。

- 读取 ES 前先确认损失符号、α、期限、单位和估计方法。
- 若尾部样本极少，显示样本数并提升压力情景权重。
- 将最大单一情景损失与 ES 并列，避免把平均尾部误当上限。
- 该度量用于风险教育与监控，不保证损失被限制在任何数值内。

## 相关概念

- [[skewness-kurtosis-fat-tails|偏度、峰度与肥尾风险]] — 尾部厚度直接决定 VaR 之外的期望损失。
- [[normal-lognormal-distributions|正态、对数正态与收益分布]] — 正态假设会系统性低估尾部风险的度量值。
- [[straddle-strangle-event-risk|Straddle、Strangle 与事件波动]] — 事件结构的尾部损失形状与卖出结构完全不同。
- [[variance-swaps-and-vix|方差互换与 VIX：从期权横截面到风险中性方差]] — 卖出方差在极端行情下的损失远超线性估计。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> VaR identifies a quantile of the loss distribution but does not say how severe losses become beyond it. Expected Shortfall averages the worse tail and therefore adds information about severity, while remaining dependent on sample, model, valuation, and liquidity assumptions.

Use a positive loss variable to align VaR and Expected Shortfall signs, compare historical, parametric, and scenario estimates, and recognize finite-tail-sample and out-of-model events.

### 01 / Concept Boundary

#### Define Loss As Positive Before Choosing Confidence

Let L=-R_p, or define L directly as a monetary loss, so larger L means a worse outcome. At confidence level alpha, VaR is the smallest loss quantile reaching alpha; Expected Shortfall is the average of the VaR quantile function from alpha to one.

For a continuous loss distribution, Expected Shortfall is often written as E[L | L at or above VaR_alpha]. If the distribution has probability mass at the VaR point, that simple conditional average can assign the wrong weight, so the quantile-integral definition is more robust.

- **VaR And General Expected Shortfall**

  ```latex
  \operatorname{VaR}_{\alpha}(L)=\inf\{\ell:F_L(\ell)\ge\alpha\},\qquad \operatorname{ES}_{\alpha}(L)=\frac{1}{1-\alpha}\int_{\alpha}^{1}\operatorname{VaR}_{u}(L)\,du
  ```

### 02 / Mechanics And Measurement

#### Different Tail Estimators Answer Different Questions

Historical estimation ranks revalued historical losses and is transparent, but assumes past states cover the future. Parametric estimation extrapolates a chosen distribution and dependence structure, gaining sample efficiency while accepting misspecification risk. Monte Carlo and stress scenarios can revalue nonlinear portfolios but depend on scenario generation, dependence, and pricing models.

As alpha rises, fewer effective observations remain in the tail. A 99% ES from one thousand approximately independent observations is dominated by roughly ten worst observations, so confidence intervals, resampling design, and stress scenarios become increasingly important. Overlapping returns and changing volatility regimes reduce effective sample size further.

| Method | Strength | Primary Model Risk |
| --- | --- | --- |
| Historical revaluation | Observable paths and nonlinear revaluation | Insufficient regime coverage |
| Parametric estimation | Smooth and sample-efficient | Tail-distribution and dependence misspecification |
| Monte Carlo | Flexible joint-factor scenarios | Scenario and pricing-model error |
| Deterministic stress | Covers interpretable extremes | No natural probability weight |

### 03 / Reading Workflow

#### A Full Chain From Position Freeze To Tail Attribution

An ES calculation must bind valuation time, holding horizon, and a frozen position snapshot. For an options portfolio, fully revalue price, volatility surface, rates, dividends, and passage of time in each scenario rather than relying only on a linear delta approximation in the tail.

- Define loss sign, currency-or-return units, holding horizon, alpha, and position snapshot.
- Build a full revaluation function and verify near-zero P&L under a zero-shock scenario.
- Run historical, statistical-simulation, and deterministic stresses separately, retaining scenario weights.
- Output VaR, ES, tail observation count, confidence interval, and worst-scenario contributions.
- Backtest exceptions against subsequent realized P&L and review model and regime changes.

### 04 / Risk Boundary

#### ES Is Not Worst-Case Loss And Does Not Cover Untradeable States

Expected Shortfall is an average inside the selected distribution's tail, not the maximum possible loss. Gaps beyond the sample, trading halts, volatility-surface breaks, margin increases, and counterparty events may sit entirely outside the estimated distribution.

Horizon scaling cannot mechanically turn one-day ES into multi-day ES with a square-root rule, especially with dynamic positions, decaying liquidity, and dependent returns. Risk limits need stress loss, cash needs, concentration, and exit capacity alongside any confidence level.

- Before reading ES, confirm loss sign, alpha, horizon, units, and estimation method.
- When tail observations are scarce, display their count and give more weight to stress scenarios.
- Show the worst individual scenario beside ES so a tail average is not mistaken for a cap.
- The measure supports risk education and monitoring and does not guarantee any loss ceiling.

## Related Concepts

- [[skewness-kurtosis-fat-tails|Skewness, Kurtosis, And Fat-Tail Risk]] — Tail thickness directly determines expected loss beyond VaR.
- [[normal-lognormal-distributions|Normal, Lognormal, And Return Distributions]] — A normal assumption systematically understates tail-risk measures.
- [[straddle-strangle-event-risk|Straddles, Strangles, And Event Volatility]] — An event structure's tail-loss shape differs completely from a short-premium structure.
- [[variance-swaps-and-vix|Variance Swaps And VIX: From Option Cross-Sections To Risk-Neutral Variance]] — Short variance loses far more than a linear estimate in extreme markets.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cfa-risk-adjusted-performance
- finra-risk
- nist-distributions
