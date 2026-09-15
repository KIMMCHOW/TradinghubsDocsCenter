---
title: "Charm：Delta 随日历时间的漂移"
title_en: "Charm: Delta Drift Through Calendar Time"
slug: "charm-delta-time-decay"
type: lesson
level: Advanced
order: 72
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "22 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "Charm：Delta 随日历时间的漂移"
  - "Charm: Delta Drift Through Calendar Time"
  - "charm-delta-time-decay"
source_url: "https://tradinghubs.org/docs/trading-knowledge/charm-delta-time-decay"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Charm：Delta 随日历时间的漂移

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[vanna-cross-sensitivity|Vanna：Delta 与波动率的交叉敏感度]] ｜ 下一课：[[volga-vomma-volatility-convexity|Volga / Vomma：波动率凸性]]

**高级 · Greeks 与敏感度 · 22 分钟**

> 本课把 Charm 定义为日历时间 t 增加时的 ∂Delta/∂t；如果系统用剩余期限 τ=T-t 求导，符号会相反。Charm 是通用模型 Greek，现有 ODV CHEX 则是预计算产品暴露字段：不能用通用 OI × Charm × Multiplier 重建 CHEX，也不能据此宣称经销商必须在某个方向对冲。

在固定市场输入的前提下衡量 Delta 随时间的局部变化，统一 t 与剩余期限 τ 的符号和每日/每年单位，并与 ODV CHEX 产品字段区分。

### 01 / 概念边界

#### Charm 是时间方向上的 Delta 偏导

计算 Charm 时，概念上保持标的价格、IV 曲面、利率与股息输入不变，只让估值日向到期日推进。它因此隔离“纯时间经过”对 Delta 的局部影响，而不是预测明天实际 Delta；现实中的价格和曲面通常也会变化。

不同资料对 Charm 的命名和符号并不统一。有的直接报告 ∂Delta/∂t，有的报告 ∂Delta/∂τ，还有的在字段中预先乘以负号或按一天缩放。必须把变量、方向和单位写进列名。

- **本课的日历时间 Charm**

  ```latex
  \operatorname{Charm}_t=\frac{\partial\Delta}{\partial t}=\frac{\partial^2V}{\partial S\,\partial t}
  ```

- **与剩余期限口径的关系**

  ```latex
  \tau=T-t,\qquad \operatorname{Charm}_t=-\frac{\partial\Delta}{\partial\tau}
  ```

| 字段 | 本质 | 关键边界 |
| --- | --- | --- |
| Charmt | 日历时间增加时 ∂Delta/∂t | 必须注明每年或每日 |
| Charmτ | 对剩余期限的 ∂Delta/∂τ | 与本课 Charmt 符号相反 |
| ODV CHEX | 现有产品课程定义的预计算暴露字段 | 不能由通用 Charm 公式重建 |

### 02 / 机制与度量

#### 一天的 Delta 漂移需要明确时间分母

若 Charm 以每年为单位，日历一天近似使用 dt=1/365；交易日口径可能使用 1/252。两者回答的问题不同，周末、节假日和事件日也不一定按线性时钟衰减。组合汇总前必须统一 day-count convention。

Charm 的符号和量级随 Call / Put、moneyness、期限、IV、利率和收益率变化。临近到期且接近平值时，Delta 转换区会压缩，局部时间导数可能非常大；离开这个切点后，线性近似很快失效。

- 模型时钟应与定价器的年化时间定义一致，不能任意混用 365 与 252。
- 组合 Charm 按已知仓位方向、数量与合约乘数汇总，并保留到期桶。
- 接近到期时同时检查 Gamma、pin risk、行权与盘后价格路径。

- **小时间步长下的 Delta 变化**

  ```latex
  \Delta(t+dt)-\Delta(t)\approx\operatorname{Charm}_t\,dt
  ```

- **每年值转换为每日近似**

  ```latex
  \operatorname{Charm}_{day}\approx\frac{\operatorname{Charm}_{year}}{D},\qquad D\in\{365,252\}
  ```

### 03 / 阅读流程

#### 固定市场快照，在两个估值日之间做有限差分

核验 Charm 时，用同一 S、同一 IV 参数、同一利率/股息曲线分别计算 t 与 t+ε 的 Delta，并将差值除以 ε。若定价器接受剩余期限而不是日历时间，则输入 τ-ε，并在解释时转换符号。

随后把纯时间漂移与实际日终变化分开归因：实际 Delta 变化还可能来自 Gamma × dS、Vanna × dσ 和曲面插值更新。先做局部桥接，再用明日完整市场情景重估，避免把所有变化都叫作 Charm。

- 步骤 1：写明 t 或 τ、每年或每日、365 或 252。
- 步骤 2：冻结除时间以外的输入，用小 ε 核验符号。
- 步骤 3：按执行价与到期桶检查 Charm 集中位置。
- 步骤 4：将纯时间、现货与 IV 贡献分开，再完整重估。

- **日历时间有限差分**

  ```latex
  \operatorname{Charm}_t\approx\frac{\Delta(t+\varepsilon)-\Delta(t)}{\varepsilon}
  ```

- **Delta 变化的局部归因**

  ```latex
  d\Delta\approx\Gamma\,dS+\operatorname{Vanna}\,d\sigma+\operatorname{Charm}_t\,dt
  ```

### 04 / 风险边界

#### Charm 不等于明天的确定对冲订单

Charm 假设其他输入不变，而隔夜跳空、IV 变化、成交、行权和仓位管理都会改变实际 Delta。尤其临近到期时，有限差分步长、市场开闭盘和离散行权会使理论连续时间近似偏离实际。

CHEX 必须继续按现有 ODV 数据契约解释。开放兴趣量没有买卖方向，也不揭示谁承担风险；用 OI × Charm 构造的自定义数值不能冒充 CHEX，更不能证明经销商将在某时刻买入或卖出标的。

- Charm 输出必须同时显示时间变量、day count、单位和估值时点。
- 只对方向已知的自有仓位汇总，不为全市场假设库存方向。
- CHEX 保持产品字段定义，禁止使用通用 OI × Charm 公式替代。
- 本课不预测对冲流、收盘路径或到期结果，也不构成交易建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> This lesson defines charm as ∂delta/∂t as calendar time t advances; a system differentiating with respect to remaining life τ=T-t will report the opposite sign. Charm is a generic model Greek, whereas the existing ODV CHEX is a precomputed product-exposure field: do not reconstruct CHEX with generic OI × charm × multiplier or claim dealers must hedge in a particular direction.

Measure local delta change through time with market inputs held fixed, align t-versus-remaining-life signs and per-day/per-year units, and separate it from the ODV CHEX product field.

### 01 / Concept Boundary

#### Charm Is Delta's Partial Derivative Along Time

Conceptually, charm holds spot, the IV surface, rates, and dividends fixed while the valuation date advances toward expiry. It isolates the local effect of pure time passage on delta, not tomorrow's realized delta; real spot and surface inputs normally move as well.

Charm naming and sign are not universal. Some sources report ∂delta/∂t, others ∂delta/∂τ, and some pre-apply a minus sign or daily scaling. The differentiated variable, direction, and unit belong in the field label.

- **Calendar-time charm in this lesson**

  ```latex
  \operatorname{Charm}_t=\frac{\partial\Delta}{\partial t}=\frac{\partial^2V}{\partial S\,\partial t}
  ```

- **Relation to the remaining-life convention**

  ```latex
  \tau=T-t,\qquad \operatorname{Charm}_t=-\frac{\partial\Delta}{\partial\tau}
  ```

| Field | What it is | Key boundary |
| --- | --- | --- |
| Charmt | ∂delta/∂t as calendar time advances | Must state per year or per day |
| Charmτ | ∂delta/∂τ with respect to remaining life | Opposite sign to this lesson's Charmt |
| ODV CHEX | Precomputed exposure defined by the existing product lesson | Must not be rebuilt from generic charm |

### 02 / Mechanics And Measurement

#### One Day Of Delta Drift Needs An Explicit Time Denominator

If charm is annualized, one calendar day uses approximately dt=1/365; a trading-day convention may use 1/252. They answer different questions, and weekends, holidays, and event dates need not decay on a linear clock. Align the day-count convention before portfolio aggregation.

Charm sign and magnitude vary with call or put, moneyness, maturity, IV, rates, and yield. Near expiry and near the money, the delta transition region compresses and the local time derivative can become very large; the linear approximation can fail quickly away from that point.

- The model clock must match the pricer's annualization; do not mix 365 and 252 arbitrarily.
- Aggregate portfolio charm by known side, quantity, and multiplier while preserving expiry buckets.
- Near expiry, inspect gamma, pin risk, exercise, and after-hours price paths together.

- **Delta change over a small time step**

  ```latex
  \Delta(t+dt)-\Delta(t)\approx\operatorname{Charm}_t\,dt
  ```

- **Converting annualized charm to a daily approximation**

  ```latex
  \operatorname{Charm}_{day}\approx\frac{\operatorname{Charm}_{year}}{D},\qquad D\in\{365,252\}
  ```

### 03 / Reading Workflow

#### Hold The Market Snapshot Fixed Across Two Valuation Dates

To validate charm, calculate delta at t and t+ε using the same S, IV parameters, and rate/dividend curves, then divide the difference by ε. If the pricer takes remaining life rather than calendar time, input τ-ε and convert the sign when interpreting the result.

Then separate pure time drift from realized end-of-day change: actual delta change may also include gamma × dS, vanna × dσ, and surface-interpolation updates. Build a local bridge first, then fully reprice tomorrow's market scenarios rather than calling every change charm.

- Step 1: State t or τ, annual or daily, and 365 or 252.
- Step 2: Freeze all inputs except time and verify the sign with a small ε.
- Step 3: Inspect charm concentration by strike and expiry bucket.
- Step 4: Separate time, spot, and IV contributions, then fully reprice.

- **Calendar-time finite difference**

  ```latex
  \operatorname{Charm}_t\approx\frac{\Delta(t+\varepsilon)-\Delta(t)}{\varepsilon}
  ```

- **Local attribution of delta change**

  ```latex
  d\Delta\approx\Gamma\,dS+\operatorname{Vanna}\,d\sigma+\operatorname{Charm}_t\,dt
  ```

### 04 / Risk Boundary

#### Charm Is Not Tomorrow's Certain Hedge Order

Charm assumes other inputs stay fixed, while overnight gaps, IV changes, trades, exercise, and position management all alter realized delta. Near expiry in particular, finite-difference step size, market closes and opens, and discrete exercise can pull practice away from a continuous-time approximation.

CHEX must continue to follow the existing ODV data contract. Open interest has no long/short sign and does not reveal who bears risk; a custom OI × charm number cannot impersonate CHEX or prove dealers will buy or sell the underlying at a given time.

- Charm output must show time variable, day count, unit, and valuation timestamp.
- Aggregate only owned positions with known signs; do not assume market-wide inventory direction.
- Preserve the product-field definition of CHEX; never replace it with generic OI × charm.
- This lesson predicts neither hedge flow, closing path, nor expiry outcome and is not trading advice.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- occ-options-disclosure
