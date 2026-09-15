---
title: "Avellaneda–Stoikov 做市模型：库存偏移、价差与校准"
title_en: "Avellaneda–Stoikov Market Making: Inventory Skew, Spread, And Calibration"
slug: "avellaneda-stoikov-market-making"
type: lesson
level: Advanced
order: 86
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "28 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "Avellaneda–Stoikov 做市模型：库存偏移、价差与校准"
  - "Avellaneda–Stoikov Market Making: Inventory Skew, Spread, And Calibration"
  - "avellaneda-stoikov-market-making"
source_url: "https://tradinghubs.org/docs/trading-knowledge/avellaneda-stoikov-market-making"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# Avellaneda–Stoikov 做市模型：库存偏移、价差与校准

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[market-making-inventory-adverse-selection|做市库存与逆向选择：价差收入不是免费收益]] ｜ 下一课：[[absorption-exhaustion-and-iceberg-orders|吸收、衰竭与冰山单]]

**高级 · 订单流与市场微观结构 · 28 分钟**

> Avellaneda–Stoikov 模型把做市拆成两步：库存通过保留价格移动报价中心，成交强度与风险厌恶共同决定总价差。这个闭式近似非常适合教学和建立基准，却依赖强假设，不能在未加入真实订单簿、延迟、费用与风控前直接驱动生产订单。

推导有限期限基线模型的保留价格、最优价差和指数成交强度，解释 A、k、γ、σ 的校准单位，并明确该模型不能直接用于生产报价。

### 01 / 概念边界

#### 基线模型优化有限期限终值的指数效用

模型令中间价 S_t 服从零漂移、常数波动率 σ 的算术布朗运动，库存 q_t 以一单位成交跳变，做市商对终值现金加库存盯市财富使用常绝对风险厌恶参数 γ 的指数效用。基线现金账户利率为零；等价地，可把全部现金与价格理解为已折现单位。

买卖市价单到达被建模为相互独立的泊松过程，报价距中间价 δ 越远，成交强度按 A e^{-kδ} 衰减。A 是零距离基准到达率，k 是强度对价格距离的衰减速度；所有价格、时间和库存单位必须一致。

- **指数成交强度**

  ```latex
  \lambda(\delta)=Ae^{-k\delta},\qquad A>0,\ k>0
  ```

| 参数 | 模型角色 | 单位检查 |
| --- | --- | --- |
| σ | 中间价扩散速度 | 价格 / √时间 |
| γ | 库存风险厌恶 | 1 / 货币 |
| A | 近中间价基准到达率 | 每时间 |
| k | 强度随距离衰减 | 每价格 |

### 02 / 机制与度量

#### 库存移动报价中心，期限风险与成交弹性决定总价差

保留价格 r_t=S_t-q_tγσ²(T-t)。当 q_t>0 为多头库存时，r_t 低于中间价，使买卖报价整体下移，降低继续买入的吸引力并提高卖出概率；空头库存产生相反偏移。

基线近似的总价差 ψ_t 由库存持有到期限的风险项和订单到达弹性项组成，并在该闭式形式下不依赖当前 q_t。买价和卖价围绕 r_t 对称放置；这项对称性来自假设，不是所有真实市场的结论。

- **保留价格**

  ```latex
  r_t=S_t-q_t\gamma\sigma^2(T-t)
  ```

- **基线最优总价差**

  ```latex
  \psi_t=\gamma\sigma^2(T-t)+\frac{2}{\gamma}\ln\!\left(1+\frac{\gamma}{k}\right)
  ```

- **围绕保留价格的买卖报价**

  ```latex
  p_t^{b}=r_t-\frac{\psi_t}{2},\qquad p_t^{a}=r_t+\frac{\psi_t}{2}
  ```

### 03 / 阅读流程

#### 校准必须处理未成交、队列、状态变化与参数单位

σ 应从与决策时钟一致的中间价变化估计，并区分跳跃与微观结构噪声。A 与 k 需要同时使用报价暴露时间和成交结果拟合 λ(δ)，未成交报价属于删失暴露而不是应删除的空记录。

γ 是风险偏好与控制参数，不是仅靠成交数据唯一识别的自然常数。它应通过库存分布、尾部损益、限额和业务目标做敏感性选择，并在样本外与简单对称报价、固定库存偏移等基准比较。

- 固定价格单位、时间单位、单次成交库存单位和终止期限 T。
- 清洗中间价并在相同时间单位下估计 σ 与状态区间。
- 按报价距离记录暴露时间、成交、未成交、撤单、队列和延迟。
- 以泊松似然或生存方法拟合 A、k，并检查距离外推与稳定性。
- 对 γ、库存限额、期限和再校准频率做样本外压力与成本后比较。
- 在任何实盘考虑前加入 tick、队列、费用、延迟、冲击、熔断与人工接管。

### 04 / 风险边界

#### 基线 Avellaneda–Stoikov 不是可直接上线的生产策略

基线假设包括零漂移算术布朗中间价、常数 σ、零货币市场利率（或已折现单位）、指数效用、固定 γ、独立泊松到达、指数距离衰减、对称买卖流、单位成交、有限期限以及简化的无摩擦执行。它忽略队列优先级、tick、延迟、费用、市场冲击、撤单竞争、逆向选择、跳跃、停牌和多资产约束。

A、k 和 σ 会随时段、波动状态、盘口深度与事件快速变化，误校准可能同时提高成交率和尾部库存。任何生产系统都需要硬库存与损失限额、数据失效保护、订单状态机、模拟与影子运行、独立风控及可验证的紧急停机；闭式公式本身不满足这些要求。

- 保留价格偏移扩大时，先检查库存、σ、期限和单位是否一致。
- 成交率偏离模型时分解 A、k 漂移、队列、延迟与逆向选择。
- 回测必须包含未成交报价、真实成本、订单状态和压力库存。
- 本模型仅用于教学与基准研究，不是生产报价、自动下单或收益承诺。

## 相关概念

- [[market-making-inventory-adverse-selection|做市库存与逆向选择：价差收入不是免费收益]] — 库存与逆向选择是该模型的直觉来源与前置概念。
- [[model-assumptions-and-model-risk|模型假设与模型风险：从公式正确到决策可靠]] — 成交强度与风险偏好假设决定模型输出是否可用。
- [[order-book-depth-and-resting-liquidity|订单簿、深度与挂单流动性]] — 最优价差最终表现为盘口上的挂单深度与距离。
- [[discrete-hedging-error-transaction-costs|离散对冲误差与交易成本：连续理论如何落到有限成交]] — 库存管理本身就是带成本的离散对冲问题。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> The Avellaneda–Stoikov model separates market making into two steps: inventory shifts the quote center through a reservation price, while fill intensity and risk aversion determine total spread. This closed-form approximation is an excellent teaching baseline but relies on strong assumptions and must not drive production orders without real order-book, latency, cost, and control layers.

Derive the finite-horizon baseline reservation price, optimal spread, and exponential arrival intensity, explain calibration and units for A, k, gamma, and sigma, and state why the model is not directly production-ready.

### 01 / Concept Boundary

#### The Baseline Optimizes Exponential Utility Of Finite-Horizon Wealth

The model lets midpoint S_t follow a zero-drift arithmetic Brownian motion with constant volatility sigma, inventory q_t jump by one unit per fill, and the market maker apply exponential utility with constant absolute risk aversion gamma to terminal cash plus marked inventory. The baseline cash account earns zero interest; equivalently, all cash and prices may be interpreted in discounted units.

Market buy and sell arrivals are modeled as independent Poisson processes, with fill intensity decaying as A exp(-k delta) as quote distance delta grows. A is the zero-distance baseline arrival rate and k is intensity decay per price distance; all price, time, and inventory units must be consistent.

- **Exponential Arrival Intensity**

  ```latex
  \lambda(\delta)=Ae^{-k\delta},\qquad A>0,\ k>0
  ```

| Parameter | Model Role | Unit Check |
| --- | --- | --- |
| sigma | Midprice diffusion scale | Price per square-root time |
| gamma | Inventory risk aversion | Inverse currency |
| A | Baseline near-mid arrival rate | Per time |
| k | Intensity decay with distance | Per price |

### 02 / Mechanics And Measurement

#### Inventory Moves The Center; Horizon Risk And Fill Elasticity Set The Spread

The reservation price is r_t=S_t-q_t gamma sigma squared (T-t). When q_t>0 represents long inventory, r_t lies below midpoint, shifting both quotes down to discourage further buying and encourage selling; short inventory creates the opposite shift.

The baseline approximate total spread psi_t combines inventory risk through the remaining horizon with an order-arrival elasticity term and, in this closed form, does not depend on current q_t. Bid and ask are placed symmetrically around r_t; that symmetry comes from assumptions and is not a universal market result.

- **Reservation Price**

  ```latex
  r_t=S_t-q_t\gamma\sigma^2(T-t)
  ```

- **Baseline Optimal Total Spread**

  ```latex
  \psi_t=\gamma\sigma^2(T-t)+\frac{2}{\gamma}\ln\!\left(1+\frac{\gamma}{k}\right)
  ```

- **Bid And Ask Around Reservation Price**

  ```latex
  p_t^{b}=r_t-\frac{\psi_t}{2},\qquad p_t^{a}=r_t+\frac{\psi_t}{2}
  ```

### 03 / Reading Workflow

#### Calibration Must Handle Nonfills, Queue, Regimes, And Parameter Units

Sigma should be estimated from midpoint changes aligned to the decision clock, with jumps and microstructure noise treated explicitly. Estimating A and k requires quote exposure time together with fill outcomes for lambda(delta); unfilled quotes are censored exposure, not empty records to discard.

Gamma is a risk-preference and control parameter, not a natural constant uniquely identified from fills. It should be selected through sensitivity of inventory distribution, tail P&L, limits, and objectives, then compared out of sample with simple symmetric quotes and fixed inventory-skew baselines.

- Fix price unit, time unit, per-fill inventory unit, and terminal horizon T.
- Clean midpoint and estimate sigma and regimes in the same time unit.
- Record exposure time, fills, nonfills, cancellations, queue, and latency by quote distance.
- Fit A and k with Poisson-likelihood or survival methods and test distance extrapolation and stability.
- Compare gamma, inventory limits, horizon, and recalibration frequency out of sample after costs.
- Before any live consideration, add ticks, queue, fees, latency, impact, kill switches, and manual takeover.

### 04 / Risk Boundary

#### Baseline Avellaneda–Stoikov Is Not A Production-Ready Strategy

Baseline assumptions include a zero-drift arithmetic-Brownian midpoint, constant sigma, zero money-market interest (or discounted units), exponential utility, fixed gamma, independent Poisson arrivals, exponential distance decay, symmetric buy and sell flow, unit fills, finite horizon, and simplified frictionless execution. It omits queue priority, ticks, latency, fees, impact, cancellation competition, adverse selection, jumps, halts, and multi-asset constraints.

A, k, and sigma can change rapidly with session, volatility regime, book depth, and events, and bad calibration can increase both fills and tail inventory. Any production system needs hard inventory and loss limits, data-failure protection, an order state machine, simulation and shadow operation, independent controls, and a tested emergency stop; the closed-form equations provide none of these.

- When reservation-price skew grows, verify inventory, sigma, horizon, and units.
- When fills diverge from the model, separate A-k drift, queue, latency, and adverse selection.
- Backtests must include nonfills, realistic costs, order state, and stressed inventory.
- This model is for teaching and benchmark research only, not production quoting, automatic orders, or return promises.

## Related Concepts

- [[market-making-inventory-adverse-selection|Market-Making Inventory And Adverse Selection: Spread Capture Is Not Free Return]] — Inventory and adverse selection are the model's intuition and its prerequisite concepts.
- [[model-assumptions-and-model-risk|Model Assumptions And Model Risk: From Correct Formula To Reliable Decision]] — Fill-intensity and risk-preference assumptions determine whether the model's output is usable.
- [[order-book-depth-and-resting-liquidity|Order Book Depth And Resting Liquidity]] — The optimal spread ultimately appears as depth and distance in the book.
- [[discrete-hedging-error-transaction-costs|Discrete Hedging Error And Transaction Costs: Bringing Continuous Theory To Finite Trades]] — Inventory management is itself a cost-bearing discrete hedging problem.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- nyu-avellaneda-stoikov
- nyfed-market-liquidity
- finra-risk
