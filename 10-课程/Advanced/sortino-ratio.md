---
title: "Sortino Ratio：只把目标下方偏差计入风险"
title_en: "Sortino Ratio: Counting Only Deviation Below A Target"
slug: "sortino-ratio"
type: lesson
level: Advanced
order: 52
track: risk-performance-and-hedging
track_label: "风险、绩效与对冲"
reading_time: "19 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/风险、绩效与对冲"
  - "权限/需登录"
aliases:
  - "Sortino Ratio：只把目标下方偏差计入风险"
  - "Sortino Ratio: Counting Only Deviation Below A Target"
  - "sortino-ratio"
source_url: "https://tradinghubs.org/docs/trading-knowledge/sortino-ratio"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# Sortino Ratio：只把目标下方偏差计入风险

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[risk-performance-and-hedging|风险、绩效与对冲]]
> 上一课：[[sharpe-ratio|Sharpe Ratio：单位总波动的超额收益]] ｜ 下一课：[[calmar-ratio-maximum-drawdown|Calmar Ratio 与最大回撤：把复合增长放回路径中]]

**高级 · 风险、绩效与对冲 · 19 分钟**

> Sortino Ratio 试图避免把目标上方的波动与亏损同等惩罚。它对收益不对称的策略更直观，但结果高度依赖目标收益、下行偏差定义和样本期，不能被视为 Sharpe 的无条件升级版。

定义最低可接受收益与下行偏差，正确区分 Sortino Ratio 的分子基准、分母样本约定和年化边界。

### 01 / 概念边界

#### 目标收益 MAR 是经济假设，不是装饰参数

最低可接受收益 MAR 可以是零、现金收益、负债增长率或投资者要求的门槛，但必须与每个观测周期匹配。分子通常使用组合平均收益减 MAR，分母只累计 R_t<MAR 时的缺口平方。

文献和软件对下行偏差存在不同分母：有的除以全部 n 个时期，有的只除以短缺时期数量。两种结果不能直接比较。课程采用“全部观测期”约定，使没有短缺的时期以零贡献进入均方。

- **Sortino Ratio 与全样本下行偏差**

  ```latex
  \operatorname{Sortino}=\frac{\mathbb{E}[R_p]-\operatorname{MAR}}{\operatorname{DD}_{\operatorname{MAR}}},\qquad \operatorname{DD}_{\operatorname{MAR}}=\sqrt{\mathbb{E}\!\left[\min(R_p-\operatorname{MAR},0)^2\right]}
  ```

### 02 / 机制与度量

#### 改变目标会同时移动分子并重塑分母

提高 MAR 不只是从收益中多减一个常数，它还会把更多观测重新分类为短缺并扩大每次缺口。因而同一策略可在不同目标下产生完全不同的排序，目标必须在查看结果前确定，不能为了改善比率事后调整。

若各期独立、目标按同一规则缩放且分布稳定，可以构造年化版本；现实中的重叠收益、动态目标和波动聚类会使 √m 缩放失效。分母接近零时比率会爆炸，此时应直接报告短缺次数和幅度，而不是展示一个看似精确的巨大数字。

| 口径 | 分母解释 | 适用提醒 |
| --- | --- | --- |
| 全部时期 | 所有时期的均方短缺，非短缺期为零 | 跨样本时仍需统一 n |
| 仅短缺时期 | 发生短缺条件下的均方缺口 | 短缺频率被移出分母 |
| 半方差 | 围绕均值或指定目标的下半部分 | 中心点必须明确 |

### 03 / 阅读流程

#### 先写目标政策，再计算下行绩效

一个可复核流程应保存每期 MAR 序列、短缺标记和短缺幅度。这样可以区分“很少但很深的亏损”与“频繁但较浅的未达标”，避免只看最终比率而丢失路径信息。

- 在读取策略结果前确定 MAR 的经济含义、币种和复利频率。
- 统一收益、费用、估值时点和缺失数据规则。
- 明确分母采用全部时期还是仅短缺时期，并永久标注。
- 同时输出短缺频率、平均短缺、最深短缺和滚动 Sortino。
- 用替代 MAR 和未见样本做敏感性分析，不以最优结果挑选目标。

### 04 / 风险边界

#### 忽略上行波动并不会消除估值、流动性或尾部问题

Sortino 仍然依赖历史观测，并可能被平滑估值、短样本和极少数尾部事件扭曲。对期权或卖出保险型策略，目标下方的分布可能极不稳定，单一二阶统计量无法表达跳跃、缺口和保证金路径。

若策略几乎没有历史短缺，分母很小并不代表风险很小，可能只是压力状态尚未出现。应结合期望损失、最大回撤、情景重估和流动性容量，而不是据此增加杠杆。

- 看到异常高 Sortino 时，先检查分母、短缺次数和样本长度。
- 跨策略比较前统一 MAR 与下行偏差分母约定。
- 将短缺深度和频率拆开显示，避免一个比率掩盖两种风险。
- 本指标不预测收益，也不构成增加风险敞口的依据。

## 相关概念

- [[sharpe-ratio|Sharpe Ratio：单位总波动的超额收益]] — Sortino 替换了分母，但读数含义仍与 Sharpe 对照。
- [[expected-shortfall-cvar|CVaR / Expected Shortfall：越过分位点后的平均损失]] — 只关注下行偏离，仍然没有描述尾部有多厚。
- [[calmar-ratio-maximum-drawdown|Calmar Ratio 与最大回撤：把复合增长放回路径中]] — 两个指标都以回撤相关量作为风险度量。
- [[multi-metric-risk-dashboard|多指标风险面板：把收益、尾部、路径、敏感度与流动性对齐]] — 单一下行指标不足，需要与其他维度并列呈现。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> The Sortino Ratio avoids penalizing variation above a chosen target in the same way as shortfall. It can be more intuitive for asymmetric returns, but its value depends strongly on the target, downside-deviation convention, and sample window, so it is not an unconditional upgrade over Sharpe.

Define a minimum acceptable return and downside deviation while separating the Sortino numerator benchmark, denominator convention, and annualization boundary.

### 01 / Concept Boundary

#### MAR Is An Economic Assumption, Not A Cosmetic Parameter

The minimum acceptable return, MAR, may be zero, a cash return, a liability growth rate, or an investor hurdle, but it must match each observation period. The numerator usually subtracts MAR from average portfolio return, while the denominator accumulates squared shortfalls only when R_t<MAR.

References and software use different denominators for downside deviation: some divide by all n periods and others only by the number of shortfall periods. Those outputs are not directly comparable. This lesson uses the all-observation convention, so periods without a shortfall contribute zero.

- **Sortino Ratio With All-Observation Downside Deviation**

  ```latex
  \operatorname{Sortino}=\frac{\mathbb{E}[R_p]-\operatorname{MAR}}{\operatorname{DD}_{\operatorname{MAR}}},\qquad \operatorname{DD}_{\operatorname{MAR}}=\sqrt{\mathbb{E}\!\left[\min(R_p-\operatorname{MAR},0)^2\right]}
  ```

### 02 / Mechanics And Measurement

#### Changing The Target Moves Both Numerator And Denominator

Raising MAR does more than subtract a larger constant: it reclassifies more observations as shortfalls and enlarges each gap. The same strategy can therefore rank very differently under another target, which must be set before inspecting results rather than adjusted afterward to improve the ratio.

An annualized version can be constructed when periods are independent, the target scales consistently, and the distribution is stable. Overlapping returns, dynamic targets, and volatility clustering invalidate simple square-root scaling. When the denominator approaches zero, report shortfall count and magnitude instead of a deceptively precise enormous ratio.

| Convention | Denominator Meaning | Use Note |
| --- | --- | --- |
| All periods | Mean squared shortfall across all periods, with zeros otherwise | Keep n consistent across samples |
| Shortfall periods only | Mean squared gap conditional on a shortfall | Shortfall frequency is removed from the denominator |
| Semivariance | Lower half around a mean or stated target | The center must be explicit |

### 03 / Reading Workflow

#### Write The Target Policy Before Computing Downside Performance

A reproducible process stores the period-by-period MAR series, shortfall flag, and shortfall magnitude. That separates rare deep losses from frequent shallow misses and prevents the final ratio from erasing path information.

- Set the MAR's economic meaning, currency, and compounding frequency before viewing strategy results.
- Align return, cost, valuation-time, and missing-data rules.
- Choose all periods or shortfall-only periods for the denominator and label it permanently.
- Output shortfall frequency, average shortfall, deepest shortfall, and rolling Sortino together.
- Run sensitivity across alternative MAR values and unseen samples without selecting the target by its best result.

### 04 / Risk Boundary

#### Ignoring Upside Variation Does Not Remove Valuation, Liquidity, Or Tail Problems

Sortino still depends on historical observations and can be distorted by smoothed marks, short samples, and a handful of tail events. For options or insurance-selling profiles, the distribution below the target can be highly unstable, and one second-moment statistic cannot express jumps, gaps, or the margin path.

If a strategy has almost no historical shortfalls, a tiny denominator does not imply tiny risk; the stress regime may simply be absent. Pair the ratio with expected shortfall, maximum drawdown, scenario revaluation, and liquidity capacity rather than using it to justify more leverage.

- For an unusually high Sortino, inspect the denominator, shortfall count, and sample length first.
- Align MAR and downside-deviation denominator conventions before comparing strategies.
- Display shortfall depth and frequency separately so one ratio cannot hide two risks.
- The metric does not forecast returns or justify increasing risk exposure.

## Related Concepts

- [[sharpe-ratio|Sharpe Ratio: Excess Return Per Unit Of Total Volatility]] — Sortino replaces the denominator while the reading is still compared with Sharpe.
- [[expected-shortfall-cvar|CVaR / Expected Shortfall: Average Loss Beyond A Quantile]] — Focusing only on downside deviation still says nothing about how fat the tail is.
- [[calmar-ratio-maximum-drawdown|Calmar Ratio And Maximum Drawdown: Returning Growth To Its Path]] — Both metrics use a drawdown-related quantity as the risk measure.
- [[multi-metric-risk-dashboard|Multi-Metric Risk Dashboard: Aligning Return, Tail, Path, Sensitivity, And Liquidity]] — A single downside metric is insufficient and must sit beside other dimensions.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cfa-risk-adjusted-performance
- finra-risk
- nist-distributions
