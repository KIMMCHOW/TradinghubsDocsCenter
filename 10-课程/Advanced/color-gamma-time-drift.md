---
title: "Color：Gamma 随时间的漂移"
title_en: "Color: Gamma Drift Through Time"
slug: "color-gamma-time-drift"
type: lesson
level: Advanced
order: 76
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "21 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "Color：Gamma 随时间的漂移"
  - "Color: Gamma Drift Through Time"
  - "color-gamma-time-drift"
source_url: "https://tradinghubs.org/docs/trading-knowledge/color-gamma-time-drift"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Color：Gamma 随时间的漂移

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[speed-gamma-spot-drift|Speed：Gamma 随标的价格的变化]] ｜ 下一课：[[zomma-gamma-volatility-drift|Zomma：Gamma 随波动率的变化]]

**高级 · Greeks 与敏感度 · 21 分钟**

> Color 衡量时间推进时 Gamma 的局部变化。本课定义 Color=∂Gamma/∂t；若平台用剩余期限 τ，则符号相反。Color 常在临近到期时变大，但其符号与量级取决于 moneyness、模型和时间单位，不能靠名称猜测。

以日历时间口径读取 Color，统一每日与每年缩放，用 Gamma 时间切片识别到期临近时二阶风险如何重排。

### 01 / 概念边界

#### Color 是 Gamma 的纯时间偏导

概念计算保持 S、IV、利率和股息不变，只推进估值时点。正 Color 表示在当前点附近随日历时间增加 Gamma 上升，负 Color 表示下降；它描述的是静态输入切片，而不是明日实际 Gamma。

Gamma 在接近平值、接近到期时会集中，而远离执行价的 Gamma 可能向零收敛，因此 Color 可在 moneyness 轴上改变符号。同一净组合中，近月与远月、实值与虚值的 Color 也可能互相抵消。

- **本课的日历时间 Color**

  ```latex
  \operatorname{Color}_t=\frac{\partial\Gamma}{\partial t}=\frac{\partial^3V}{\partial S^2\,\partial t}
  ```

- **剩余期限符号转换**

  ```latex
  \operatorname{Color}_t=-\frac{\partial\Gamma}{\partial\tau},\qquad \tau=T-t
  ```

| 输入变化 | Gamma 敏感度 | 问题 |
| --- | --- | --- |
| Spot | Speed | 价格移动后 Gamma 如何变 |
| IV | Zomma | IV 移动后 Gamma 如何变 |
| Calendar time | Color | 纯时间经过后 Gamma 如何变 |

### 02 / 机制与度量

#### Color 的每日缩放必须匹配定价时钟

若模型 Color 按年输出，一天的 Gamma 漂移近似除以 365 或 252，具体取决于定价器如何定义 T。周末并非自动等于三个交易日，事件方差和市场闭市也可能使时间衰减非线性。

对组合，应在统一 Gamma 单位后按方向、数量与乘数汇总 Color，并保留 strike-expiry 网格。Gamma 本身可能在净值上接近零，但两侧巨大且相反的 Color 会让这种抵消在时间推进后迅速消失。

- 列名同时包含 t 或 τ、day-count 和 Gamma 计价单位。
- 组合净值之外保存到期桶与执行价桶，观察抵消是否稳定。
- 到期周同时检查结算、pin risk、行权与盘后变化。

- **小时间步长下的 Gamma 漂移**

  ```latex
  \Gamma(t+dt)-\Gamma(t)\approx\operatorname{Color}_t\,dt
  ```

- **年化 Color 到每日近似**

  ```latex
  \operatorname{Color}_{day}\approx\frac{\operatorname{Color}_{year}}{D},\qquad D\in\{365,252\}
  ```

### 03 / 阅读流程

#### 比较相邻时间切片上的整条 Gamma 曲线

在实验中固定 S 网格、IV、利率和股息，分别绘制 t 与 t+ε 的 Gamma 曲线。对每个 S 节点取差并除以 ε，可看到 Color 在峰值中心与两翼的不同符号，而不是只读当前 Spot 的一个数。

实盘桥接应把 Gamma 变化拆成 Speed×dS、Zomma×dσ 与 Color×dt，再与完整模型重估比较。若 spot、IV 和时间同时大幅变化，交叉项与更高阶效应会令简单相加失效。

- 步骤 1：固定除时间外的输入，选择与定价器一致的 ε。
- 步骤 2：比较整条 Gamma 曲线而不只看当前点。
- 步骤 3：按 strike-expiry 桶定位时间导致的风险迁移。
- 步骤 4：加入 spot、IV 与离散事件后完整重估。

- **Color 的日历时间有限差分**

  ```latex
  \operatorname{Color}_t\approx\frac{\Gamma(t+\varepsilon)-\Gamma(t)}{\varepsilon}
  ```

- **Gamma 变化的局部桥接**

  ```latex
  d\Gamma\approx\operatorname{Speed}\,dS+\operatorname{Zomma}\,d\sigma+\operatorname{Color}_t\,dt
  ```

### 04 / 风险边界

#### 临近到期的 Color 既大又局部

当 Gamma 峰值在到期前迅速变窄，Color 会对 Spot 网格、时间步长和 IV 输入高度敏感。用过粗的日步长会跨过局部结构，用过细步长又可能放大数值噪声；必须做步长稳定性检查。

Color 不包含隔夜跳空、曲面滚动规则、成交、指派或结算不连续。它不能证明价格会被某执行价吸引，也不能从未知市场仓位推导对冲需求。

- 始终显示时间符号约定、day-count、步长与 Gamma 单位。
- 到期附近进行多个 ε 的稳定性检查，并观察完整 Gamma 曲线。
- 局部桥接只用于解释，小范围外使用完整重估。
- 本课不把 Color 解释为价格磁吸或对冲流信号，也不构成交易建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Color measures the local change in gamma as time advances. This lesson defines color as ∂gamma/∂t; a platform using remaining life τ reports the opposite sign. Color often grows in magnitude near expiry, but sign and size depend on moneyness, model, and time units and cannot be guessed from the name.

Read color under a calendar-time convention, align daily and annual scaling, and use gamma time slices to see how second-order risk rearranges toward expiry.

### 01 / Concept Boundary

#### Color Is Gamma's Pure Time Derivative

The conceptual calculation holds S, IV, rates, and dividends fixed and advances only the valuation timestamp. Positive color means gamma rises locally as calendar time advances; negative color means it falls. It describes a fixed-input slice, not tomorrow's realized gamma.

Gamma concentrates near the money and near expiry while gamma far from a strike may converge toward zero, so color can change sign across moneyness. Within one net portfolio, front versus back months and in- versus out-of-the-money positions can also offset.

- **Calendar-time color in this lesson**

  ```latex
  \operatorname{Color}_t=\frac{\partial\Gamma}{\partial t}=\frac{\partial^3V}{\partial S^2\,\partial t}
  ```

- **Remaining-life sign conversion**

  ```latex
  \operatorname{Color}_t=-\frac{\partial\Gamma}{\partial\tau},\qquad \tau=T-t
  ```

| Input change | Gamma sensitivity | Question |
| --- | --- | --- |
| Spot | Speed | How gamma changes after a spot move |
| IV | Zomma | How gamma changes after an IV move |
| Calendar time | Color | How gamma changes through pure time passage |

### 02 / Mechanics And Measurement

#### Daily Color Scaling Must Match The Pricing Clock

If model color is annualized, one day's gamma drift is approximated by division by 365 or 252 according to how the pricer defines T. A weekend is not automatically three trading days, and event variance or market closure can make time decay nonlinear.

For a portfolio, aggregate color by side, quantity, and multiplier after aligning gamma units, and preserve the strike-expiry grid. Net gamma may be near zero while large opposing color on both sides causes that cancellation to disappear quickly through time.

- Include t or τ, day count, and gamma price unit in the field label.
- Keep expiry and strike buckets alongside net totals to test whether offsets are stable.
- During expiry week, inspect settlement, pin risk, exercise, and after-hours moves together.

- **Gamma drift over a small time step**

  ```latex
  \Gamma(t+dt)-\Gamma(t)\approx\operatorname{Color}_t\,dt
  ```

- **Annualized color to daily approximation**

  ```latex
  \operatorname{Color}_{day}\approx\frac{\operatorname{Color}_{year}}{D},\qquad D\in\{365,252\}
  ```

### 03 / Reading Workflow

#### Compare Entire Gamma Curves On Adjacent Time Slices

In the lab, hold the S grid, IV, rates, and dividends fixed and plot gamma curves at t and t+ε. Difference each S node and divide by ε to see color's different signs around the peak and wings rather than reading one number at current spot.

A practical bridge should separate gamma change into speed × dS, zomma × dσ, and color × dt, then compare it with full-model repricing. If spot, IV, and time all move materially, cross terms and higher orders can defeat simple addition.

- Step 1: Freeze all inputs except time and choose ε consistent with the pricer.
- Step 2: Compare the full gamma curve, not only the current point.
- Step 3: Locate time-driven risk migration by strike-expiry bucket.
- Step 4: Fully reprice after adding spot, IV, and discrete events.

- **Calendar-time finite difference for color**

  ```latex
  \operatorname{Color}_t\approx\frac{\Gamma(t+\varepsilon)-\Gamma(t)}{\varepsilon}
  ```

- **Local bridge for gamma change**

  ```latex
  d\Gamma\approx\operatorname{Speed}\,dS+\operatorname{Zomma}\,d\sigma+\operatorname{Color}_t\,dt
  ```

### 04 / Risk Boundary

#### Near Expiry, Color Can Be Both Large And Very Local

As the gamma peak narrows into expiry, color becomes highly sensitive to the spot grid, time step, and IV input. A coarse daily step can jump over local structure while a tiny step can amplify numerical noise; step-size stability must be checked.

Color excludes overnight gaps, surface-roll rules, trades, assignment, and settlement discontinuities. It cannot prove price attraction to a strike or derive hedge demand from unknown market positions.

- Always display time-sign convention, day count, step size, and gamma unit.
- Near expiry, check stability across multiple ε values and inspect the full gamma curve.
- Use the local bridge for explanation only; fully reprice outside a small neighborhood.
- This lesson does not interpret color as price magnetism or a hedge-flow signal and is not trading advice.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- occ-options-disclosure
