---
title: "无套利边界与合成头寸"
title_en: "No-Arbitrage Bounds And Synthetic Positions"
slug: "no-arbitrage-and-synthetics"
type: lesson
level: Intermediate
order: 29
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "20 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "无套利边界与合成头寸"
  - "No-Arbitrage Bounds And Synthetic Positions"
  - "no-arbitrage-and-synthetics"
source_url: "https://tradinghubs.org/docs/trading-knowledge/no-arbitrage-and-synthetics"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# 无套利边界与合成头寸

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[option-spread-structures|价差与组合结构]] ｜ 下一课：[[covered-protective-collar|Covered、Protective 与 Collar 结构]]

**中级 · 结构、定价与波动率 · 20 分钟**

> 无套利不是“价格看起来不一样就下单”，而是：如果两组可执行现金流在所有相关状态都相同，它们的净现值就应在成本范围内接近。复制思维首先是一种错误检查工具。

通过复制相同到期现金流理解合成多头、合成空头、Conversion、Reversal 与 Box，并识别理论等价在真实成交中的边界。

### 01 / 复制语言

#### 把腿的名称翻译成到期现金流

同执行价、同到期的 Long Call 与 Short Put 组合，在到期时随标的价格变化一比一，但还差一笔执行价现金流。加入执行价现值后，该组合复制的是到期交付一单位标的的预付远期；在连续收益率 q 下，其当前价值是公式中的折现标的项，不是支付现货价并收取期间股息的实际股票。

合成关系的价值在于拆解：当一个组合看似复杂时，可以用等价现金流看清它到底保留了方向、融资、波动率还是尾部风险。等价只针对定义好的到期和结算条件，不代表两组头寸在到期前拥有完全相同的保证金与流动性。

- **合成远期多头**

  ```latex
  C(K,T)-P(K,T)=e^{-rT}(F_{0,T}-K)
  ```

- **Call-Put 加现金复制预付远期**

  ```latex
  C-P+Ke^{-rT}=F_{0,T}^{P}=S_0e^{-qT}
  ```

- **同价宽跨式的到期绝对值**

  ```latex
  C_T+P_T=|S_T-K|
  ```

| 组合 | 简化现金流 | 仍需核对 |
| --- | --- | --- |
| Long Call − Long Put | 同执行价远期多头。 | 融资、股息、风格与结算。 |
| Prepaid Forward + Long Put | Long Call 加执行价现金腿。 | 实际持股还需加入期间股息权利。 |
| Prepaid Forward − Long Call | Short Put 加执行价现金腿。 | 下行风险、实际股息和指派。 |

### 02 / 锁定现金流

#### Conversion、Reversal 与 Box 主要表达融资关系

Conversion 通常由 Long Stock、Long Put 与 Short Call 组成；Reversal 将这些方向反转。若执行价与到期完全对齐，标的方向风险在理论上被抵消，剩余价值主要反映执行价现金流、股息、借券和融资。

Box 可由一个 Bull Call Spread 与一个 Bear Put Spread 组合，到期支付执行价宽度。其理论现值类似零息现金流，但真实回报会受所有腿的 Bid / Ask、费用、保证金、提前指派、税务和结算违约流程影响。

- 报价中间价组合不等于能同时成交的组合价格。
- 美式腿的提前指派可能打断原本锁定的融资结构。
- 借券紧张或股息预期变化会改变合成标的关系。

- **欧式 Box 到期支付**

  ```latex
  \text{Box payoff}=K_2-K_1
  ```

- **简化理论现值**

  ```latex
  \text{Box PV}=(K_2-K_1)e^{-rT}
  ```

### 03 / 核验流程

#### 从可执行净现金流验证，而不是从截图差值验证

先对齐标的、到期、执行价、期权风格、乘数和结算单位；再为买入腿使用 Ask、卖出腿使用 Bid，并加入手续费、融资、股息和借券。只有各状态的净现金流仍一致，才进入保证金和操作风险检查。

即使理论差值为正，也要确认所有腿能否同步成交、报价是否陈旧、规模是否足够以及到期前是否会出现指派。无套利等式适合发现数据、输入或理解错误，但不保证现实中存在可获取的无风险收益。

- 第一步：逐状态写出每条腿到期现金流，确认复制目标确实一致。
- 第二步：改用可成交 Bid / Ask，并加入融资、股息、借券、费用与保证金。
- 第三步：压力测试提前指派、部分成交和结算差异。
- 合成关系用于理解与核验，不构成实施套利组合的建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> No-arbitrage does not mean trade whenever two screen prices look different. It means that if two executable cash-flow sets match across all relevant states, their present values should be close within costs. Replication is first an error-checking tool.

Use matching terminal cash flows to understand synthetic longs, synthetic shorts, conversions, reversals, and boxes, while recognizing where theoretical equivalence meets real execution constraints.

### 01 / Replication Language

#### Translate Leg Names Into Terminal Cash Flows

A long call and short put at the same strike and expiry move one-for-one with the underlying at maturity, but differ by the strike cash flow. Adding the present value of the strike replicates a prepaid forward delivering one unit at expiry. With continuous yield q, its current value is the discounted-underlying term shown below, not an actual share bought at spot with interim dividends attached.

Synthetic relationships simplify complex packages by showing whether direction, financing, volatility, or tail risk remains. Equivalence applies to defined maturity and settlement conditions; it does not mean the two positions have identical margin and liquidity before expiry.

- **Synthetic long forward**

  ```latex
  C(K,T)-P(K,T)=e^{-rT}(F_{0,T}-K)
  ```

- **Call-put plus cash replicates a prepaid forward**

  ```latex
  C-P+Ke^{-rT}=F_{0,T}^{P}=S_0e^{-qT}
  ```

- **Same-strike straddle terminal value**

  ```latex
  C_T+P_T=|S_T-K|
  ```

| Package | Simplified Cash Flow | Still Requires Checking |
| --- | --- | --- |
| Long call − long put | Long forward at the shared strike. | Financing, dividends, style, and settlement. |
| Prepaid forward + long put | Long call plus a strike cash leg. | Actual stock also requires its interim dividend entitlement. |
| Prepaid forward − long call | Short put plus a strike cash leg. | Downside risk, actual dividends, and assignment. |

### 02 / Locked Cash Flows

#### Conversions, Reversals, And Boxes Primarily Express Financing Relationships

A conversion commonly combines long stock, long put, and short call; a reversal flips those directions. With perfectly aligned strikes and expiry, theoretical underlying direction cancels, leaving value driven mainly by strike cash flows, dividends, borrow, and financing.

A box can combine a bull call spread with a bear put spread and pays the strike width at expiry. Its theoretical present value resembles a zero-coupon cash flow, but realized return is affected by bid-ask on every leg, fees, margin, early assignment, tax, and settlement-default procedures.

- A package assembled from midpoint quotes is not necessarily executable.
- Early assignment on American legs can interrupt an otherwise locked financing structure.
- Tight borrow or changed dividend expectations can alter synthetic-underlying relationships.

- **European box terminal payment**

  ```latex
  \text{Box payoff}=K_2-K_1
  ```

- **Simplified theoretical present value**

  ```latex
  \text{Box PV}=(K_2-K_1)e^{-rT}
  ```

### 03 / Validation Workflow

#### Validate Executable Net Cash Flows, Not Screenshot Differences

Align underlying, expiry, strike, exercise style, multiplier, and settlement unit. Then price buys at ask and sells at bid, adding fees, financing, dividends, and borrow. Only if net cash flows still match across states should the analysis proceed to margin and operating risk.

Even with a positive theoretical difference, confirm simultaneous execution, quote freshness, available size, and assignment risk before expiry. No-arbitrage equalities are excellent for detecting data, input, or reasoning errors, but do not guarantee an attainable risk-free return.

- Step 1: Write each leg's terminal cash flow by state and confirm that the replication target truly matches.
- Step 2: Replace mids with executable bid and ask, then add financing, dividends, borrow, fees, and margin.
- Step 3: Stress-test early assignment, partial fills, and settlement differences.
- Synthetic relationships are for understanding and validation, not a recommendation to implement an arbitrage package.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

