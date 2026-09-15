---
title: "Calendar、Diagonal、Butterfly、Condor 与 Iron Condor"
title_en: "Calendars, Diagonals, Butterflies, Condors, And Iron Condors"
slug: "calendar-diagonal-butterfly-condor"
type: lesson
level: Advanced
order: 80
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
  - "Calendar、Diagonal、Butterfly、Condor 与 Iron Condor"
  - "Calendars, Diagonals, Butterflies, Condors, And Iron Condors"
  - "calendar-diagonal-butterfly-condor"
source_url: "https://tradinghubs.org/docs/trading-knowledge/calendar-diagonal-butterfly-condor"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# Calendar、Diagonal、Butterfly、Condor 与 Iron Condor

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[charm-exposure-chex|CHEX：Charm Exposure 怎么看]] ｜ 下一课：[[christmas-tree-and-ladder-spreads|Christmas Tree 与 Ladder：先核对腿部口径]]

**高级 · 结构、定价与波动率 · 24 分钟**

> 这些名称常被归为“区间策略”，但其风险来源并不相同。跨期限组合依赖远期波动率与前腿到期时后腿的剩余价值；翼型组合则主要由多个执行价之间的离散曲率构成。

把跨期限结构与同期限翼型结构分开分析，理解 Calendar/Diagonal 的前端到期重估，以及 Butterfly/Condor/Iron Condor 的有限宽度与执行风险。

### 01 / 跨期限结构

#### Calendar 同执行价跨期限，Diagonal 同时跨执行价与期限

典型 Long Calendar 卖出较近到期的期权并买入同执行价较远到期的期权。前腿到期时，后腿仍有时间价值，因此组合没有只依赖最终标的价格的一条固定前端到期盈亏线；它还取决于当时后腿 IV、Skew 与剩余期限。

Diagonal 将后腿执行价也移开，叠加方向与偏斜差异。Long Calendar 常被概括为 Long Vega、Positive Theta，但这些标签会随标的远离执行价、期限结构倒挂、前腿接近到期和模型单位变化，不能当作永久符号。

下式中的 C(T1) 与 P(T1) 是前腿到期时后腿的市场价值，N(0) 是 Long Calendar 的带符号初始净成本：Debit 为正，Credit 为负，并按利率持有至 T1。同一理论标记下，Short Calendar 盈亏是对应 Long Calendar 的相反数；实际成交还会因 Bid / Ask、费用与指派而不完全对称。

远期方差只能用同一标的、同一年化口径和相同远期对数价差 k 的可比总方差切片相减，并要求 T_2>T_1 且 w(T_2,k) 不低于 w(T_1,k)。它是期限结构诊断，不是某一执行价 Calendar 的固定到期收益；若结果为负，应先检查曲面、插值和输入是否存在日历套利或口径错误。

- **Long Call Calendar 的前端到期盈亏**

  ```latex
  \Pi_C^{\mathrm{long}}(T_1)=C_{T_1}(K,T_2)-\max(S_{T_1}-K,0)-N_0e^{rT_1}
  ```

- **Long Put Calendar 的前端到期盈亏**

  ```latex
  \Pi_P^{\mathrm{long}}(T_1)=P_{T_1}(K,T_2)-\max(K-S_{T_1},0)-N_0e^{rT_1}
  ```

- **Short Calendar 是对应 Long Calendar 的反向**

  ```latex
  \Pi_{C,P}^{\mathrm{short}}(T_1)=-\Pi_{C,P}^{\mathrm{long}}(T_1)
  ```

- **可比切片间的远期方差**

  ```latex
  \sigma_{\mathrm{fwd}}^2(T_1,T_2;k)=\frac{w(T_2,k)-w(T_1,k)}{T_2-T_1},\qquad w(T,k)=\sigma_{\mathrm{imp}}^2(T,k)T
  ```

- **远期方差的期限条件**

  ```latex
  T_2>T_1,\qquad w(T_2,k)\geq w(T_1,k),\qquad k=\ln\!\left(\frac{K}{F_{0,T}}\right)
  ```

| 结构 | 对齐项 | 新增风险 |
| --- | --- | --- |
| Calendar | 通常执行价相同。 | 期限结构与后腿重估。 |
| Diagonal | 通常期权类型相同。 | 方向、Skew 与期限同时变化。 |
| 到期管理 | 前腿先结束。 | 指派后可能留下后腿与标的。 |

### 02 / 同期限翼型

#### Butterfly 集中中间执行价，Condor 拉开中间区间

对等宽 Call Butterfly，可买入一个低执行价 Call、卖出两个中间执行价 Call、再买入一个高执行价 Call。它把到期价值集中在中间附近；若翼宽不等或数量变化，峰值与尾部不再具有标准对称形状。

Condor 使用四个递增执行价并把两个中间执行价分开，形成更宽的中间平台。Iron Condor 通常组合一个 Put Vertical 与一个 Call Vertical，可用 Credit 形式表达类似的有限区间风险，但提前指派、现金流、流动性和保证金路径与全 Call/Put 版本并不完全相同。

- “最大损失有限”依赖所有保护翼真实存在、数量正确且结算一致。
- 临近中间 Short Strike 时，Gamma、Pin Risk 与指派不确定性可能快速上升。
- 多腿初始 Credit 不等于高概率，也不描述尾部损失相对收益的比例。

- **等宽 Call Butterfly 到期价值**

  ```latex
  (S_T-K_1)^+-2(S_T-K_2)^++(S_T-K_3)^+,\quad K_2-K_1=K_3-K_2
  ```

- **Call Condor 到期价值**

  ```latex
  (S_T-K_1)^+-(S_T-K_2)^+-(S_T-K_3)^++(S_T-K_4)^+
  ```

- **Iron Condor 简化最大宽度**

  ```latex
  \text{Maximum wing width}=\max(K_{P,\mathrm{short}}-K_{P,\mathrm{long}},\ K_{C,\mathrm{long}}-K_{C,\mathrm{short}})
  ```

### 03 / 分层核验

#### 跨期限先做重估，翼型先做区间现金流，再统一检查执行

Calendar 与 Diagonal 应在前腿到期时对后腿做价格 × IV × Skew 情景重估，并检查期限总方差与事件位置。Butterfly、Condor 与 Iron Condor 则先按执行价区间写出净斜率、翼宽、初始净权利金和保护腿数量。

所有结构最后都要加入多腿 Bid / Ask、部分成交、前腿指派、Pin Risk、保证金和滚动成本。策略名称不能证明订单输入正确；逐腿确认类型、方向、数量、执行价、到期和乘数是不可省略的操作检查。

- 第一步：先判断结构是跨期限风险还是同期限执行价几何，使用不同的主图。
- 第二步：跨期限做后腿重估；翼型做逐区间现金流和保护翼核对。
- 第三步：统一压力测试 IV、Skew、时间、部分成交、指派和结算后的仓位。
- 多腿结构可能复杂且成本敏感，本课不推荐特定组合、执行价、期限或持有方式。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> These names are often grouped as range strategies, but their risk sources differ. Cross-expiry packages depend on forward volatility and the back leg's residual value when the front expires; wing structures are primarily discrete curvature across several strikes.

Analyze cross-expiry structures separately from same-expiry wing structures, including front-expiry revaluation for calendars and diagonals and bounded-width geometry for butterflies, condors, and iron condors.

### 01 / Cross-Expiry Structures

#### A Calendar Spans Expiries At One Strike; A Diagonal Spans Strikes And Expiries

A typical long calendar sells a nearer-expiry option and buys a farther-expiry option at the same strike. When the front leg expires, the back leg still has time value, so the package has no single front-expiry payoff determined only by underlying price; it also depends on back-leg IV, skew, and remaining time.

A diagonal also shifts the back-leg strike, adding direction and skew differences. A long calendar is often summarized as long vega and positive theta, but those labels can change as spot moves away from strike, term structure inverts, the front leg nears expiry, or model conventions differ.

In the formulas below, C(T1) and P(T1) are the back-leg market values when the front expires. N(0) is the signed initial net cost of the long calendar: a debit is positive, a credit negative, and it is carried to T1 at the interest rate. At the same theoretical marks, a short calendar has the opposite P&L; actual execution is not perfectly symmetric after bid-ask, fees, and assignment.

Forward variance can be subtracted only from comparable total-variance slices for the same underlying, annualization convention, and forward log-moneyness k, with T_2>T_1 and w(T_2,k) no lower than w(T_1,k). It is a term-structure diagnostic, not the fixed terminal payoff of a calendar at one strike. A negative result calls for checks of the surface, interpolation, and inputs for calendar arbitrage or convention errors.

- **Long call calendar P&L at front expiry**

  ```latex
  \Pi_C^{\mathrm{long}}(T_1)=C_{T_1}(K,T_2)-\max(S_{T_1}-K,0)-N_0e^{rT_1}
  ```

- **Long put calendar P&L at front expiry**

  ```latex
  \Pi_P^{\mathrm{long}}(T_1)=P_{T_1}(K,T_2)-\max(K-S_{T_1},0)-N_0e^{rT_1}
  ```

- **A short calendar reverses its matching long calendar**

  ```latex
  \Pi_{C,P}^{\mathrm{short}}(T_1)=-\Pi_{C,P}^{\mathrm{long}}(T_1)
  ```

- **Forward variance between comparable slices**

  ```latex
  \sigma_{\mathrm{fwd}}^2(T_1,T_2;k)=\frac{w(T_2,k)-w(T_1,k)}{T_2-T_1},\qquad w(T,k)=\sigma_{\mathrm{imp}}^2(T,k)T
  ```

- **Maturity conditions for forward variance**

  ```latex
  T_2>T_1,\qquad w(T_2,k)\geq w(T_1,k),\qquad k=\ln\!\left(\frac{K}{F_{0,T}}\right)
  ```

| Structure | Aligned Dimension | Additional Risk |
| --- | --- | --- |
| Calendar | Usually shares one strike. | Term structure and back-leg revaluation. |
| Diagonal | Usually shares the option type. | Direction, skew, and term all change. |
| Expiry management | The front leg ends first. | Assignment can leave the back leg plus underlying. |

### 02 / Same-Expiry Wings

#### A Butterfly Concentrates The Middle Strike; A Condor Widens The Middle

An equal-width call butterfly can buy one low-strike call, sell two middle-strike calls, and buy one high-strike call. It concentrates terminal value near the middle; unequal wings or changed quantities remove the standard symmetric peak and tail shape.

A condor uses four increasing strikes and separates the two middle strikes, creating a wider central plateau. An iron condor commonly combines a put vertical and a call vertical, often expressing a similar bounded range through a credit, but early assignment, cash flow, liquidity, and margin paths differ from an all-call or all-put version.

- A bounded maximum loss depends on every protective wing existing, having the correct quantity, and settling consistently.
- Near a middle short strike, gamma, pin risk, and assignment uncertainty can rise quickly.
- An initial multi-leg credit does not equal high probability and does not describe tail loss relative to reward.

- **Equal-width call-butterfly terminal value**

  ```latex
  (S_T-K_1)^+-2(S_T-K_2)^++(S_T-K_3)^+,\quad K_2-K_1=K_3-K_2
  ```

- **Call-condor terminal value**

  ```latex
  (S_T-K_1)^+-(S_T-K_2)^+-(S_T-K_3)^++(S_T-K_4)^+
  ```

- **Simplified iron-condor maximum width**

  ```latex
  \text{Maximum wing width}=\max(K_{P,\mathrm{short}}-K_{P,\mathrm{long}},\ K_{C,\mathrm{long}}-K_{C,\mathrm{short}})
  ```

### 03 / Layered Validation

#### Revalue Cross-Expiry Structures; Map Wing Cash Flows; Then Check Execution

Calendars and diagonals require price-by-IV-by-skew revaluation of the back leg at front expiry, with checks on total term variance and event placement. Butterflies, condors, and iron condors begin with net slope by strike region, wing width, initial net premium, and protective-leg quantities.

Every structure then needs multi-leg bid-ask, partial fills, front-leg assignment, pin risk, margin, and roll costs. A strategy name cannot prove the ticket is correct; leg-by-leg confirmation of type, side, quantity, strike, expiry, and multiplier is an essential operating check.

- Step 1: Classify the package as cross-expiry risk or same-expiry strike geometry and use the appropriate primary map.
- Step 2: Revalue the back leg for cross-expiry packages; map regional cash flows and protective wings for wing structures.
- Step 3: Stress-test IV, skew, time, partial fills, assignment, and post-settlement positions.
- Multi-leg structures can be complex and cost-sensitive; this lesson recommends no package, strike, expiry, or holding method.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

