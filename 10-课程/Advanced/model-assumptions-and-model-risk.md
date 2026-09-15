---
title: "模型假设与模型风险：从公式正确到决策可靠"
title_en: "Model Assumptions And Model Risk: From Correct Formula To Reliable Decision"
slug: "model-assumptions-and-model-risk"
type: lesson
level: Advanced
order: 58
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "23 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "模型假设与模型风险：从公式正确到决策可靠"
  - "Model Assumptions And Model Risk: From Correct Formula To Reliable Decision"
  - "model-assumptions-and-model-risk"
source_url: "https://tradinghubs.org/docs/trading-knowledge/model-assumptions-and-model-risk"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# 模型假设与模型风险：从公式正确到决策可靠

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[risk-neutral-vs-physical-probability|风险中性概率与现实概率：定价分布不是行情预测]] ｜ 下一课：[[binomial-risk-neutral-pricing|二叉树与风险中性定价]]

**高级 · 结构、定价与波动率 · 23 分钟**

> 模型可以在代码和代数上完全正确，却因为市场机制、输入数据、参数稳定性或使用场景不匹配而给出危险结论。模型治理的核心不是证明模型永远正确，而是明确它在哪些条件下足够有用、何时必须降级或停用。

把模型风险拆成概念、数据、参数、实现和使用风险，建立从用途定义、独立验证到监控与停用的完整治理流程。

### 01 / 概念边界

#### 模型风险来自模型本身，也来自模型被如何使用

概念风险包括价格过程、流动性、相关性和行为假设不适合目标市场；数据风险包括缺失、时间错位、幸存者偏差和错误单位；参数风险来自有限样本与状态漂移；实现风险来自公式、代码、数值方法和接口错误。

使用风险发生在输出脱离批准用途时，例如把用于相对比较的近似价格当成可成交价格，或把局部 Greeks 当成大幅压力损失。每个模型都应有用途、禁止用途、输入范围、输出单位、负责人和依赖清单。

| 风险类别 | 示例 | 主要控制 |
| --- | --- | --- |
| 概念 | 连续扩散忽略跳跃与停牌 | 用途边界与替代模型 |
| 数据 | 期权与现货时间戳错位 | 血缘、新鲜度与单位校验 |
| 参数 | 波动率状态已经改变 | 稳定性、置信区间与重估 |
| 实现与使用 | 乘数错误或输出超范围复用 | 单元测试、审批与监控 |

### 02 / 机制与度量

#### 拟合误差只是模型风险证据的一部分

可观察报价下的残差 ε_i=P_i^{obs}-P_i^{model} 能揭示横截面偏差，但小残差不保证对冲动态、尾部情景或样本外预测正确。过多参数还可能通过过拟合降低样本内误差，却扩大未来不稳定性。

验证应覆盖理论性质、无套利关系、参数识别、数值收敛、基准实现、敏感性和极端输入。误差阈值必须绑定经济单位与用途：一分钱价格误差对长期情景可能无关紧要，对高频报价却可能超过全部边际。

- **报价残差与加权拟合误差**

  ```latex
  \varepsilon_i=P_i^{\mathrm{obs}}-P_i^{\mathrm{model}},\qquad \operatorname{WRMSE}=\sqrt{\frac{\sum_i w_i\varepsilon_i^2}{\sum_i w_i}}
  ```

### 03 / 阅读流程

#### 模型生命周期从问题定义开始，以可停用性结束

治理流程应在开发前写清决策问题和容忍误差，开发后由不同视角复核理论、数据、代码和使用方式。上线监控不仅看拟合，还要看输入漂移、覆盖率、实现损益、人工覆盖与超范围调用。

- 登记模型用途、禁止用途、输出单位、依赖、负责人和重要等级。
- 建立基准数据集、手工可验证案例、极端输入和数值收敛测试。
- 使用替代模型与样本外数据验证价格、风险和对冲结论。
- 设定输入漂移、残差、参数跳变、失败率和覆盖率阈值。
- 预先定义降级输出、人工升级、回滚版本和停用条件。

### 04 / 风险边界

#### 压力状态最可能同时破坏多个模型假设

流动性下降时，报价噪声、相关性、波动率、跳跃、融资和可执行性可能同时变化。逐个参数的小幅敏感性无法覆盖这种联合失效，应保留确定性压力、替代估值和不依赖模型的名义敞口检查。

“通过验证”只表示在指定证据和用途下达到当前标准，不是永久认证。重大市场变化、新产品、数据源变更、代码迁移或用途扩张都应触发重新验证。

- 输出异常时先区分市场变化、输入失败、参数漂移与实现错误。
- 模型超出训练或批准范围时显示不可用，而不是外推精确数字。
- 用替代模型和完整重估复核大额风险，不只依赖局部敏感度。
- 模型输出辅助判断，不保证市场价格、成交能力或损失边界。

## 相关概念

- [[bsm-pricing-model|Black-Scholes-Merton Pricing Model]] — BSM 的假设清单是评估模型风险的具体对象。
- [[volatility-forecasting|波动率预测：从实现方差到样本外条件预测]] — 波动率输入是否稳定是模型误差的主要来源之一。
- [[implied-volatility-surface|隐含波动率 IV 与波动率曲面]] — 曲面偏斜是市场对「单一常数波动率」假设的直接反驳。
- [[options-pnl-attribution|期权 P&L 归因：从起止重估到 Greek 解释残差]] — 盈亏归因是把模型残差从可解释损益中分离出来的方法。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> A model can be algebraically and programmatically correct yet produce dangerous conclusions because market mechanics, inputs, parameter stability, or use context do not fit. Governance does not prove permanent correctness; it defines when the model is useful enough and when it must be degraded or stopped.

Decompose model risk into conceptual, data, parameter, implementation, and use risk, then build a lifecycle from purpose definition and independent validation through monitoring and retirement.

### 01 / Concept Boundary

#### Model Risk Comes From The Model And From Its Use

Conceptual risk includes price-process, liquidity, dependence, or behavior assumptions that do not fit the target market. Data risk includes missing values, timestamp misalignment, survivorship bias, and bad units. Parameter risk arises from finite samples and regime drift, while implementation risk covers formula, code, numerical, and interface errors.

Use risk appears when output escapes its approved purpose, such as treating an approximate relative-value mark as an executable price or local Greeks as a large-shock stress loss. Every model needs a stated purpose, prohibited uses, input range, output units, owner, and dependency inventory.

| Risk Class | Example | Primary Control |
| --- | --- | --- |
| Conceptual | Continuous diffusion omits jumps and halts | Use boundary and challenger model |
| Data | Options and spot timestamps are misaligned | Lineage, freshness, and unit checks |
| Parameter | Volatility regime has changed | Stability, uncertainty, and recalibration |
| Implementation and use | Bad multiplier or out-of-scope reuse | Unit tests, approval, and monitoring |

### 02 / Mechanics And Measurement

#### Fit Error Is Only One Piece Of Model-Risk Evidence

Residuals epsilon_i=P_i^{obs}-P_i^{model} can reveal cross-sectional bias where quotes are observable, but small residuals do not validate hedge dynamics, tail scenarios, or out-of-sample forecasts. Extra parameters may reduce in-sample error through overfitting while increasing future instability.

Validation should cover theoretical properties, no-arbitrage relations, parameter identification, numerical convergence, benchmark implementation, sensitivities, and extreme inputs. Error thresholds need economic units and purpose: a one-cent error may be irrelevant to a long-horizon scenario but larger than the entire edge in rapid quoting.

- **Quote Residual And Weighted Fit Error**

  ```latex
  \varepsilon_i=P_i^{\mathrm{obs}}-P_i^{\mathrm{model}},\qquad \operatorname{WRMSE}=\sqrt{\frac{\sum_i w_i\varepsilon_i^2}{\sum_i w_i}}
  ```

### 03 / Reading Workflow

#### The Model Lifecycle Starts With The Question And Ends With Retireability

Governance should state the decision problem and tolerated error before development, then review theory, data, code, and use from an independent perspective. Production monitoring looks beyond fit to input drift, coverage, realized P&L, overrides, and out-of-scope calls.

- Register purpose, prohibited uses, output units, dependencies, owner, and materiality.
- Build benchmark data, hand-checkable cases, extreme inputs, and numerical-convergence tests.
- Validate price, risk, and hedge conclusions with challenger models and out-of-sample data.
- Set thresholds for input drift, residuals, parameter jumps, failures, and coverage.
- Predefine degraded output, manual escalation, rollback version, and retirement conditions.

### 04 / Risk Boundary

#### Stress Is When Multiple Assumptions Are Most Likely To Fail Together

When liquidity falls, quote noise, dependence, volatility, jumps, funding, and executability can change together. Small one-parameter sensitivities cannot cover that joint failure, so deterministic stresses, alternative valuations, and model-independent notional checks remain necessary.

Validation approval means the model meets a current standard for stated evidence and use; it is not permanent certification. Material market change, a new product, changed input pipeline, code migration, or expanded use should trigger revalidation.

- When output looks abnormal, separate market change, input failure, parameter drift, and implementation error.
- Outside training or approved scope, show unavailable rather than extrapolating a precise number.
- Recheck material risk with challengers and full revaluation, not only local sensitivities.
- Model output supports judgment and does not guarantee price, execution, or a loss boundary.

## Related Concepts

- [[bsm-pricing-model|Black-Scholes-Merton Pricing Model]] — The BSM assumption list is the concrete object of model-risk assessment.
- [[volatility-forecasting|Volatility Forecasting: From Realized Variance To Out-Of-Sample Conditional Forecasts]] — Whether the volatility input is stable is a main source of model error.
- [[implied-volatility-surface|Implied Volatility And Volatility Surface]] — Surface skew is the market's direct rebuttal of a single constant-volatility assumption.
- [[options-pnl-attribution|Options P&L Attribution: From Endpoint Revaluation To Greek Explanations]] — P&L attribution is how model residual is separated from explainable profit and loss.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- finra-risk
- occ-options-disclosure
- nist-distributions
