---
title: "期望效用、机会成本与风险收益"
title_en: "Expected Utility, Opportunity Cost, And Risk-Reward"
slug: "expected-utility-opportunity-cost"
type: lesson
level: Beginner
order: 3
track: markets-macro-and-behavior
track_label: "市场、宏观与行为"
reading_time: "16 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/市场、宏观与行为"
  - "权限/需登录"
aliases:
  - "期望效用、机会成本与风险收益"
  - "Expected Utility, Opportunity Cost, And Risk-Reward"
  - "expected-utility-opportunity-cost"
source_url: "https://tradinghubs.org/docs/trading-knowledge/expected-utility-opportunity-cost"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-market-data.ts"
generated: 2026-09-15
---

# 期望效用、机会成本与风险收益

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[markets-macro-and-behavior|市场、宏观与行为]]
> 上一课：[[price-discovery-market-clearing|价格发现与市场出清]] ｜ 下一课：[[risk-free-rate-discounting|无风险利率、贴现与时间价值]]

**初级 · 市场、宏观与行为 · 16 分钟**

> 风险收益比只描述某种情景的几何关系；没有概率、仓位大小、资金约束和替代方案，它不能回答“是否值得做”。

从概率加权结果、资金效用与最佳替代方案出发评估交易，而不是用胜率、赔率或最大盈利中的单一数字替代决策。

### 01 / 概念边界

#### 期望值衡量平均结果，效用衡量结果对账户的意义

期望收益把互斥情景按概率加权；期望效用进一步承认同样的金额变化对不同财富水平、回撤状态和目标约束可能意义不同。风险厌恶并不是拒绝一切波动，而是要求额外风险有足够补偿。

机会成本是选择当前方案时放弃的最佳可行替代方案价值。现金、较小仓位、不同期限或完全不交易都可能是替代方案；已经发生且无法收回的成本不应改变未来增量决策。

- **离散情景期望收益**

  ```latex
  \mathbb{E}[R]=\sum_{i=1}^{n}p_iR_i,\quad \sum_i p_i=1
  ```

- **期望效用**

  ```latex
  \mathbb{E}[U]=\sum_{i=1}^{n}p_i\,u(W+\Pi_i)
  ```

| 指标 | 有用之处 | 缺失信息 |
| --- | --- | --- |
| 胜率 | 结果频率 | 盈亏大小与尾部 |
| 盈亏比 | 选定止损止盈的几何 | 触发概率与滑点 |
| 期望值 | 长期平均贡献 | 路径、资本约束与估计误差 |

### 02 / 机制与度量

#### 仓位大小把抽象概率转换为生存问题

两个正期望策略可能因损失分布和相关性不同而需要完全不同的仓位。少数极端损失可以抵消大量小盈利；在有限资本和保证金约束下，先触发强平的策略无法等待长期平均实现。

概率不是固定真值，而是基于样本、模型和当前状态的估计。应对基准概率做乐观、基准和悲观三套敏感度，并把费用、滑点、跳空和无法按计划退出纳入损益。

- **单笔账户风险**

  ```latex
  \text{Account Risk}=\text{Position Size}\times\text{Loss Per Unit}
  ```

- **机会成本**

  ```latex
  OC(a)=\max_{b\in\mathcal{F}}V(b)-V(a)
  ```

| 情景 | 必须估计 | 压力项 |
| --- | --- | --- |
| 正常退出 | 概率与净收益 | 费用与滑点上升 |
| 不利延伸 | 最大计划损失 | 跳空越过止损 |
| 相关性冲击 | 组合同时亏损 | 流动性共同收缩 |

### 03 / 阅读流程

#### 先写完整情景表，再决定是否占用风险预算

事前流程的价值在于迫使自己写出可被证伪的概率、损益和退出假设，而不是在结果出现后为它寻找解释。

- 1. 列出至少三个互斥情景，并确保概率总和为 1。
- 2. 用可执行价格计算每个情景的净损益，不使用理论 Mid 代替。
- 3. 同时计算期望值、最坏合理损失、保证金占用和组合相关冲击。
- 4. 与现金、减仓或其他方案比较；没有明显优势时，不交易也是有效选择。

### 04 / 风险边界

#### 估计误差可能比公式本身更重要

小样本胜率、回测选择偏差和状态变化都会让期望值失真。效用函数也不是客观市场参数，而是账户目标与风险政策的表达；它不能把不可靠概率变成可靠决策。

- 对概率和损益同时做压力测试，不只调一个输入。
- 把相关持仓视为一个风险簇，而不是多笔独立交易。
- 最大计划损失不是跳空、流动性和系统故障下的保证上限。

- 正期望不等于每次盈利，也不等于任何仓位都合理。
- 机会成本要求把“不交易”和“更小仓位”放进比较集。
- 风险收益判断应在交易前固定，并在新信息出现时按规则更新。
- 本课不提供个性化仓位或收益目标。

## 相关概念

- [[risk-free-rate-discounting|无风险利率、贴现与时间价值]] — 机会成本需要一个可比较的无风险替代方案作为基准。
- [[sunk-cost-commitment-escalation|沉没成本与承诺升级]] — 效用应用于从当前时点开始的增量结果，而不是已发生成本。
- [[sharpe-ratio|Sharpe Ratio：单位总波动的超额收益]] — 效用框架解释了为什么单看收益率不足以评价一个结果。
- [[anchoring-framing-trading-decisions|锚定、框架与交易决策]] — 主观价值会被参考点扭曲，因此实际决策常偏离效用计算。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> A reward-to-risk ratio describes the geometry of selected scenarios. Without probabilities, size, capital constraints, and alternatives, it cannot answer whether a trade is worth taking.

Evaluate a trade through probability-weighted outcomes, utility of capital, and the best alternative instead of replacing the decision with win rate, payoff ratio, or maximum profit alone.

### 01 / Concept Boundary

#### Expectation Measures Average Outcome; Utility Measures Its Meaning To The Account

Expected return probability-weights mutually exclusive outcomes. Expected utility additionally recognizes that the same monetary change can matter differently at different wealth levels, drawdown states, and goal constraints. Risk aversion does not reject all volatility; it requires sufficient compensation for added risk.

Opportunity cost is the value of the best feasible alternative forgone by choosing the current action. Cash, smaller size, another horizon, or no trade can all be alternatives. A cost already incurred and unrecoverable should not alter the forward incremental decision.

- **Expected return across discrete scenarios**

  ```latex
  \mathbb{E}[R]=\sum_{i=1}^{n}p_iR_i,\quad \sum_i p_i=1
  ```

- **Expected utility**

  ```latex
  \mathbb{E}[U]=\sum_{i=1}^{n}p_i\,u(W+\Pi_i)
  ```

| Measure | Useful For | Missing Information |
| --- | --- | --- |
| Win rate | Outcome frequency | Payoff size and tails |
| Payoff ratio | Geometry of selected exits | Trigger probability and slippage |
| Expected value | Long-run average contribution | Path, capital limits, and estimation error |

### 02 / Mechanics And Measurement

#### Position Size Turns Abstract Probabilities Into A Survival Problem

Two positive-expectation strategies can require very different sizes because loss distributions and correlations differ. A few extreme losses can erase many small gains; under finite capital and margin constraints, a strategy liquidated first cannot wait for its long-run average.

Probability is not a fixed truth; it is estimated from samples, models, and current regimes. Stress optimistic, base, and pessimistic probabilities, and include fees, slippage, gaps, and failure to exit as planned.

- **Account risk per trade**

  ```latex
  \text{Account Risk}=\text{Position Size}\times\text{Loss Per Unit}
  ```

- **Opportunity cost**

  ```latex
  OC(a)=\max_{b\in\mathcal{F}}V(b)-V(a)
  ```

| Scenario | Must Estimate | Stress Item |
| --- | --- | --- |
| Normal exit | Probability and net payoff | Higher fees and slippage |
| Adverse extension | Maximum planned loss | Gap through the stop |
| Correlation shock | Concurrent portfolio loss | Joint liquidity contraction |

### 03 / Reading Workflow

#### Write The Full Scenario Table Before Spending Risk Budget

The value of a pre-trade process is forcing falsifiable probability, payoff, and exit assumptions before the outcome, rather than finding explanations afterward.

- 1. List at least three mutually exclusive scenarios whose probabilities sum to one.
- 2. Calculate net payoff at executable prices rather than substituting theoretical mid.
- 3. Compute expectation, worst reasonable loss, margin use, and portfolio correlation shock together.
- 4. Compare with cash, smaller size, and alternatives; no trade is valid when advantage is unclear.

### 04 / Risk Boundary

#### Estimation Error Can Matter More Than The Formula

Small-sample win rates, backtest selection bias, and regime changes can distort expectation. A utility function is not an objective market parameter; it expresses account goals and risk policy. It cannot turn unreliable probabilities into a reliable decision.

- Stress probabilities and payoffs together, not one input alone.
- Treat correlated positions as one risk cluster, not independent trades.
- Maximum planned loss is not a guaranteed cap under gaps, illiquidity, or system failure.

- Positive expectation means neither every trade wins nor every size is sensible.
- Opportunity cost requires including no trade and smaller size in the comparison set.
- Risk-reward judgments should be fixed before entry and updated by rule when new information arrives.
- This lesson provides no personalized position size or return target.

## Related Concepts

- [[risk-free-rate-discounting|Risk-Free Rates, Discounting, And Time Value]] — Opportunity cost needs a comparable risk-free alternative as its benchmark.
- [[sunk-cost-commitment-escalation|Sunk Costs And Escalation Of Commitment]] — Utility applies to incremental outcomes from the current decision point, not to costs already incurred.
- [[sharpe-ratio|Sharpe Ratio: Excess Return Per Unit Of Total Volatility]] — The utility frame explains why a raw return is not enough to evaluate an outcome.
- [[anchoring-framing-trading-decisions|Anchoring, Framing, And Trading Decisions]] — Subjective value is distorted by reference points, so real decisions drift from the utility calculation.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- finra-risk
- cfa-risk-adjusted-performance
