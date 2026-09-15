---
title: "远期、期货、基差与持有成本：从现货到股指公平价值"
title_en: "Forwards, Futures, Basis, And Cost Of Carry: From Spot To Equity-Index Fair Value"
slug: "forwards-futures-basis-cost-of-carry"
type: lesson
level: Advanced
order: 56
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "25 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "远期、期货、基差与持有成本：从现货到股指公平价值"
  - "Forwards, Futures, Basis, And Cost Of Carry: From Spot To Equity-Index Fair Value"
  - "forwards-futures-basis-cost-of-carry"
source_url: "https://tradinghubs.org/docs/trading-knowledge/forwards-futures-basis-cost-of-carry"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-quant-data.ts"
generated: 2026-09-15
---

# 远期、期货、基差与持有成本：从现货到股指公平价值

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[multi-metric-risk-dashboard|多指标风险面板：把收益、尾部、路径、敏感度与流动性对齐]] ｜ 下一课：[[risk-neutral-vs-physical-probability|风险中性概率与现实概率：定价分布不是行情预测]]

**高级 · 结构、定价与波动率 · 25 分钟**

> 期货价格与现货指数不同并不自动代表错价。持有现货需要融资却能获得股息，期货不拥有股票篮子且每日结算；基差必须先扣除理论持有成本，才能讨论相对丰富或便宜。

区分远期与期货的现金流机制，固定基差符号，并用融资、收益与到期时间解释股指期货公平价值和净基差。

### 01 / 概念边界

#### 远期锁定终值，期货把损益沿途现金结算

远期是双方约定在 T 以交割价 K 交换标的或现金差额的场外合约，初始公平远期通常价值接近零。期货采用标准化合约并每日盯市，盈利和亏损通过保证金现金流逐日实现。

对与利率不相关或利率近似确定的标的，远期与期货报价可能接近；当价格变化与利率相关时，每日现金流再投资会产生期货—远期凸性差异。信用、抵押、清算、流动性和税务处理也不同。

| 特征 | 远期 | 期货 |
| --- | --- | --- |
| 现金流 | 通常到期或终止时结算 | 每日盯市与保证金 |
| 条款 | 双边定制 | 标准化合约 |
| 主要附加风险 | 对手方、抵押与终止成本 | 基差、展期与保证金流动性 |

### 02 / 机制与度量

#### 股指公平价值等于现货加融资、减去预期股息

在连续融资率 r、连续股息收益率 q、无摩擦且可复制的简化条件下，到期剩余时间 τ 的理论远期为 S_t e^{(r-q)τ}。若已知到期前离散现金收入现值为 I_t，则可先从现货扣除 I_t 再按融资率增长。

本课固定股指基差 b_t=F_{t,T}-S_t；其他市场可能使用相反符号，引用数字前必须确认。更有解释力的净基差是实际期货减理论公平价值。随着到期临近，理论基差收敛到零，但股息预期、资金、供需与交易摩擦会使实际路径偏离。

- **连续收益标的的持有成本**

  ```latex
  F^{*}_{t,T}=S_t e^{(r-q)\tau},\qquad \tau=T-t
  ```

- **已知离散收入与净基差**

  ```latex
  F^{*}_{t,T}=(S_t-I_t)e^{r\tau},\qquad b_t=F_{t,T}-S_t,\qquad b^{\mathrm{net}}_t=F_{t,T}-F^{*}_{t,T}
  ```

### 03 / 阅读流程

#### 把期货报价拆成现货、资金、股息和残差

公平价值比较要求现货指数与期货使用可比时间戳，并准确处理到期时刻、节假日、股息点、融资曲线和合约乘数。可交易复制成本还要加入买卖价差、税费、借券、资本和保证金现金流。

- 确认标的指数、合约月份、结算方式、乘数、币种与精确到期时间。
- 固定基差为期货减现货，并在所有图表中保留该符号说明。
- 用期限匹配的融资曲线和逐笔预期股息计算公平价值。
- 计算实际基差与净基差，并对齐现货与期货报价时间戳。
- 加入复制摩擦、保证金压力和展期情景后再判断可交易性。

### 04 / 风险边界

#### 公平价值是模型锚，不是无风险成交价格

股息预测错误、融资利差、现货指数不可直接成交、篮子跟踪误差和不同交易时段都能形成持久净基差。所谓套利还面临执行不同步、资金占用、保证金追加、结算规则和极端市场下的流动性风险。

到期收敛依赖合约与现货参考值的最终结算定义，并不保证任意持仓能在此前无成本退出。远期与期货也不能在显著随机利率和抵押差异下被默认等价。

- 看到期货升贴水时，先比较理论基差而不是直接判断方向。
- 净基差跳变时分解股息、资金、时间戳和供需因素。
- 展期分析要分开旧合约收敛、新合约持有成本和成交摩擦。
- 本课解释定价关系，不构成基差交易或套利建议。

## 相关概念

- [[risk-free-rate-discounting|无风险利率、贴现与时间价值]] — 持有成本中的利率部分就是无风险贴现率。
- [[option-value-moneyness-put-call-parity|期权价值、价内价外与 Put-Call Parity]] — 远期价是平价关系中把期权与现货连接起来的那一项。
- [[oil-opec-energy-markets|原油、OPEC 与能源市场]] — 库存与便利收益让商品期限结构显著偏离简单持有成本。
- [[futures-contract-mechanics-tick-value|期货合约机制：最小变动、点值与展期]] — 基差交易的点值换算依赖合约乘数与最小跳动。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> A futures price differing from a cash index is not automatically mispriced. Holding cash requires financing but earns dividends, while a futures position does not own the stock basket and is marked daily. Basis must first be compared with theoretical carry before discussing relative richness or cheapness.

Separate forward and futures cash-flow mechanics, fix the basis sign convention, and explain equity-index futures fair value and net basis through financing, income, and time to expiry.

### 01 / Concept Boundary

#### A Forward Locks A Terminal Exchange; A Future Settles Along The Path

A forward is an agreement to exchange an asset or cash difference at T for delivery price K, with a fair new forward usually near zero value at inception. A future is standardized and marked to market daily, realizing gains and losses through margin cash flows along the path.

For an asset uncorrelated with rates, or under nearly deterministic rates, forward and futures quotes may be close. When price changes correlate with rates, reinvestment of daily cash flows creates a futures-forward convexity difference. Credit, collateral, clearing, liquidity, and tax treatment also differ.

| Feature | Forward | Future |
| --- | --- | --- |
| Cash flow | Usually settled at maturity or termination | Daily mark-to-market and margin |
| Terms | Bilaterally customized | Standardized contract |
| Additional risk | Counterparty, collateral, and termination | Basis, roll, and margin liquidity |

### 02 / Mechanics And Measurement

#### Equity-Index Fair Value Adds Financing And Subtracts Expected Dividends

Under simplified continuous financing r, continuous dividend yield q, frictionless trading, and replicability, the theoretical forward with time tau remaining is S_t exp((r-q)tau). If known discrete cash income before expiry has present value I_t, subtract I_t from spot before growing at the financing rate.

This lesson fixes equity-index basis as b_t=F_{t,T}-S_t; other markets may use the opposite sign, so verify convention before quoting a number. Net basis is more informative: actual futures minus theoretical fair value. The theoretical basis converges toward zero near expiry, while dividend expectations, funding, supply and demand, and frictions can move the realized path away from it.

- **Cost Of Carry With Continuous Yield**

  ```latex
  F^{*}_{t,T}=S_t e^{(r-q)\tau},\qquad \tau=T-t
  ```

- **Known Discrete Income And Net Basis**

  ```latex
  F^{*}_{t,T}=(S_t-I_t)e^{r\tau},\qquad b_t=F_{t,T}-S_t,\qquad b^{\mathrm{net}}_t=F_{t,T}-F^{*}_{t,T}
  ```

### 03 / Reading Workflow

#### Decompose A Futures Quote Into Spot, Funding, Dividends, And Residual

A fair-value comparison needs comparable timestamps for cash index and futures plus accurate expiry time, holidays, dividend points, funding curve, and contract multiplier. A tradable replication cost also adds bid-ask, taxes, borrow, capital, and margin cash flows.

- Confirm cash index, contract month, settlement method, multiplier, currency, and exact expiry time.
- Fix basis as futures minus spot and retain that sign note on every chart.
- Use maturity-matched funding and expected dividend cash flows to calculate fair value.
- Calculate actual and net basis with synchronized cash and futures timestamps.
- Add replication frictions, margin pressure, and roll scenarios before judging tradability.

### 04 / Risk Boundary

#### Fair Value Is A Model Anchor, Not A Risk-Free Executable Price

Dividend forecast error, funding spreads, a nontradable cash index, basket tracking error, and different trading hours can sustain net basis. Apparent arbitrage also faces asynchronous execution, capital use, margin calls, settlement rules, and stressed-market liquidity.

Expiry convergence depends on the contract's final settlement definition and does not guarantee a position can exit costlessly before then. Forwards and futures also cannot be assumed equivalent under materially stochastic rates and different collateral terms.

- When futures trade at a premium or discount, compare theoretical basis before inferring direction.
- When net basis jumps, decompose dividends, funding, timestamp, and supply-demand effects.
- Roll analysis should separate old-contract convergence, new-contract carry, and execution friction.
- This lesson explains pricing relations and is not a basis-trade or arbitrage recommendation.

## Related Concepts

- [[risk-free-rate-discounting|Risk-Free Rates, Discounting, And Time Value]] — The rate component of cost of carry is the risk-free discount rate.
- [[option-value-moneyness-put-call-parity|Option Value, Moneyness, And Put-Call Parity]] — The forward price is the term in parity that links options and spot.
- [[oil-opec-energy-markets|Crude Oil, OPEC, And Energy Markets]] — Inventory and convenience yield push commodity term structure away from simple carry.
- [[futures-contract-mechanics-tick-value|Futures Contract Mechanics: Tick Size, Tick Value, And Rolls]] — Basis trading's tick-value arithmetic depends on the contract multiplier and minimum tick.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cftc-futures-basics
- cme-equity-index-basis
- finra-risk
