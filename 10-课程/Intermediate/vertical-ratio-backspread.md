---
title: "垂直价差、Ratio Spread 与 Backspread"
title_en: "Vertical Spreads, Ratio Spreads, And Backspreads"
slug: "vertical-ratio-backspread"
type: lesson
level: Intermediate
order: 31
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "22 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "垂直价差、Ratio Spread 与 Backspread"
  - "Vertical Spreads, Ratio Spreads, And Backspreads"
  - "vertical-ratio-backspread"
source_url: "https://tradinghubs.org/docs/trading-knowledge/vertical-ratio-backspread"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# 垂直价差、Ratio Spread 与 Backspread

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[covered-protective-collar|Covered、Protective 与 Collar 结构]] ｜ 下一课：[[straddle-strangle-event-risk|Straddle、Strangle 与事件波动]]

**中级 · 结构、定价与波动率 · 22 分钟**

> 执行价之间的数量关系比策略名称更重要。一比一结构通常能定义最大到期宽度；数量不相等后，某一尾部可能重新开放，保证金和跳空风险随之改变。

从同到期不同执行价出发，比较一比一垂直价差、净卖出尾部的 Ratio Spread 与净买入尾部的 Backspread。

### 01 / 一比一价差

#### Vertical 用执行价宽度交换成本与封顶

Call Vertical 由同到期的两个不同执行价 Call 组成，Put Vertical 同理。买入一腿并卖出更远执行价的一腿后，单腿无限或较大范围的收益形状被截断，组合最大到期价值通常受执行价宽度约束。

Debit 或 Credit 只描述初始净现金流，不自动说明看涨、看跌或胜率。方向要从各价格区间的净到期价值判断；到期前还需观察两腿 Delta、Gamma、Theta、Vega 与偏斜的差。

- **Bull Call Spread 到期价值**

  ```latex
  \max(S_T-K_1,0)-\max(S_T-K_2,0),\quad K_1<K_2
  ```

- **一比一价差最大毛价值**

  ```latex
  \text{Max gross value}=K_2-K_1
  ```

- **净到期盈亏**

  ```latex
  \text{Net P\&L}=\text{Terminal value}-\text{Initial debit}
  ```

| 结构特征 | 一比一 Vertical | 数量不相等后 |
| --- | --- | --- |
| 尾部 | 通常由执行价宽度封顶。 | 某一尾部可能重新开放。 |
| 保证金 | 常可由最大宽度估算。 | 取决于净卖出数量与账户规则。 |
| 主要检查 | 宽度、净权利金、到期。 | 每个价格区间的净合约数。 |

### 02 / 数量不对称

#### Ratio Spread 与 Backspread 的区别在于哪一侧净卖出期权

Ratio Call Spread 的常见示例是买入一个较低执行价 Call，同时卖出多个较高执行价 Call。价格越过所有执行价后，额外的 Short Call 会使上方尾部重新暴露；初始 Credit 不能抵消无限延伸的理论风险。

Call Backspread 则通常卖出较少近执行价 Call、买入更多远执行价 Call，使极端上涨一侧净 Long Options，但中间区域可能出现损失谷。Put 版本镜像到下方尾部。到期前，IV 变化和 Gamma 集中会让最佳或最差区域随时间移动。

- “Ratio”不说明具体比例，必须直接读取每条腿数量。
- Backspread 的尾部为 Long Options，不代表整个价格区间都受保护。
- 提前指派可能把净期权结构暂时变成标的加剩余期权。

- **1×2 Ratio Call 到期价值**

  ```latex
  \max(S_T-K_1,0)-2\max(S_T-K_2,0)
  ```

- **1×2 Call Backspread 到期价值**

  ```latex
  -\max(S_T-K_1,0)+2\max(S_T-K_2,0)
  ```

### 03 / 情景地图

#### 先按价格区间数净合约，再看 Greeks 与执行

把所有执行价从低到高排列，在每个区间写出已进入内在价值的腿和净数量，由此得到到期斜率如何变化。随后加入初始 Debit / Credit，计算各拐点、最大有限损失以及是否存在开放尾部。

到期图之后，再用价格 × 时间 × IV 情景重估当前价值，并检查多腿价差、部分成交、保证金、提前指派和 Pin Risk。比例结构对数量错误极其敏感，订单确认页必须与研究表逐腿核对。

- 第一步：按执行价排序并计算每个区间的净斜率与净期权数量。
- 第二步：标记有限宽度、中间损失谷和任何开放尾部。
- 第三步：用完整重估和实际 Bid / Ask 检查到期前路径与可执行性。
- 结构比较只展示风险形状，不推荐具体比例、执行价或方向。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Quantity relationships across strikes matter more than strategy names. One-for-one structures usually define a maximum terminal width; once quantities differ, a tail may reopen and change margin and gap risk.

Start with same-expiry different-strike options and compare one-for-one verticals, ratio spreads with net short-tail exposure, and backspreads with net long-tail exposure.

### 01 / One-For-One Verticals

#### A Vertical Exchanges Strike Width For Cost And A Cap

A call vertical uses two calls with the same expiry and different strikes; a put vertical does the same with puts. Buying one leg and selling a farther strike truncates the single leg's broad payoff shape, and maximum terminal package value is generally bounded by strike width.

Debit or credit describes initial net cash flow, not automatically bullishness, bearishness, or win probability. Direction comes from net terminal value across price regions; before expiry, differences in delta, gamma, theta, vega, and skew between legs also matter.

- **Bull call spread terminal value**

  ```latex
  \max(S_T-K_1,0)-\max(S_T-K_2,0),\quad K_1<K_2
  ```

- **Maximum gross value of a one-for-one vertical**

  ```latex
  \text{Max gross value}=K_2-K_1
  ```

- **Net terminal P&L**

  ```latex
  \text{Net P\&L}=\text{Terminal value}-\text{Initial debit}
  ```

| Structure Feature | One-For-One Vertical | After Unequal Ratios |
| --- | --- | --- |
| Tail | Usually capped by strike width. | One tail may reopen. |
| Margin | Often estimable from maximum width. | Depends on net short quantity and account rules. |
| Primary Check | Width, net premium, and expiry. | Net contract count in every price region. |

### 02 / Unequal Quantities

#### Ratio Spreads And Backspreads Differ By Which Side Is Net Short Options

A common ratio call spread buys one lower-strike call and sells multiple higher-strike calls. Once price moves beyond all strikes, the extra short calls reopen the upper tail; an initial credit cannot offset theoretically unbounded extension.

A call backspread usually sells fewer near-strike calls and buys more farther calls, leaving net long options in the extreme upper tail but a loss valley in the middle. The put version mirrors this to the downside. Before expiry, IV changes and concentrated gamma can move the best and worst regions through time.

- Ratio does not state the actual ratio; read each leg's quantity.
- Long-option tail exposure in a backspread does not protect the entire price range.
- Early assignment can temporarily transform the option package into underlying plus residual options.

- **1-by-2 ratio call terminal value**

  ```latex
  \max(S_T-K_1,0)-2\max(S_T-K_2,0)
  ```

- **1-by-2 call backspread terminal value**

  ```latex
  -\max(S_T-K_1,0)+2\max(S_T-K_2,0)
  ```

### 03 / Scenario Map

#### Count Net Contracts By Price Region Before Reading Greeks And Execution

Sort all strikes from low to high, then write which legs are intrinsic and their net quantity in each region to derive changes in terminal slope. Add the initial debit or credit, calculate each kink, any finite maximum loss, and whether an open tail exists.

After the terminal diagram, revalue across price, time, and IV scenarios, then inspect multi-leg spread, partial fills, margin, early assignment, and pin risk. Ratio structures are highly sensitive to quantity errors, so the order ticket must be checked leg by leg against the research table.

- Step 1: Sort strikes and calculate net slope and net option count in each region.
- Step 2: Mark bounded width, middle loss valleys, and any open tail.
- Step 3: Use full revaluation and executable bid-ask prices to check pre-expiry path and executability.
- The comparison shows risk shapes and recommends no ratio, strike, or direction.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

