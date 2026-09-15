---
title: "Zomma：Gamma 随波动率的变化"
title_en: "Zomma: How Gamma Changes With Volatility"
slug: "zomma-gamma-volatility-drift"
type: lesson
level: Advanced
order: 77
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
  - "Zomma：Gamma 随波动率的变化"
  - "Zomma: How Gamma Changes With Volatility"
  - "zomma-gamma-volatility-drift"
source_url: "https://tradinghubs.org/docs/trading-knowledge/zomma-gamma-volatility-drift"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Zomma：Gamma 随波动率的变化

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[color-gamma-time-drift|Color：Gamma 随时间的漂移]] ｜ 下一课：[[vanna-exposure-vex|VEX：Vanna Exposure 怎么看]]

**高级 · Greeks 与敏感度 · 21 分钟**

> Zomma 是 Gamma 对隐含波动率的局部偏导，也等价于 Vega 对 Spot 的二阶偏导。它说明 IV 改变后 Gamma 曲线如何重塑，但不说明 IV 将向哪里走，也不说明未知参与者如何对冲。

用 Zomma 连接 Gamma 与 IV，统一 vol point 缩放，并在平行、偏斜和 Spot–IV 联合情景中验证 Gamma 风险的再分布。

### 01 / 概念边界

#### Zomma 是 Gamma–IV 交叉敏感度

保持 S、期限、利率与股息不变时，Zomma 衡量 σ 小幅改变造成的 Gamma 变化。在平滑模型中，它是 V 对 S、S、σ 的三阶偏导。正负号随 d1d2、moneyness、期限和模型输入变化。

在 Black–Scholes 型模型中，Zomma 可写成 Gamma×(d1d2-1)/σ。由于括号项可以跨越零，不能把 Long Option 简化成固定 Long 或 Short Zomma；同一合约在价格与期限变化后也可能翻转。

- **Zomma 定义**

  ```latex
  \operatorname{Zomma}=\frac{\partial\Gamma}{\partial\sigma}=\frac{\partial^3V}{\partial S^2\,\partial\sigma}=\frac{\partial^2\operatorname{Vega}}{\partial S^2}
  ```

- **Black–Scholes 型恒等式**

  ```latex
  \operatorname{Zomma}=\Gamma\frac{d_1d_2-1}{\sigma}
  ```

| Greek | 输入方向 | 输出变化 |
| --- | --- | --- |
| Speed | Spot | Gamma |
| Color | Calendar time | Gamma |
| Zomma | IV | Gamma |

### 02 / 机制与度量

#### 每 1 vol point 的 Zomma 需要乘 0.01

若解析导数以 σ 从 0 到 1 的变化为单位，IV 上升 1 vol point 对应 dσ=0.01，因此 Gamma 变化近似为 raw Zomma×0.01。平台可能直接输出每 vol point 数值，导入组合前必须核对元数据。

组合 Zomma 按方向、数量、合约乘数和统一 Gamma 单位求和，并保存执行价与期限节点。IV 曲面不是单一 σ：ATM level、put skew、call wing 和 term structure 的变化会激活不同节点的 Zomma。

- 确认 Gamma 是每价格单位、每 1% spot move 还是现金 Gamma。
- 确认 Zomma 的 σ 输入是 absolute vol decimal、vol point 还是相对变化。
- 不要用一个平行 IV 数字替代整张 strike-expiry 曲面的节点风险。

- **小幅 IV 变化下的 Gamma 漂移**

  ```latex
  d\Gamma\approx\operatorname{Zomma}\,d\sigma
  ```

- **每 vol point 换算**

  ```latex
  \operatorname{Zomma}_{1vp}=0.01\,\operatorname{Zomma}_{raw}
  ```

### 03 / 阅读流程

#### 在两个 IV 切片之间比较 Gamma 曲线

固定 Spot 网格、期限、利率和股息，在 σ-ε 与 σ+ε 分别绘制 Gamma 曲线。每个 S 节点的曲线差除以 2ε 给出 Zomma 有限差分；这能直接看到 ATM 峰值变宽、变窄以及两翼符号变化。

实盘先用小幅平行 IV 冲击核验字段，再运行 skew twist、前端事件溢价和 spot–IV 同向/反向联合情景。比较 Zomma 局部预测与完整 Gamma 重估，误差扩大时停止线性外推。

- 步骤 1：统一 σ、Gamma 与 Zomma 单位。
- 步骤 2：用对称 IV 小冲击比较整条 Gamma 曲线。
- 步骤 3：按 strike-expiry 节点运行 level、skew 与 term 情景。
- 步骤 4：加入 Spot 与时间路径，和完整重估核对。

- **Zomma 的中央有限差分**

  ```latex
  \operatorname{Zomma}\approx\frac{\Gamma(\sigma+\varepsilon)-\Gamma(\sigma-\varepsilon)}{2\varepsilon}
  ```

- **Gamma 的多变量局部桥接**

  ```latex
  d\Gamma\approx\operatorname{Speed}\,dS+\operatorname{Zomma}\,d\sigma+\operatorname{Color}_t\,dt
  ```

### 04 / 风险边界

#### Zomma 只能描述当前曲面附近的 Gamma 变化

大幅 IV 变化会改变曲面坐标、Vega、Vomma 以及更高阶项；若同时发生 spot 跳空，固定 strike 与固定 Delta 曲面的映射也会变化。此时一个 Zomma 值不足以代表组合。

Zomma 的正负不能证明 Gamma 会改善或恶化，因为实际结果还取决于 IV 方向、价格路径、仓位符号和交易成本。它也不能从开放兴趣量推断做市商 Gamma 或未来对冲流。

- Zomma 与 Gamma 基础口径、IV 单位和曲面节点一起展示。
- 平行小冲击用于诊断，非平行和大冲击使用完整曲面重估。
- 不要假设固定符号，也不要由 OI 推断未知参与者仓位。
- 本课用于管理 Gamma–IV 交叉风险，不构成波动率或方向交易建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Zomma is gamma's local derivative with respect to implied volatility and, equivalently, vega's second derivative with respect to spot. It describes how the gamma curve reshapes after an IV change, but not where IV will move or how unknown participants will hedge.

Use zomma to connect gamma and IV, align vol-point scaling, and validate gamma redistribution under parallel, skew, and joint spot-IV scenarios.

### 01 / Concept Boundary

#### Zomma Is The Gamma–IV Cross Sensitivity

Holding S, maturity, rates, and dividends fixed, zomma measures the gamma change caused by a small change in σ. In a smooth model it is V's third derivative with respect to S, S, and σ. Its sign varies with d1d2, moneyness, maturity, and model inputs.

In a Black–Scholes-type model, zomma can be written as gamma × (d1d2-1)/σ. Because the bracketed term can cross zero, a long option cannot be reduced to permanently long or short zomma; the same contract may reverse as spot and maturity change.

- **Zomma definition**

  ```latex
  \operatorname{Zomma}=\frac{\partial\Gamma}{\partial\sigma}=\frac{\partial^3V}{\partial S^2\,\partial\sigma}=\frac{\partial^2\operatorname{Vega}}{\partial S^2}
  ```

- **Black–Scholes-type identity**

  ```latex
  \operatorname{Zomma}=\Gamma\frac{d_1d_2-1}{\sigma}
  ```

| Greek | Input direction | Output change |
| --- | --- | --- |
| Speed | Spot | Gamma |
| Color | Calendar time | Gamma |
| Zomma | IV | Gamma |

### 02 / Mechanics And Measurement

#### Zomma Per One Vol Point Requires A 0.01 Scale

If the analytical derivative uses σ on a zero-to-one decimal scale, a one-vol-point IV rise means dσ=0.01, so gamma change is approximately raw zomma × 0.01. A platform may already report per-vol-point zomma, so verify metadata before portfolio ingestion.

Portfolio zomma sums by side, quantity, multiplier, and aligned gamma units while retaining strike and maturity nodes. An IV surface is not one σ: changes in ATM level, put skew, call wing, and term structure activate different zomma nodes.

- Confirm whether gamma is per price unit, per 1% spot move, or cash gamma.
- Confirm whether zomma uses absolute volatility decimal, vol point, or relative change.
- Do not replace node risk across the strike-expiry surface with one parallel-IV number.

- **Gamma drift under a small IV move**

  ```latex
  d\Gamma\approx\operatorname{Zomma}\,d\sigma
  ```

- **Per-vol-point conversion**

  ```latex
  \operatorname{Zomma}_{1vp}=0.01\,\operatorname{Zomma}_{raw}
  ```

### 03 / Reading Workflow

#### Compare Gamma Curves Across Two IV Slices

Hold the spot grid, maturity, rates, and dividends fixed and plot gamma curves at σ-ε and σ+ε. The curve difference at each S node divided by 2ε gives finite-difference zomma, directly showing the ATM peak widening or narrowing and sign changes in the wings.

In practice, first use a small parallel-IV shock to validate the field, then run skew twists, front-event premium, and same/opposite-direction joint spot-IV scenarios. Compare the local zomma prediction with fully repriced gamma and stop linear extrapolation as error grows.

- Step 1: Align σ, gamma, and zomma units.
- Step 2: Compare the full gamma curve under symmetric small IV shocks.
- Step 3: Run level, skew, and term scenarios by strike-expiry node.
- Step 4: Add spot and time paths and reconcile with full repricing.

- **Central finite difference for zomma**

  ```latex
  \operatorname{Zomma}\approx\frac{\Gamma(\sigma+\varepsilon)-\Gamma(\sigma-\varepsilon)}{2\varepsilon}
  ```

- **Multivariable local bridge for gamma**

  ```latex
  d\Gamma\approx\operatorname{Speed}\,dS+\operatorname{Zomma}\,d\sigma+\operatorname{Color}_t\,dt
  ```

### 04 / Risk Boundary

#### Zomma Describes Gamma Change Only Near The Current Surface

A large IV move changes surface coordinates, vega, vomma, and higher-order terms; with a simultaneous spot gap, the mapping between fixed-strike and fixed-delta surfaces also changes. One zomma value is then insufficient for the portfolio.

Zomma's sign cannot prove gamma will improve or deteriorate because the realized outcome also depends on IV direction, spot path, position sign, and costs. Nor can it infer dealer gamma or future hedge flow from open interest.

- Display zomma with the gamma convention, IV unit, and surface node.
- Use small parallel shocks for diagnostics and full-surface repricing for non-parallel or large shocks.
- Assume neither a fixed sign nor unknown participant positions from OI.
- This lesson manages gamma-IV cross risk and is not volatility or directional trading advice.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- occ-options-disclosure
