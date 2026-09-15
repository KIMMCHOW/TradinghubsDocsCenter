---
title: "组合 Greeks 与节点聚合：先统一单位，再讨论净敞口"
title_en: "Portfolio Greeks And Node Aggregation: Align Units Before Net Exposure"
slug: "portfolio-greeks-node-aggregation"
type: lesson
level: Advanced
order: 65
track: risk-performance-and-hedging
track_label: "风险、绩效与对冲"
reading_time: "24 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/风险、绩效与对冲"
  - "权限/需登录"
aliases:
  - "组合 Greeks 与节点聚合：先统一单位，再讨论净敞口"
  - "Portfolio Greeks And Node Aggregation: Align Units Before Net Exposure"
  - "portfolio-greeks-node-aggregation"
source_url: "https://tradinghubs.org/docs/trading-knowledge/portfolio-greeks-node-aggregation"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# 组合 Greeks 与节点聚合：先统一单位，再讨论净敞口

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[risk-performance-and-hedging|风险、绩效与对冲]]
> 上一课：[[vega-exposure-vol-hedging|Vega Exposure 与 Vol Hedging]] ｜ 下一课：[[options-pnl-attribution|期权 P&L 归因：从起止重估到 Greek 解释残差]]

**高级 · 风险、绩效与对冲 · 24 分钟**

> 组合 Delta、Gamma、Vega 或 Theta 不是把屏幕数字直接相加。每条腿的方向、报价单位、合约乘数、币种、波动率点和时间单位都必须一致，而且总净额必须能下钻到关键节点。

按方向、数量、合约乘数和币种聚合组合 Greeks，并用标的、期限和波动率节点保留净额背后的集中风险。

### 01 / 概念边界

#### Greek 是局部导数，组合 Greek 是带单位的局部导数之和

令 q_i 为带方向的合约数量，M_i 为合约乘数，c_i 为本币现金转换到报告币种的汇率，g_i 为每单位标的、每个明确本地因子冲击单位的价格敏感度，并且明确不含合约乘数。若引擎输出每份合约 Greek，必须先除以 M_i 规范化，或在独立实现中把有效乘数设为 1，绝不能再次盲乘 M_i。

Vega 可能按波动率变化 1.00 或一个百分点 0.01 报告，Theta 可能按年、日历日或交易日报告，Gamma 也可能是每价格单位二阶导数或现金化情景量。原始单位 Delta 不能先乘汇率后跨不同标的直接求和；应按同一标的节点保留，或乘 S_i×1% 转为报告币种的一百分点现金 Delta。

- **同单位组合 Greek 聚合**

  ```latex
  G_{\mathrm{port}}=\sum_{i=1}^{n}q_i M_i c_i g_i
  ```
  该总和只适用于映射到同一因子节点、同一冲击单位的现金敏感度；g_i 不含 M_i。

- **同一标的节点的一百分点现金 Delta**

  ```latex
  \operatorname{CashDelta}_{1\%,b}=0.01\sum_{i\in b}q_iM_ic_i\Delta_iS_i
  ```
  节点 b 内的合约共享同一标的与本地现货冲击口径；结果单位为报告货币/标的上涨 1%。

| Greek | 聚合前必须确认 | 常见节点 |
| --- | --- | --- |
| Delta | 标的单位、乘数、币种 | 标的与期限 |
| Gamma | 价格冲击单位与是否美元化 | 标的、期限与执行价 |
| Vega | 每 1.00 还是每 1 波动率点 | 期限与曲面节点 |
| Theta | 时间流逝符号与日历单位 | 期限与事件日 |

### 02 / 机制与度量

#### 总净额会掩盖期限、执行价和曲面基差

节点聚合用指示函数把同一 Greek 分配到标的、到期、执行价区间或波动率曲面点。两个到期的 Vega 在当前平行移动下可能净额很小，但期限结构扭曲时会产生显著损益。

多因子局部二阶近似应使用冲击向量 Δx、梯度 g 与 Hessian H；每个现货、曲面节点、利率或时间因子都有自己的单位。只有单一标的加平行波动率冲击时，才可把它压缩成标量 Delta–Gamma–Vega 表达；大冲击仍需完整重估。跨标的相关对冲也不是同一风险因子的代数净额，必须在联合情景中检验。

- **节点 Greek**

  ```latex
  G_b=\sum_{i=1}^{n}\mathbf{1}\{i\in b\}\,q_iM_ic_ig_i
  ```
  节点 b 必须固定共同因子、冲击单位与币种转换时点。

- **多因子局部组合损益近似**

  ```latex
  \Delta V\approx \mathbf{g}^{\mathsf T}\Delta\mathbf{x}+\frac{1}{2}\Delta\mathbf{x}^{\mathsf T}\mathbf{H}\Delta\mathbf{x}
  ```
  g 与 H 必须按与 Δx 完全相同的因子顺序和冲击单位构造。

### 03 / 阅读流程

#### 逐腿规范化、逐节点对账、逐情景重估

从持仓与定价引擎导出每条腿的原始 Greek、定义和单位，转换到统一报告口径后再聚合。总计必须等于节点之和，节点又必须能回到逐腿贡献；任何无法解释的残差都应阻止发布。

- 冻结持仓、市场快照、模型版本和报告币种。
- 为每个 Greek 建立原始单位、乘数包含状态和目标单位映射。
- 按标的、到期、执行价与曲面节点聚合并验证节点和等于总计。
- 用小冲击差分检查解析 Greek，再用大冲击完整重估。
- 将净额、最大同向节点、对冲基差和数据失败同时展示。

### 04 / 风险边界

#### 局部净 Delta 或净 Vega 接近零不代表组合低风险

Greeks 只在当前状态附近描述一阶或高阶导数。现货跳跃、波动率曲面非平行移动、时间推进、相关性变化和执行价穿越都会让局部净额迅速改变。

模型、乘数、币种或单位错误会系统性污染全部聚合。组合对冲还面临流动性、离散再平衡、保证金和执行风险，因此节点 Greeks 必须与完整情景和现金需求一起使用。

- 先核对单位和乘数，再解释 Greek 的正负与大小。
- 总净额很小时，查看最大正负节点和期限错配。
- 局部近似与完整重估差异扩大时，升级到非线性情景。
- 组合 Greeks 是风险地图，不是损失上限或自动对冲指令。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Portfolio delta, gamma, vega, or theta is not the direct sum of screen values. Side, quote units, contract multiplier, currency, volatility-point convention, and time unit must align for every leg, and every net total must drill down to material nodes.

Aggregate portfolio Greeks by side, quantity, contract multiplier, and currency while preserving underlying, maturity, and volatility-node concentrations beneath the net total.

### 01 / Concept Boundary

#### A Greek Is A Local Derivative; A Portfolio Greek Is A Unit-Aware Sum

Let q_i be signed contract quantity, M_i the contract multiplier, c_i the conversion of local-currency cash into reporting currency, and g_i the price sensitivity per underlying unit and per explicitly stated local-factor shock unit, explicitly excluding the contract multiplier. If an engine returns a per-contract Greek, normalize it by dividing by M_i, or set the effective multiplier to one in a separate implementation; never multiply by M_i again blindly.

Vega may be quoted per 1.00 volatility change or per one percentage point, theta per year, calendar day, or trading day, and gamma as a second derivative per price unit or a cash-normalized scenario measure. Raw unit delta cannot be FX-converted and summed directly across different underlyings; retain it by common-underlying node or multiply by S_i times 1% to obtain one-percent cash delta in the reporting currency.

- **Same-Unit Portfolio Greek Aggregation**

  ```latex
  G_{\mathrm{port}}=\sum_{i=1}^{n}q_i M_i c_i g_i
  ```
  This sum applies only to cash sensitivities mapped to the same factor node and shock unit; g_i excludes M_i.

- **One-Percent Cash Delta For A Common-Underlying Node**

  ```latex
  \operatorname{CashDelta}_{1\%,b}=0.01\sum_{i\in b}q_iM_ic_i\Delta_iS_i
  ```
  Contracts in node b share one underlying and local spot-shock convention; the result is reporting currency per 1% underlying rise.

| Greek | Confirm Before Aggregating | Common Node |
| --- | --- | --- |
| Delta | Underlying units, multiplier, currency | Underlying and expiry |
| Gamma | Price-shock unit and dollarization | Underlying, expiry, and strike |
| Vega | Per 1.00 or per one volatility point | Expiry and surface node |
| Theta | Passage-of-time sign and calendar unit | Expiry and event date |

### 02 / Mechanics And Measurement

#### A Grand Net Can Hide Expiry, Strike, And Surface Basis

Node aggregation uses an indicator to assign a Greek to underlying, expiry, strike interval, or volatility-surface point. Vega across two expiries may nearly net under a current parallel move while generating material P&L when the term structure twists.

A multifactor local second-order approximation should use shock vector delta-x, gradient g, and Hessian H, with separate units for each spot, surface node, rate, or time factor. Only for one underlying plus a parallel volatility shock may it be compressed into a scalar delta-gamma-vega expression; large shocks still require full revaluation. Cross-underlying correlated hedges are not algebraic netting of the same factor and need joint scenarios.

- **Node Greek**

  ```latex
  G_b=\sum_{i=1}^{n}\mathbf{1}\{i\in b\}\,q_iM_ic_ig_i
  ```
  Node b must fix a common factor, shock unit, and FX-conversion timestamp.

- **Multifactor Local Portfolio P&L Approximation**

  ```latex
  \Delta V\approx \mathbf{g}^{\mathsf T}\Delta\mathbf{x}+\frac{1}{2}\Delta\mathbf{x}^{\mathsf T}\mathbf{H}\Delta\mathbf{x}
  ```
  The gradient g and Hessian H must use exactly the same factor order and shock units as delta-x.

### 03 / Reading Workflow

#### Normalize By Leg, Reconcile By Node, Revalue By Scenario

Export raw Greek, definition, and units for every position from positions and pricing engines, normalize them to one reporting convention, and only then aggregate. The total must equal the sum of nodes, and nodes must drill back to leg contributions; any unexplained residual should block publication.

- Freeze positions, market snapshot, model version, and reporting currency.
- Map raw units, multiplier-inclusion status, and target units for every Greek.
- Aggregate by underlying, expiry, strike, and surface node and verify nodes sum to totals.
- Check analytic Greeks with small finite differences, then fully revalue large shocks.
- Show net total, largest same-direction node, hedge basis, and data failures together.

### 04 / Risk Boundary

#### Near-Zero Net Delta Or Vega Does Not Mean A Low-Risk Portfolio

Greeks describe first- or higher-order derivatives only near the current state. Spot jumps, nonparallel volatility-surface moves, passage of time, changing dependence, and crossing strikes can change local nets rapidly.

A model, multiplier, currency, or unit error can contaminate every aggregate systematically. Portfolio hedges also face liquidity, discrete rebalancing, margin, and execution risk, so node Greeks belong beside full scenarios and cash needs.

- Reconcile units and multipliers before interpreting a Greek's sign or magnitude.
- When the grand net is small, inspect largest positive and negative nodes and maturity mismatch.
- When local approximation diverges from full revaluation, escalate to nonlinear scenarios.
- Portfolio Greeks are a risk map, not a loss limit or automatic hedge instruction.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- msci-riskmetrics-technical
- black-scholes-original
- cme-greeks
- occ-options-disclosure
- finra-risk
