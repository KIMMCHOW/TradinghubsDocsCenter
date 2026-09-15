---
title: "Skew / Term Structure"
title_en: "Skew / Term Structure"
slug: "skew-term-structure"
type: lesson
level: Advanced
order: 61
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "15 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "Skew / Term Structure"
  - "skew-term-structure"
source_url: "https://tradinghubs.org/docs/trading-knowledge/skew-term-structure"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# Skew / Term Structure

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[variance-swaps-and-vix|方差互换与 VIX：从期权横截面到风险中性方差]] ｜ 下一课：[[combined-odv-reads|组合读法：趋势延续、吸附与波动放大]]

**高级 · 结构、定价与波动率 · 15 分钟**

> Skew 和 Term Structure 让 IV 从单点数字变成一张风险地图。

理解 IV 如何随行权价和到期日变化，并读出尾部风险和事件风险定价。

### 01 / Skew

#### Skew 描述不同行权价的 IV 差异

Put Skew 变陡通常意味着市场愿意为下跌保护支付更高溢价。Call Wing 抬升可能反映上方追逐或事件溢价。比较时必须固定到期日，并尽量使用相近 Delta，而不是直接比较距离现价不同的行权价。

常用的 25-Delta Risk Reversal 比较看涨与看跌翼部，Butterfly 则观察两翼相对 ATM 的整体抬升。它们压缩了曲面信息，但不会说明成交是谁发起，也不能单独判断方向。

- **25-Delta Risk Reversal**

  ```latex
  RR_{25}=\sigma_{25\Delta,\,call}-\sigma_{25\Delta,\,put}
  ```
  衡量两侧翼部的相对 IV。

- **25-Delta Butterfly**

  ```latex
  BF_{25}=\tfrac{1}{2}(\sigma_{25\Delta,\,call}+\sigma_{25\Delta,\,put})-\sigma_{ATM}
  ```
  衡量两翼相对 ATM 的平均弯曲程度。

### 02 / Term Structure

#### 期限结构描述不同到期日的 IV 差异

期限结构比较相似 Delta 或相似价内外程度在不同到期日的 IV。近端低于远端时通常称为正向期限结构；近端因事件或压力显著高于远端时，曲线可能倒挂。不要把波动率期限结构与期货升贴水混为同一个概念。

- Front Expiration IV 抬升：近期事件或短期不确定性更贵。
- Back Expiration IV 稳定：市场认为风险不一定延续。

### 03 / 盘面影响

#### Skew 和期限结构异常时，期货更容易围绕事件重定价

短期限 IV 抬升可能意味着市场正在给近期事件定价；Put Skew 变陡可能说明下方保护需求增强。ES / NQ 盘面可能出现事件前收缩和事件后重新定价。

- Skew 是风险需求的形状，不是方向指令。
- 期限结构帮助区分短期事件和长期风险溢价。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Skew and term structure turn IV from a single number into a risk map.

Understand how IV changes across strikes and expirations, then read tail-risk and event-risk pricing.

### 01 / Skew

#### Skew Describes IV Differences Across Strikes

A steeper put skew often means the market is paying more for downside protection. A lifted call wing can reflect upside chase or event premium. Hold expiry constant and compare similar deltas rather than strikes at unequal distances from spot.

A common 25-delta risk reversal compares the call and put wings, while the butterfly measures how far both wings sit above or below ATM. These summaries compress the surface but do not identify the trade initiator or determine direction by themselves.

- **25-Delta Risk Reversal**

  ```latex
  RR_{25}=\sigma_{25\Delta,\,call}-\sigma_{25\Delta,\,put}
  ```
  Measures relative implied volatility across the two wings.

- **25-Delta Butterfly**

  ```latex
  BF_{25}=\tfrac{1}{2}(\sigma_{25\Delta,\,call}+\sigma_{25\Delta,\,put})-\sigma_{ATM}
  ```
  Measures the average wing curvature relative to ATM.

### 02 / Term Structure

#### Term Structure Describes IV Differences Across Expirations

Volatility term structure compares similar deltas or moneyness across expiries. When the front is below later expiries the curve is usually upward sloping; a near-term event or stress can lift the front into inversion. Do not treat volatility term structure and futures carry as the same concept.

- Front expiration IV lifted: near-term event or uncertainty is more expensive.
- Back expiration IV stable: the market may not price the risk as persistent.

### 03 / Market Impact

#### Abnormal Skew And Term Structure Can Drive Event Repricing

Lifted short-dated IV can mean the market is pricing a near-term event; steeper put skew can mean stronger downside protection demand. ES / NQ may compress before the event and reprice afterward.

- Skew is the shape of risk demand, not a direction instruction.
- Term structure helps separate short-term event premium from longer-term risk premium.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

