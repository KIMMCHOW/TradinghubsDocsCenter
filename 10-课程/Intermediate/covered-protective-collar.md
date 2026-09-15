---
title: "Covered、Protective 与 Collar 结构"
title_en: "Covered, Protective, And Collar Structures"
slug: "covered-protective-collar"
type: lesson
level: Intermediate
order: 30
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "19 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "Covered、Protective 与 Collar 结构"
  - "Covered, Protective, And Collar Structures"
  - "covered-protective-collar"
source_url: "https://tradinghubs.org/docs/trading-knowledge/covered-protective-collar"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# Covered、Protective 与 Collar 结构

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[no-arbitrage-and-synthetics|无套利边界与合成头寸]] ｜ 下一课：[[vertical-ratio-backspread|垂直价差、Ratio Spread 与 Backspread]]

**中级 · 结构、定价与波动率 · 19 分钟**

> 给标的持仓加一条期权腿并不会让风险消失，只会改变风险的形状与现金流时间。名称中的“Covered”或“Protective”也不能代替逐状态计算。

比较 Covered Call、Protective Put 与 Collar 如何重塑标的持仓的上行、下行、权利金与行权结果，并用合成关系识别隐藏敞口。

### 01 / 三种结构

#### Covered Call 让出执行价以上上行，Protective Put 买入下行地板

Covered Call 由 Long Underlying 与 Short Call 组成。收到的权利金可以缓冲一小部分下跌，但标的继续下跌时，大部分下行风险仍然存在；上涨超过 Call 执行价后，组合上行被 Short Call 抵消，并可能发生指派交付。

Protective Put 由 Long Underlying 与 Long Put 组成。Put 在执行价以下提供到期价值地板，但其权利金与持续滚动成本会降低其他状态的净结果。Collar 再卖出一个较高执行价 Call，以部分补偿 Put 成本，同时限制上行。

- **Covered Call 到期价值**

  ```latex
  S_T-\max(S_T-K_C,0)
  ```

- **Protective Put 到期价值**

  ```latex
  S_T+\max(K_P-S_T,0)
  ```

- **Collar 到期价值**

  ```latex
  S_T+\max(K_P-S_T,0)-\max(S_T-K_C,0),\quad K_P<K_C
  ```

| 结构 | 主要改变 | 仍然保留 |
| --- | --- | --- |
| Covered Call | 收取权利金并限制执行价以上上行。 | 接近完整的标的下行风险。 |
| Protective Put | 买入执行价以下的到期地板。 | 保险成本、Basis 与行权流程。 |
| Collar | 同时定义下方地板和上方封顶。 | 两腿期限、偏斜与执行风险。 |

### 02 / 合成视角

#### Parity 揭示“收益增强”背后的 Short Put 风险

在相同执行价、到期和欧式假设下，Long Call、Short Put 与执行价现金腿精确复制的是预付远期。连续收益率 q 会降低该预付远期的当前价值；实际股票则支付现货价，并保留期间股息权利。因此 Protective Put 与 Covered Call 若用实际股票表达，必须把实际股票与预付远期之间的股息权利价值单列，不能把折现标的项直接称为 Long Stock。

到期前，结构的 Delta、Gamma、Theta 与 Vega 会随价格、IV 和时间变化。Short Call 还涉及股息日前提前指派，Long Put 可能受 Bid / Ask 与波动率偏斜影响；用最初收取或支付的净权利金描述全程风险是不完整的。

- 合成等价针对现金流，不保证税务、保证金或提前行权结果相同。
- “零成本 Collar”只描述初始净权利金接近零，不代表没有机会成本或尾部风险。
- 不同到期或不同标的单位会破坏简单的一对一复制。

- **连续收益率下的预付远期**

  ```latex
  F_{0,T}^{P}=S_0e^{-qT}
  ```

- **实际持股 Protective Put 价值拆分**

  ```latex
  S_0+P=C+Ke^{-rT}+\left(S_0-F_{0,T}^{P}\right)
  ```

- **实际持股 Covered Call 价值拆分**

  ```latex
  S_0-C=Ke^{-rT}-P+\left(S_0-F_{0,T}^{P}\right)
  ```

### 03 / 结构阅读

#### 按下行、区间、上行和到期后仓位逐层检查

先把标的成本基础、期权净权利金、执行价、到期、乘数和股息列在同一张表，再计算大跌、区间、上涨至 Short Call 以上三种到期现金流。对 Collar 还要分别观察 Put Skew 与 Call Skew 对成本的贡献。

随后列出提前指派、Put 行权、两腿均失效和部分成交后的持仓。若结构需要滚动，必须把关闭旧腿与建立新腿的双重价差、期限变化和新执行价风险加入分析。

- 第一步：把初始现金流与标的成本基础分开记录。
- 第二步：逐区间计算到期价值，并用合成关系复核隐藏敞口。
- 第三步：加入股息、指派、滚动、成交与结算后的仓位情景。
- 这些结构用于教学比较，不代表适合任何特定投资目标或账户。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Adding an option leg to an underlying position does not erase risk; it changes the shape and timing of cash flows. Words such as covered or protective cannot replace state-by-state calculation.

Compare how covered calls, protective puts, and collars reshape an underlying position's upside, downside, premium, and exercise outcomes, using synthetic relationships to reveal hidden exposure.

### 01 / Three Structures

#### A Covered Call Gives Up Upside Above The Strike; A Protective Put Buys A Downside Floor

A covered call combines a long underlying position with a short call. Premium can cushion a small decline, but most downside remains if the underlying keeps falling; above the call strike, the short call offsets further upside and may result in assignment delivery.

A protective put combines long underlying with a long put. The put provides a terminal value floor below its strike, but premium and recurring roll cost reduce net results elsewhere. A collar adds a short higher-strike call to offset part of the put cost while limiting upside.

- **Covered-call terminal value**

  ```latex
  S_T-\max(S_T-K_C,0)
  ```

- **Protective-put terminal value**

  ```latex
  S_T+\max(K_P-S_T,0)
  ```

- **Collar terminal value**

  ```latex
  S_T+\max(K_P-S_T,0)-\max(S_T-K_C,0),\quad K_P<K_C
  ```

| Structure | Main Change | Still Retains |
| --- | --- | --- |
| Covered call | Collects premium and caps upside above the strike. | Nearly full underlying downside risk. |
| Protective put | Buys a terminal floor below the strike. | Insurance cost, basis, and exercise mechanics. |
| Collar | Defines a lower floor and an upper cap. | Two-leg expiry, skew, and execution risk. |

### 02 / Synthetic View

#### Parity Reveals The Short-Put Risk Behind An Income Label

With aligned strike, expiry, and European assumptions, the long-call, short-put, and strike-cash relationship exactly replicates a prepaid forward. Continuous yield q reduces that prepaid forward's current value; an actual share instead costs spot and retains interim dividend rights. Protective-put and covered-call identities written with actual stock must therefore show the dividend-entitlement value between stock and the prepaid forward separately rather than calling the discounted-underlying term long stock.

Before expiry, structure delta, gamma, theta, and vega change with price, IV, and time. A short call also carries early-assignment risk around dividends, while a long put can be affected by bid-ask and skew; describing the full lifecycle only by initial net premium is incomplete.

- Synthetic equivalence applies to cash flows, not identical tax, margin, or early-exercise outcomes.
- A zero-cost collar describes near-zero initial net premium, not zero opportunity cost or tail risk.
- Different expiries or underlying units break simple one-for-one replication.

- **Prepaid forward under continuous yield**

  ```latex
  F_{0,T}^{P}=S_0e^{-qT}
  ```

- **Actual-stock protective-put value decomposition**

  ```latex
  S_0+P=C+Ke^{-rT}+\left(S_0-F_{0,T}^{P}\right)
  ```

- **Actual-stock covered-call value decomposition**

  ```latex
  S_0-C=Ke^{-rT}-P+\left(S_0-F_{0,T}^{P}\right)
  ```

### 03 / Structure Reading

#### Check Downside, Range, Upside, And Post-Expiry Positions Separately

Place underlying cost basis, net option premium, strikes, expiry, multiplier, and dividends in one table, then calculate terminal cash flows for a large decline, a range outcome, and a rise above the short-call strike. For a collar, inspect put skew and call skew contributions separately.

Then enumerate positions after early call assignment, put exercise, both options expiring, and partial execution. If the structure is rolled, include the double spread from closing old legs and opening new ones, the maturity change, and the new strike risk.

- Step 1: Record initial option cash flows separately from underlying cost basis.
- Step 2: Calculate terminal value by price region and cross-check hidden exposure with synthetics.
- Step 3: Add dividend, assignment, roll, execution, and post-settlement position scenarios.
- These structures are compared for education and are not represented as suitable for any particular objective or account.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

