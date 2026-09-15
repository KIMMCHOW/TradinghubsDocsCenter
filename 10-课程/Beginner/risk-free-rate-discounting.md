---
title: "无风险利率、贴现与时间价值"
title_en: "Risk-Free Rates, Discounting, And Time Value"
slug: "risk-free-rate-discounting"
type: lesson
level: Beginner
order: 4
track: markets-macro-and-behavior
track_label: "市场、宏观与行为"
reading_time: "15 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/市场、宏观与行为"
  - "权限/需登录"
aliases:
  - "无风险利率、贴现与时间价值"
  - "Risk-Free Rates, Discounting, And Time Value"
  - "risk-free-rate-discounting"
source_url: "https://tradinghubs.org/docs/trading-knowledge/risk-free-rate-discounting"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-market-data.ts"
generated: 2026-09-15
---

# 无风险利率、贴现与时间价值

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[markets-macro-and-behavior|市场、宏观与行为]]
> 上一课：[[expected-utility-opportunity-cost|期望效用、机会成本与风险收益]] ｜ 下一课：[[business-cycle-labor-indicators|商业周期与劳动力市场指标]]

**初级 · 市场、宏观与行为 · 15 分钟**

> “无风险”是特定币种、期限、抵押与市场约定下的定价基准，不是所有投资者都能无限借入或贷出的真实账户利率。

理解贴现因子、复利口径、期限匹配与无风险基准的实际含义，并把利率正确带入远期、债券和期权估值。

### 01 / 概念边界

#### 贴现把不同时点现金流换到同一计量时点

今天的一单位货币可以投资并在未来增长，所以未来确定现金流的今天价值通常低于其未来名义金额。贴现因子取决于币种、期限、利率曲线和复利约定；不能用一个隔夜利率贴现所有年份的现金流。

实际定价常使用与抵押、结算和币种相匹配的市场曲线。政府债券收益率、隔夜指数互换或融资利率各回答不同问题，把它们统称为同一个无风险利率会掩盖基差。

- **离散复利贴现**

  ```latex
  PV=\frac{CF_T}{(1+r/m)^{mT}}
  ```

- **连续复利贴现**

  ```latex
  PV=CF_Te^{-rT}
  ```

| 输入 | 必须匹配 | 常见错误 |
| --- | --- | --- |
| 币种 | 现金流计价币种 | 用美元曲线贴现其他币种 |
| 期限 | 现金流日期 | 用单一期限利率覆盖整条曲线 |
| 复利 | 报价与公式口径 | 百分比、年化和日计数混用 |

### 02 / 机制与度量

#### 利率影响现值、远期价格和期权相对价值

没有持有收益时，融资成本会让远期价格相对现货随时间增长；股息、便利收益或其他持有收益会抵消一部分融资成本。期权定价中的 Rho 描述小幅利率变化的局部敏感度，但曲线形状和隐含波动率也可能同步变化。

报价利率不等于净可获得收益。税费、信用、抵押品、借贷差、日计数和提前现金流都会改变实际结果，因此估值输入与账户融资应分开记录。

- **连续持有成本远期关系**

  ```latex
  F_{0,T}=S_0e^{(r-q)T}
  ```
  q 表示连续持有收益；现实合约还需检查融资、借券、结算和基差。

- **局部 Rho 近似**

  ```latex
  \Delta V\approx\rho\,\Delta r
  ```

| 利率变化渠道 | 直接影响 | 需要联动观察 |
| --- | --- | --- |
| 贴现 | 未来现金流现值 | 期限与曲线节点 |
| 融资 / Carry | 现货—远期关系 | 股息、借券与储存 |
| 期权 Rho | 理论价值局部变化 | IV、期限与行权方式 |

### 03 / 阅读流程

#### 用五项对齐检查利率输入

利率错误常不是公式错误，而是输入的币种、期限或复利口径没有对齐。先核对定义，再运行敏感度。

- 1. 对齐估值日、现金流日、时区和日计数。
- 2. 对齐币种、抵押或结算安排及对应曲线。
- 3. 把百分数转为小数，并明确单利、离散复利或连续复利。
- 4. 分别冲击平行利率、短端和长端，避免只做单点 Rho。
- 5. 将模型曲线与账户真实融资、借券和费用分开对账。

### 04 / 风险边界

#### 无风险基准不消除信用、流动性或再投资风险

政府证券也会随收益率变化产生市值波动，长久期现金流对小幅利率变化尤其敏感。不同市场参与者面对的融资价差不同，理论无套利关系可能被资本、借券和资产负债表约束隔开。

- 不把信用较低等同于价格不会波动。
- 不把模型基准利率当作账户可交易利率。
- 不忽略曲线非平行移动和期限错配。

- 贴现率上升通常压低固定未来现金流的现值。
- 远期与期权反应取决于融资、持有收益、期限和合约类型的组合。
- Rho 是局部敏感度，不是完整利率情景损益。
- 本课不构成债券、现金工具或利率方向建议。

## 相关概念

- [[rates-treasuries-central-bank-transmission|利率、国债与央行传导]] — 贴现率来自政策利率与期限溢价，而不是一个固定常数。
- [[forwards-futures-basis-cost-of-carry|远期、期货、基差与持有成本：从现货到股指公平价值]] — 同一贴现逻辑决定远期价格中的持有成本与基差。
- [[rho-rate-sensitivity|Rho：利率敏感度为什么通常排在最后]] — 贴现率变化对期权价格的敏感度就是 Rho。
- [[phi-foreign-rate-sensitivity|Foreign Rho / Phi：外币利率与持有收益敏感度]] — 引入第二种货币时，第二个利率进入贴现，形成 Phi 敞口。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Risk-free is a pricing benchmark under a specific currency, maturity, collateral, and market convention. It is not an account rate at which every investor can borrow or lend without limit.

Understand discount factors, compounding conventions, maturity matching, and the practical meaning of a risk-free benchmark, then apply rates correctly to forwards, bonds, and options.

### 01 / Concept Boundary

#### Discounting Converts Cash Flows To A Common Valuation Date

One unit of currency today can be invested and grow, so a certain future cash flow is generally worth less today than its future nominal amount. The discount factor depends on currency, maturity, the rate curve, and compounding convention; one overnight rate cannot discount every future year.

Practical valuation uses curves aligned with collateral, settlement, and currency. Government yields, overnight-indexed swaps, and funding rates answer different questions. Calling them one identical risk-free rate hides basis differences.

- **Discrete-compounding discounting**

  ```latex
  PV=\frac{CF_T}{(1+r/m)^{mT}}
  ```

- **Continuous-compounding discounting**

  ```latex
  PV=CF_Te^{-rT}
  ```

| Input | Must Match | Common Error |
| --- | --- | --- |
| Currency | Cash-flow currency | Using a USD curve for another currency |
| Maturity | Cash-flow date | Using one tenor for the whole curve |
| Compounding | Quote and formula convention | Mixing percent, annualization, and day count |

### 02 / Mechanics And Measurement

#### Rates Affect Present Value, Forward Price, And Relative Option Value

Without carry income, financing makes forward price grow relative to spot through time; dividends, convenience yield, or other holding benefits offset part of that cost. Option rho measures local sensitivity to a small rate change, but the curve shape and implied volatility can move at the same time.

A quoted rate is not the net yield an account can realize. Taxes, fees, credit, collateral, borrowing spreads, day count, and interim cash flows change the result, so valuation inputs and account financing should be recorded separately.

- **Continuous carry relationship**

  ```latex
  F_{0,T}=S_0e^{(r-q)T}
  ```
  q is continuous carry income; real contracts still require funding, borrow, settlement, and basis checks.

- **Local rho approximation**

  ```latex
  \Delta V\approx\rho\,\Delta r
  ```

| Rate Channel | Direct Effect | Observe Together |
| --- | --- | --- |
| Discounting | Present value of future cash flows | Maturity and curve nodes |
| Funding / Carry | Spot-forward relationship | Dividends, borrow, and storage |
| Option rho | Local theoretical-value change | IV, maturity, and exercise style |

### 03 / Reading Workflow

#### Validate A Rate Input With Five Alignments

Rate mistakes often come not from the formula but from mismatched currency, tenor, or compounding. Validate definitions before running sensitivity.

- 1. Align valuation date, cash-flow date, timezone, and day count.
- 2. Align currency, collateral or settlement arrangement, and the corresponding curve.
- 3. Convert percentages to decimals and specify simple, discrete, or continuous compounding.
- 4. Shock parallel rates, the front end, and the long end separately rather than using one-point rho only.
- 5. Reconcile the model curve separately from actual account funding, borrow, and fees.

### 04 / Risk Boundary

#### A Risk-Free Benchmark Does Not Remove Credit, Liquidity, Or Reinvestment Risk

Government securities can fluctuate in market value as yields move, and long-duration cash flows are especially sensitive to small rate changes. Participants face different funding spreads, so capital, borrow, and balance-sheet constraints can separate theoretical no-arbitrage relations from executable trades.

- Do not equate low credit risk with no price volatility.
- Do not treat a model benchmark as the account's executable rate.
- Do not ignore nonparallel curve moves or maturity mismatch.

- A higher discount rate generally lowers the present value of fixed future cash flows.
- Forward and option responses depend jointly on financing, carry income, maturity, and contract type.
- Rho is a local sensitivity, not complete rate-scenario P&L.
- This lesson is not advice on bonds, cash instruments, or rate direction.

## Related Concepts

- [[rates-treasuries-central-bank-transmission|Rates, Treasuries, And Central-Bank Transmission]] — The discount rate comes from the policy rate plus a term premium, not from a fixed constant.
- [[forwards-futures-basis-cost-of-carry|Forwards, Futures, Basis, And Cost Of Carry: From Spot To Equity-Index Fair Value]] — The same discounting logic sets the cost of carry and basis inside a forward price.
- [[rho-rate-sensitivity|Rho: Why Rate Sensitivity Usually Comes Last]] — The sensitivity of an option price to the discount rate is rho.
- [[phi-foreign-rate-sensitivity|Foreign Rho / Phi: Foreign-Rate And Carry Sensitivity]] — With a second currency, a second rate enters discounting and creates phi exposure.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- treasury-marketable-securities
- federal-reserve-monetary-policy
