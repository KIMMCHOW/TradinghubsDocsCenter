---
title: "Calmar Ratio 与最大回撤：把复合增长放回路径中"
title_en: "Calmar Ratio And Maximum Drawdown: Returning Growth To Its Path"
slug: "calmar-ratio-maximum-drawdown"
type: lesson
level: Advanced
order: 51
track: risk-performance-and-hedging
track_label: "风险、绩效与对冲"
reading_time: "21 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/风险、绩效与对冲"
  - "权限/需登录"
aliases:
  - "Calmar Ratio 与最大回撤：把复合增长放回路径中"
  - "Calmar Ratio And Maximum Drawdown: Returning Growth To Its Path"
  - "calmar-ratio-maximum-drawdown"
source_url: "https://tradinghubs.org/docs/trading-knowledge/calmar-ratio-maximum-drawdown"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# Calmar Ratio 与最大回撤：把复合增长放回路径中

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[risk-performance-and-hedging|风险、绩效与对冲]]
> 上一课：[[sortino-ratio|Sortino Ratio：只把目标下方偏差计入风险]] ｜ 下一课：[[expected-shortfall-cvar|CVaR / Expected Shortfall：越过分位点后的平均损失]]

**高级 · 风险、绩效与对冲 · 21 分钟**

> 最大回撤不是某一天最差收益，而是净值从此前峰值到随后谷底的最大相对跌幅。Calmar Ratio 将年化复合增长与这段最深历史下行相除，因而比只看波动率更直接地呈现资金路径，却也更依赖样本窗口。

用历史高水位定义回撤与最大回撤，并理解 Calmar Ratio 对窗口、估值频率、复合收益和恢复路径的敏感性。

### 01 / 概念边界

#### 高水位、谷底与恢复日构成一个完整回撤事件

对正的净值序列 V_t，历史高水位 H_t 是截至 t 的最大净值，回撤 D_t 是当前净值相对高水位的跌幅。最大回撤 MDD 是窗口内最大的 D_t，并应同时记录对应峰值日、谷底日和净值达到或超过旧高点的恢复日。

尚未恢复的回撤没有恢复日，但仍必须纳入最大回撤。注资、赎回和分红应通过单位净值或时间加权收益处理，否则外部现金流会被误判为投资损失或收益。

- **回撤与最大回撤**

  ```latex
  H_t=\max_{u\le t}V_u,\qquad D_t=\frac{H_t-V_t}{H_t},\qquad \operatorname{MDD}=\max_t D_t
  ```

### 02 / 机制与度量

#### Calmar 的分子是复合增长，分母是窗口内单次极值

常见定义用窗口内 CAGR 除以最大回撤的绝对比例。CAGR 使用起止净值和以年计的窗口长度；MDD 则可能由窗口中很短的一段事件决定。起点移动到峰值之前或之后，都可能显著改变分母和策略排序。

估值频率也会改变观测到的谷底。日线净值看不到日内追加保证金和盘中流动性压力，月线净值又可能掩盖整段急跌与恢复。报告 Calmar 时必须同时给出窗口、频率、成本口径和最深回撤日期。

- **年化复合增长与 Calmar Ratio**

  ```latex
  \operatorname{CAGR}=\left(\frac{V_{\mathrm{end}}}{V_{\mathrm{start}}}\right)^{1/Y}-1,\qquad \operatorname{Calmar}=\frac{\operatorname{CAGR}}{\operatorname{MDD}}
  ```

| 指标 | 主要回答 | 主要盲点 |
| --- | --- | --- |
| Sharpe | 单位总波动的超额收益 | 路径与尾部形状 |
| Sortino | 单位目标下方偏差的超额收益 | 目标与分母约定 |
| Calmar | 单位最深历史回撤的复合增长 | 窗口极值与未见压力 |

### 03 / 阅读流程

#### 逐事件保存回撤账本

不要只保存最终 MDD 数字。逐日或更高频更新高水位，识别每次峰值、谷底、深度、持续时间与恢复时间，并把仓位、波动率、流动性和保证金变化对齐到事件时间轴。

- 使用扣除费用且正确处理外部现金流的连续净值序列。
- 固定窗口与估值频率，保存峰值、谷底、恢复日和未恢复标记。
- 计算 CAGR 前验证起止净值为正，并注明复利年数。
- 对多个滚动窗口重复计算，而不是只选择最有利的起点。
- 将 MDD 与压力情景、流动性需求和保证金峰值交叉核验。

### 04 / 风险边界

#### 历史最深回撤只是已发生极值，不是损失上限

MDD 只反映所选路径中出现过的最坏峰谷。未来跳空、相关性断裂、交易暂停或融资收缩可以产生更深回撤；期权组合还可能在净值更新之间经历更严重的盘中压力。

Calmar 分母由单个极值决定，统计不稳定且容易被窗口选择优化。它不能替代损失分布、期望损失、情景重估或现金流规划，也不能用作自动加杠杆规则。

- 看到 Calmar 改善时，拆分是 CAGR 上升还是旧回撤离开窗口。
- 对未恢复回撤单独显示水下天数和当前距高点幅度。
- 比较策略时统一窗口、频率、净值口径和现金流处理。
- 该比率描述历史路径，不设定未来最大损失。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Maximum drawdown is not the worst single-day return; it is the largest relative decline from a prior equity peak to a later trough. The Calmar Ratio divides annualized compound growth by that deepest historical decline, making the capital path visible while becoming highly window-dependent.

Define drawdown and maximum drawdown from the running high-water mark, then understand how Calmar depends on window, valuation frequency, compound return, and recovery path.

### 01 / Concept Boundary

#### Peak, Trough, And Recovery Define A Complete Drawdown Event

For a positive equity series V_t, the running high-water mark H_t is the largest value observed through t, and drawdown D_t is the decline from that high. Maximum drawdown, MDD, is the largest D_t in the window and should be accompanied by its peak date, trough date, and the recovery date when equity reaches or exceeds the old high.

An unrecovered drawdown has no recovery date but still belongs in MDD. Contributions, withdrawals, and distributions should be handled through unitized equity or time-weighted returns, or external cash flows will be mistaken for investment gains or losses.

- **Drawdown And Maximum Drawdown**

  ```latex
  H_t=\max_{u\le t}V_u,\qquad D_t=\frac{H_t-V_t}{H_t},\qquad \operatorname{MDD}=\max_t D_t
  ```

### 02 / Mechanics And Measurement

#### Calmar Combines Compound Growth With A Single Window Extreme

A common definition divides CAGR over the selected window by maximum drawdown as a positive fraction. CAGR uses start and end equity and window length in years, while MDD can be determined by a brief event inside the window. Moving the start date before or after a peak can materially change the denominator and ranking.

Valuation frequency also changes the observed trough. Daily equity misses intraday margin calls and liquidity pressure, while monthly equity can hide an entire decline and recovery. A Calmar report must state window, frequency, cost convention, and dates of the deepest drawdown.

- **Compound Annual Growth And Calmar Ratio**

  ```latex
  \operatorname{CAGR}=\left(\frac{V_{\mathrm{end}}}{V_{\mathrm{start}}}\right)^{1/Y}-1,\qquad \operatorname{Calmar}=\frac{\operatorname{CAGR}}{\operatorname{MDD}}
  ```

| Metric | Primary Question | Primary Blind Spot |
| --- | --- | --- |
| Sharpe | Excess return per unit of total variability | Path and tail shape |
| Sortino | Excess return per unit of target shortfall | Target and denominator convention |
| Calmar | Compound growth per unit of deepest historical drawdown | Window extreme and unseen stress |

### 03 / Reading Workflow

#### Maintain A Drawdown Event Ledger

Do not retain only the final MDD number. Update the high-water mark at the chosen frequency, identify each peak, trough, depth, duration, and recovery, and align positions, volatility, liquidity, and margin changes to the event timeline.

- Use a continuous net-equity series net of costs and adjusted for external cash flows.
- Fix window and valuation frequency; store peak, trough, recovery, and unrecovered flags.
- Before calculating CAGR, verify positive start and end equity and state years of compounding.
- Repeat over multiple rolling windows rather than selecting the most favorable start.
- Cross-check MDD against stress scenarios, liquidity needs, and peak margin.

### 04 / Risk Boundary

#### Historical Maximum Drawdown Is An Observed Extreme, Not A Loss Limit

MDD reflects only the worst peak-to-trough event observed on the selected path. Future gaps, correlation breaks, trading halts, or financing contraction can create deeper declines, and an options portfolio may experience more severe intraday pressure between equity marks.

The Calmar denominator is a single extreme, making it statistically unstable and easy to optimize through window selection. It cannot replace the loss distribution, expected shortfall, scenario revaluation, or cash-flow planning, and it must not become an automatic leverage rule.

- When Calmar improves, separate higher CAGR from an old drawdown leaving the window.
- For an unrecovered drawdown, show days underwater and current distance from the high.
- Align window, frequency, equity convention, and cash-flow treatment across strategies.
- The ratio describes a historical path and does not set a future maximum loss.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cfa-risk-adjusted-performance
- finra-risk
