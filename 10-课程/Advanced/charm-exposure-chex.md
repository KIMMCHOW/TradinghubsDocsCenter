---
title: "CHEX：Charm Exposure 怎么看"
title_en: "CHEX: How To Read Charm Exposure"
slug: "charm-exposure-chex"
type: lesson
level: Advanced
order: 81
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "13 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "CHEX：Charm Exposure 怎么看"
  - "CHEX: How To Read Charm Exposure"
  - "charm-exposure-chex"
source_url: "https://tradinghubs.org/docs/trading-knowledge/charm-exposure-chex"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# CHEX：Charm Exposure 怎么看

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[vanna-exposure-vex|VEX：Vanna Exposure 怎么看]] ｜ 下一课：[[calendar-diagonal-butterfly-condor|Calendar、Diagonal、Butterfly、Condor 与 Iron Condor]]

**高级 · 做市商定位与期权敞口 · 13 分钟**

> 即使价格和 IV 都不动，时间也可能推动期权 Delta 变化。CHEX 把这条模型路径单独拆出来，但页面符号不证明 dealer 库存或实际对冲方向。

理解 Charm 如何描述 Delta 随时间流逝而漂移，并用 ODV 预计算 CHEX 定位临近到期的模型时间敏感区。

### 01 / 定义

#### 先分清 Charm 概念与页面预计算 CHEX

Charm 衡量 Delta 对时间流逝的敏感度。理论上要先确认导数针对日历时间还是剩余期限，并声明 365、252 或其他日计数。一般 Charm 暴露与 Charm、某种仓位度量和合约乘数成比例；ODV 则直接展示已包含具体缩放、符号和聚合的预计算 CHEX，不能用 OI 或固定乘数复算。

0DTE、临近收盘和临近到期时，ATM 附近的 Delta 可能随时间快速漂移；深 ITM / OTM 的 Charm 则可能收缩或改变符号。因此短 DTE 只表示更需要逐 Strike 检查，不代表 CHEX 必然最大。

在本课的产品读法里，正负号、OI 与 Volume 都不能单独证明做市商库存、持仓归属或对冲方向；K / M / B 仅为紧凑显示缩写，不是美元、股数、合约数或每点冲击的经济单位。只可在同一标的、同一指标、同一 DTE 窗口和同一数据快照内比较分布。0DTE、1DTE+ 与 90D Window 均为独立预计算值，90D Window 不等于前两者相加。

- D 是模型声明的年化日计数；若使用剩余期限 T，时间导数符号会反转。
- C_n 只在同一标的、CHEX、DTE 窗口和数据快照内累计；显示正负号不能推出做市商时间对冲方向。

- **每 1 日的 Charm**

  ```latex
  \mathrm{Charm}_{1\mathrm{day}}=\frac{1}{D}\frac{\partial\Delta}{\partial t_{\mathrm{calendar}}}
  ```

- **一般概念关系，不能复算页面**

  ```latex
  \text{Charm exposure}\;\propto\;\mathrm{Charm}\times\text{position measure}\times\text{contract multiplier}
  ```

- **同一视图的有符号累计**

  ```latex
  C_n=\sum_{i=1}^{n}x_i
  ```

### 02 / 到期日

#### 越接近到期，越要按 Strike 核对时间路径

中远期合约的单位时间 Delta 漂移通常较慢，但大仓位仍可形成重要 CHEX；0DTE 或临近到期时，ATM 附近漂移可能更快，而翼部敏感度可能消失。窗口只能决定检查顺序，不能预设绝对大小。

| 窗口 | 条件式特征 | 阅读重点 |
| --- | --- | --- |
| 0DTE | ATM 附近可能快速变化，翼部可能收缩。 | 逐 Strike 核对符号、现价距离与收盘时间。 |
| 1DTE+ | 时间漂移较缓，但仓位规模可能更大。 | 在 1DTE+ 视图内定位热点，不与 0DTE 原始绝对值直接比较。 |
| 90D Window | 单位时间变化慢，但可形成背景暴露。 | 把它作为独立窗口阅读，不等于 0DTE 与 1DTE+ 相加。 |

### 03 / 期货传导

#### CHEX 帮助解释不靠价格推动的对冲漂移

当价格靠近 OI、GEX 与 CHEX 各自视图里的热点时，记录这些位置是否重合，并观察临近到期的实际价格接受、拒绝与成交变化；不能只凭 CHEX 符号把行为归因于 dealer 对冲。

- CHEX 是模型时间敏感度读数，不是方向信号或已观测到的对冲流。
- 到期越近，越要把 CHEX 和 DTE 分开看。

## 相关概念

- [[charm-delta-time-decay|Charm：Delta 随日历时间的漂移]] — CHEX 是 Charm 在真实仓位上的聚合。
- [[dte-window-selection|DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选]] — 时间维度敞口必须按到期窗口分开读。
- [[gamma-exposure-gex|GEX / vGEX：Gamma Exposure 怎么看]] — 把 GEX 与 CHEX 联读，可以看到仓位在价格与时间两个方向的变化。
- [[combined-odv-reads|组合读法：趋势延续、吸附与波动放大]] — CHEX 常作为确认层的一部分，而不是独立的交易信号。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Even if price and IV do not move, time can still move option delta. CHEX isolates that modeled path, but its displayed sign does not establish dealer inventory or actual hedge direction.

Understand how charm describes delta drift as time passes, then use ODV's precomputed CHEX to locate modeled time-sensitivity areas near expiration.

### 01 / Definition

#### Separate Charm Theory From Precomputed CHEX

Charm measures delta sensitivity to passing time. Theory must first state whether the derivative uses calendar time or time remaining and whether the day-count basis is 365, 252, or another convention. Conceptually, charm exposure is proportional to charm, a position measure, and a contract multiplier. ODV directly displays precomputed CHEX with its scaling, signs, and aggregation already embedded, so OI or a fixed multiplier cannot reproduce it.

In 0DTE, late-session, and near-expiry windows, delta near ATM can drift quickly with time; deep-ITM or deep-OTM charm may shrink or change sign. Short DTE therefore calls for strike-level inspection rather than implying CHEX must be largest.

In this product reading, signs, OI, and volume do not establish dealer inventory, ownership, or hedge direction. K / M / B are compact display suffixes, not economic units such as dollars, shares, contracts, or a per-point shock. Compare distributions only within the same symbol, metric, DTE window, and snapshot. 0DTE, 1DTE+, and 90D Window are independent precomputed values; 90D Window is not the sum of the first two.

- D is the model's stated annual day-count basis; differentiating by time remaining T reverses the time-derivative sign.
- C_n accumulates only within the same symbol, CHEX view, DTE window, and snapshot; displayed signs do not establish dealer time-hedging direction.

- **Charm per one day**

  ```latex
  \mathrm{Charm}_{1\mathrm{day}}=\frac{1}{D}\frac{\partial\Delta}{\partial t_{\mathrm{calendar}}}
  ```

- **General concept; not a page-reproduction formula**

  ```latex
  \text{Charm exposure}\;\propto\;\mathrm{Charm}\times\text{position measure}\times\text{contract multiplier}
  ```

- **Signed cumulative line within one view**

  ```latex
  C_n=\sum_{i=1}^{n}x_i
  ```

### 02 / Expiration

#### Nearer Expiry Requires Strike-Level Checks Of The Time Path

Longer-dated contracts usually have slower delta drift per unit time, but large positioning can still create material CHEX. In 0DTE or near expiry, ATM drift may accelerate while wing sensitivity can disappear. The window sets inspection order, not guaranteed magnitude.

| Window | Conditional Feature | Reading Focus |
| --- | --- | --- |
| 0DTE | May change quickly near ATM while wings can shrink. | Check sign, spot distance, and time to close strike by strike. |
| 1DTE+ | Time drift is slower, but positioning may be larger. | Locate hotspots within the 1DTE+ view without directly comparing raw magnitude with 0DTE. |
| 90D Window | Slower per unit time, but capable of material background exposure. | Read it as an independent window, not 0DTE plus 1DTE+. |

### 03 / Futures Transmission

#### CHEX Helps Explain Hedge Drift Without Price Moving First

When price nears hotspots found separately in OI, GEX, and CHEX views, record whether their strike locations overlap and observe actual acceptance, rejection, and participation near expiry. CHEX sign alone cannot attribute that behavior to dealer hedging.

- CHEX is a modeled time-sensitivity reading, not a directional signal or observed hedge flow.
- The closer to expiry, the more CHEX must be read by DTE window.

## Related Concepts

- [[charm-delta-time-decay|Charm: Delta Drift Through Calendar Time]] — CHEX is charm aggregated over real positioning.
- [[dte-window-selection|DTE Windows: How To Choose 0DTE, 1DTE+, And 90D Window]] — Time-dimension exposure must be read separately by expiry window.
- [[gamma-exposure-gex|GEX / vGEX: How To Read Gamma Exposure]] — Reading GEX with CHEX shows how a book changes in both the price and time directions.
- [[combined-odv-reads|Combined Reads: Trend Continuation, Pinning, And Volatility Expansion]] — CHEX is usually part of the confirmation layer rather than a standalone trading signal.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

