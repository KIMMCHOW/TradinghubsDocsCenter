---
title: "Speed：Gamma 随标的价格的变化"
title_en: "Speed: How Gamma Changes With Spot"
slug: "speed-gamma-spot-drift"
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
  - "Speed：Gamma 随标的价格的变化"
  - "Speed: How Gamma Changes With Spot"
  - "speed-gamma-spot-drift"
source_url: "https://tradinghubs.org/docs/trading-knowledge/speed-gamma-spot-drift"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Speed：Gamma 随标的价格的变化

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[vega-decay-veta|Vega Decay / Veta：Vega 随时间的变化]] ｜ 下一课：[[color-gamma-time-drift|Color：Gamma 随时间的漂移]]

**高级 · Greeks 与敏感度 · 21 分钟**

> Gamma 说明 Delta 曲线当前有多陡；Speed 进一步说明标的移动后 Gamma 会怎样改变。它是三阶局部导数，适合诊断 Gamma 集中区的非线性，不是上涨、下跌或反转信号。

把 Speed 读作 Gamma 曲线对 Spot 的局部斜率，用有限差分、单位检查和价格路径重估识别“Gamma 并非常数”的风险。

### 01 / 概念边界

#### Speed 是 Gamma 曲线在当前 Spot 的斜率

设 V 对标的价格 S 足够光滑。Delta 是一阶、Gamma 是二阶，而 Speed 是对 S 的三阶导数。正 Speed 表示在当前坐标附近向更高 S 移动时 Gamma 增加；负 Speed 表示 Gamma 减少。这个符号只描述局部曲线方向。

Gamma 曲线通常在接近平值区域形成峰值，因此 Speed 常在峰值两侧改变符号，并在峰顶附近接近零。Call 与 Put 在相同参数下可共享 Gamma 与 Speed，但美式行权、股息、不同 IV 节点和报价误差会破坏简单对称。

- **Speed 定义**

  ```latex
  \operatorname{Speed}=\frac{\partial\Gamma}{\partial S}=\frac{\partial^3V}{\partial S^3}
  ```

- **Black–Scholes 型恒等式**

  ```latex
  \operatorname{Speed}=-\frac{\Gamma}{S}\left(1+\frac{d_1}{\sigma\sqrt{\tau}}\right)
  ```

| Greek | 局部问题 | 典型价格单位 |
| --- | --- | --- |
| Delta | V 随 S 改变多少 | 价值 / 价格 |
| Gamma | Delta 随 S 改变多少 | Delta / 价格 |
| Speed | Gamma 随 S 改变多少 | Gamma / 价格 |

### 02 / 机制与度量

#### Speed 修正恒定 Gamma 假设

在小幅 Spot 变化下，Speed 给出 Gamma 的一阶漂移。若继续展开 Delta，除 Gamma × dS 外还会出现 1/2 × Speed × (dS)²；这解释了为什么在快速穿越执行价时，用初始 Gamma 线性更新 Delta 会逐渐偏离。

Speed 的数值随 S 的计价单位改变：同一经济风险用美元点、指数点或经过拆股调整的价格表示时，数字尺度不同。跨标的比较应使用一致的价格冲击、合约乘数和名义金额，或直接比较统一情景下的现金 Delta 变化。

- 确认 Gamma 与 Speed 是每股、每点还是整份合约口径。
- 组合汇总需纳入 position side、数量、乘数和估值币种。
- 保留 strike-expiry 分桶，净 Speed 可能掩盖两侧相反斜率。

- **小幅 Spot 变化下的 Gamma 漂移**

  ```latex
  d\Gamma\approx\operatorname{Speed}\,dS
  ```

- **Delta 的三阶局部展开**

  ```latex
  d\Delta\approx\Gamma\,dS+\frac{1}{2}\operatorname{Speed}(dS)^2
  ```

### 03 / 阅读流程

#### 沿 Gamma 曲线读取峰值、斜率与路径误差

在 Gamma 实验中固定 IV、期限、利率与股息，沿 S 绘制 Gamma。当前点切线斜率就是 Speed；用 S-ε 与 S+ε 的中央有限差分核验。然后比较初始 Gamma、Gamma+Speed×dS 与新 Spot 的完整 Gamma。

对实盘组合，分别测试向上和向下价格路径，因为 Speed 会随路径改变，单次大跳与多次小步并不必然得到相同的对冲轨迹。还应同时重估 IV skew，因为 spot 变化常伴随节点 IV 改变。

- 步骤 1：冻结非 Spot 输入并绘制 Gamma(S)。
- 步骤 2：用对称小价格步长核验 Speed。
- 步骤 3：比较恒定 Gamma、Speed 修正与完整重估。
- 步骤 4：运行上行、下行及 spot–skew 联合路径。

- **Speed 的中央有限差分**

  ```latex
  \operatorname{Speed}\approx\frac{\Gamma(S+\varepsilon)-\Gamma(S-\varepsilon)}{2\varepsilon}
  ```

### 04 / 风险边界

#### 三阶导数对步长、模型与到期距离更敏感

Speed 会放大定价噪声。有限差分 ε 太小会受浮点与报价误差影响，太大又不再代表局部斜率；临近到期、接近执行价时，Gamma 峰值变窄，稳定窗口尤其有限。

Speed 不包含 IV、时间、跳空、流动性或离散行权效应。任何大行情风险判断都应使用多节点路径与完整重估，不能把正负 Speed 解读为价格磁吸、支撑阻力或必然对冲方向。

- 把 Speed 与对应 Gamma 曲线、价格单位和差分步长一起展示。
- 仅在小范围内使用 Speed 更新 Gamma 或 Delta。
- 大行情和到期附近改用逐节点完整重估。
- 本课不把 Speed 解释为市场方向信号，也不构成交易建议。

## 相关概念

- [[gamma-convexity|Gamma 与凸性：为什么买方 Long Gamma]] — Speed 是 Gamma 对现货的三阶导，描述凸性自身的变化。
- [[delta-curve|Delta 曲线：从 Buy Call 推导方向敏感度]] — 只有把 Delta 曲线画出来，Speed 才有可读的几何含义。
- [[dynamic-delta-hedging|动态 Delta 对冲与路径风险]] — 高 Speed 意味着较大位移后原有对冲比例会迅速失效。
- [[model-assumptions-and-model-risk|模型假设与模型风险：从公式正确到决策可靠]] — 三阶敏感度对模型设定极为敏感，只宜用于小幅位移。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Gamma tells how steep the delta curve is now; speed tells how gamma itself changes after spot moves. It is a local third derivative useful for diagnosing nonlinearity around concentrated gamma, not a signal for a rally, selloff, or reversal.

Read speed as the local spot slope of the gamma curve, using finite differences, unit checks, and path repricing to recognize that gamma is not constant.

### 01 / Concept Boundary

#### Speed Is The Gamma Curve's Slope At Current Spot

Assume V is sufficiently smooth in spot S. Delta is first order, gamma second order, and speed the third derivative with respect to S. Positive speed means gamma increases locally as S rises; negative speed means it decreases. The sign describes only the local curve direction.

The gamma curve usually peaks around an at-the-money region, so speed often changes sign across that peak and approaches zero near the top. Calls and puts can share gamma and speed under identical parameters, while American exercise, dividends, different IV nodes, and quote errors break simple symmetry.

- **Speed definition**

  ```latex
  \operatorname{Speed}=\frac{\partial\Gamma}{\partial S}=\frac{\partial^3V}{\partial S^3}
  ```

- **Black–Scholes-type identity**

  ```latex
  \operatorname{Speed}=-\frac{\Gamma}{S}\left(1+\frac{d_1}{\sigma\sqrt{\tau}}\right)
  ```

| Greek | Local question | Typical price unit |
| --- | --- | --- |
| Delta | How V changes with S | Value / price |
| Gamma | How delta changes with S | Delta / price |
| Speed | How gamma changes with S | Gamma / price |

### 02 / Mechanics And Measurement

#### Speed Corrects The Constant-Gamma Assumption

For a small spot move, speed gives the first-order drift in gamma. Expanding delta adds one-half × speed × (dS)² beyond gamma × dS; this explains why updating delta with constant initial gamma diverges as spot moves quickly through a strike.

Speed's numerical value changes with the unit used for S: the same economics represented in dollars, index points, or split-adjusted prices produces different scales. Cross-underlying comparisons need consistent price shocks, multipliers, and notionals, or should compare cash delta changes under one standardized scenario.

- Confirm whether gamma and speed are per share, per point, or per contract.
- Portfolio aggregation needs position side, quantity, multiplier, and valuation currency.
- Preserve strike-expiry buckets because net speed can hide opposing slopes on either side.

- **Gamma drift under a small spot move**

  ```latex
  d\Gamma\approx\operatorname{Speed}\,dS
  ```

- **Third-order local expansion of delta**

  ```latex
  d\Delta\approx\Gamma\,dS+\frac{1}{2}\operatorname{Speed}(dS)^2
  ```

### 03 / Reading Workflow

#### Read Peaks, Slopes, And Path Error Along The Gamma Curve

In the gamma lab, hold IV, maturity, rates, and dividends fixed and plot gamma across S. The tangent slope at the current point is speed; validate it with a central difference at S-ε and S+ε. Then compare initial gamma, gamma plus speed × dS, and fully repriced gamma at the new spot.

For a live portfolio, test both up and down price paths because speed changes along the path; one large jump and many small steps need not produce the same hedge trajectory. Reprice IV skew at the same time because spot moves often come with node-IV changes.

- Step 1: Freeze non-spot inputs and plot gamma as a function of S.
- Step 2: Validate speed with symmetric small price steps.
- Step 3: Compare constant gamma, speed-corrected, and full repricing.
- Step 4: Run upward, downward, and joint spot-skew paths.

- **Central finite difference for speed**

  ```latex
  \operatorname{Speed}\approx\frac{\Gamma(S+\varepsilon)-\Gamma(S-\varepsilon)}{2\varepsilon}
  ```

### 04 / Risk Boundary

#### A Third Derivative Is More Sensitive To Step Size, Model, And Expiry

Speed amplifies pricing noise. A finite-difference ε that is too small picks up floating-point and quote error; one that is too large no longer represents a local slope. Near expiry and a strike, the gamma peak narrows and the stable window is especially limited.

Speed excludes IV, time, gaps, liquidity, and discrete exercise effects. Any large-move risk assessment requires multi-node paths and full repricing; positive or negative speed is not price magnetism, support/resistance, or a forced hedge direction.

- Show speed with its gamma curve, price unit, and difference step.
- Use speed to update gamma or delta only over a small neighborhood.
- Use node-by-node full repricing for large moves and near expiry.
- This lesson does not interpret speed as a market-direction signal and is not trading advice.

## Related Concepts

- [[gamma-convexity|Gamma And Convexity: Why Buyers Are Long Gamma]] — Speed is the third derivative with respect to spot: how convexity itself changes.
- [[delta-curve|Delta Curve: Deriving Directional Sensitivity From A Buy Call]] — Speed only becomes geometrically readable once the delta curve is drawn.
- [[dynamic-delta-hedging|Dynamic Delta Hedging And Path Risk]] — High speed means the existing hedge ratio fails quickly after a larger move.
- [[model-assumptions-and-model-risk|Model Assumptions And Model Risk: From Correct Formula To Reliable Decision]] — Third-order sensitivities are highly model-dependent and are only usable for small moves.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- occ-options-disclosure
