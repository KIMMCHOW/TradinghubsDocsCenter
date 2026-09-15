---
title: "期权订单流：Delta、Gamma 与凸性加权"
title_en: "Options Order Flow: Delta, Gamma, And Convexity Weighting"
slug: "options-order-flow-dex-gex-convexity"
type: lesson
level: Advanced
order: 87
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "21 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "期权订单流：Delta、Gamma 与凸性加权"
  - "Options Order Flow: Delta, Gamma, And Convexity Weighting"
  - "options-order-flow-dex-gex-convexity"
source_url: "https://tradinghubs.org/docs/trading-knowledge/options-order-flow-dex-gex-convexity"
source_file: "Tradinghub-Web/components/site/options-knowledge/orderflow-data.ts"
generated: 2026-09-15
---

# 期权订单流：Delta、Gamma 与凸性加权

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[liquidity-sweeps-stop-runs-trapped-traders|流动性扫荡、止损猎杀与被困交易者]] ｜ 下一课：[[synthetic-futures-and-delta-equivalent-sizing|用期权表达期货敞口：合成结构与等值换算]]

**高级 · 做市商定位与期权敞口 · 21 分钟**

> 本课处理的是“已分类成交”的加权口径，而不是敞口登记表。两者常被混用：一个累计当日成交，另一个描述尚未平仓的存量。

把已分类的期权成交转换为方向与凸性两类信息：Delta 加权序列、Gamma 加权序列、凸性序列与累计口径，以及分类推断带来的限制。

### 01 / 分类成交口径

#### 先定义买与卖，再谈加权

期权订单流的第一步是把每笔成交标记为买方发起或卖方发起。买卖双方在数量上永远相等，因此分类的依据是主动方，而不是“有更多人买”。口径常见有两种：按成交价位于报价的哪一侧分类，或按成交价相对中间价的移动方向分类。

方向口径由 Delta 符号给出：买入 Call 与卖出 Put 属于正 Delta 一侧，卖出 Call 与买入 Put 属于负 Delta 一侧。这一映射只描述成交当刻的方向暴露，不描述标的、对冲工具或后续调整。

| 成交 | 方向暴露 | 凸性暴露 |
| --- | --- | --- |
| 买入 Call | 正 Delta | 正凸性（买入期权） |
| 卖出 Put | 正 Delta | 负凸性（卖出期权） |
| 卖出 Call | 负 Delta | 负凸性（卖出期权） |
| 买入 Put | 负 Delta | 正凸性（买入期权） |

### 02 / 三种加权

#### 同一笔成交按 Delta、Gamma 与凸性分别加权

Delta 加权序列把每笔成交换算成等价的方向暴露：正 Delta 成交与负 Delta 成交各自乘以该合约的 Delta 后相减。它衡量的是通过期权市场获得的方向敞口规模，而不是标的成交。

Gamma 加权序列用同一构造但改用 Gamma 加权，衡量的是对凸性的需求。凸性序列则按“买入期权”与“卖出期权”分组，用 Gamma 加权后相减，得到当期净买入的凸性。两者的差别很关键：前者按方向分组，后者按流动性提供的方向分组。

- **Delta 加权净敞口**

  ```latex
  \text{Net}_{\Delta}=V_{\text{bull}}\cdot\Delta_{\text{exp}}-V_{\text{bear}}\cdot\Delta_{\text{exp}}
  ```

- **凸性净买入**

  ```latex
  \text{Net}_{\Gamma}=V_{\text{long}}\cdot\Gamma_{\text{exp}}-V_{\text{short}}\cdot\Gamma_{\text{exp}}
  ```
  Delta 暴露与 Gamma 暴露分别乘该合约的合约乘数后才是金额口径。

- **累计口径**

  ```latex
  \text{Cumulative}_t=\text{Cumulative}_{t-1}+\text{Net}_t
  ```
  累计序列从区间起点开始累加，与存量型敞口口径不同。

### 03 / 对齐阅读与溢出问题

#### 三条序列对齐时才构成一句完整的话

单独一条 Delta 加权序列只能说明规模。当方向、Gamma 与凸性指向同一结论时，信息才完整：负 Delta 且同量级的负 Gamma 配合正凸性，对应以买入看跌期权的方式取得空头暴露；负 Delta 而 Gamma 很小，则更可能来自深度价内合约的换手或组合中的一条腿。

这一现象常被称为 Delta 溢出：深度价内合约的 Delta 接近 1，使用它们可能只是为了结束某个组合或对冲，而不是表达方向观点。因此实务上更重视 Delta 绝对值中等、略为价外的成交，并优先确认对应的 Gamma 是否同时出现。

- 方向与凸性同向：可能是通过期权建立的、带凸性的方向暴露。
- 方向很大而凸性很小：先怀疑价内合约、组合腿或平仓交易。
- 凸性为正但方向互相对冲：更接近波动率交易而非方向判断。

### 04 / 限制与影响

#### 净额与存量必须分开记录

同类指标有三种不同口径：当日累计的净成交、当前尚未平仓的存量敞口、以及按区段（例如不同到期窗口）划分的敞口。把它们放进同一张对比图之前，必须先确认符号约定、到期覆盖范围与是否可相加，否则两条曲线讲的不是同一件事。

分类成交还存在结构性误差：价差与多腿组合会被拆分记账、场外或协商交易可能不进入公开数据、隐藏订单可能改变主动方归属。因此这类序列适合描述相对强度与关系变化，不适合作为精确持仓数字引用。

- 先声明口径：主动方分类方式、到期覆盖范围、是否包含组合交易。
- 用三条序列同时对齐来读单一成交，避免以规模代替含义。
- 把深度价内的 Delta 大额成交视为可能的结构交易或平仓。
- 累计净成交与存量敞口分开记录，不可互相替代或相加。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> This lesson covers the weighting of classified transactions, not an exposure ledger. The two are often confused: one accumulates same-day trade, the other describes standing positions that remain open.

Convert classified option transactions into two kinds of information — direction and convexity: delta-weighted flow, gamma-weighted flow, the convexity series, cumulative readings, and the limits created by inference.

### 01 / Classified Flow Conventions

#### Define Buy And Sell Before Weighting Anything

The first step in option order flow is labelling each print as buyer- or seller-initiated. Quantity is always equal on both sides, so classification depends on the aggressor rather than on counting more buyers. Two common conventions exist: classifying by which side of the quote the print occurred, or by the direction the print moved relative to the mid.

Direction is given by the delta sign: buying a call and selling a put belong to the positive-delta side, while selling a call and buying a put belong to the negative-delta side. That mapping describes the directional exposure at the moment of the fill only, not the underlying, the hedging instrument, or any later adjustment.

| Transaction | Directional exposure | Convexity exposure |
| --- | --- | --- |
| Buy call | Positive delta | Positive convexity (long option) |
| Sell put | Positive delta | Negative convexity (short option) |
| Sell call | Negative delta | Negative convexity (short option) |
| Buy put | Negative delta | Positive convexity (long option) |

### 02 / Three Weightings

#### The Same Print Weighted By Delta, Gamma, And Convexity

The delta-weighted series converts each print into equivalent directional exposure: positive-delta volume and negative-delta volume are each multiplied by the contract's delta and differenced. It measures the size of directional exposure obtained through options, not the underlying's own trade.

The gamma-weighted series uses the same construction with gamma as the weight and measures demand for convexity. The convexity series instead groups by bought versus sold options and differences their gamma-weighted values, producing net convexity purchased. The distinction matters: the first groups by direction, the second by whether liquidity was taken or supplied.

- **Delta-weighted net exposure**

  ```latex
  \text{Net}_{\Delta}=V_{\text{bull}}\cdot\Delta_{\text{exp}}-V_{\text{bear}}\cdot\Delta_{\text{exp}}
  ```

- **Net convexity purchased**

  ```latex
  \text{Net}_{\Gamma}=V_{\text{long}}\cdot\Gamma_{\text{exp}}-V_{\text{short}}\cdot\Gamma_{\text{exp}}
  ```
  Delta and gamma exposure only become currency amounts after multiplication by the contract's multiplier.

- **Cumulative convention**

  ```latex
  \text{Cumulative}_t=\text{Cumulative}_{t-1}+\text{Net}_t
  ```
  The cumulative series accumulates from the start of the chosen range and is not a standing-exposure measure.

### 03 / Alignment Reading And The Overflow Problem

#### The Three Series Only Say Something When They Align

A delta-weighted series alone only reports size. The information becomes complete when direction, gamma, and convexity agree: negative delta with comparably negative gamma and positive convexity corresponds to taking short exposure by buying out-of-the-money puts, while negative delta with negligible gamma is more likely a deep in-the-money leg or one side of a structure.

This is the delta-overflow problem: deep in-the-money contracts carry delta near one, and they are often used to unwind a structure or hedge rather than to express a view. In practice, prints with moderate absolute delta in slightly out-of-the-money contracts receive more weight, and the corresponding gamma print is checked for confirmation.

- Direction and convexity agree: possibly a convex directional exposure built through options.
- Large direction with negligible convexity: suspect in-the-money legs, structures, or unwinds first.
- Positive convexity with offsetting direction: closer to a volatility trade than a directional view.

### 04 / Limits And Market Impact

#### Net Flow And Standing Exposure Must Be Recorded Separately

These tools have three different conventions: cumulative same-day net trade, standing exposure that remains open, and exposure split by segment such as expiry window. Before placing any of them on one comparison chart, confirm the sign convention, the expiry coverage, and whether the values are additive; otherwise the two curves describe different things.

Classified flow also carries structural error: spreads and multi-leg structures may be booked as separate legs, off-exchange or negotiated trades may not reach the public feed, and hidden orders can change the apparent aggressor. The series is therefore suited to describing relative strength and changes in relationships, not to being quoted as exact positioning.

- State the conventions first: aggressor classification, expiry coverage, and whether spread trades are included.
- Read one print through all three weightings so size is not mistaken for meaning.
- Treat large deep in-the-money delta prints as possible structure or unwind trades.
- Record cumulative net trade and standing exposure separately; they are neither substitutes nor additive.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

