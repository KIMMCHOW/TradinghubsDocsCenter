---
title: "沉没成本与承诺升级"
title_en: "Sunk Costs And Escalation Of Commitment"
slug: "sunk-cost-commitment-escalation"
type: lesson
level: Beginner
order: 7
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
  - "沉没成本与承诺升级"
  - "Sunk Costs And Escalation Of Commitment"
  - "sunk-cost-commitment-escalation"
source_url: "https://tradinghubs.org/docs/trading-knowledge/sunk-cost-commitment-escalation"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-market-data.ts"
generated: 2026-09-15
---

# 沉没成本与承诺升级

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[markets-macro-and-behavior|市场、宏观与行为]]
> 上一课：[[anchoring-framing-trading-decisions|锚定、框架与交易决策]] ｜ 下一课：[[options-contract-and-quote|期权基础：合约与报价]]

**初级 · 市场、宏观与行为 · 16 分钟**

> 市场不会因为账户已经亏损就提高下一笔交易的胜率。每个调整都应作为一项从当前时点开始的新决策接受比较。

把不可收回的过去成本与未来可变现金流分开，识别加仓、展期和延迟退出何时是在维护旧叙事而非提高未来价值。

### 01 / 概念边界

#### 沉没成本已经无法改变，承诺升级却会增加未来暴露

沉没成本是无论下一步做什么都无法收回的时间、费用或损失。它可以用于复盘，却不应进入两个未来方案的增量比较。仍可避免的费用、平仓冲击、税务后果、剩余权利金和切换成本则属于未来现金流，不能被误删。

承诺升级发生在坏消息出现后，决策者继续投入更多资金、时间或声誉，以证明原决定正确。交易中的摊低成本、反复展期、延后失效标准和把短线改称长期投资，都可能是升级，也可能是合理再配置；区别在于新证据和未来回报是否独立支持该动作。

| 成本类型 | 从现在能否改变？ | 决策处理 |
| --- | --- | --- |
| 已支付手续费 / 已实现损失 | 否 | 用于复盘，不加入未来增量价值 |
| 剩余权利金 / 当前清算价值 | 是 | 按当前机会成本计入 |
| 未来手续费、滑点与融资 | 是 | 加入每个替代方案 |

### 02 / 机制与度量

#### 只比较从当前时点开始的增量价值和风险

将继续持有、减仓、退出、展期与替代头寸都视为今天可选择的方案。对每个方案使用相同情景、概率、期限和资金约束，计算未来收益减未来成本；原始入场支出不因方案而变，因此在比较中相消。

承诺升级常借助选择性更新：有利证据被称为趋势确认，不利证据被称为暂时噪声。解决方法是预先规定什么证据会增加、降低或终止暴露，并由未参与原决策的人做一次反方评估。

- **未来增量价值**

  ```latex
  \Delta V_{future}(a)=\sum_s p_s\,[B_s(a)-C_s(a)]-OC(a)
  ```
  a 是从现在可选的行动，B_s 与 C_s 是未来收益与成本，OC 是占用资本的机会成本；已经不可收回的成本不在式中。

| 调整 | 合理证据 | 升级警报 |
| --- | --- | --- |
| 加仓 | 赔率改善且组合风险仍合规 | 唯一理由是降低平均成本 |
| 展期 | 新合约独立优于退出与替代 | 隐藏已实现损失或延迟复盘 |
| 延长时间 | 原催化剂时点有新可验证信息 | 失效日期反复后移 |

### 03 / 阅读流程

#### 把每次调整作为一张新的投资备忘录

调整前先暂时隐藏累计盈亏，只保留当前可平仓价值、未来现金流与组合约束。完成独立判断后再恢复历史记录，用于检验原流程而不是为新风险辩护。

- 1. 将过去支出分成不可收回成本、当前可变价值与未来可避免成本。
- 2. 同时列出持有、缩小、退出、展期和最佳替代方案。
- 3. 在共同情景下比较增量期望值、最大损失、保证金与组合相关性。
- 4. 要求一条不含“回本”“证明”或“已经投入很多”的正向理由。
- 5. 记录决定、反方意见、下一次复核条件和不可再扩大的规模上限。

### 04 / 风险边界

#### 退出也有真实成本，去沉没成本不等于机械止损

买卖价差、税务、市场冲击、夜盘跳空和多腿执行都可能使立即退出不是最佳动作。正确做法是把这些未来后果显式纳入比较，而不是因为“过去不重要”就假设退出免费，也不是因为退出昂贵就无限延长承诺。

- 不把亏损头寸自动诊断为沉没成本错误。
- 不通过增加杠杆来追赶预设回本时间。
- 不把展期后的新合约与原合约视为同一个决策。

- 沉没成本影响行为，不会直接改变证券的未来现金流。
- 承诺升级会把原本有限的判断错误转化为组合级风险。
- 独立比较替代方案比围绕成本价寻找理由更稳健。
- 本课不提供个性化止损、加仓或税务指令。

## 相关概念

- [[expected-utility-opportunity-cost|期望效用、机会成本与风险收益]] — 正确基准是从当前时点开始的增量结果与机会成本。
- [[anchoring-framing-trading-decisions|锚定、框架与交易决策]] — 成本锚点让亏损仓位被持续重新解释为「还没结束」。
- [[discrete-hedging-error-transaction-costs|离散对冲误差与交易成本：连续理论如何落到有限成交]] — 对冲与调整决策同样应忽略已发生成本，只看剩余敞口与增量成本。
- [[calmar-ratio-maximum-drawdown|Calmar Ratio 与最大回撤：把复合增长放回路径中]] — 承诺升级的代价最终体现在回撤幅度与恢复时间上。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> The market does not raise the probability of the next trade because an account has already lost money. Every adjustment should be evaluated as a new decision from the current moment.

Separate unrecoverable past costs from variable future cash flows, and recognize when adding, rolling, or delaying exit protects an old narrative rather than improving forward value.

### 01 / Concept Boundary

#### Sunk Costs Cannot Be Changed; Escalation Adds Future Exposure

A sunk cost is time, expense, or loss that cannot be recovered regardless of the next action. It may inform a review, but it should not enter the incremental comparison of forward alternatives. Avoidable fees, exit impact, tax effects, remaining premium, and switching costs are future cash flows and must not be removed by mistake.

Escalation of commitment occurs when a decision-maker invests more money, time, or reputation after adverse evidence in order to vindicate the original choice. Averaging down, repeated rolls, postponed invalidation, and relabeling a short trade as a long investment can be escalation or rational reallocation. The difference is whether new evidence and forward return independently support the action.

| Cost Type | Changeable From Now? | Decision Treatment |
| --- | --- | --- |
| Paid fee / realized loss | No | Use for review, not forward incremental value |
| Remaining premium / liquidation value | Yes | Include at current opportunity cost |
| Future fees, impact, and funding | Yes | Include in each alternative |

### 02 / Mechanics And Measurement

#### Compare Only Incremental Forward Value And Risk From The Current Moment

Treat holding, reducing, exiting, rolling, and replacing as choices available today. Apply the same scenarios, probabilities, horizon, and capital constraints to each, then calculate future benefit minus future cost. The original entry outlay does not vary by alternative, so it cancels in the comparison.

Escalation often uses selective updating: favorable evidence is called trend confirmation, while adverse evidence is called temporary noise. Counter it by specifying in advance which evidence increases, reduces, or ends exposure, and have someone uninvolved in the original choice perform a dissenting review.

- **Forward incremental value**

  ```latex
  \Delta V_{future}(a)=\sum_s p_s\,[B_s(a)-C_s(a)]-OC(a)
  ```
  a is an action available now, B_s and C_s are future benefits and costs, and OC is the opportunity cost of committed capital; unrecoverable past cost is absent.

| Adjustment | Rational Evidence | Escalation Warning |
| --- | --- | --- |
| Add | Improved odds with portfolio risk still compliant | Only reason is lowering average cost |
| Roll | New contract independently beats exit and alternatives | Hides realized loss or delays review |
| Extend horizon | New verifiable timing evidence for the catalyst | Invalidation date repeatedly moves |

### 03 / Reading Workflow

#### Treat Every Adjustment As A New Investment Memo

Before adjusting, temporarily hide cumulative profit and loss and retain only current liquidation value, forward cash flows, and portfolio constraints. Restore history after the independent decision, using it to review the original process rather than justify new risk.

- 1. Split past outlays into unrecoverable cost, current variable value, and avoidable future cost.
- 2. List hold, reduce, exit, roll, and the best alternative at the same time.
- 3. Compare incremental expected value, maximum loss, margin, and portfolio correlation under common scenarios.
- 4. Require a forward reason that does not use get even, prove, or already invested heavily.
- 5. Record the decision, dissenting view, next review condition, and a hard no-more-additions size limit.

### 04 / Risk Boundary

#### Exit Has Real Costs; Ignoring Sunk Cost Does Not Mean Mechanical Stops

Bid-ask spread, taxes, market impact, overnight gaps, and multi-leg execution can make immediate exit suboptimal. Include those forward consequences explicitly rather than assuming exit is free because the past is irrelevant, or extending commitment indefinitely because exit is costly.

- Do not automatically diagnose every losing position as a sunk-cost error.
- Do not add leverage to meet a preset recovery deadline.
- Do not treat the rolled contract as the same decision as the original contract.

- Sunk cost affects behavior; it does not directly change a security's forward cash flows.
- Escalation can turn a bounded judgment error into portfolio-level risk.
- Independent comparison of alternatives is more robust than finding reasons around cost basis.
- This lesson does not provide personalized stop, sizing, or tax instructions.

## Related Concepts

- [[expected-utility-opportunity-cost|Expected Utility, Opportunity Cost, And Risk-Reward]] — The correct benchmark is incremental outcome and opportunity cost from the current decision point.
- [[anchoring-framing-trading-decisions|Anchoring, Framing, And Trading Decisions]] — A cost anchor keeps reinterpreting a losing position as "not over yet."
- [[discrete-hedging-error-transaction-costs|Discrete Hedging Error And Transaction Costs: Bringing Continuous Theory To Finite Trades]] — Hedging decisions should likewise ignore sunk cost and look only at residual exposure and incremental cost.
- [[calmar-ratio-maximum-drawdown|Calmar Ratio And Maximum Drawdown: Returning Growth To Its Path]] — Escalation of commitment ultimately shows up in drawdown depth and recovery time.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- investor-gov-behavior
- finra-risk
