---
title: "Time Butterfly：期限曲率与三到期日重估"
title_en: "Time Butterflies: Term Curvature And Three-Expiry Revaluation"
slug: "time-butterfly-term-structure"
type: lesson
level: Advanced
order: 82
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "24 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "Time Butterfly：期限曲率与三到期日重估"
  - "Time Butterflies: Term Curvature And Three-Expiry Revaluation"
  - "time-butterfly-term-structure"
source_url: "https://tradinghubs.org/docs/trading-knowledge/time-butterfly-term-structure"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Time Butterfly：期限曲率与三到期日重估

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[christmas-tree-and-ladder-spreads|Christmas Tree 与 Ladder：先核对腿部口径]] ｜ 下一课：[[market-making-inventory-adverse-selection|做市库存与逆向选择：价差收入不是免费收益]]

**高级 · 结构、定价与波动率 · 24 分钟**

> Time Butterfly 交易的是期限方向的曲率，不是执行价方向的传统 Butterfly。由于三条腿没有共同到期日，任何固定最大盈利、最大亏损或唯一盈亏平衡点都必须先声明估值日和各期限市场输入。

理解同执行价、三到期日的 Time Butterfly，把 -1:+2:-1 识别为等间隔下的负中心二阶差分，并使用逐腿 Greeks 和前端到期重估。

### 01 / 三个到期日

#### 同一执行价的 -1 : +2 : -1 是负的中心二阶差分

设 T₁<T₂<T₃，三条腿使用同一标的、同一期权类型和同一执行价 K。本课把 Long Time Butterfly 定义为卖出近月一份、买入中月两份、卖出远月一份，即 -1:+2:-1。这个命名在不同资料中可能反向，因此订单仍需逐腿确认。

当 T₂-T₁=T₃-T₂=h 时，该组合等于常规中心二阶差分的相反数，局部近似为 -h²VTT；它可以看成一份 Long T₁/T₂ Calendar 与一份方向相反的 T₂/T₃ Calendar 叠加。若两个期限间隔不等，固定 -1:+2:-1 不再是标准曲率权重，必须逐腿估值或使用与间隔匹配的差分权重。Call 与 Put 版本都可构造，但利率、股息、提前行权和各期限远期会使二者在到期前不必等价。

- **Long Time Butterfly 价值**

  ```latex
  B_j(t)=-V_j(t;K,T_1)+2V_j(t;K,T_2)-V_j(t;K,T_3),\quad j\in\{C,P\}
  ```

- **等间隔下的曲率符号**

  ```latex
  B_j(t)\approx-h^2\left.\frac{\partial^2V_j}{\partial T^2}\right|_{T_2},\qquad T_2-T_1=T_3-T_2=h
  ```

- **相邻 Calendar 分解**

  ```latex
  [-V_j(T_1)+V_j(T_2)]+[V_j(T_2)-V_j(T_3)]
  ```

| 腿 | Long Time Butterfly | 主要风险 |
| --- | --- | --- |
| 近月 T₁ | Short 1 | 最先到期、Gamma 与指派 |
| 中月 T₂ | Long 2 | 蝶身 IV 与流动性 |
| 远月 T₃ | Short 1 | 长期 Vega、利率与尾部曲面 |

### 02 / 估值时点

#### 近月到期时，另外两条腿仍有市场价值

在任意 t<T₁ 时，三条腿都必须用当时各自的远期、IV、利率、股息或持有收益完整估值。到 T₁ 时，近月腿变成到期内在价值，但 T₂ 和 T₃ 仍含剩余时间价值，所以组合不是只由 S(T₁) 决定的一条静态折线。

期限结构发生非平行变化时，净 Vega 可能掩盖中月单独上移或两侧到期月上移的相反影响。应保留每个到期节点的 Vega 与总方差，并对中月事件、前端倒挂和远端风险溢价分别做情景，而不是把三个 IV 压成一个数字。

- 先声明估值日与平仓规则，再计算盈亏或盈亏平衡。
- 按到期节点保存 IV、Vega、Rho 与股息敏感度，不只保存净值。
- 若让某条腿自然到期，必须重新识别剩余组合和可能出现的标的持仓。

- **近月到期前的简化融资调整 Mark P&L**

  ```latex
  \Pi_{t<T_1}=B_j(t)-B_j(t_0)e^{r(t-t_0)}
  ```
  仅适用于连续复利融资率 r 恒定、期间没有费用、现金流、行权或指派的简化标记；一般情形须另计实际融资因子、交易现金流和成本。

- **近月到期时的 Long Call Time Butterfly**

  ```latex
  B_C(T_1)=-(S_{T_1}-K)^++2C_{T_1}(K,T_2)-C_{T_1}(K,T_3)
  ```

- **任一 Greek 的策略加权和**

  ```latex
  G_B=-G(T_1)+2G(T_2)-G(T_3)
  ```

### 03 / 期限曲率流程

#### 把期限曲率、价格路径与执行风险分层处理

在各腿接近平值、期限间隔相近且曲面平滑的局部情景下，Long Time Butterfly 可能呈现 Long Theta、Long Vega、Short Gamma，但这不是全局符号。标的远离 K、期限间隔不均、前端事件溢价或远月 IV 单独变化，都可能翻转其中一项。

三到期组合还叠加了价差、部分成交与多次到期管理。美式 Short Leg 可能提前指派；靠近 K 时，盘后价格变化会制造 Pin Risk。研究时的模型标记必须与可成交 Bid / Ask 分开，保证金和到期后仓位也应作为独立输出。

- 第一步：确认共同执行价、三个到期日、-1:+2:-1 数量与 Call / Put 类型。
- 第二步：绘制三个期限节点的 IV、总方差与逐腿 Greeks，而非只看净值。
- 第三步：指定 T₁ 前、T₁ 当日和 T₁ 后三类管理路径并完整重估。
- 期限曲率结构成本与路径敏感，本课不推荐任何到期组合或持有方式。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> A time butterfly expresses curvature across maturities rather than the strike geometry of a traditional butterfly. Because its legs do not share one expiry, any fixed maximum profit, maximum loss, or unique break-even requires a stated valuation date and market inputs for every maturity.

Understand a same-strike, three-expiry time butterfly by recognizing -1:+2:-1 as a negative centered second difference under equal spacing, then using leg-level Greeks and front-expiry revaluation.

### 01 / Three Expiries

#### A Same-Strike -1 : +2 : -1 Package Is A Negative Centered Second Difference

Let T₁<T₂<T₃, with all legs sharing the same underlying, option type, and strike K. This lesson defines a long time butterfly as short one near expiry, long two middle-expiry options, and short one far expiry: -1:+2:-1. Other sources may reverse the label, so the ticket must still be confirmed leg by leg.

When T₂-T₁=T₃-T₂=h, this package is the negative of the conventional centered second difference and is locally approximately -h²VTT. It can be decomposed into a long T₁/T₂ calendar plus an oppositely directed T₂/T₃ calendar. If the maturity gaps are unequal, fixed -1:+2:-1 quantities are no longer standard curvature weights; value the legs directly or use gap-adjusted difference weights. Call and put versions are both possible, but rates, dividends, early exercise, and maturity-specific forwards mean they need not be equivalent before expiry.

- **Long time-butterfly value**

  ```latex
  B_j(t)=-V_j(t;K,T_1)+2V_j(t;K,T_2)-V_j(t;K,T_3),\quad j\in\{C,P\}
  ```

- **Curvature sign under equal spacing**

  ```latex
  B_j(t)\approx-h^2\left.\frac{\partial^2V_j}{\partial T^2}\right|_{T_2},\qquad T_2-T_1=T_3-T_2=h
  ```

- **Adjacent-calendar decomposition**

  ```latex
  [-V_j(T_1)+V_j(T_2)]+[V_j(T_2)-V_j(T_3)]
  ```

| Leg | Long time butterfly | Primary risk |
| --- | --- | --- |
| Near T₁ | Short 1 | First expiry, gamma, and assignment |
| Middle T₂ | Long 2 | Body IV and liquidity |
| Far T₃ | Short 1 | Long-horizon vega, rates, and surface |

### 02 / Valuation Date

#### At The Front Expiry, Two Other Legs Still Have Market Value

At any t<T₁, all three legs require full valuation using their maturity-specific forward, IV, rates, and dividends or carry. At T₁, the front option becomes terminal intrinsic value, while T₂ and T₃ still contain time value, so the package is not a static line determined only by S(T₁).

When term structure moves non-parallel, net vega can hide opposite effects from a middle-expiry rise versus wing-expiry rises. Preserve vega and total variance at each maturity, and scenario-test a middle-month event, front inversion, and back-end risk premium separately rather than compressing three IVs into one number.

- State valuation date and exit rule before calculating P&L or break-even.
- Keep maturity-node IV, vega, rho, and dividend sensitivity rather than net values alone.
- If one leg expires naturally, re-identify the remaining package and any resulting underlying position.

- **Simplified funding-adjusted mark P&L before the front expiry**

  ```latex
  \Pi_{t<T_1}=B_j(t)-B_j(t_0)e^{r(t-t_0)}
  ```
  This simplified mark assumes a constant continuously compounded funding rate r and no interim costs, cash flows, exercise, or assignment; a general ledger must add the actual funding factor, trading cash flows, and costs.

- **Long call time butterfly at the front expiry**

  ```latex
  B_C(T_1)=-(S_{T_1}-K)^++2C_{T_1}(K,T_2)-C_{T_1}(K,T_3)
  ```

- **Strategy-weighted sum for any Greek**

  ```latex
  G_B=-G(T_1)+2G(T_2)-G(T_3)
  ```

### 03 / Term-Curvature Workflow

#### Separate Term Curvature, Price Path, And Execution Risk

When all legs are near the money, maturity gaps are similar, and the surface is smooth, a long time butterfly may be locally long theta, long vega, and short gamma, but these are not global signs. Spot moving away from K, uneven maturity gaps, a front-event premium, or an isolated far-IV move can reverse one or more exposures.

A three-expiry package also adds spreads, partial-fill risk, and repeated expiry management. An American short leg may be assigned early, and after-hours moves near K can create pin risk. Research marks must be separated from executable bid-ask prices, with margin and post-expiry positions recorded as separate outputs.

- Step 1: Confirm the common strike, three expiries, -1:+2:-1 quantities, and call or put type.
- Step 2: Map IV, total variance, and leg Greeks at all three maturity nodes rather than net values alone.
- Step 3: Fully revalue management paths before T₁, at T₁, and after T₁.
- Term-curvature packages are cost- and path-sensitive; this lesson recommends no expiry set or holding method.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- oic-options-strategies
- occ-options-disclosure
