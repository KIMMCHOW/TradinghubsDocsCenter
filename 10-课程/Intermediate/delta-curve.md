---
title: "Delta 曲线：从 Buy Call 推导方向敏感度"
title_en: "Delta Curve: Deriving Directional Sensitivity From A Buy Call"
slug: "delta-curve"
type: lesson
level: Intermediate
order: 34
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "Delta 曲线：从 Buy Call 推导方向敏感度"
  - "Delta Curve: Deriving Directional Sensitivity From A Buy Call"
  - "delta-curve"
source_url: "https://tradinghubs.org/docs/trading-knowledge/delta-curve"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# Delta 曲线：从 Buy Call 推导方向敏感度

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[greeks-introduction|Greeks 入门]] ｜ 下一课：[[gamma-convexity|Gamma 与凸性：为什么买方 Long Gamma]]

**中级 · Greeks 与敏感度 · 18 分钟**

> Delta 不是凭空出现的数字。它来自期权价值曲线在当前 Spot 位置的局部斜率：Spot 轻微移动时，期权价值大约跟着移动多少。

从 Buy Call 到期前价值曲线、时间价值、凸性和切线斜率推导 Delta 的 S 型曲线。

### 01 / Buy Call 价值曲线

#### 到期前的 Buy Call 不是硬折线，而是含时间价值的弯曲曲线

到期时，Long Call 的 payoff 是一条从 Strike 开始向上折起的折线：低于 Strike 时价值为 0，高于 Strike 后随 Spot 上升。但到期前，期权还有时间价值，所以曲线不会突然折断，而是围绕 Strike 平滑过渡。

这条到期前价值曲线可以拆成两层：内在价值描述已经价内的部分，时间价值描述未来进入价内或继续扩张的可能性。ATM 附近通常时间价值最高，因为上行和下行路径仍然都很重要。

- **到期 Call payoff**

  ```latex
  \max(S-K,0)
  ```

- **到期前 Call 价值**

  ```latex
  C(S,t)=\text{Intrinsic Value}+\text{Time Value}
  ```

- **时间价值**

  ```latex
  \text{Time Value}=C(S,t)-\max(S-K,0)
  ```

### 02 / 切线斜率

#### Delta 是 Buy Call 价值曲线在当前 Spot 的切线斜率

如果只看很小的一段 Spot 变化，弯曲的期权价值曲线可以被一条切线近似。切线越陡，说明 Spot 每动 1 点，期权价值变化越大。这个局部斜率就是 Delta。

当 Spot 远低于 Strike，Buy Call 进入价内的概率较低，价值曲线较平，Delta 接近 0；当 Spot 远高于 Strike，Call 更像持有标的，Delta 接近 1。中间从 0 过渡到 1 的形状就是 Delta 的 S 型曲线。

- **Delta 定义**

  ```latex
  \Delta=\frac{\partial C}{\partial S}
  ```

- **小幅移动近似**

  ```latex
  \Delta C\approx\Delta\times\Delta S
  ```

### 03 / 可视化阅读

#### 图表的目的不是装饰，而是把斜率变化看出来

本课图表先显示 Buy Call 到期前价值、内在价值和时间价值，再在当前 Spot 上放一条切线。拖动 Spot 时，切线斜率会变化；把不同 Spot 的斜率连起来，就得到 Delta 曲线。

- Delta 描述方向暴露，但不是方向预测。
- 大量仓位的 Delta 变化会传导到 Dealer 的期货对冲需求。
- 先理解局部斜率，再讨论中性、对冲或盘中流动性。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Delta is not an isolated number. It is the local slope of the option value curve at the current spot: how much option value changes for a small spot move.

Derive the delta S-curve from a buy call's pre-expiry value curve, time value, convexity, and tangent slope.

### 01 / Buy Call Value Curve

#### Before Expiry, A Buy Call Is A Curved Value Line With Time Value

At expiration, a long-call payoff is a kinked line: zero below the strike and rising above it. Before expiration, the option still has time value, so the curve transitions smoothly around the strike instead of breaking abruptly.

The pre-expiry value curve has two layers: intrinsic value describes what is already in the money, while time value describes the remaining possibility of moving into or further into the money. Around ATM, time value is often highest because both paths still matter.

- **Expiration call payoff**

  ```latex
  \max(S-K,0)
  ```

- **Pre-expiry call value**

  ```latex
  C(S,t)=\text{Intrinsic Value}+\text{Time Value}
  ```

- **Time value**

  ```latex
  \text{Time Value}=C(S,t)-\max(S-K,0)
  ```

### 02 / Tangent Slope

#### Delta Is The Tangent Slope Of The Buy Call Value Curve

Over a very small spot move, the curved option value line can be approximated by a tangent. The steeper the tangent, the more the option value changes for a one-point spot move. That local slope is delta.

When spot is far below the strike, the buy call is less likely to finish in the money, the value curve is flatter, and delta is near 0. When spot is far above the strike, the call behaves more like the underlying, and delta approaches 1. The transition between 0 and 1 creates the delta S-curve.

- **Delta definition**

  ```latex
  \Delta=\frac{\partial C}{\partial S}
  ```

- **Small-move approximation**

  ```latex
  \Delta C\approx\Delta\times\Delta S
  ```

### 03 / Visual Reading

#### The Chart Exists To Make The Changing Slope Visible

The lab first shows buy-call pre-expiry value, intrinsic value, and time value, then places a tangent at the current spot. As spot moves, the tangent slope changes; connecting those slopes across spot gives the delta curve.

- Delta describes directional exposure, not direction prediction.
- Delta changes across large positioning can transmit into dealer futures hedging demand.
- Understand local slope before discussing neutrality, hedging, or intraday liquidity.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

