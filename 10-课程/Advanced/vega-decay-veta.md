---
title: "Vega Decay / Veta：Vega 随时间的变化"
title_en: "Vega Decay / Veta: How Vega Changes With Time"
slug: "vega-decay-veta"
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
  - "Vega Decay / Veta：Vega 随时间的变化"
  - "Vega Decay / Veta: How Vega Changes With Time"
  - "vega-decay-veta"
source_url: "https://tradinghubs.org/docs/trading-knowledge/vega-decay-veta"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Vega Decay / Veta：Vega 随时间的变化

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[volga-vomma-volatility-convexity|Volga / Vomma：波动率凸性]] ｜ 下一课：[[speed-gamma-spot-drift|Speed：Gamma 随标的价格的变化]]

**高级 · Greeks 与敏感度 · 21 分钟**

> Vega Decay 常被称为 Veta、DvegaDtime 或 Vega bleed，但字段符号并不统一。本课定义为日历时间推进时 ∂Vega/∂t；如果系统按剩余期限 τ 求导，应转换符号后再比较。

用 Veta 衡量 Vega 的纯时间漂移，处理日历时间与剩余期限的符号、每日单位和 moneyness 路径，而不是套用“Vega 总会衰减”。

### 01 / 概念边界

#### Veta 是波动率斜率的时间偏导

Vega 告诉我们 IV 小幅变化时价格如何变化；Veta 告诉我们在其他输入固定时，这个 Vega 随日历时间如何漂移。它是 V 对 σ 和 t 的混合偏导，也可理解为 Theta 对 σ 的敏感度，在足够光滑的同一模型口径下两条路径等价。

“Decay”不保证数值一直为负。固定 spot 时，简单模型中的平值 Vega 常随到期临近而下降，但虚值或实值期权的 Vega 路径、远期漂移、离散事件与曲面滚动都可能造成不同形态。符号必须从当前模型与坐标计算。

- **本课的 Vega Decay / Veta**

  ```latex
  \operatorname{Veta}_t=\frac{\partial\operatorname{Vega}}{\partial t}=\frac{\partial^2V}{\partial\sigma\,\partial t}
  ```

- **剩余期限口径**

  ```latex
  \operatorname{Veta}_t=-\frac{\partial\operatorname{Vega}}{\partial\tau},\qquad \tau=T-t
  ```

| 变化来源 | 局部项 | 解释 |
| --- | --- | --- |
| IV 变化 | Vomma × dσ | 同一时点 Vega 随 IV 改变 |
| Spot 变化 | Vanna × dS | 同一时点 Vega 随标的改变 |
| 时间推进 | Veta × dt | 其他输入固定时的 Vega 漂移 |

### 02 / 机制与度量

#### Veta 同时需要 Vega 单位和时间单位

若 Vega 按 σ 变化 1.00 输出、Veta 又按年输出，要得到每 1 vol point、每天的 Vega 变化，需要同时乘 0.01 并除以 day-count D。平台也可能已经完成其中一个缩放；重复换算会造成 100 倍或 365 倍错误。

组合 Veta 应按方向、数量、合约乘数和到期桶汇总。净值可能隐藏近月快速变化与远月缓慢变化的抵消；滚动日期时，合约从一个 DTE 桶迁移到另一个桶也要与纯模型 Veta 分开记录。

- 记录 Vega 本身按 vol decimal 还是 vol point 输出。
- 记录 Veta 按日历日、交易日或年化时间输出。
- 事件方差从期限中移除时可能不连续，不能一律按线性日衰减。

- **小时间步长下的 Vega 漂移**

  ```latex
  \operatorname{Vega}(t+dt)-\operatorname{Vega}(t)\approx\operatorname{Veta}_t\,dt
  ```

- **Raw 年化值的双重缩放示例**

  ```latex
  \operatorname{Veta}_{1vp/day}\approx0.01\,\frac{\operatorname{Veta}_{raw/year}}{D}
  ```

### 03 / 阅读流程

#### 沿固定输入的时间切片观察 Vega 曲线

在实验图中固定 spot、IV、利率和股息，只缩短剩余期限 ε，比较两个估值日的 Vega。若使用日历时间定义，则用 Vega(t+ε)-Vega(t)；若直接使用 τ，则记住其导数符号相反。

随后建立 Vega 变化桥接：分别归因时间、spot 和 IV，再与完整重估后的 Vega 变化比较。对日历价差或跨月组合，还要分别冲击每个期限节点，观察近月事件溢价消失后净 Vega 是否翻转。

- 步骤 1：确认 t / τ、Vega 缩放与 day-count。
- 步骤 2：冻结其他输入，用相邻时间切片核验 Veta。
- 步骤 3：按到期和 moneyness 分桶定位 Vega 漂移。
- 步骤 4：加入 spot、IV 与曲面滚动后完整重估。

- **Veta 的日历时间有限差分**

  ```latex
  \operatorname{Veta}_t\approx\frac{\operatorname{Vega}(t+\varepsilon)-\operatorname{Vega}(t)}{\varepsilon}
  ```

- **Vega 变化的局部桥接**

  ```latex
  d\operatorname{Vega}\approx\operatorname{Vanna}\,dS+\operatorname{Vomma}\,d\sigma+\operatorname{Veta}_t\,dt
  ```

### 04 / 风险边界

#### 纯时间 Veta 不等于实际隔夜 Vega 变化

实际隔夜会同时经历价格跳空、IV 更新、事件日移动、利率与股息信息变化。若曲面使用固定 Delta 而不是固定 strike 坐标，spot 变化还会造成节点迁移；这些效应都不属于纯 Veta。

临近到期时，Vega 和 Veta 可能对微小时间步长高度敏感，且流动性、行权和离散结算主导实际结果。应用可成交报价与完整情景验证，不应把“Vega decay”作为固定收益来源。

- Veta 必须与 t / τ、每日/每年和 Vega 缩放一起显示。
- 不要默认 Vega 永远衰减；按 moneyness、期限和事件结构计算。
- 纯时间诊断与真实隔夜联合情景分开保存。
- 本课不推荐任何日历结构、到期日或 Vega 方向。

## 相关概念

- [[vega-iv-sensitivity|Vega：IV 敏感度与波动率重定价]] — Veta 度量 Vega 随剩余期限衰减的速度，而不是 Vega 本身。
- [[time-value-and-theta|时间价值与 Theta]] — Veta 与 Theta 是同一时间轴上的两个不同敏感度。
- [[dte-window-selection|DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选]] — Vega 衰减速度随到期窗口急剧变化，因此窗口选择本身就是 Veta 决策。
- [[calendar-diagonal-butterfly-condor|Calendar、Diagonal、Butterfly、Condor 与 Iron Condor]] — 跨期限结构的核心风险正是两条腿的 Veta 差异。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Vega decay is often called veta, DvegaDtime, or vega bleed, but field signs are not standardized. This lesson defines it as ∂vega/∂t as calendar time advances; systems differentiating with respect to remaining life τ must have their signs converted before comparison.

Use veta to measure pure time drift in vega, handling calendar-versus-remaining-life signs, daily units, and moneyness paths rather than assuming vega always decays.

### 01 / Concept Boundary

#### Veta Is The Time Derivative Of The Volatility Slope

Vega tells how price changes for a small IV move; veta tells how that vega drifts through calendar time with other inputs fixed. It is the mixed derivative of V with respect to σ and t and can also be read as theta's sensitivity to σ when both paths use one sufficiently smooth model convention.

The word decay does not guarantee a negative value. With spot fixed, at-the-money vega in a simple model often falls toward expiry, but vega paths for in- or out-of-the-money options, forward drift, discrete events, and surface roll can behave differently. The sign must come from the current model and coordinates.

- **Vega decay / veta in this lesson**

  ```latex
  \operatorname{Veta}_t=\frac{\partial\operatorname{Vega}}{\partial t}=\frac{\partial^2V}{\partial\sigma\,\partial t}
  ```

- **Remaining-life convention**

  ```latex
  \operatorname{Veta}_t=-\frac{\partial\operatorname{Vega}}{\partial\tau},\qquad \tau=T-t
  ```

| Source of change | Local term | Interpretation |
| --- | --- | --- |
| IV move | Vomma × dσ | Vega changes with IV at one time |
| Spot move | Vanna × dS | Vega changes with spot at one time |
| Time passage | Veta × dt | Vega drift with other inputs fixed |

### 02 / Mechanics And Measurement

#### Veta Needs Both Vega Units And Time Units

If vega is reported per a 1.00 change in σ and veta is annualized, a daily change in vega per one vol point requires both multiplication by 0.01 and division by day count D. A platform may already apply either scale; applying it twice creates factors-of-100 or factors-of-365 errors.

Portfolio veta should aggregate by side, quantity, contract multiplier, and expiry bucket. A net value can hide fast front-month change offset by slow back-month change; as dates roll, contracts migrating between DTE buckets should also be recorded separately from pure model veta.

- Record whether vega itself is per volatility decimal or per vol point.
- Record whether veta is per calendar day, trading day, or year.
- Event variance can leave a maturity discontinuously and need not decay linearly by day.

- **Vega drift over a small time step**

  ```latex
  \operatorname{Vega}(t+dt)-\operatorname{Vega}(t)\approx\operatorname{Veta}_t\,dt
  ```

- **Example scaling of a raw annualized value**

  ```latex
  \operatorname{Veta}_{1vp/day}\approx0.01\,\frac{\operatorname{Veta}_{raw/year}}{D}
  ```

### 03 / Reading Workflow

#### Observe The Vega Curve Across Fixed-Input Time Slices

In the lab, hold spot, IV, rates, and dividends fixed, shorten remaining life by ε, and compare vega on the two valuation dates. Under the calendar-time definition use vega(t+ε)-vega(t); if working directly in τ, remember the derivative has the opposite sign.

Next build a vega-change bridge: attribute time, spot, and IV separately, then compare with the fully repriced vega change. For calendars or cross-month packages, shock each maturity node separately and observe whether net vega reverses when front-month event premium leaves the surface.

- Step 1: Confirm t/τ, vega scaling, and day count.
- Step 2: Freeze other inputs and validate veta on adjacent time slices.
- Step 3: Locate vega drift by expiry and moneyness bucket.
- Step 4: Fully reprice after adding spot, IV, and surface roll.

- **Calendar-time finite difference for veta**

  ```latex
  \operatorname{Veta}_t\approx\frac{\operatorname{Vega}(t+\varepsilon)-\operatorname{Vega}(t)}{\varepsilon}
  ```

- **Local bridge for vega change**

  ```latex
  d\operatorname{Vega}\approx\operatorname{Vanna}\,dS+\operatorname{Vomma}\,d\sigma+\operatorname{Veta}_t\,dt
  ```

### 04 / Risk Boundary

#### Pure-Time Veta Is Not Realized Overnight Vega Change

An actual overnight interval also includes spot gaps, IV updates, event-date movement, and rate or dividend information. If the surface uses fixed-delta rather than fixed-strike coordinates, spot moves also remap nodes; none of those effects is pure veta.

Near expiry, vega and veta can be highly sensitive to step size while liquidity, exercise, and discrete settlement dominate realized outcomes. Validate with executable prices and full scenarios; do not treat 'vega decay' as a fixed return source.

- Display veta together with t/τ, daily/annual time, and vega scaling.
- Do not assume vega always decays; calculate by moneyness, maturity, and event structure.
- Store pure-time diagnostics separately from realistic joint overnight scenarios.
- This lesson recommends no calendar structure, expiry, or vega direction.

## Related Concepts

- [[vega-iv-sensitivity|Vega: IV Sensitivity And Volatility Repricing]] — Veta measures how fast vega decays with remaining time, not vega itself.
- [[time-value-and-theta|Time Value And Theta]] — Veta and theta are two different sensitivities along the same time axis.
- [[dte-window-selection|DTE Windows: How To Choose 0DTE, 1DTE+, And 90D Window]] — Vega decay speed changes sharply with the expiry window, so choosing a window is a veta decision.
- [[calendar-diagonal-butterfly-condor|Calendars, Diagonals, Butterflies, Condors, And Iron Condors]] — The core risk of a cross-expiry structure is precisely the veta difference between its legs.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- occ-options-disclosure
