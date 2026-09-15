---
title: "Christmas Tree 与 Ladder：先核对腿部口径"
title_en: "Christmas Tree And Ladder Spreads: Verify The Leg Convention"
slug: "christmas-tree-and-ladder-spreads"
type: lesson
level: Advanced
order: 83
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "22 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "Christmas Tree 与 Ladder：先核对腿部口径"
  - "Christmas Tree And Ladder Spreads: Verify The Leg Convention"
  - "christmas-tree-and-ladder-spreads"
source_url: "https://tradinghubs.org/docs/trading-knowledge/christmas-tree-and-ladder-spreads"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Christmas Tree 与 Ladder：先核对腿部口径

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[calendar-diagonal-butterfly-condor|Calendar、Diagonal、Butterfly、Condor 与 Iron Condor]] ｜ 下一课：[[time-butterfly-term-structure|Time Butterfly：期限曲率与三到期日重估]]

**高级 · 结构、定价与波动率 · 22 分钟**

> Christmas Tree 不是足以直接下单的统一腿部描述。权威策略资料常用六份期权的 1:-3:+2 有界结构，部分交易资料则把买一、分散卖二的开放尾部结构称为 Christmas Tree 或 Ladder；本课并列两种口径，并要求实盘分析始终回到期权类型、执行价、数量和方向。

对照有界的 1:-3:+2 Christmas Tree 与开放尾部的 1:-1:-1 Ladder 口径，避免仅凭策略名称误判最大风险。

### 01 / 先列腿

#### 同名可能对应有界 1:-3:+2，也可能对应开放尾部 1:-1:-1

设同一标的、同一期权类型和同一到期日的执行价满足 K₁<K₂<K₃。有界 Call Christmas Tree 买入 K₁ 一份、卖出 K₂ 三份、买入 K₃ 两份，并在 K₁ 与 K₂ 之间跳过一个等距执行价；Put 版本镜像数量与跳档方向。三组数量净和为零，且特定间距令两端到期斜率都回到零。

开放尾部 Ladder 只买一份近端期权，并在另外两个执行价各卖一份，数量为 1:-1:-1；它不会由名称自动获得保护翼。实际订单必须写成逐腿清单。若平台、经纪商或研究资料采用另一种命名，应以订单的买卖方向、数量与间距为准，而不是把名称强行套入某一条公式。

- **有界 Call Christmas Tree**

  ```latex
  V_{CT,C}=C(K_1)-3C(K_2)+2C(K_3),\quad K_2-K_1=2h,\;K_3-K_2=h
  ```

- **开放尾部 Call Ladder**

  ```latex
  V_{L,C}=C(K_1)-C(K_2)-C(K_3),\qquad K_1<K_2<K_3
  ```

| 口径 | 逐腿数量 | 间距 | 尾部 |
| --- | --- | --- | --- |
| 有界 Call Christmas Tree | +1 K₁ / -3 K₂ / +2 K₃ | 2h / h | 两端有界 |
| 开放 Call Ladder | +1 K₁ / -1 K₂ / -1 K₃ | 可不等宽 | 上方开放 |
| 有界 Put Christmas Tree | +2 K₁ / -3 K₂ / +1 K₃ | h / 2h | 两端有界 |
| 开放 Put Ladder | -1 K₁ / -1 K₂ / +1 K₃ | 可不等宽 | 下方开放 |

### 02 / 分段形状

#### 开放 Ladder 看净斜率；有界 Tree 看数量与间距同时抵消

开放 Call Ladder 在 K₁ 以下没有内在价值，在 K₁ 与 K₂ 之间随标的上涨，在 K₂ 与 K₃ 之间形成由第一段翼宽决定的平台。越过 K₃ 后，两条 Short Call 都进入价内，而只有一条 Long Call 抵消其中一份，因此组合净斜率变为 -1；若标的理论上没有上界，该尾部亏损也没有预设上限。Put Ladder 把开放尾部镜像到下方。

有界 Christmas Tree 的 1:-3:+2 数量让所有期权都价内时的标的系数为零，跳档间距又令剩余执行价常数抵消，因此两端最大风险都有限。初始 Debit 或 Credit 会把到期盈亏整体平移；交易成本、不同乘数、错误间距或缺失任一保护腿都会破坏理论边界，所以不能把模板结论复制到未经核对的订单。

- 逐区间计算净斜率，并核对数量加总与加权执行价；不从策略名称猜最大风险。
- 把不等宽、初始权利金和标的价格下界纳入盈亏平衡检查。
- 空头版本是整组反向，但实际 Bid / Ask、费用和指派会破坏成交层面的完美对称。

- **开放 Call Ladder 到期内在价值**

  ```latex
  G_{L,C}(S_T)=(S_T-K_1)^+-(S_T-K_2)^+-(S_T-K_3)^+
  ```

- **开放 Put Ladder 到期内在价值**

  ```latex
  G_{L,P}(S_T)=(K_3-S_T)^+-(K_2-S_T)^+-(K_1-S_T)^+
  ```

- **有界 Call Christmas Tree 到期内在价值**

  ```latex
  G_{CT,C}(S_T)=(S_T-K_1)^+-3(S_T-K_2)^++2(S_T-K_3)^+
  ```

- **有界 Put Christmas Tree 到期内在价值**

  ```latex
  G_{CT,P}(S_T)=2(K_1-S_T)^+-3(K_2-S_T)^++(K_3-S_T)^+
  ```

- **包含有符号初始现金流的到期盈亏**

  ```latex
  \Pi_T=G(S_T)+B,\qquad B>0\;\text{for credit},\quad B<0\;\text{for debit}
  ```

### 03 / 风险核验

#### 先确认是哪一种结构，再讨论 Theta、Vega 与保证金

有界 Tree 与开放 Ladder 在设计中心附近都可能呈现局部 Short Gamma、Long Theta、Short Vega，但两者的数量、尾部和保证金完全不同，且这些 Greek 符号会随价格跨过执行价、时间缩短和偏斜变化而改变。组合 Greek 必须按每条腿的方向、数量和合约乘数加总；局部标签不能替代全曲面重估。

执行风险包括三组报价、最多六份期权、部分成交、Short Leg 提前指派和临近执行价的 Pin Risk。开放 Ladder 还可能按裸空尾部计算保证金；有界 Tree 若保护腿漏成交也会暂时变成开放风险。研究表、订单确认和成交后持仓三处必须逐腿一致。

- 第一步：写出 Call / Put、K₁/K₂/K₃、买卖方向、数量、到期和乘数。
- 第二步：在每个执行价区间计算净斜率；明确结果是两端斜率归零，还是仍有 -1 开放尾部。
- 第三步：用 Spot × IV × Time 联合情景完整重估，再加入价差、保证金与指派。
- 该结构展示风险形状，不构成对任何执行价、方向或持有期限的建议。

## 相关概念

- [[vertical-ratio-backspread|垂直价差、Ratio Spread 与 Backspread]] — Christmas Tree 与 Ladder 是比率结构的非对称变体。
- [[option-spread-structures|价差与组合结构]] — 多腿定价与盈亏边界仍按各腿相加计算。
- [[expected-shortfall-cvar|CVaR / Expected Shortfall：越过分位点后的平均损失]] — 当卖出腿多于买入腿时，尾部风险必须单独评估。
- [[calendar-diagonal-butterfly-condor|Calendar、Diagonal、Butterfly、Condor 与 Iron Condor]] — 与其他有界结构对照阅读，可看清风险边界的差别。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Christmas tree is not a sufficiently precise order description. Authoritative strategy material commonly uses a six-option 1:-3:+2 defined-risk package, while some trading references use Christmas tree or ladder for a buy-one, sell-two open-tail package. This lesson separates both conventions and requires every practical analysis to return to option type, strike, quantity, and side.

Compare the defined-risk 1:-3:+2 Christmas tree with the open-tail 1:-1:-1 ladder convention so a strategy label never substitutes for maximum-risk analysis.

### 01 / List The Legs First

#### One Label Can Mean A Defined-Risk 1:-3:+2 Or An Open-Tail 1:-1:-1

Let strikes on the same underlying, option type, and expiry satisfy K₁<K₂<K₃. A defined-risk call Christmas tree buys one K₁ call, sells three K₂ calls, and buys two K₃ calls, with one equally spaced strike skipped between K₁ and K₂; the put version mirrors the quantities and skipped side. The three quantities sum to zero, and the specified spacing returns both terminal tail slopes to zero.

An open-tail ladder buys one near option and sells one option at each of two farther strikes, for 1:-1:-1 quantities; the label does not create a protective wing. A real order must be written as a leg list. If a platform, broker, or research source uses another naming convention, the ticket's sides, quantities, and spacing control rather than forcing the label into one formula.

- **Defined-risk call Christmas tree**

  ```latex
  V_{CT,C}=C(K_1)-3C(K_2)+2C(K_3),\quad K_2-K_1=2h,\;K_3-K_2=h
  ```

- **Open-tail call ladder**

  ```latex
  V_{L,C}=C(K_1)-C(K_2)-C(K_3),\qquad K_1<K_2<K_3
  ```

| Convention | Leg quantities | Spacing | Tail |
| --- | --- | --- | --- |
| Defined-risk call Christmas tree | +1 K₁ / -3 K₂ / +2 K₃ | 2h / h | Bounded on both sides |
| Open-tail call ladder | +1 K₁ / -1 K₂ / -1 K₃ | May be unequal | Open upper tail |
| Defined-risk put Christmas tree | +2 K₁ / -3 K₂ / +1 K₃ | h / 2h | Bounded on both sides |
| Open-tail put ladder | -1 K₁ / -1 K₂ / +1 K₃ | May be unequal | Open lower tail |

### 02 / Piecewise Shape

#### Open Ladders Depend On Net Slope; Defined Trees Cancel Quantity And Spacing

The open call ladder has no intrinsic value below K₁, rises between K₁ and K₂, and forms a plateau between K₂ and K₃ based on the first wing width. Above K₃, both short calls are intrinsic while only one long call offsets one of them, so package slope becomes -1; if the underlying has no theoretical upper bound, that tail loss has no preset cap. The put ladder mirrors the open tail to the downside.

In a defined-risk Christmas tree, 1:-3:+2 quantities make the underlying coefficient zero when all options are intrinsic, while skipped-strike spacing cancels the remaining strike constant, leaving both terminal tails bounded. An opening debit or credit shifts terminal P&L vertically. Costs, mismatched multipliers, wrong spacing, or a missing protective leg break the theoretical boundary, so template conclusions cannot be copied to an unverified ticket.

- Calculate net slope in every price region and verify both quantity sum and strike-weighted sum; do not infer maximum risk from the strategy name.
- Include unequal wings, opening premium, and any underlying price floor in break-even checks.
- The short version reverses the theoretical package, but bid-ask, fees, and assignment break perfect execution symmetry.

- **Open call-ladder terminal intrinsic value**

  ```latex
  G_{L,C}(S_T)=(S_T-K_1)^+-(S_T-K_2)^+-(S_T-K_3)^+
  ```

- **Open put-ladder terminal intrinsic value**

  ```latex
  G_{L,P}(S_T)=(K_3-S_T)^+-(K_2-S_T)^+-(K_1-S_T)^+
  ```

- **Defined-risk call Christmas-tree terminal intrinsic value**

  ```latex
  G_{CT,C}(S_T)=(S_T-K_1)^+-3(S_T-K_2)^++2(S_T-K_3)^+
  ```

- **Defined-risk put Christmas-tree terminal intrinsic value**

  ```latex
  G_{CT,P}(S_T)=2(K_1-S_T)^+-3(K_2-S_T)^++(K_3-S_T)^+
  ```

- **Terminal P&L with signed opening cash flow**

  ```latex
  \Pi_T=G(S_T)+B,\qquad B>0\;\text{for credit},\quad B<0\;\text{for debit}
  ```

### 03 / Risk Validation

#### Identify The Structure Before Discussing Theta, Vega, Or Margin

A defined tree and an open ladder may both look locally short gamma, long theta, and short vega near their design centers, yet their quantities, tails, and margin are fundamentally different, and those Greek signs can change as spot crosses strikes, time shortens, or skew moves. Portfolio Greeks must be summed with each leg's side, quantity, and contract multiplier; local labels cannot replace full-surface revaluation.

Execution risk includes three quote groups, as many as six options, partial fills, early assignment of a short leg, and pin risk near a strike. An open ladder may be margined for its naked tail, while a defined tree becomes temporarily open-risk if protective legs fail to fill. The research sheet, order confirmation, and post-fill position must agree leg by leg.

- Step 1: Write option type, K₁/K₂/K₃, side, quantity, expiry, and multiplier.
- Step 2: Calculate net slope in every strike region and state whether both tails return to zero or a -1 open tail remains.
- Step 3: Fully revalue joint spot-by-IV-by-time scenarios, then add spreads, margin, and assignment.
- The structure demonstrates a risk shape and is not a recommendation for any strike, direction, or holding period.

## Related Concepts

- [[vertical-ratio-backspread|Vertical Spreads, Ratio Spreads, And Backspreads]] — Christmas trees and ladders are asymmetric variants of ratio structures.
- [[option-spread-structures|Spread And Multi-Leg Structures]] — Multi-leg pricing and payoff boundaries still add across the legs.
- [[expected-shortfall-cvar|CVaR / Expected Shortfall: Average Loss Beyond A Quantile]] — When sold legs outnumber bought legs, tail risk must be assessed separately.
- [[calendar-diagonal-butterfly-condor|Calendars, Diagonals, Butterflies, Condors, And Iron Condors]] — Reading these against other defined-risk structures makes the boundary difference clear.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cboe-christmas-tree
- oic-options-strategies
- occ-options-disclosure
