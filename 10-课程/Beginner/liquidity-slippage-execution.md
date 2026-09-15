---
title: "流动性、滑点与期权执行"
title_en: "Liquidity, Slippage, And Option Execution"
slug: "liquidity-slippage-execution"
type: lesson
level: Beginner
order: 12
track: options-foundations
track_label: "期权基础与合约"
reading_time: "18 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/期权基础与合约"
  - "权限/需登录"
aliases:
  - "流动性、滑点与期权执行"
  - "Liquidity, Slippage, And Option Execution"
  - "liquidity-slippage-execution"
source_url: "https://tradinghubs.org/docs/trading-knowledge/liquidity-slippage-execution"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# 流动性、滑点与期权执行

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[options-foundations|期权基础与合约]]
> 上一课：[[exercise-assignment-settlement-pin-risk|行权、指派、结算与 Pin Risk]] ｜ 下一课：[[open-interest-oi|OI 未平仓量：期权仓位账本]]

**初级 · 期权基础与合约 · 18 分钟**

> 期权策略的理论曲线按一个价格计算，真实账户却要跨越买卖价差并面对有限深度。若不把执行成本放入结构分析，精确的收益图也可能只是不可成交的草图。

从 Bid / Ask、深度、规模、报价新鲜度和多腿成交理解屏幕价格与实际成交之间的差异，并建立可复核的执行成本记录。

### 01 / 报价质量

#### Mid 是参考点，Bid 与 Ask 才定义当前边界

Bid 表示当前可见买方愿意支付的最高价，Ask 表示当前可见卖方愿意接受的最低价，二者之间的 Spread 是立即成交的基础摩擦。Mid 适合标记相对位置，但不保证有任何数量能在该价格成交。

流动性还包括每档规模、更多档位的深度、报价更新时间、成交频率和冲击后的恢复速度。较窄的一档价差可能只有很小数量，而较宽价差也可能在提交有限价组合后改善，因此单一快照不能完整描述可执行性。

- **报价中间价**

  ```latex
  M=\frac{\text{Bid}+\text{Ask}}{2}
  ```

- **绝对价差**

  ```latex
  \text{Spread}=\text{Ask}-\text{Bid}
  ```

- **相对价差**

  ```latex
  \text{Relative spread}=\frac{\text{Ask}-\text{Bid}}{M}
  ```

| 指标 | 有助于观察 | 单独使用的局限 |
| --- | --- | --- |
| Spread | 立即成交摩擦。 | 不显示可用规模。 |
| Volume | 某期间已成交活动。 | 不保证下一笔深度。 |
| Open Interest | 存量未平仓合约。 | 不是即时买卖意愿。 |

### 02 / 成交偏差

#### 滑点要相对决策时基准计算，多腿还要处理同步风险

滑点应相对一个有时间戳的基准衡量，例如决策时 Mid、到达市场时的最佳报价或预设限价。若没有基准和方向，事后把所有不利差值称为滑点会混合市场移动、价差、延迟与订单冲击。

多腿结构可按组合净价提交，也可逐腿执行。组合订单减少裸露某一腿的时间，但可能更难成交；逐腿可能获得更好单腿价格，却暴露 Legging Risk。部分成交、撤单延迟和快速 Delta 变化都应进入最坏情景。

- 有限价控制最差价格，但不保证成交或完整成交。
- 市场单提高成交概率，却可能在薄弱深度中产生超预期冲击。
- 事件窗口中的陈旧报价可能让显示价差低估真实风险。

- **买入执行偏差**

  ```latex
  \text{Shortfall}_{\mathrm{buy}}=P_{\mathrm{fill}}-P_{\mathrm{benchmark}}
  ```

- **卖出执行偏差**

  ```latex
  \text{Shortfall}_{\mathrm{sell}}=P_{\mathrm{benchmark}}-P_{\mathrm{fill}}
  ```

- **现金成本缩放**

  ```latex
  \text{Cash cost}=\text{Price shortfall}\times\text{Multiplier}\times\text{Contracts}
  ```

### 03 / 执行清单

#### 把流动性检查放在结构选择之前与成交之后

下单前记录合约、乘数、Bid / Ask、可见规模、报价时间、近期成交和组合净价，并把价差转换成账户现金单位。对多腿结构同时估算组合成交与逐腿失败时的风险，确认保证金和指派边界。

成交后保存每一笔时间、数量、价格和当时基准，分开计算价差成本、市场移动与费用。长期记录按合约类别、到期、时段和订单规模聚合，才能判断某种理论优势是否长期被执行摩擦吞噬。

- 第一步：用绝对与相对价差、深度、报价年龄和乘数描述可执行性。
- 第二步：为组合成交、部分成交与逐腿成交分别画出风险边界。
- 第三步：按决策时基准归因成交偏差，避免只用事后 Mid 评价。
- 执行质量分析用于理解成本与操作风险，不推荐任何订单类型、时机或规模。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Option payoff diagrams use a single price, while real accounts must cross spreads and face finite depth. If execution costs are omitted, a precise payoff chart may be only an untradeable sketch.

Use bid-ask, depth, size, quote freshness, and multi-leg fills to understand the gap between screen price and actual execution and to build an auditable cost record.

### 01 / Quote Quality

#### Mid Is A Reference; Bid And Ask Define The Current Boundary

Bid is the highest currently displayed buying interest and ask the lowest displayed selling interest; their spread is the basic friction of immediate execution. Mid is useful as a reference but does not guarantee that any size can trade there.

Liquidity also includes size at each level, depth beyond the best quote, quote age, trade frequency, and recovery after impact. A narrow top-of-book spread may cover very little size, while a wide quote may improve for a resting limit package; one snapshot cannot fully describe executability.

- **Quoted midpoint**

  ```latex
  M=\frac{\text{Bid}+\text{Ask}}{2}
  ```

- **Absolute spread**

  ```latex
  \text{Spread}=\text{Ask}-\text{Bid}
  ```

- **Relative spread**

  ```latex
  \text{Relative spread}=\frac{\text{Ask}-\text{Bid}}{M}
  ```

| Metric | Helps Observe | Limit When Used Alone |
| --- | --- | --- |
| Spread | Immediate execution friction. | Does not show available size. |
| Volume | Completed activity in a period. | Does not guarantee depth for the next order. |
| Open interest | Standing open contracts. | Is not immediate buying or selling interest. |

### 02 / Execution Shortfall

#### Measure Slippage Against A Decision-Time Benchmark; Multi-Leg Orders Add Synchronization Risk

Slippage should be measured against a timestamped benchmark such as decision-time mid, arrival best quote, or a preset limit. Without a benchmark and side, labeling every adverse difference as slippage mixes market movement, spread, latency, and order impact.

A multi-leg structure can be submitted at a net package price or legged individually. A package reduces time exposed to one naked leg but may fill less readily; legging may improve individual prices but adds legging risk. Partial fills, cancel latency, and rapidly changing delta belong in the worst-case scenario.

- A limit price controls the worst fill price but does not guarantee a fill or a complete fill.
- A market order raises fill probability but may create unexpectedly large impact in thin depth.
- Stale quotes around events can make the displayed spread understate actual risk.

- **Buy execution shortfall**

  ```latex
  \text{Shortfall}_{\mathrm{buy}}=P_{\mathrm{fill}}-P_{\mathrm{benchmark}}
  ```

- **Sell execution shortfall**

  ```latex
  \text{Shortfall}_{\mathrm{sell}}=P_{\mathrm{benchmark}}-P_{\mathrm{fill}}
  ```

- **Cash-cost scaling**

  ```latex
  \text{Cash cost}=\text{Price shortfall}\times\text{Multiplier}\times\text{Contracts}
  ```

### 03 / Execution Checklist

#### Check Liquidity Before Structure Selection And Again After Execution

Before ordering, record contract, multiplier, bid and ask, displayed size, quote time, recent trades, and package net price, converting spread into account cash units. For multi-leg structures, estimate both package execution and the risk of a failed legging sequence, including margin and assignment boundaries.

After execution, retain each timestamp, quantity, price, and contemporaneous benchmark, separating spread cost, market movement, and fees. Aggregate records by contract class, expiry, session, and order size to determine whether execution friction persistently consumes a theoretical edge.

- Step 1: Describe executability with absolute and relative spread, depth, quote age, and multiplier.
- Step 2: Map risk boundaries for package fills, partial fills, and legged execution.
- Step 3: Attribute execution shortfall against a decision-time benchmark rather than an after-the-fact midpoint.
- Execution-quality analysis explains cost and operating risk; it recommends no order type, timing, or size.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

