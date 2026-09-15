---
title: "Vanna：Delta 与波动率的交叉敏感度"
title_en: "Vanna: The Delta–Volatility Cross Sensitivity"
slug: "vanna-cross-sensitivity"
type: lesson
level: Advanced
order: 71
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
  - "Vanna：Delta 与波动率的交叉敏感度"
  - "Vanna: The Delta–Volatility Cross Sensitivity"
  - "vanna-cross-sensitivity"
source_url: "https://tradinghubs.org/docs/trading-knowledge/vanna-cross-sensitivity"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Vanna：Delta 与波动率的交叉敏感度

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[phi-foreign-rate-sensitivity|Foreign Rho / Phi：外币利率与持有收益敏感度]] ｜ 下一课：[[charm-delta-time-decay|Charm：Delta 随日历时间的漂移]]

**高级 · Greeks 与敏感度 · 22 分钟**

> Vanna 是给定期权或组合的模型交叉导数；VEX 是 TradingHub 现有 ODV 课程中讲解的预计算产品暴露字段。两者用途和数据契约不同：本课不会用通用的 OI × Vanna × Multiplier 公式重建 VEX，也不会据此推断做市商库存或对冲方向。

从 ∂Delta/∂σ 与 ∂Vega/∂S 两个等价视角理解 Vanna，统一波动率单位，并与现有 ODV VEX 产品暴露课程严格区分。

### 01 / 概念边界

#### 一次偏导的两条路径汇合成同一个交叉项

Vanna 衡量波动率变化时 Delta 如何改变，也等价于标的变化时 Vega 如何改变。在足够光滑且变量口径一致的模型中，混合偏导次序可以交换，因此两个定义给出同一局部敏感度。

符号不是固定的，取决于 moneyness、期限、利率、股息以及现货、远期或其他标准化 Delta 坐标。在满足 Put–Call Parity 的同执行价、同期限欧式模型中，Call 与 Put 的 Vanna 相同，因为 C-P 不依赖 σ；若观察到 Call / Put 差异，应先检查美式提前行权、奇异条款、不同 Delta 坐标或不一致输入，而不是把期权类型本身当作原因。

- **Vanna 的等价定义**

  ```latex
  \operatorname{Vanna}=\frac{\partial^2V}{\partial S\,\partial\sigma}=\frac{\partial\Delta}{\partial\sigma}=\frac{\partial\operatorname{Vega}}{\partial S}
  ```

- **小幅波动率变化下的 Delta 漂移**

  ```latex
  d\Delta\approx\operatorname{Vanna}\,d\sigma
  ```

| 对象 | 含义 | 能否相互替代 |
| --- | --- | --- |
| 单腿 Vanna | 指定模型下的 ∂Delta/∂σ | 统一坐标后进入同一标的组合 |
| 同一标的组合 Vanna | 逐腿方向、数量、乘数加权和 | 不能说明未知参与者持仓 |
| ODV VEX | 现有产品课程定义的预计算暴露字段 | 不能用通用 Vanna 公式替代 |

### 02 / 机制与度量

#### 先统一 Vol Decimal、Vol Point 与合约价值

若解析 Vanna 以 σ 从 0 到 1 的小数变化为单位，那么 IV 上升 1 个 vol point 等于 dσ=0.01，屏幕上的每 vol point Vanna 应乘 0.01。若 Delta 是每标的单位口径，乘以仓位数量与合约乘数后得到的是组合 Delta（或对冲单位）对 IV 的敏感度，并不是直接的损益；局部交叉损益还需要乘 dS·dσ。

原始 ∂Delta/∂σ 以标的单位表达，只能在同一标的、现货定义、波动率单位、估值币种和时间点下直接相加。跨标的风险应转换为现金 Delta 对各自波动率节点的敏感度，完成汇率换算，并保留逐标的/逐节点冲击向量；不能把原始 Vanna 标量直接相加。同一标的跨期限的标量和也只有在所有期限 IV 节点接受共同平行冲击 dσᵢ=dσ 时才成立；一般曲面情景应保留 strike × expiry Vanna 向量，且总数要与分桶同时展示，避免净值掩盖相反暴露。

- 记录 Delta 是 spot delta、forward delta 还是 premium-adjusted delta。
- 记录 Vanna 按 σ=1.00、1 vol point 还是 1% 相对 IV 变化输出。
- 组合表同时保存腿级 Vanna、分桶小计和全局净值。

- **每 1 vol point 的单位换算**

  ```latex
  \operatorname{Vanna}_{1vp}=0.01\,\frac{\partial\Delta}{\partial\sigma}
  ```

- **同一标的、共同平行 IV 节点冲击下的组合 Vanna**

  ```latex
  \operatorname{Vanna}_P^{parallel}=\sum_i q_iM_i\operatorname{Vanna}_i,\quad d\sigma_i=d\sigma
  ```

- **局部现货 × IV 交叉损益项**

  ```latex
  dV_{cross}\approx\operatorname{Vanna}_P^{parallel}\,dS\,d\sigma
  ```

### 03 / 阅读流程

#### 用 Delta 曲线在两个 IV 切片之间读 Vanna

在实验图中固定 S、期限、利率和股息，分别画出 σ-ε 与 σ+ε 的 Delta 曲线。两条曲线在某个 S 的垂直差除以 2ε，就是该点 Vanna 的有限差分近似；沿 S 移动则能看到符号和量级如何随 moneyness 变化。

实盘读取先做单变量 IV 冲击以核验模型值，再做 spot 与 IV 同向、反向的联合情景。交叉项只有在两个变量同时移动时才进入价格二阶近似；大行情或曲面重塑应逐腿完整重估。

- 步骤 1：固定模型、Delta 定义、估值时点和 IV 单位。
- 步骤 2：用小幅上下 IV 冲击核验 Vanna 符号与量级。
- 步骤 3：按执行价与到期桶查看，不让净值掩盖相反区域。
- 步骤 4：运行 Spot × IV 联合情景，并用完整重估检查交叉近似。

- **Vanna 的中央有限差分**

  ```latex
  \operatorname{Vanna}\approx\frac{\Delta(\sigma+\varepsilon)-\Delta(\sigma-\varepsilon)}{2\varepsilon}
  ```

- **价格展开中的 Spot–IV 交叉项**

  ```latex
  dV\supset\operatorname{Vanna}\,dS\,d\sigma
  ```

### 04 / 风险边界

#### Vanna 描述模型曲面，不证明谁会怎样对冲

单腿或自有组合 Vanna 可以从已知合约和模型计算；全市场的参与者方向、开平仓、覆盖头寸和对冲规则通常未知。开放兴趣量不是带方向的库存，因此不能把 OI 与 Vanna 相乘后宣称得到经销商对冲流。

现有 ODV VEX 课程应按其产品字段定义读取；Vanna 本课只教授通用 Greek。任何 VEX 数值、聚合、正负号与归因都不能从本课公式倒推或覆盖。

- 将 Vanna 标注为指定模型、指定单位、指定时点的局部导数。
- 只对已知方向的自有仓位求和；未知市场持仓保持未知。
- VEX 保持产品字段语义，不使用通用 OI × Vanna 公式重建。
- 本课不推断做市商库存、强制对冲方向或未来现货路径，也不构成交易建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Vanna is a model cross derivative for a stated option or portfolio; VEX is a precomputed product-exposure field taught in the existing TradingHub ODV lesson. Their purposes and data contracts differ: this lesson does not reconstruct VEX with a generic OI × Vanna × multiplier formula or infer dealer inventory or hedging direction from it.

Understand vanna through the equivalent ∂delta/∂σ and ∂vega/∂S views, align volatility units, and keep it strictly separate from the existing ODV VEX product-exposure lesson.

### 01 / Concept Boundary

#### Two First-Derivative Paths Meet In One Cross Term

Vanna measures how delta changes as volatility changes and, equivalently, how vega changes as spot changes. In a sufficiently smooth model with consistent variables, the mixed derivatives commute, so the two definitions represent one local sensitivity.

Its sign is not fixed and depends on moneyness, maturity, rates, dividends, and whether delta is spot, forward, or otherwise standardized. In a parity-consistent European model at the same strike and expiry, call and put vanna are equal because C-P is independent of σ. If call and put values differ, first inspect American exercise, exotic terms, delta coordinates, or inconsistent inputs rather than treating option type itself as the cause.

- **Equivalent vanna definitions**

  ```latex
  \operatorname{Vanna}=\frac{\partial^2V}{\partial S\,\partial\sigma}=\frac{\partial\Delta}{\partial\sigma}=\frac{\partial\operatorname{Vega}}{\partial S}
  ```

- **Delta drift under a small volatility move**

  ```latex
  d\Delta\approx\operatorname{Vanna}\,d\sigma
  ```

| Object | Meaning | Interchangeable? |
| --- | --- | --- |
| Single-leg vanna | ∂delta/∂σ under a stated model | Can enter a same-underlying portfolio after coordinate alignment |
| Same-underlying portfolio vanna | Leg sum weighted by side, quantity, and multiplier | Cannot reveal an unknown participant's position |
| ODV VEX | Precomputed exposure field defined by the existing product lesson | Must not be replaced by a generic vanna formula |

### 02 / Mechanics And Measurement

#### Align Vol Decimal, Vol Point, And Contract Value First

If analytical vanna uses a volatility decimal from 0 to 1, a one-vol-point IV rise means dσ=0.01, so displayed vanna per vol point is multiplied by 0.01. If delta is quoted per underlying unit, applying position quantity and contract multiplier produces the sensitivity of portfolio delta (or hedge units) to IV, not P&L by itself; the local cross-P&L term also requires dS·dσ.

Raw ∂delta/∂σ is expressed in underlying units and is directly additive only for the same underlying, spot definition, volatility unit, valuation currency, and timestamp. Cross-underlying risk should be converted into cash-delta sensitivity to each volatility node, translated into one currency, and preserved as per-underlying/per-node shock vectors; raw vanna scalars must not simply be added. A scalar sum across expiries of one underlying is valid only when every expiry-volatility node receives the same parallel shock dσᵢ=dσ. General surface scenarios should preserve a strike-by-expiry vanna vector and show bucket detail beside any total so opposing exposures are not hidden.

- Record whether delta is spot, forward, or premium-adjusted delta.
- Record whether vanna is per σ=1.00, one vol point, or a 1% relative IV move.
- Keep leg vanna, bucket subtotals, and the global net value together.

- **Conversion per one vol point**

  ```latex
  \operatorname{Vanna}_{1vp}=0.01\,\frac{\partial\Delta}{\partial\sigma}
  ```

- **Same-underlying portfolio vanna under a common parallel IV-node shock**

  ```latex
  \operatorname{Vanna}_P^{parallel}=\sum_i q_iM_i\operatorname{Vanna}_i,\quad d\sigma_i=d\sigma
  ```

- **Local spot-by-IV cross-P&L term**

  ```latex
  dV_{cross}\approx\operatorname{Vanna}_P^{parallel}\,dS\,d\sigma
  ```

### 03 / Reading Workflow

#### Read Vanna Between Delta Curves At Two IV Slices

In the lab, hold S, maturity, rates, and dividends fixed and plot delta curves at σ-ε and σ+ε. Their vertical difference at a given S divided by 2ε approximates vanna there; moving along S shows how sign and magnitude vary with moneyness.

For practical reading, first shock IV alone to validate the model value, then run joint spot-and-IV scenarios in the same and opposite directions. The cross term enters a second-order price approximation only when both variables move; large moves or surface reshaping require full leg-level repricing.

- Step 1: Fix the model, delta definition, valuation timestamp, and IV unit.
- Step 2: Verify vanna sign and magnitude with small up/down IV shocks.
- Step 3: Inspect strike and expiry buckets so netting does not hide opposing regions.
- Step 4: Run joint spot-by-IV scenarios and check the cross approximation against full repricing.

- **Central finite difference for vanna**

  ```latex
  \operatorname{Vanna}\approx\frac{\Delta(\sigma+\varepsilon)-\Delta(\sigma-\varepsilon)}{2\varepsilon}
  ```

- **Spot–IV cross term in a price expansion**

  ```latex
  dV\supset\operatorname{Vanna}\,dS\,d\sigma
  ```

### 04 / Risk Boundary

#### Vanna Describes A Model Surface, Not Who Will Hedge How

Single-leg or owned-portfolio vanna can be computed from known contracts and a model. Market-wide participant direction, opening versus closing, covered positions, and hedge rules are generally unknown. Open interest is not signed inventory, so multiplying OI by vanna does not establish dealer hedge flow.

The existing ODV VEX lesson must be read under its product-field definition; this lesson teaches only the generic Greek vanna. No VEX value, aggregation, sign, or attribution may be reverse-engineered or overwritten from this lesson's formulas.

- Label vanna as a local derivative for a stated model, unit, and timestamp.
- Aggregate only owned positions with known signs; unknown market positions remain unknown.
- Preserve VEX's product-field semantics; do not reconstruct it with generic OI × vanna.
- This lesson infers neither dealer inventory, forced hedge direction, nor future spot path and is not trading advice.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- occ-options-disclosure
