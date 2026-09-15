---
title: "做市商对冲：Delta 中性与 Gamma 再平衡"
title_en: "Market-Maker Hedging: Delta Neutrality And Gamma Rebalancing"
slug: "market-maker-flow"
type: lesson
level: Intermediate
order: 42
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "16 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "做市商对冲：Delta 中性与 Gamma 再平衡"
  - "Market-Maker Hedging: Delta Neutrality And Gamma Rebalancing"
  - "market-maker-flow"
source_url: "https://tradinghubs.org/docs/trading-knowledge/market-maker-flow"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 做市商对冲：Delta 中性与 Gamma 再平衡

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[dte-window-selection|DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选]] ｜ 下一课：[[options-flow-direction|Flow：期权成交分类怎么读]]

**中级 · 做市商定位与期权敞口 · 16 分钟**

> 做市商的核心工作不是预测方向，而是在成为成交对手方时管理库存风险。公开的 OI 与 Volume 本身不能证明做市商持仓方向；对期货交易员来说，关键是先确认持仓归属假设，再讨论这些风险何时可能变成标的、ETF 或对应期货上的对冲流。

分清交易者 Flow 与做市商对冲，用 1,000 张 Call 的例子理解 Delta 中性、Gamma 再平衡和期货传导。

### 01 / 两类力量

#### 交易者 Flow 和做市商对冲要分开看

Flow 字段通常按成交主动侧把交易分类为 Call 买入、Put 买入、Call 卖出或 Put 卖出，但它不自动说明开仓、平仓、多腿意图或最终对手方。做市商对冲则是在已知库存方向后，为让风险回到目标范围而买卖标的资产、相关 ETF、现货篮子或对应期货。

所以“有人买 Call”不等于“期货一定上涨”。先问这笔成交是开仓还是平仓、是否属于多腿组合、最终对手方是谁；只有这些信息明确时，才能继续计算某一已知持仓的 Delta、Gamma 与对冲需求。

- 第一条近似只在成交被识别为客户开仓且做市商为对手方时成立。
- 只有 OI 或 Volume 时，库存方向必须标记为未知。

- **条件式库存变化**

  ```latex
  \Delta I_{\mathrm{dealer},[t_0,t_1]}\approx-F_{\mathrm{customer,opening}}^{\mathrm{signed}}
  ```

- **简化对冲目标**

  ```latex
  \Delta_{\text{hedge}}\approx-\Delta_{\text{dealer book}}
  ```

### 02 / 手算例子

#### 卖出 1,000 张 Call 后，做市商可能需要买入标的风险

假设某个机构在标的价格为 200 美元时，向你买入 1,000 张看涨期权，每张 Delta 为 0.4。本例只讨论标准美股期权，并令合约乘数 M_contract = 100；期货期权与其他产品必须查阅各自合约规范，不能照搬 100。这个手算例子与 ODV 页面显示值无关。

在这个明确的假设里，你作为做市商卖出了这些 Call，因此期权库存 Delta 约为 -40,000 个等价标的单位。为了接近 Delta 中性，你可能需要买入相同数量的等价标的风险；若改用 ETF 或期货，必须再按相应合约规格换算。

- **初始期权库存 Delta**

  ```latex
  \text{Position }\Delta=-1{,}000\times0.4\times M_{\mathrm{contract}},\quad M_{\mathrm{contract}}=100\Rightarrow-40{,}000
  ```

- **初始对冲规模**

  ```latex
  \text{Equivalent Underlying Units}=40{,}000
  ```

- 在这个标准美股期权例子里，若标的小幅上涨 1 美元且 Delta 近似不变，空期权库存的一阶损益约为 -40,000 美元，等价标的对冲约为 +40,000 美元。
- 这个例子说明对冲流可能出现在相关期货上，而不是只留在期权链里。

### 03 / Gamma 再平衡

#### 真正麻烦的是价格变动后 Delta 会变

沿用这个 M_contract = 100 的标准美股期权例子，假设标的从 200 美元涨到 205 美元，该 Call 的 Delta 从 0.4 升到 0.5。空期权库存 Delta 从 -40,000 变成 -50,000 个等价标的单位，原对冲不再足够。

为了重新接近中性，这个已知空 Call 持仓需要再买入约 10,000 个等价标的单位。只有其他交易商也持有相似方向的已知库存并选择相似对冲工具时，相关 ETF 或期货才可能出现同类机械性流；公开 Flow、OI 或 ODV 暴露符号本身不能证明这些条件成立。

- **新库存 Delta**

  ```latex
  \text{New Position }\Delta=-1{,}000\times0.5\times M_{\mathrm{contract}},\quad M_{\mathrm{contract}}=100\Rightarrow-50{,}000
  ```

- **新增对冲需求**

  ```latex
  \text{Additional Equivalent Units}=50{,}000-40{,}000=10{,}000
  ```

### 04 / 回到 ODV

#### GEX 和 Greeks Profile 用来寻找模型敏感度集中区

ODV 的 GEX、DEX、VEX 与 CHEX 是各窗口的预计算模型值，用来定位敏感度集中区；其正负号不能单独证明 dealer 库存或未来对冲方向。上面的 M_contract = 100 只是独立的标准美股期权手算例子，不是页面值的复算方法。

| 页面观察 | 可支持的读法 | 边界 |
| --- | --- | --- |
| 显示值为正 | 只表示当前模型的正号口径。 | 不能据此推断 dealer Long Gamma 或卖出对冲。 |
| 显示值为负 | 只表示当前模型的负号口径。 | 不能据此推断 dealer Short Gamma 或买入对冲。 |
| 同一视图内条形较宽 | 表示该行权价相对同视图其他行权价更突出。 | 不可跨标的、指标、DTE 或快照比较绝对值。 |

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> A market maker's core job is not predicting direction but managing inventory when acting as a trade counterparty. Public OI and volume alone do not reveal dealer positioning; futures traders must state the ownership assumption before asking when that risk might become hedging flow in the underlying, ETF, or related futures.

Separate trader flow from dealer hedging, then use a 1,000-call example to understand delta neutrality, gamma rebalancing, and futures transmission.

### 01 / Two Forces

#### Trader Flow And Dealer Hedging Must Be Separated

Flow fields commonly classify trades by aggressor side as call buys, put buys, call sells, or put sells, but they do not automatically reveal opening versus closing, multi-leg intent, or the final counterparty. Dealer hedging is the later purchase or sale of the underlying, related ETFs, cash baskets, or futures after inventory direction is known.

'Someone bought calls' does not mean futures must rise. First ask whether the trade opens or closes risk, whether it belongs to a multi-leg package, and who the final counterparty is. Only with those facts can delta, gamma, and hedge needs for a known position be calculated.

- The first approximation applies only when the trade is identified as customer opening flow with a dealer as counterparty.
- With OI or volume alone, inventory direction must remain unknown.

- **Conditional inventory change**

  ```latex
  \Delta I_{\mathrm{dealer},[t_0,t_1]}\approx-F_{\mathrm{customer,opening}}^{\mathrm{signed}}
  ```

- **Simplified hedge target**

  ```latex
  \Delta_{\text{hedge}}\approx-\Delta_{\text{dealer book}}
  ```

### 02 / Manual Example

#### After Selling 1,000 Calls, A Dealer May Need To Buy Underlying Exposure

Suppose an institution buys 1,000 call options from you while the reference price is 200 and each option has delta of 0.4. This example is limited to a standard US equity option with contract multiplier M_contract = 100. Futures options and other products require their own contract specifications; 100 must not be carried over. This manual example is separate from ODV display values.

Under this explicit assumption, you are the dealer who sold the calls, so the option inventory delta is about -40,000 equivalent underlying units. Moving toward delta neutrality may require buying the same amount of equivalent underlying exposure; an ETF or futures hedge requires a separate conversion using its own contract specification.

- **Initial option inventory delta**

  ```latex
  \text{Position }\Delta=-1{,}000\times0.4\times M_{\mathrm{contract}},\quad M_{\mathrm{contract}}=100\Rightarrow-40{,}000
  ```

- **Initial hedge size**

  ```latex
  \text{Equivalent Underlying Units}=40{,}000
  ```

- In this standard US equity-option example, if the underlying rises by one dollar and delta is locally stable, the short option inventory has first-order P&L of about -40,000 dollars and the equivalent underlying hedge about +40,000 dollars.
- This example shows why hedging flow can appear in related futures, not only inside the option chain.

### 03 / Gamma Rebalancing

#### The Hard Part Is That Delta Changes After Price Moves

Continuing the standard US equity-option example with M_contract = 100, suppose the reference price rises from 200 to 205 and call delta increases from 0.4 to 0.5. The short option inventory delta moves from -40,000 to -50,000 equivalent underlying units, so the original hedge is no longer enough.

Returning this known short-call position toward neutrality requires about 10,000 additional equivalent underlying units. Similar mechanical flow may reach related ETFs or futures only if other dealers hold comparable known inventory and choose comparable hedge instruments. Public flow, OI, or an ODV exposure sign does not establish those conditions.

- **New inventory delta**

  ```latex
  \text{New Position }\Delta=-1{,}000\times0.5\times M_{\mathrm{contract}},\quad M_{\mathrm{contract}}=100\Rightarrow-50{,}000
  ```

- **Additional hedge demand**

  ```latex
  \text{Additional Equivalent Units}=50{,}000-40{,}000=10{,}000
  ```

### 04 / Back To ODV

#### GEX And Greeks Profile Locate Model-Sensitivity Clusters

ODV GEX, DEX, VEX, and CHEX are precomputed model values for each window and help locate sensitivity clusters. Their signs alone do not establish dealer inventory or future hedge direction. The M_contract = 100 calculation above is an independent standard US equity-option example, not a way to reproduce page values.

| Page Observation | Supported Reading | Boundary |
| --- | --- | --- |
| Displayed value is positive | It records the positive side of the current model convention. | It does not establish long dealer gamma or selling hedges. |
| Displayed value is negative | It records the negative side of the current model convention. | It does not establish short dealer gamma or buying hedges. |
| A wider bar within one view | That strike is more prominent relative to other strikes in the same view. | Do not compare raw magnitude across symbols, metrics, DTE windows, or snapshots. |

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

