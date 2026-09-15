---
title: "Volga / Vomma：波动率凸性"
title_en: "Volga / Vomma: Volatility Convexity"
slug: "volga-vomma-volatility-convexity"
type: lesson
level: Advanced
order: 75
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
  - "Volga / Vomma：波动率凸性"
  - "Volga / Vomma: Volatility Convexity"
  - "volga-vomma-volatility-convexity"
source_url: "https://tradinghubs.org/docs/trading-knowledge/volga-vomma-volatility-convexity"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Volga / Vomma：波动率凸性

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[charm-delta-time-decay|Charm：Delta 随日历时间的漂移]] ｜ 下一课：[[vega-decay-veta|Vega Decay / Veta：Vega 随时间的变化]]

**高级 · Greeks 与敏感度 · 22 分钟**

> Volga、Vomma 与 volatility gamma 常指同一对象：期权价值对隐含波动率的二阶偏导。名字并不保证字段单位一致，也不保证数值总为正；先确认模型、IV 坐标和缩放，再讨论凸性。

理解 Vega 对 IV 的二阶变化，统一每 vol point 与每平方 vol point 单位，并用二阶近似与完整重估识别大波动率冲击风险。

### 01 / 概念边界

#### Vomma 衡量 Vega 随 IV 如何改变

Vega 是价值曲线对 σ 的斜率，Vomma 是这条斜率随 σ 的变化率。正 Vomma 表示在当前切点附近，沿指定 IV 方向移动时 Vega 上升；负 Vomma 表示 Vega 下降。该描述是局部曲率，不等同于组合一定从“波动率变化”中获利。

在 Black–Scholes 型模型中，Vomma 可写成 Vega、d1、d2 与 σ 的组合。由于 d1d2 可正可负，Vomma 会随 moneyness 和期限改变符号；“Long Option 总是 Long Volga”并不是普遍正确的规则。

- **Volga / Vomma 定义**

  ```latex
  \operatorname{Vomma}=\frac{\partial^2V}{\partial\sigma^2}=\frac{\partial\operatorname{Vega}}{\partial\sigma}
  ```

- **Black–Scholes 型恒等式**

  ```latex
  \operatorname{Vomma}=\operatorname{Vega}\frac{d_1d_2}{\sigma}
  ```

| 输出口径 | IV 变化单位 | 使用方式 |
| --- | --- | --- |
| Raw Vega | σ 改变 1.00 | 一阶项乘 dσ |
| Vega per vol point | σ 改变 0.01 | Raw Vega × 0.01 |
| Vomma per squared vol point | (0.01)² | Raw Vomma × 0.0001 |

### 02 / 机制与度量

#### 二阶项修正只用 Vega 线性外推的误差

对小幅 IV 变化，Vega 给出线性损益，Vomma 给出 1/2 倍的二次修正。若 dσ 用小数，+5 vol points 应输入 0.05，而不是 5；二次项中的平方会把单位错误放大一万倍。

组合 Vomma 按方向、数量、乘数和估值币种汇总，但一个平行 IV 冲击只是一种诊断。实际波动率曲面常按到期和 Delta 非平行移动，因此应保存每个 strike-expiry 节点的 Vega 与 Vomma，并分别冲击 level、skew 和 term structure。

- 将 Vega 与 Vomma 的 IV 坐标统一为 absolute vol decimal 或明确的另一口径。
- 确认输出是否已包含 1/2；标准 Vomma 定义不包含 Taylor 展开中的 1/2。
- 跨币种组合先换算估值币，再按期限与 moneyness 分桶。

- **IV 方向的二阶价格近似**

  ```latex
  dV\approx\operatorname{Vega}\,d\sigma+\frac{1}{2}\operatorname{Vomma}(d\sigma)^2
  ```

- **每平方 vol point 的换算**

  ```latex
  \operatorname{Vomma}_{1vp^2}=0.01^2\,\operatorname{Vomma}_{raw}=0.0001\,\operatorname{Vomma}_{raw}
  ```

### 03 / 阅读流程

#### 比较 Vega 切线、Vomma 抛物线与完整重估

固定 S、期限、利率和股息，在 σ 附近选择对称小冲击。用期权价值的二阶中央差分核验 Vomma，再分别计算仅 Vega、一阶加二阶以及完整模型三条损益。二阶近似应在小冲击区改善线性误差。

市场阅读时至少运行平行 IV、前端独立变化、skew 旋转和 spot–IV 联合变化。若二阶近似与完整重估差距迅速扩大，说明更高阶项或曲面坐标变化已重要，应停止用单一 Vomma 概括。

- 步骤 1：确认 σ 与 Vega/Vomma 的缩放单位。
- 步骤 2：用对称小冲击核验二阶差分。
- 步骤 3：并排比较线性、二阶与完整重估误差。
- 步骤 4：对 level、skew、term 与 spot–IV 联合路径分别压力测试。

- **二阶中央差分核验**

  ```latex
  \operatorname{Vomma}\approx\frac{V(\sigma+\varepsilon)-2V(\sigma)+V(\sigma-\varepsilon)}{\varepsilon^2}
  ```

### 04 / 风险边界

#### 大 IV 冲击会离开局部曲率的有效邻域

Vomma 是当前模型曲面的局部二阶导数。大幅 IV 变化会改变 Vega、skew、期限结构，甚至改变定价模型适用性；离散股息、跳跃、波动率微笑和流动性也可能使简单 Black–Scholes 恒等式不足。

正 Vomma 只描述局部凸性，不能抵消初始权利金、Theta、方向风险或价差成本。实际风险预算应使用可成交报价和完整多变量情景，而不是以“正凸性”作为安全标签。

- 同时显示 Vega、Vomma、IV 单位和冲击大小。
- 小冲击可用二阶近似，大冲击必须完整重估。
- 不要假设 Vomma 恒正，也不要从单一平行冲击推断整张曲面。
- 本课用于识别波动率曲率风险，不构成买入或卖出波动率的建议。

## 相关概念

- [[vega-iv-sensitivity|Vega：IV 敏感度与波动率重定价]] — Volga 是 Vega 对波动率的二阶导，即波动率凸性。
- [[implied-volatility-surface|隐含波动率 IV 与波动率曲面]] — 曲面曲率决定同一结构在不同波动率水平上的表现差异。
- [[straddle-strangle-event-risk|Straddle、Strangle 与事件波动]] — 事件前后 IV 大幅变化时，Volga 决定结构的非对称反应。
- [[model-assumptions-and-model-risk|模型假设与模型风险：从公式正确到决策可靠]] — 二阶敏感度高度依赖模型设定，模型误差会被放大。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Volga, vomma, and volatility gamma often name the same object: the second derivative of option value with respect to implied volatility. The label guarantees neither common units nor a positive sign; confirm model, IV coordinate, and scaling before discussing convexity.

Understand the second-order change of value with IV, align per-vol-point and per-squared-vol-point units, and compare quadratic approximation with full repricing under large volatility shocks.

### 01 / Concept Boundary

#### Vomma Measures How Vega Changes With IV

Vega is the slope of value with respect to σ; vomma is the rate at which that slope changes with σ. Positive vomma means vega rises locally along the stated IV direction, while negative vomma means it falls. This is local curvature, not a promise that a position profits from any change in volatility.

In a Black–Scholes-type model, vomma can be expressed through vega, d1, d2, and σ. Because d1d2 can be positive or negative, vomma can change sign across moneyness and maturity; 'a long option is always long volga' is not a generally valid rule.

- **Volga / vomma definition**

  ```latex
  \operatorname{Vomma}=\frac{\partial^2V}{\partial\sigma^2}=\frac{\partial\operatorname{Vega}}{\partial\sigma}
  ```

- **Black–Scholes-type identity**

  ```latex
  \operatorname{Vomma}=\operatorname{Vega}\frac{d_1d_2}{\sigma}
  ```

| Output convention | IV move unit | How to use it |
| --- | --- | --- |
| Raw vega | σ changes by 1.00 | Multiply first-order term by dσ |
| Vega per vol point | σ changes by 0.01 | Raw vega × 0.01 |
| Vomma per squared vol point | (0.01)² | Raw vomma × 0.0001 |

### 02 / Mechanics And Measurement

#### The Quadratic Term Corrects A Vega-Only Extrapolation

For a small IV move, vega gives linear P&L and vomma supplies a one-half quadratic correction. If dσ is a decimal, +5 vol points is 0.05, not 5; squaring the move can amplify a unit error by ten thousand.

Portfolio vomma aggregates by side, quantity, multiplier, and valuation currency, but a parallel IV shock is only one diagnostic. Real volatility surfaces move non-parallel across maturity and delta, so preserve vega and vomma at each strike-expiry node and shock level, skew, and term structure separately.

- Align vega and vomma to absolute volatility decimal or another explicitly stated coordinate.
- Confirm whether output already includes one-half; standard vomma does not include the Taylor coefficient.
- Convert cross-currency positions to one valuation currency, then bucket by maturity and moneyness.

- **Second-order price approximation along IV**

  ```latex
  dV\approx\operatorname{Vega}\,d\sigma+\frac{1}{2}\operatorname{Vomma}(d\sigma)^2
  ```

- **Conversion per squared vol point**

  ```latex
  \operatorname{Vomma}_{1vp^2}=0.01^2\,\operatorname{Vomma}_{raw}=0.0001\,\operatorname{Vomma}_{raw}
  ```

### 03 / Reading Workflow

#### Compare The Vega Tangent, Vomma Quadratic, And Full Repricing

Hold S, maturity, rates, and dividends fixed and choose symmetric small shocks around σ. Validate vomma with a second central difference of option value, then compare vega-only, first-plus-second-order, and full-model P&L. The quadratic approximation should improve the linear error in a sufficiently small neighborhood.

For market reading, run at least parallel IV, isolated front-end, skew-rotation, and joint spot–IV scenarios. If the quadratic approximation diverges quickly from full repricing, higher-order terms or surface-coordinate changes matter and one vomma number should no longer summarize the risk.

- Step 1: Confirm σ and vega/vomma scaling units.
- Step 2: Validate the second difference with symmetric small shocks.
- Step 3: Compare linear, quadratic, and full-repricing errors side by side.
- Step 4: Stress level, skew, term, and joint spot–IV paths separately.

- **Second central-difference validation**

  ```latex
  \operatorname{Vomma}\approx\frac{V(\sigma+\varepsilon)-2V(\sigma)+V(\sigma-\varepsilon)}{\varepsilon^2}
  ```

### 04 / Risk Boundary

#### Large IV Shocks Leave The Local-Curvature Neighborhood

Vomma is a local second derivative of the current model surface. A large IV move changes vega, skew, term structure, and potentially model suitability; discrete dividends, jumps, smiles, and liquidity can also make a simple Black–Scholes identity insufficient.

Positive vomma describes local convexity only. It does not erase initial premium, theta, directional risk, or transaction spreads. Risk budgets should use executable quotes and full multivariable scenarios rather than treating positive convexity as a safety label.

- Display vega, vomma, IV units, and shock size together.
- Use a quadratic approximation for small shocks; fully reprice large shocks.
- Assume neither always-positive vomma nor an entire surface from one parallel shock.
- This lesson identifies volatility-curvature risk and does not advise buying or selling volatility.

## Related Concepts

- [[vega-iv-sensitivity|Vega: IV Sensitivity And Volatility Repricing]] — Volga is the second derivative of vega with respect to volatility, i.e. volatility convexity.
- [[implied-volatility-surface|Implied Volatility And Volatility Surface]] — Surface curvature determines how the same structure behaves at different volatility levels.
- [[straddle-strangle-event-risk|Straddles, Strangles, And Event Volatility]] — When IV moves sharply around an event, volga determines the structure's asymmetric response.
- [[model-assumptions-and-model-risk|Model Assumptions And Model Risk: From Correct Formula To Reliable Decision]] — Second-order sensitivities depend heavily on the model, so model error is amplified.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- occ-options-disclosure
