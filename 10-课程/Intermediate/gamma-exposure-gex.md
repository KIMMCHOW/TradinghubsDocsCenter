---
title: "GEX / vGEX：Gamma Exposure 怎么看"
title_en: "GEX / vGEX: How To Read Gamma Exposure"
slug: "gamma-exposure-gex"
type: lesson
level: Intermediate
order: 44
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "17 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "GEX / vGEX：Gamma Exposure 怎么看"
  - "GEX / vGEX: How To Read Gamma Exposure"
  - "gamma-exposure-gex"
source_url: "https://tradinghubs.org/docs/trading-knowledge/gamma-exposure-gex"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# GEX / vGEX：Gamma Exposure 怎么看

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[options-flow-direction|Flow：期权成交分类怎么读]] ｜ 下一课：[[delta-exposure-dex|DEX：Delta Exposure 怎么看]]

**中级 · 做市商定位与期权敞口 · 17 分钟**

> GEX 回答的不是“会涨还是会跌”，而是同一视图里哪些行权价的模型敏感度更突出。页面符号沿用当前模型口径，不能单独证明 dealer 库存或未来对冲方向；vGEX 只说明当日活动热点，不能由 Volume 证明库存正在改变。

理解 ODV 预计算 GEX 与 vGEX 的符号、相对条宽和窗口边界：前者定位模型 Gamma 敏感度，后者定位当日 Gamma 加权活动。

### 01 / 定义

#### 先分清一般概念与页面预计算值

一般风险概念里，Gamma 暴露与 Gamma、某种仓位度量和合约乘数成比例，但具体实现还取决于价格缩放、冲击单位、符号和聚合规则。ODV 页面直接展示已计算的 0DTE、1DTE+ 与 90D Window 值；当前页面没有统一合约乘数说明或逐行权价的 Call / Put 分解，因此不能用通用公式复算页面。

在本课的产品读法里，正负号、OI 与 Volume 都不能单独证明做市商库存、持仓归属或对冲方向；K / M / B 仅为紧凑显示缩写，不是美元、股数、合约数或每点冲击的经济单位。只可在同一标的、同一指标、同一 DTE 窗口和同一数据快照内比较分布。0DTE、1DTE+ 与 90D Window 均为独立预计算值，90D Window 不等于前两者相加。

- w_i 只解释同一张图里的条形宽度；颜色和值仍保留原始符号。
- 90D Window 是独立的预计算窗口，不等于 0DTE 与 1DTE+ 相加。

- **一般概念关系，不能复算页面**

  ```latex
  \text{Gamma exposure}\;\propto\;\Gamma\times\text{position measure}\times\text{contract multiplier}
  ```

- **同一视图的相对条宽**

  ```latex
  w_i=\frac{|x_i|}{\max_j|x_j|},\quad \max_j|x_j|>0
  ```

### 02 / 符号边界

#### 页面符号不能直接翻译成 Dealer 库存

当前页面没有 dealer ownership 元数据。正值、负值与零附近只描述当前模型下的数值位置；它们不能直接翻译成 dealer Long / Short Gamma、期货买卖方向、吸附或放大结论。先定位同视图的集中区，再用期货价格与成交验证实际行为。

| 页面状态 | 可读信息 | 不可推出 |
| --- | --- | --- |
| 正值 | 当前模型的正号一侧。 | Dealer Long Gamma 或卖出期货。 |
| 负值 | 当前模型的负号一侧。 | Dealer Short Gamma 或买入期货。 |
| 接近零 | 只在同一视图和快照内表示数值接近零。 | 自动的状态切换或交易信号。 |

### 03 / vGEX

#### vGEX 用 Volume 定位当天 Gamma 加权活动

vGEX 用预计算值定位当日交易活动与 Gamma 敏感度重合的位置。一般概念可把它理解为 Gamma 与某种活动度量的加权关系，但页面的价格缩放、符号和聚合已包含在预计算结果中，不能用 Volume、OI 或固定乘数复算。

Volume 包含开仓、平仓、换手与多腿交易，所以 vGEX 不是新增库存，也不揭示 dealer 对手方。它适合定位日内活动热点，但不能单独证明原结构被强化、冲击或会长期有效。

- **一般概念关系，不能复算页面**

  ```latex
  \text{Gamma-weighted activity}\;\propto\;|\Gamma|\times\text{activity measure}\times\text{contract multiplier}
  ```

- **同一视图的相对条宽**

  ```latex
  w_i=\frac{|x_i|}{\max_j|x_j|},\quad \max_j|x_j|>0
  ```

| 组合 | 常见含义 | 读法边界 |
| --- | --- | --- |
| GEX 与 vGEX 热点重合 | 两个指标各自在本视图内突出的行权价重合。 | 不能据此判断开仓或 dealer 方向；仍需价格确认。 |
| GEX 与 vGEX 热点错位 | 当日活动热点位于 GEX 集中区之外。 | 等待下一次 OI 更新与价格接受，不能称为结构迁移。 |
| vGEX 热点缺少附近结构重合 | 属于当日活动热点，持久性未知。 | 不要在 OI 更新前把活动量写成新增仓位。 |

- vGEX 是 Gamma 加权活动指标，不是 dealer 库存变化。
- 出现位置差异时，联读成交分类、期货价格，并等待 OI 更新。

### 04 / ODV 读法

#### 先看总环境，再看行权价集中区

先确认 Data Dashboard 中 GEX 的更新时间、标的、指标和 DTE 窗口，再到 Greeks Profile 定位同一视图内的突出行权价。页面没有逐行权价的 Call / Put 分解或做市商持仓归属信息；正负号和 K / M / B 缩写都不能用于反推仓位归属、经济单位或对冲方向。

如果价格接近同视图内突出的 GEX Strike，同时 Flow 和 Volume 放大，就观察该区域的实际价格接受、拒绝或穿越；不要先把结果归因于 dealer 对冲。

- GEX 是模型敏感度读数，不是方向胜率或 dealer 库存标签。
- 高 GEX 区域必须和 OI、Flow、Volume、IV 以及期货盘面反应一起看。
- 0DTE 和临近到期时，GEX 变化会更快。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> GEX does not answer whether price will rise or fall; it shows which strikes are more prominent within the same modeled view. Displayed signs follow the current model convention and do not establish dealer inventory or future hedge direction. vGEX identifies same-session activity hotspots and volume cannot prove that inventory is changing.

Understand the sign, relative bar width, and window boundaries of ODV's precomputed GEX and vGEX: the former locates modeled gamma sensitivity and the latter locates same-session gamma-weighted activity.

### 01 / Definition

#### Separate The General Concept From The Precomputed Display

As a general risk concept, gamma exposure is proportional to gamma, a position measure, and a contract multiplier, but an implementation also depends on price scaling, shock units, signs, and aggregation rules. ODV directly displays precomputed 0DTE, 1DTE+, and 90D Window values. The current view does not provide a universal multiplier or per-strike call-put split, so a generic formula cannot reproduce the page.

In this product reading, signs, OI, and volume do not establish dealer inventory, ownership, or hedge direction. K / M / B are compact display suffixes, not economic units such as dollars, shares, contracts, or a per-point shock. Compare distributions only within the same symbol, metric, DTE window, and snapshot. 0DTE, 1DTE+, and 90D Window are independent precomputed values; 90D Window is not the sum of the first two.

- w_i explains bar width within one chart only; color and value retain the original sign.
- 90D Window is an independent precomputed window, not 0DTE plus 1DTE+.

- **General concept; not a page-reproduction formula**

  ```latex
  \text{Gamma exposure}\;\propto\;\Gamma\times\text{position measure}\times\text{contract multiplier}
  ```

- **Relative bar width within one view**

  ```latex
  w_i=\frac{|x_i|}{\max_j|x_j|},\quad \max_j|x_j|>0
  ```

### 02 / Sign Boundary

#### A Displayed Sign Is Not Dealer Inventory

The current view does not include dealer-ownership metadata. Positive, negative, and near-zero values describe positions on the current model scale only. They do not translate directly into long or short dealer gamma, futures buying or selling, pinning, or amplification. Locate clusters within one view, then use futures price and participation to test actual behavior.

| Display State | Supported Information | Not Established |
| --- | --- | --- |
| Positive value | The positive side of the current model convention. | Long dealer gamma or futures selling. |
| Negative value | The negative side of the current model convention. | Short dealer gamma or futures buying. |
| Near zero | Near zero only within the same view and snapshot. | An automatic regime change or trade signal. |

### 03 / vGEX

#### vGEX Uses Volume To Locate Same-Session Gamma-Weighted Activity

vGEX uses precomputed values to locate where same-session trading activity overlaps gamma sensitivity. Conceptually it relates gamma to an activity measure, but price scaling, signs, and aggregation are already embedded in the displayed result; volume, OI, or a fixed multiplier cannot reproduce it.

Volume includes opening, closing, turnover, and multi-leg trades, so vGEX is not new inventory and does not reveal the dealer counterparty. It locates intraday activity hotspots but cannot by itself prove that prior structure is reinforced, attacked, or persistent.

- **General concept; not a page-reproduction formula**

  ```latex
  \text{Gamma-weighted activity}\;\propto\;|\Gamma|\times\text{activity measure}\times\text{contract multiplier}
  ```

- **Relative bar width within one view**

  ```latex
  w_i=\frac{|x_i|}{\max_j|x_j|},\quad \max_j|x_j|>0
  ```

| Combination | Common Meaning | Boundary |
| --- | --- | --- |
| GEX and vGEX hotspots overlap | Strikes prominent within each metric's own view overlap. | This does not identify opening flow or dealer side; price confirmation is still required. |
| GEX and vGEX hotspots differ | The same-session activity hotspot sits away from the GEX cluster. | Wait for the next OI update and price acceptance before calling it structural migration. |
| A vGEX hotspot lacks nearby structural overlap | It is a same-session activity hotspot with unknown durability. | Do not label activity as new positioning before OI updates. |

- vGEX is a gamma-weighted activity measure, not a change in dealer inventory.
- When locations differ, read trade classification and futures price, then wait for the OI update.

### 04 / ODV Reading

#### Read The Overall Regime First, Then Strike Clusters

First confirm the GEX timestamp, symbol, metric, and DTE window on Data Dashboard, then use Greeks Profile to locate prominent strikes within that same view. The page does not provide per-strike call-put decomposition or dealer-ownership metadata. Neither signs nor K, M, and B suffixes reveal ownership, economic units, or hedge direction.

If price approaches a GEX strike that is prominent within the same view while flow and volume expand, observe actual acceptance, rejection, or a cross. Do not attribute the outcome to dealer hedging in advance.

- GEX is a modeled sensitivity reading, not directional odds or a dealer-inventory label.
- High-GEX areas must be read with OI, flow, volume, IV, and futures price reaction.
- In 0DTE and near-expiry windows, GEX can change faster.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

