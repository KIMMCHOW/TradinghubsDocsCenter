---
title: "Black-Scholes-Merton Pricing Model"
title_en: "Black-Scholes-Merton Pricing Model"
slug: "bsm-pricing-model"
type: lesson
level: Advanced
order: 58
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "Black-Scholes-Merton Pricing Model"
  - "bsm-pricing-model"
source_url: "https://tradinghubs.org/docs/trading-knowledge/bsm-pricing-model"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# Black-Scholes-Merton Pricing Model

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[binomial-risk-neutral-pricing|二叉树与风险中性定价]] ｜ 下一课：[[volatility-forecasting|波动率预测：从实现方差到样本外条件预测]]

**高级 · 结构、定价与波动率 · 18 分钟**

> 定价公式必须匹配合约标的。现货或指数现货口径可从含收益率 q 的 BSM 出发；以 Futures / Forward 为直接输入的欧式期权通常用 Black-76 表达。两种模型不能只替换变量名后混用。

理解 Spot、Forward / Futures、Strike、DTE、Rate、Yield 与 Volatility 如何进入现货 BSM 或期货 Black-76，并据此解释理论价格和 Greeks。

### 01 / 输入输出

#### 先区分 Spot BSM 与 Futures / Forward Black-76

含连续收益率的现货 BSM 使用 S₀、K、T、r、q 与 σ。若 q=0，才可退化为不含股息或持有收益的简式。Black-76 则用同到期 Futures / Forward 价格 F₀,T 替代现货持有路径，并对期权终值整体折现。

- **含连续收益率的现货 BSM Call**

  ```latex
  C=S_0e^{-qT}N(d_1)-Ke^{-rT}N(d_2)
  ```
  适用于欧式现货口径，并显式包含连续股息或持有收益率 q。

- **含连续收益率的现货 BSM Put**

  ```latex
  P=Ke^{-rT}N(-d_2)-S_0e^{-qT}N(-d_1)
  ```
  与 Call 使用同一组现货 BSM 输入。

- **现货 BSM 标准化距离**

  ```latex
  d_1=\frac{\ln(S_0/K)+(r-q+\tfrac{1}{2}\sigma^2)T}{\sigma\sqrt{T}},\qquad d_2=d_1-\sigma\sqrt{T}
  ```
  r − q 表示现货持有关系中的净 Carry。

- **Black-76 欧式 Futures / Forward Call**

  ```latex
  C_F=e^{-rT}\left[F_{0,T}N(d_1^F)-KN(d_2^F)\right]
  ```
  使用与期权同到期的 F₀,T 作为直接价格输入。

- **Black-76 距离与 Put**

  ```latex
  d_1^F=\frac{\ln(F_{0,T}/K)+\tfrac{1}{2}\sigma^2T}{\sigma\sqrt{T}},\quad d_2^F=d_1^F-\sigma\sqrt{T},\quad P_F=e^{-rT}\left[KN(-d_2^F)-F_{0,T}N(-d_1^F)\right]
  ```
  Black-76 的 d₁ 不再额外加入 r − q，因为 Carry 已反映在 F₀,T 中。

| 输入 | 影响 |
| --- | --- |
| Spot 或 F₀,T / Strike | 必须匹配现货 BSM 或 Black-76 的模型基准。 |
| DTE | 影响时间价值和 Gamma / Theta。 |
| Volatility | 影响未来价格分布宽度。 |
| Rate | 影响折现和远期价值。 |
| Yield / Carry | 现货 BSM 通过 q 表达；Black-76 中已进入 F₀,T。 |

### 02 / 假设与边界

#### 模型是框架，不是现实市场的完整副本

BSM 与 Black-76 的基础闭式公式都针对欧式行权，并依赖连续价格路径、无交易成本、波动率常数和利率常数等简化。美式提前行权、离散股息、期货保证金结算、跳空、滑点、流动性断层、偏斜和事件风险需要其他模型或显式调整。

在 0DTE 和事件日中，模型输出只能作为变量敏感度参考，而不能当作现实价格的保证。

### 03 / 风险传导

#### 理论价格变化会改变 Dealer 风险暴露

分析 ES / NQ 相关期权前，先确认合约究竟以指数现货、ETF、Futures 还是 Forward 为定价基准，以及行权风格和结算方式。模型输入变化会改变 Delta / Gamma；只有 dealer 持仓方向已知时，才能进一步讨论相应期货对冲方向。

- 现货 BSM 与 Black-76 都帮助解释变量传导，但必须先匹配合约基准。
- 理论敏感度不是 dealer 持仓方向；对冲流仍需要持仓归属与盘面证据。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> A pricing formula must match the contract's underlying basis. Spot or cash-index cases can start with BSM including yield q, while European options quoted directly on a futures or forward input are commonly expressed with Black-76. The two models are not interchangeable by merely renaming a variable.

Understand how spot, forward or futures, strike, DTE, rate, yield, and volatility enter spot BSM or futures Black-76 and shape theoretical value and Greeks.

### 01 / Inputs And Outputs

#### Separate Spot BSM From Futures Or Forward Black-76 First

Spot BSM with continuous yield uses S0, K, T, r, q, and sigma. Only when q equals zero does it reduce to the no-dividend or no-carry formula. Black-76 instead uses the same-expiry futures or forward price F0,T and discounts the option payoff as a whole.

- **Spot-BSM call with continuous yield**

  ```latex
  C=S_0e^{-qT}N(d_1)-Ke^{-rT}N(d_2)
  ```
  European spot-basis formula with continuous dividend or carry yield q stated explicitly.

- **Spot-BSM put with continuous yield**

  ```latex
  P=Ke^{-rT}N(-d_2)-S_0e^{-qT}N(-d_1)
  ```
  Uses the same spot-BSM inputs as the call.

- **Spot-BSM standardized distance**

  ```latex
  d_1=\frac{\ln(S_0/K)+(r-q+\tfrac{1}{2}\sigma^2)T}{\sigma\sqrt{T}},\qquad d_2=d_1-\sigma\sqrt{T}
  ```
  The r minus q term represents net carry in the spot relationship.

- **Black-76 European futures or forward call**

  ```latex
  C_F=e^{-rT}\left[F_{0,T}N(d_1^F)-KN(d_2^F)\right]
  ```
  Uses the same-expiry F0,T as the direct price input.

- **Black-76 distance and put**

  ```latex
  d_1^F=\frac{\ln(F_{0,T}/K)+\tfrac{1}{2}\sigma^2T}{\sigma\sqrt{T}},\quad d_2^F=d_1^F-\sigma\sqrt{T},\quad P_F=e^{-rT}\left[KN(-d_2^F)-F_{0,T}N(-d_1^F)\right]
  ```
  Black-76 d1 does not add r minus q because carry is already represented in F0,T.

| Input | Impact |
| --- | --- |
| Spot or F0,T / Strike | Must match the spot-BSM or Black-76 model basis. |
| DTE | Affects extrinsic value and gamma / theta. |
| Volatility | Affects the width of future price distribution. |
| Rate | Affects discounting and forward value. |
| Yield / Carry | Appears as q in spot BSM and is already embedded in F0,T under Black-76. |

### 02 / Assumptions And Boundaries

#### The Model Is A Framework, Not A Full Copy Of Reality

The base BSM and Black-76 closed forms are European-style formulas and rely on simplifying assumptions such as continuous price paths, no transaction costs, and constant volatility and rates. American exercise, discrete dividends, futures margin settlement, gaps, slippage, liquidity breaks, skew, and event risk require another model or explicit adjustment.

In 0DTE and event days, model output is only a sensitivity reference, not a guarantee of real market pricing.

### 03 / Risk Transmission

#### Theoretical Price Changes Can Reprice Dealer Exposure

Before analyzing ES- or NQ-related options, confirm whether the contract is priced on a cash index, ETF, futures, or forward basis, together with exercise style and settlement. Changes in model inputs alter delta and gamma; corresponding futures hedge direction can be discussed only when dealer position side is known.

- Spot BSM and Black-76 both explain variable transmission, but the contract basis must be matched first.
- Theoretical sensitivity is not dealer position direction; hedge-flow interpretation still requires ownership and market evidence.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

