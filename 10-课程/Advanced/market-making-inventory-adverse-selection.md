---
title: "做市库存与逆向选择：价差收入不是免费收益"
title_en: "Market-Making Inventory And Adverse Selection: Spread Capture Is Not Free Return"
slug: "market-making-inventory-adverse-selection"
type: lesson
level: Advanced
order: 83
track: order-flow-and-microstructure
track_label: "订单流与市场微观结构"
reading_time: "24 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/订单流与市场微观结构"
  - "权限/需登录"
aliases:
  - "做市库存与逆向选择：价差收入不是免费收益"
  - "Market-Making Inventory And Adverse Selection: Spread Capture Is Not Free Return"
  - "market-making-inventory-adverse-selection"
source_url: "https://tradinghubs.org/docs/trading-knowledge/market-making-inventory-adverse-selection"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# 做市库存与逆向选择：价差收入不是免费收益

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[order-flow-and-microstructure|订单流与市场微观结构]]
> 上一课：[[time-butterfly-term-structure|Time Butterfly：期限曲率与三到期日重估]] ｜ 下一课：[[avellaneda-stoikov-market-making|Avellaneda–Stoikov 做市模型：库存偏移、价差与校准]]

**高级 · 订单流与市场微观结构 · 24 分钟**

> 被动报价以提供流动性换取价差，但成交往往不是随机礼物：更有信息或更急迫的订单可能在价格即将不利移动时优先击中报价。做市结果是价差、库存、对冲、逆向选择和成本的联合结果。

分解做市的价差捕获、库存重估、逆向选择和执行成本，使用节点库存与多期限 markout 识别表面成交质量。

### 01 / 概念边界

#### 成交增加现金或库存，也改变后续风险

令 q_t 为带方向库存，S_t 为中间价，X_t 为现金，则盯市财富为 W_t=X_t+q_tS_t。买入成交增加 q 并减少现金，卖出成交减少 q 并增加现金；在期权做市中还要按 Delta、Gamma、Vega 和期限节点观察库存。

库存风险不是只有净数量。跨标的对冲可能含相关基差，跨期限 Vega 可能在平行移动下净额却在曲面扭曲时暴露，短期期权还会快速改变 Gamma 与 Delta。总净额必须能下钻到节点。

- **盯市财富**

  ```latex
  W_t=X_t+q_tS_t
  ```

### 02 / 机制与度量

#### 用成交价差与后续中间价移动拆分 markout

定义 s_i=+1 表示做市商买入，s_i=-1 表示做市商卖出，成交价为 p_i，成交时中间价为 m_i。入场价差捕获 C_i=s_i(m_i-p_i) 在买在中间价下方或卖在上方时为正；C_i、A_i 与 M_i 都是每一单位已成交标的的价格量，不是现金 P&L。

h 时间后的不利选择成本可定义为 A_i(h)=-s_i(m_{i+h}-m_i)。若买入后中间价下跌或卖出后中间价上涨，A 为正并侵蚀价差。不同期限 markout 能区分瞬时反弹、短期信息与更慢的库存风险，但不是单笔交易知情程度的确定证明。

- **每单位价差捕获、逆向选择与总 markout**

  ```latex
  C_i=s_i(m_i-p_i),\quad A_i(h)=-s_i(m_{i+h}-m_i),\quad M_i(h)=s_i(m_{i+h}-p_i)=C_i-A_i(h)
  ```

- **报告币种现金 markout**

  ```latex
  \operatorname{CashMarkout}_i(h)=v_i m_i^{\mathrm{ctr}}c_iM_i(h)
  ```
  v_i>0 是成交合约数量，m_i^{ctr} 是每份合约的标的乘数，c_i 是成交本币到报告币种的汇率。

| 观察 | 可能解释 | 需要复核 |
| --- | --- | --- |
| 成交多、短期 markout 差 | 报价过近或逆向选择 | 事件、延迟、队列与方向 |
| 价差捕获正、日终 P&L 差 | 库存与对冲基差 | 节点库存与完整重估 |
| 成交少、markout 好 | 报价过远或样本选择 | 机会成本与未成交样本 |

### 03 / 阅读流程

#### 把每次报价、队列、成交、对冲和 markout 串成事件链

只保存成交会产生选择偏差，因为看不到未成交报价和撤单。完整评估需要当时盘口、报价距离、队列位置代理、延迟、订单大小、事件状态、成交方向和后续多个期限中间价。

- 统一买卖方向符号，并用可重现规则构造中间价。
- 保存所有报价生命周期，包括未成交、修改、撤单与数据失败。
- 按方向、距离、规模、节点、事件和流动性状态分组计算 markout。
- 拆分入场价差、后续中间价、不对称对冲、费用与库存重估。
- 用日内库存峰值、尾部 P&L 与压力成交能力复核平均结果。

### 04 / 风险边界

#### 平均正 markout 不能覆盖跳跃、队列和容量风险

中间价本身可能在宽价差、锁盘或单边盘口中失真。幸存成交、延迟时间戳和未记录撤单也会让 markout 看似改善。统计关系需要稳定样本、置信区间和未成交对照。

库存限额与熔断不能由平均价差收益替代。公告、跳空、交易暂停、保证金变化和对冲工具失灵可在很短时间内超过长期累计价差；真实系统还需要硬限额、撤单能力和人工接管。

- 成交率上升时同时检查 markout、库存峰值和市场状态。
- 价差收入与后续不利移动必须使用统一符号分别展示。
- 平均结果之外报告尾部、连续亏损和无法对冲情景。
- 本课解释做市风险，不构成自动报价或流动性提供建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Passive quotes seek spread for supplying liquidity, but fills are not random gifts: informed or urgent flow may hit a quote just before price moves against it. Market-making results jointly reflect spread, inventory, hedging, adverse selection, and costs.

Decompose market making into spread capture, inventory revaluation, adverse selection, and execution cost, using node inventory and multi-horizon markouts to diagnose apparent fill quality.

### 01 / Concept Boundary

#### A Fill Changes Cash Or Inventory And Therefore Future Risk

Let q_t be signed inventory, S_t midpoint, and X_t cash, so marked wealth is W_t=X_t+q_tS_t. A purchase increases q and reduces cash, while a sale decreases q and increases cash. Options market making also needs inventory views by delta, gamma, vega, and expiry nodes.

Inventory risk is more than net quantity. Cross-underlying hedges contain correlation basis, cross-expiry vega may net for parallel moves but not surface twists, and short-dated options can change gamma and delta rapidly. Grand totals must drill down to nodes.

- **Marked-To-Market Wealth**

  ```latex
  W_t=X_t+q_tS_t
  ```

### 02 / Mechanics And Measurement

#### Separate Entry Spread From Subsequent Midprice Movement

Define s_i=+1 when the market maker buys and s_i=-1 when the market maker sells, with fill price p_i and contemporaneous midpoint m_i. Entry spread capture C_i=s_i(m_i-p_i) is positive when buying below or selling above midpoint; C_i, A_i, and M_i are price amounts per filled underlying unit, not cash P&L.

Adverse-selection cost at horizon h can be defined as A_i(h)=-s_i(m_{i+h}-m_i). If midpoint falls after a buy or rises after a sale, A is positive and erodes spread capture. Markouts across horizons help separate immediate bounce, short-lived information, and slower inventory risk, but do not prove whether an individual counterparty was informed.

- **Per-Unit Spread Capture, Adverse Selection, And Total Markout**

  ```latex
  C_i=s_i(m_i-p_i),\quad A_i(h)=-s_i(m_{i+h}-m_i),\quad M_i(h)=s_i(m_{i+h}-p_i)=C_i-A_i(h)
  ```

- **Cash Markout In Reporting Currency**

  ```latex
  \operatorname{CashMarkout}_i(h)=v_i m_i^{\mathrm{ctr}}c_iM_i(h)
  ```
  Here v_i>0 is filled contract quantity, m_i^{ctr} is underlying units per contract, and c_i is the FX conversion from fill currency to reporting currency.

| Observation | Possible Explanation | Review Needed |
| --- | --- | --- |
| Many fills, poor short markout | Quotes too close or adverse selection | Events, latency, queue, and side |
| Positive entry capture, poor daily P&L | Inventory and hedge basis | Node inventory and full revaluation |
| Few fills, good markout | Quotes too far or selection bias | Opportunity cost and nonfills |

### 03 / Reading Workflow

#### Join Quotes, Queue, Fills, Hedges, And Markouts Into One Event Chain

Saving fills alone creates selection bias because unfilled quotes and cancellations disappear. A complete evaluation needs contemporaneous book, quote distance, queue-position proxy, latency, order size, event state, fill side, and midpoints at several later horizons.

- Standardize buy-sell signs and construct midpoint with a reproducible rule.
- Retain every quote lifecycle, including nonfills, amendments, cancellations, and data failures.
- Calculate markouts by side, distance, size, node, event, and liquidity regime.
- Separate entry spread, subsequent midpoint, asymmetric hedge, fees, and inventory revaluation.
- Challenge averages with peak intraday inventory, tail P&L, and stressed execution capacity.

### 04 / Risk Boundary

#### A Positive Average Markout Does Not Cover Jump, Queue, Or Capacity Risk

Midpoint can be misleading in wide, locked, or one-sided books. Surviving fills, timestamp latency, and unrecorded cancellations can also make markouts look better. Statistical relationships need stable samples, uncertainty intervals, and nonfill controls.

Average spread revenue cannot replace inventory limits or kill switches. Announcements, gaps, halts, margin changes, and hedge failures can overwhelm long-accumulated spread in a short interval; real systems also need hard limits, cancellation capacity, and manual takeover.

- When fill rate rises, inspect markout, peak inventory, and market regime together.
- Show spread capture and adverse movement separately under one sign convention.
- Report tails, loss streaks, and unhedgeable scenarios beyond averages.
- This lesson explains market-making risk and is not automatic quoting or liquidity-provision advice.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- glosten-milgrom-original
- nyu-avellaneda-stoikov
- nyfed-market-liquidity
- finra-risk
- occ-options-disclosure
