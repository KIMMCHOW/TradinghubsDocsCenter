---
title: "期货合约机制：最小变动、点值与展期"
title_en: "Futures Contract Mechanics: Tick Size, Tick Value, And Rolls"
slug: "futures-contract-mechanics-tick-value"
type: lesson
level: Intermediate
order: 24
track: futures-and-options-linkage
track_label: "期货与期权衔接"
reading_time: "17 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/期货与期权衔接"
  - "权限/需登录"
aliases:
  - "期货合约机制：最小变动、点值与展期"
  - "Futures Contract Mechanics: Tick Size, Tick Value, And Rolls"
  - "futures-contract-mechanics-tick-value"
source_url: "https://tradinghubs.org/docs/trading-knowledge/futures-contract-mechanics-tick-value"
source_file: "Tradinghub-Web/components/site/options-knowledge/orderflow-data.ts"
generated: 2026-09-15
---

# 期货合约机制：最小变动、点值与展期

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[futures-and-options-linkage|期货与期权衔接]]
> 上一课：[[game-theory-strategic-interaction|博弈论与市场策略互动]] ｜ 下一课：[[auction-market-theory-value-and-imbalance|拍卖市场理论：价值、平衡与失衡]]

**中级 · 期货与期权衔接 · 17 分钟**

> 订单流指标在期货上读到的“数量”必须先换算成钱。本课只处理合约规格与换算，不讨论方向判断。

把期货合约的规格翻译成可比较的风险语言：最小变动价位、每一跳价值、乘数、到期与展期、成交量与未平仓量，以及期货与期权之间的手数换算。

### 01 / 合约规格

#### 最小变动价位与乘数决定每一跳的价值

期货合约规定标的、报价单位、最小变动价位（tick）、合约乘数、交割月份与结算方式。价格变化以跳为单位发生，而每一跳对应固定金额：权益类指数期货通常按“每点金额”报价，最小变动价位与每点金额相乘即为一跳价值。

因此不同品种的“1 手”含义完全不同：名义价值、每跳价值和保证金要求都可能相差数倍。比较两个品种的成交量或持仓量时，必须先统一到名义价值或金额风险，否则数字大小没有可比性。

- **每一跳价值**

  ```latex
  \text{Tick value}=\text{Tick size}\times\text{Currency per point}
  ```
  以权益指数期货为例：最小变动价位乘以每点金额。

- **合约名义价值**

  ```latex
  \text{Notional}=\text{Price}\times\text{Multiplier}
  ```
  名义价值用于比较规模，不等于实际需要的保证金。

- **持仓损益**

  ```latex
  \Delta \text{P\&L}=n\times\text{Multiplier}\times\Delta \text{Price}
  ```
  n 为合约手数；方向为空头时价格变化取反。

### 02 / 到期与展期

#### 持仓必须迁移，成交量会在展期时迁移

期货是到期合约，长期持有必须展期：在近月合约平仓、在远月合约建仓。展期期间近月流动性下降、远月上升，两个合约的价格差（基差）反映持有成本、股息或便利收益与供需差；同一时刻不同合约的报价差异不是套利信号，而是成本结构。

展期会让成交量和未平仓量在合约之间跳变，也会让以单一合约为基础的指标出现人为断层。观察订单流或持仓变化时，必须确认数据来自哪个到期月份，以及当前处于展期周期的哪一段。

### 03 / 量、持仓与换算

#### 成交量是活动，未平仓量是存量，手数换算需要金额对齐

成交量统计当日已成交合约数，每个交易日重新计数；未平仓量统计尚未平仓的合约数，通常每日更新一次，且是一笔买入对应一笔卖出的零和存量。活动量上升不代表仓位增加，也可能是同一批仓位反复换手。

当用期货对冲期权敞口时，手数由金额而非张数决定。若一份指数期权的 Delta 1 对应该指数每一个点的固定金额，而一份期货合约每个点对应另一金额，两者的手数比例就是这两个“每点金额”之比。使用错误的乘数会得到数倍偏差的对冲规模，这也是期货与期权联动分析中最常见的算术错误。

| 概念 | 口径 | 误读边界 |
| --- | --- | --- |
| 成交量 | 当日已成交合约数。 | 高成交量不等于新增持仓。 |
| 未平仓量 | 仍未平仓的合约数。 | 只给出总量，不说明多空归属。 |
| 手数换算 | 按每点金额对齐风险。 | 按张数 1:1 对冲通常错误。 |

### 04 / 市场影响

#### 先换算风险，再解读行为

期货市场的高流动性使大额成交成为可能，也意味着单笔成交的价格影响可能很小。判断一笔成交是否“有意义”，必须同时知道合约规格、当时深度与所处到期月份。

- 把成交量换算成名义金额或每一跳价值，再与其他品种比较。
- 确认数据所属到期月份，并避开展期造成的断点。
- 用每点金额比而不是张数比来推算对冲手数。
- 把保证金要求视为风险约束，而不是可承受亏损的替代指标。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Any quantity read from a futures order-flow tool must first be converted into money. This lesson covers contract specification and conversion only, not directional judgement.

Translate a futures contract specification into comparable risk terms: tick size, value per tick, multiplier, expiry and roll, volume and open interest, and the lot conversion between futures and options.

### 01 / Contract Specification

#### Tick Size And Multiplier Set The Value Of One Tick

A futures contract specifies the underlying, the quote unit, the minimum price increment (tick), the contract multiplier, the delivery months, and the settlement method. Price moves in whole ticks, and each tick maps to a fixed amount of money: equity-index futures quote an amount per index point, so tick size multiplied by that amount gives the value of one tick.

One contract therefore means something different in every market: notional value, value per tick, and margin requirement can differ by multiples. Any volume or open-interest comparison between products must first be normalised into notional value or money risk, otherwise the numbers are not comparable.

- **Value of one tick**

  ```latex
  \text{Tick value}=\text{Tick size}\times\text{Currency per point}
  ```
  For equity-index futures this is the minimum increment multiplied by the currency amount per index point.

- **Contract notional value**

  ```latex
  \text{Notional}=\text{Price}\times\text{Multiplier}
  ```
  Notional value compares size across products; it is not the margin actually required.

- **Position profit and loss**

  ```latex
  \Delta \text{P\&L}=n\times\text{Multiplier}\times\Delta \text{Price}
  ```
  n is the number of contracts, and the price change is negated for short positions.

### 02 / Expiry And Roll

#### Positions Must Migrate, And Volume Migrates With Them

Futures expire, so a long-lived position must be rolled: close the nearby contract and open a further-dated one. During the roll, nearby liquidity falls and deferred liquidity rises. The price difference between the contracts reflects carry, dividends or convenience yield, and supply-demand balance; it is a cost structure, not automatically an arbitrage signal.

A roll makes volume and open interest jump between contract months and can put an artificial break in any indicator built on a single contract. Before reading flow or positioning changes, confirm which expiry the data belongs to and where the roll currently sits.

### 03 / Volume, Open Interest, And Lot Conversion

#### Volume Is Activity, Open Interest Is Stock, And Lot Conversion Needs Equal Money Risk

Volume counts contracts traded during the session and restarts each day. Open interest counts contracts still open and is usually updated once daily; it is a zero-sum stock in which every long is matched by a short. Rising activity does not imply rising positioning; the same positions can turn over repeatedly.

When futures hedge an options exposure, the lot ratio is set by money rather than by contract count. If one index-option delta corresponds to a fixed currency amount per index point and one futures contract corresponds to a different amount, the lot ratio is the ratio of those two per-point amounts. Using the wrong multiplier produces a hedge that is off by a multiple, and it is the most common arithmetic error in futures and options linkage analysis.

| Concept | What it measures | Misreading boundary |
| --- | --- | --- |
| Volume | Contracts traded today. | High volume does not mean new positions. |
| Open interest | Contracts still open. | Gives a total, not who is long or short. |
| Lot conversion | Align money risk per point. | A one-to-one contract hedge is usually wrong. |

### 04 / Market Impact

#### Convert Risk Before Interpreting Behaviour

Futures liquidity makes large trades possible, which also means one large print may barely move price. Deciding whether a print matters requires the contract specification, the depth at the time, and the expiry being traded.

- Convert volume into notional value or tick value before comparing products.
- Confirm the expiry behind the data and avoid roll-induced breaks.
- Derive hedge lots from the per-point amount ratio, not the contract count ratio.
- Treat margin as a risk constraint, not a substitute for acceptable loss.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

