---
title: "Vega：IV 敏感度与波动率重定价"
title_en: "Vega: IV Sensitivity And Volatility Repricing"
slug: "vega-iv-sensitivity"
type: lesson
level: Intermediate
order: 39
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "16 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "Vega：IV 敏感度与波动率重定价"
  - "Vega: IV Sensitivity And Volatility Repricing"
  - "vega-iv-sensitivity"
source_url: "https://tradinghubs.org/docs/trading-knowledge/vega-iv-sensitivity"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# Vega：IV 敏感度与波动率重定价

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[time-value-and-theta|时间价值与 Theta]] ｜ 下一课：[[rho-rate-sensitivity|Rho：利率敏感度为什么通常排在最后]]

**中级 · Greeks 与敏感度 · 16 分钟**

> Vega 回答的是：IV 每变动 1 个百分点，期权价格大约变多少。数学导数通常以波动率小数 1.00 为单位，屏幕上的 Vega 常已缩放到 1 个百分点；两种单位必须先对齐。它不是方向敏感度，而是市场重新定价未来波动时的敏感度。

用价格对 IV 的切线斜率理解 Vega，并区分 Long Vega、Short Vega 与方向判断。

### 01 / 价格对 IV 的斜率

#### Vega 是期权价值曲线对 IV 的切线斜率

把横轴换成 IV、纵轴换成期权理论价值，就能看到一条随 IV 上升而抬高的曲线。当前 IV 位置上的切线斜率，就是 Vega。

如果界面明确把 Vega 按 1 个百分点缩放并显示为 3.20，意思不是价格一定涨 3.20，而是在其他输入不变时，IV 上升 1 个百分点，理论价值大约增加 3.20。若使用未缩放导数，则同一变化必须写成 0.01。

- 买入 Call 和买入 Put 通常都是 Long Vega；卖出 Call 和卖出 Put 通常都是 Short Vega。

- **未缩放 Vega 定义**

  ```latex
  \nu=\frac{\partial V}{\partial \sigma}
  ```

- **每 1 个 IV 点的 Vega**

  ```latex
  \nu_{1\mathrm{pt}}=0.01\,\frac{\partial V}{\partial \sigma}
  ```

- **IV 点数近似**

  ```latex
  \Delta V\approx \nu_{1\mathrm{pt}}\times \Delta\sigma_{\mathrm{points}}
  ```

### 02 / Vega 集中区

#### Vega 通常集中在 ATM 与更长 DTE

Vega 来自未来路径的不确定性。越接近 ATM，方向还没有被定死，波动率重定价对期权价值的影响越明显。

DTE 越长，市场有更多时间让波动兑现，Vega 往往越大；临近到期、深 ITM 或深 OTM 时，Vega 通常会收缩。

| 区域 | Vega 特征 | 阅读方式 |
| --- | --- | --- |
| ATM + 较长 DTE | 通常最高 | 最容易受到 IV 重定价影响 |
| 深 ITM / 深 OTM | 通常较低 | 方向或归零概率已经更明确 |
| 临近到期 | 快速收缩 | Theta 与 Gamma 更容易主导 |

### 03 / 买方与卖方

#### Long Vega 与 Short Vega 是波动率方向，不是价格方向

Long Vega 希望 IV 上升，或者至少不被 IV crush 抹掉权利金；Short Vega 希望 IV 下行，或者用时间流逝抵消被波动率重新定价的风险。

实战里不要只问“方向看多还是看空”。还要问：我是在买波动率，还是在卖波动率？现在的 IV 是便宜、合理，还是已经把事件风险提前定价了？

- 财报、CPI、FOMC 前后，Vega 往往决定权利金是否会被 IV crush 重定价。
- 较大的 Vega 暴露会让组合对波动率曲面移动更敏感，而不只是对 Spot 方向敏感。
- 买方 Long Vega、卖方 Short Vega 是基础方向；组合结构会让净 Vega 在不同 strike 和期限上重新分布。

## 相关概念

- [[realized-vs-implied-volatility|已实现波动率与隐含波动率]] — Vega 把隐含波动率变化换算成持仓损益。
- [[implied-volatility-surface|隐含波动率 IV 与波动率曲面]] — 同一 Vega 敞口在不同执行价与期限上的取值并不相同。
- [[volga-vomma-volatility-convexity|Volga / Vomma：波动率凸性]] — Vega 本身随波动率变化，这个二阶效应就是 Volga。
- [[vega-decay-veta|Vega Decay / Veta：Vega 随时间的变化]] — Vega 随剩余期限衰减的速度由 Veta 度量。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Vega answers how much option value changes for a one-percentage-point move in IV. The mathematical derivative is usually per 1.00 volatility, while displayed vega is often scaled to one volatility point; those units must be aligned first. It is volatility repricing sensitivity, not spot direction.

Read Vega as the slope of option value against IV, then separate long Vega, short Vega, and directional exposure.

### 01 / Slope Against IV

#### Vega Is The Tangent Slope Of Value Against IV

Put IV on the x-axis and theoretical option value on the y-axis. The curve rises as IV rises; the tangent slope at the current IV is Vega.

If an interface explicitly reports one-point-scaled vega as 3.20, it does not mean the option must rise by 3.20. Holding other inputs constant, a one-percentage-point IV increase adds roughly 3.20 to theoretical value. With an unscaled derivative, the same move must be written as 0.01.

- Long calls and long puts are usually long Vega; short calls and short puts are usually short Vega.

- **Unscaled vega definition**

  ```latex
  \nu=\frac{\partial V}{\partial \sigma}
  ```

- **Vega per one IV point**

  ```latex
  \nu_{1\mathrm{pt}}=0.01\,\frac{\partial V}{\partial \sigma}
  ```

- **IV-point approximation**

  ```latex
  \Delta V\approx \nu_{1\mathrm{pt}}\times \Delta\sigma_{\mathrm{points}}
  ```

### 02 / Where Vega Lives

#### Vega Usually Concentrates Near ATM And Longer DTE

Vega comes from uncertainty about the future path. Near ATM, direction is still undecided, so volatility repricing has more impact on option value.

With more DTE, the market has more time for volatility to matter, so Vega tends to be larger. Near expiry, deep ITM, or deep OTM, Vega often shrinks.

| Zone | Vega Profile | How To Read It |
| --- | --- | --- |
| ATM + longer DTE | Usually highest | Most exposed to IV repricing |
| Deep ITM / deep OTM | Usually lower | Direction or expiry outcome is more defined |
| Near expiry | Contracts quickly | Theta and Gamma can dominate faster |

### 03 / Buyers And Sellers

#### Long Vega And Short Vega Are Volatility Views, Not Price Views

Long Vega benefits from IV rising, or at least from IV not crushing premium. Short Vega benefits from IV falling, or from time decay offsetting volatility repricing risk.

In practice, do not only ask whether the trade is bullish or bearish. Ask whether you are buying volatility or selling it, and whether current IV is cheap, fair, or already pricing the event.

- Around earnings, CPI, or FOMC, Vega often determines whether premium is repriced by IV crush.
- Large Vega exposure makes a portfolio sensitive to volatility-surface moves, not only to spot direction.
- Buyers are long Vega and sellers are short Vega as a baseline; structures redistribute net Vega across strikes and expiries.

## Related Concepts

- [[realized-vs-implied-volatility|Realized Versus Implied Volatility]] — Vega converts a change in implied volatility into position profit and loss.
- [[implied-volatility-surface|Implied Volatility And Volatility Surface]] — The same vega exposure takes different values across strikes and expiries.
- [[volga-vomma-volatility-convexity|Volga / Vomma: Volatility Convexity]] — Vega itself changes with volatility, and that second-order effect is volga.
- [[vega-decay-veta|Vega Decay / Veta: How Vega Changes With Time]] — How fast vega decays with remaining time is measured by veta.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

