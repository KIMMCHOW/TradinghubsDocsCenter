---
title: "行权、指派、结算与 Pin Risk"
title_en: "Exercise, Assignment, Settlement, And Pin Risk"
slug: "exercise-assignment-settlement-pin-risk"
type: lesson
level: Beginner
order: 11
track: options-foundations
track_label: "期权基础与合约"
reading_time: "17 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/期权基础与合约"
  - "权限/需登录"
aliases:
  - "行权、指派、结算与 Pin Risk"
  - "Exercise, Assignment, Settlement, And Pin Risk"
  - "exercise-assignment-settlement-pin-risk"
source_url: "https://tradinghubs.org/docs/trading-knowledge/exercise-assignment-settlement-pin-risk"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# 行权、指派、结算与 Pin Risk

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[options-foundations|期权基础与合约]]
> 上一课：[[single-leg-payoff|单腿盈亏结构]] ｜ 下一课：[[liquidity-slippage-execution|流动性、滑点与期权执行]]

**初级 · 期权基础与合约 · 17 分钟**

> 到期盈亏图只画出了终点价格关系，没有画出通知时间、自动行权规则、盘后价格变化和资金占用。真正的到期管理必须把这些操作事实放回图中。

沿着到期前、行权截止、指派与结算的时间线理解持仓如何变成现金或标的敞口，以及为什么临近执行价时仍可能留下隔夜风险。

### 01 / 生命周期

#### 欧式与美式描述行权时间，不描述风险大小

欧式期权通常只能在到期时行权，美式期权通常可在到期前行权。买方决定是否提交行权，卖方则可能在分配流程中收到指派；卖方无法预先选择由哪一位买方触发自己的指派。

交易场所、清算机构和经纪服务可能有不同的截止时间、自动行权阈值与例外申请流程。屏幕显示“价内”不等于所有账户都会得到相同处理，课程中的通用规则不能替代当前合约规范和账户通知。

| 阶段 | 需要确认 | 常见遗漏 |
| --- | --- | --- |
| 到期前 | 剩余外在价值、股息、借券与资金需求。 | 只看到期盈亏图。 |
| 行权截止 | 通知时间、阈值与例外流程。 | 把收盘价当作最终决定。 |
| 结算后 | 现金流、标的数量、保证金与下一个交易时段。 | 忘记新产生的标的仓位。 |

### 02 / 结算与提前行权

#### 实物与现金结算改变交付内容，外在价值改变提前行权判断

实物结算可能把期权转换为标的多头或空头，现金结算则按规定的结算值支付差额。指数、期货期权与股票期权还可能采用不同的最后交易时间和结算价格计算方式，因此同样的到期图不代表同样的运营结果。

提前行权会放弃尚存的外在价值，所以不能只凭“深度价内”判断。股息、融资成本、借券可得性、Put 的利息价值和账户限制都可能改变比较；较稳妥的分析是把继续持有、卖出期权和行权三种可执行现金流放在同一时间点比较。

- 股息日前的 Short Call 指派风险可能上升，但不是所有价内 Call 都会被指派。
- 卖出平仓与行权是不同流程，报价、费用和交割结果也不同。
- 任何通用示例都必须让位于具体合约和账户规则。

- **简化的行权价值比较**

  ```latex
  \text{Exercise advantage}=\text{Immediate cash-flow benefit}-\text{Lost extrinsic value}-\text{Financing and delivery costs}
  ```

### 03 / Pin Risk

#### 靠近执行价时，最危险的往往不是曲线，而是结果不确定

当标的在到期时靠近执行价，微小价格变化就可能改变某些合约是否被行权。盘后消息、不同的结算参考、持有人例外指令和分配结果会让卖方直到较晚才知道最终标的敞口，这就是 Pin Risk 的核心。

多腿结构也不会自动消除该风险：如果一腿被行权而另一腿没有，原本看似封顶的组合可能暂时变成标的仓位或单腿期权。到期管理要按每条腿分别列出可能结果，而不是只看组合的理论净图形。

- 第一步：读取合约的最后交易时间、结算方式、自动行权与例外截止规则。
- 第二步：按“全部行权、部分行权、均不行权”列出每条腿的结算后敞口。
- 第三步：检查盘后变动、资金、保证金和下一时段的风险承受能力。
- 本课解释操作风险，不提供应持有到期或提前平仓的建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> An expiration payoff chart shows only the terminal price relationship. It omits notice timing, automatic-exercise rules, after-hours moves, and funding needs. Real expiration management must put those operating facts back into the picture.

Follow the pre-expiry, exercise-cutoff, assignment, and settlement timeline to understand how positions become cash or underlying exposure and why risk can remain near the strike.

### 01 / Lifecycle

#### European And American Describe Exercise Timing, Not Risk Size

European options are generally exercisable only at expiry, while American options are generally exercisable before expiry. The holder decides whether to exercise; a writer may then receive assignment through an allocation process and cannot choose which holder triggers it.

Venues, clearing organizations, and brokerage services may use different cutoffs, automatic-exercise thresholds, and exception procedures. A screen label of in the money does not guarantee identical treatment across accounts; general course rules cannot replace current contract specifications and account notices.

| Stage | What To Confirm | Common Omission |
| --- | --- | --- |
| Before expiry | Remaining extrinsic value, dividends, borrow, and funding. | Looking only at the expiry payoff. |
| Exercise cutoff | Notice time, threshold, and exception process. | Treating the close as the final decision. |
| After settlement | Cash flow, underlying quantity, margin, and the next session. | Forgetting the newly created underlying position. |

### 02 / Settlement And Early Exercise

#### Physical Versus Cash Settlement Changes Delivery; Extrinsic Value Changes Exercise Logic

Physical settlement may turn an option into a long or short underlying position, while cash settlement pays a difference based on a defined settlement value. Index, futures, and equity options can also use different last-trading times and settlement calculations, so identical payoff diagrams do not imply identical operating outcomes.

Early exercise gives up remaining extrinsic value, so deep in the money alone is not enough. Dividends, financing costs, borrow availability, the interest value of a put, and account constraints can change the comparison; a sounder analysis aligns the executable cash flows from holding, selling, and exercising at the same time.

- Short-call assignment risk may rise before an ex-dividend date, but not every in-the-money call will be assigned.
- Selling to close and exercising are different processes with different quotes, fees, and delivery outcomes.
- Any general example must yield to the actual contract and account rules.

- **Simplified exercise-value comparison**

  ```latex
  \text{Exercise advantage}=\text{Immediate cash-flow benefit}-\text{Lost extrinsic value}-\text{Financing and delivery costs}
  ```

### 03 / Pin Risk

#### Near The Strike, Outcome Uncertainty Can Matter More Than The Curve

When the underlying finishes near a strike, a small move can change whether some contracts are exercised. After-hours news, different settlement references, holder exceptions, and allocation outcomes can leave a writer uncertain about final underlying exposure until later; that uncertainty is the core of pin risk.

Multi-leg structures do not automatically remove this risk. If one leg is exercised and another is not, a seemingly bounded package can temporarily become an underlying position or a single option. Expiry management should enumerate outcomes leg by leg rather than relying only on the theoretical net diagram.

- Step 1: Read the contract's last-trading time, settlement method, automatic-exercise rule, and exception cutoff.
- Step 2: Map each leg's post-settlement exposure under all, partial, and no-exercise outcomes.
- Step 3: Check after-hours movement, funding, margin, and next-session risk capacity.
- This lesson explains operating risk and does not advise holding to expiry or closing early.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

