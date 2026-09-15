---
title: "Gamma 与凸性：为什么买方 Long Gamma"
title_en: "Gamma And Convexity: Why Buyers Are Long Gamma"
slug: "gamma-convexity"
type: lesson
level: Intermediate
order: 35
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "17 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "Gamma 与凸性：为什么买方 Long Gamma"
  - "Gamma And Convexity: Why Buyers Are Long Gamma"
  - "gamma-convexity"
source_url: "https://tradinghubs.org/docs/trading-knowledge/gamma-convexity"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# Gamma 与凸性：为什么买方 Long Gamma

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[delta-curve|Delta 曲线：从 Buy Call 推导方向敏感度]] ｜ 下一课：[[time-value-and-theta|时间价值与 Theta]]

**中级 · Greeks 与敏感度 · 17 分钟**

> Gamma 回答的问题是：Delta 自己变化得有多快。Delta 是价格曲线的斜率，Gamma 就是斜率的斜率，也就是曲率。

用 Delta S 曲线的切线斜率解释 Gamma，并说明标准期权买方为什么是 Long Gamma、卖方为什么是 Short Gamma。

### 01 / Delta 的斜率

#### Gamma 是 Delta S 型曲线在当前 Spot 的切线斜率

在 Delta 曲线上再次画切线，可以看到 Spot 变化时 Delta 本身变化有多快。ATM 附近 Delta 从 0 向 1 过渡最快，因此 Gamma 往往集中在 Strike 附近。

DTE 越短、IV 越低时，这个过渡区可能越窄，Gamma 峰值越尖；DTE 越长或 IV 越高时，Delta 变化通常更分散，Gamma 曲线更平缓。

- **Gamma 定义**

  ```latex
  \Gamma=\frac{\partial \Delta}{\partial S}=\frac{\partial^2 C}{\partial S^2}
  ```

- **Delta 更新近似**

  ```latex
  \Delta_{new}\approx\Delta_{old}+\Gamma\times\Delta S
  ```

### 02 / 买方与卖方

#### 标准期权买方持有凸性，所以 Long Gamma；卖方卖出凸性，所以 Short Gamma

Long Call 和 Long Put 的价值曲线都是凸的：价格往有利方向移动时，Delta 会让收益敏感度增加；价格往不利方向移动时，损失敏感度被权利金边界限制。这种向买方有利的弯曲就是 Long Gamma。

卖方的仓位是买方曲线的相反数。买方曲线向上凸，卖方曲线就向下凹；买方 Gamma 为正，卖方 Gamma 就为负。因此标准期权里，买方是 Long Gamma，卖方是 Short Gamma。

| 仓位 | 曲线形状 | Gamma 符号 |
| --- | --- | --- |
| Long Call / Long Put | 向上凸，持有权利和非线性收益。 | Long Gamma / 正 Gamma |
| Short Call / Short Put | 买方曲线的相反数，向下凹。 | Short Gamma / 负 Gamma |

### 03 / 对冲传导

#### Gamma 决定 Delta hedge 调整的速度和方向压力

如果一个 Dealer 净 Short Gamma，价格上涨会让需要对冲的 Delta 往上涨方向变化，价格下跌会让 Delta 往下跌方向变化，对冲可能追随价格并放大波动。净 Long Gamma 则可能形成相反的再平衡压力。

- Gamma 是对冲敏感度，不是方向信号。
- Gamma 高的 Strike 附近，Delta hedge 可能更频繁。
- 理解 Long / Short Gamma 后，再看吸附、加速和 0DTE 盘中波动会更清楚。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Gamma asks how fast delta itself changes. Delta is the slope of the price curve; gamma is the slope of that slope, or curvature.

Use the tangent slope of the delta S-curve to explain gamma, and why standard option buyers are long gamma while sellers are short gamma.

### 01 / Slope Of Delta

#### Gamma Is The Tangent Slope Of The Delta S-Curve

Draw a tangent on the delta curve and you can see how quickly delta itself changes as spot moves. Around ATM, delta transitions fastest from 0 toward 1, so gamma often concentrates near the strike.

When DTE is lower or IV is lower, the transition zone can narrow and the gamma peak can become sharper. With more time or higher IV, delta changes are usually more spread out and gamma is flatter.

- **Gamma definition**

  ```latex
  \Gamma=\frac{\partial \Delta}{\partial S}=\frac{\partial^2 C}{\partial S^2}
  ```

- **Delta update approximation**

  ```latex
  \Delta_{new}\approx\Delta_{old}+\Gamma\times\Delta S
  ```

### 02 / Buyer And Seller

#### Standard Option Buyers Own Convexity, So They Are Long Gamma; Sellers Sell Convexity, So They Are Short Gamma

Long calls and long puts both have convex value curves: when price moves favorably, delta makes upside sensitivity increase; when price moves unfavorably, loss sensitivity is constrained by the premium boundary. That buyer-owned curvature is long gamma.

The seller's position is the negative of the buyer's curve. If the buyer's curve is convex upward, the seller's curve is concave downward; positive buyer gamma becomes negative seller gamma. In standard options, buyers are long gamma and sellers are short gamma.

| Position | Curve shape | Gamma sign |
| --- | --- | --- |
| Long Call / Long Put | Convex upward; owns optionality and nonlinear upside. | Long Gamma / positive gamma |
| Short Call / Short Put | The inverse of the buyer curve, concave downward. | Short Gamma / negative gamma |

### 03 / Hedging Transmission

#### Gamma Drives How Quickly Delta Hedges Must Adjust

If a dealer is net short gamma, rising prices can push hedge delta in the rising direction and falling prices can push it lower, so hedging can follow price and amplify movement. Net long gamma can create the opposite rebalancing pressure.

- Gamma is hedge sensitivity, not a direction signal.
- Around high-gamma strikes, delta hedges may need more frequent adjustment.
- Once long / short gamma is clear, pinning, acceleration, and 0DTE intraday movement become easier to read.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

