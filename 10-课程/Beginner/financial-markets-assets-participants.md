---
title: "金融市场、资产与参与者角色"
title_en: "Financial Markets, Assets, And Participant Roles"
slug: "financial-markets-assets-participants"
type: lesson
level: Beginner
order: 1
track: markets-macro-and-behavior
track_label: "市场、宏观与行为"
reading_time: "16 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/市场、宏观与行为"
  - "权限/需登录"
aliases:
  - "金融市场、资产与参与者角色"
  - "Financial Markets, Assets, And Participant Roles"
  - "financial-markets-assets-participants"
source_url: "https://tradinghubs.org/docs/trading-knowledge/financial-markets-assets-participants"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-market-data.ts"
generated: 2026-09-15
---

# 金融市场、资产与参与者角色

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[markets-macro-and-behavior|市场、宏观与行为]]
> 下一课：[[price-discovery-market-clearing|价格发现与市场出清]]

**初级 · 市场、宏观与行为 · 16 分钟**

> 资产名称只说明法律与现金流结构，不说明它在任何价格都值得持有。先问清楚“谁付钱、何时付、由什么风险驱动”，再讨论方向。

建立股票、债券、现金、商品与衍生品的现金流地图，并区分投资者、套保者、投机者、套利者与做市商各自承担的风险。

### 01 / 概念边界

#### 市场连接融资需求、风险转移与价格发现

股票代表企业剩余权益，债券代表约定偿付的债权，现金及短期工具强调流动性与名义稳定，商品连接现实供需，衍生品则把未来价格、波动率、利率或其他状态写进合约。它们的风险来源、结算方式和持有成本不同，不能只按“涨跌快慢”归类。

一级市场把新证券或合约交给最初买方，二级市场让既有头寸转手。交易所、清算机构、经纪商、托管人与做市商分别处理撮合、履约、接入、持有与双边报价；任何一层失灵都可能把经济观点变成执行风险。

| 资产 / 合约 | 核心现金流 | 主要风险 |
| --- | --- | --- |
| 股票 | 股息与剩余价值 | 盈利、估值与治理 |
| 债券 | 利息与本金 | 利率、信用与流动性 |
| 商品 / 期货 | 实物价值或差额结算 | 供需、基差与展期 |
| 期权 | 非线性或有支付 | 方向、波动率、时间与尾部 |

### 02 / 机制与度量

#### 同一笔成交可以同时满足不同目标

套保者愿意支付成本降低经营或组合的不确定性；投机者主动承担风险换取预期收益；套利者比较相互约束的价格并承担融资、时点和执行风险；做市商用库存与资本承接短期不平衡。角色由当前目标和头寸决定，不由机构名称永久决定。

总回报应把价格变化和期间现金流放在一起。对衍生品还要加入权利金、保证金资金占用、每日结算、费用和可能的实物交割，不能只看图表上的价格百分比。

- **持有期总回报**

  ```latex
  R=\frac{P_1-P_0+CF}{P_0}
  ```
  CF 表示期间收到或支付的净现金流；杠杆产品还需单独核对保证金与融资。

| 参与者 | 主要目标 | 最容易忽略的风险 |
| --- | --- | --- |
| 套保者 | 压低既有风险 | 基差与过度套保 |
| 投机者 | 承担风险获取预期收益 | 杠杆与路径依赖 |
| 套利者 | 交易相对错价 | 腿间、融资与规则风险 |
| 做市商 | 提供双边报价并管理库存 | 逆向选择与库存尾部 |

### 03 / 阅读流程

#### 用现金流—风险—执行三张表读任何产品

不要从产品名称直接跳到交易结论。先建立最小合约卡，再把观点翻译成可验证的风险因子和退出条件。

- 1. 写明法律权利、现金流、到期、结算方式、乘数和币种。
- 2. 标出方向、波动率、利率、信用、流动性、基差与尾部风险中真正存在的项目。
- 3. 确认自己当前是投资、套保、投机、套利还是提供流动性；同一账户可同时有多种角色。
- 4. 用 Bid / Ask、深度、保证金、费用、交易时段和退出路径检验观点能否执行。

### 04 / 风险边界

#### 资产分类不能替代适当性、估值与风险预算

“债券较稳”“期权风险有限”或“套利无风险”都只有在精确头寸、交易对手、融资和持有路径下才可能成立。相关性会变化，流动性会在压力期收缩，法律与结算规则也可能改变最终现金流。

- 不以资产名称推断最大损失；逐腿或逐证券计算。
- 不把历史平均回报当作未来合约承诺。
- 不在不了解结算、保证金和流动性的情况下使用杠杆。

- 先识别现金流，再识别风险因子，最后才选择工具。
- 相同方向观点可由不同资产表达，但路径、成本与尾部风险不同。
- 角色标签解释交易动机，不证明下一步价格方向。
- 本课用于市场结构教育，不构成资产配置或产品推荐。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> An asset label describes legal rights and cash flows, not whether it is attractive at every price. Ask who pays, when payment occurs, and which risks drive it before discussing direction.

Map the cash flows of equities, bonds, cash, commodities, and derivatives, then distinguish the risks carried by investors, hedgers, speculators, arbitrageurs, and market makers.

### 01 / Concept Boundary

#### Markets Connect Funding, Risk Transfer, And Price Discovery

Equities represent residual ownership, bonds represent contractual claims, cash and short-term instruments emphasize liquidity and nominal stability, commodities connect to physical supply and demand, and derivatives encode future prices, volatility, rates, or other states. Their risk drivers, settlement, and carrying costs differ, so speed of price movement is not a sufficient classification.

Primary markets place new securities or contracts with initial buyers; secondary markets transfer existing positions. Venues, clearinghouses, brokers, custodians, and market makers handle matching, performance, access, safekeeping, and two-sided quotes. Failure at any layer can turn an economic view into execution risk.

| Asset / Contract | Core Cash Flow | Primary Risk |
| --- | --- | --- |
| Equity | Dividends and residual value | Earnings, valuation, and governance |
| Bond | Interest and principal | Rate, credit, and liquidity risk |
| Commodity / Futures | Physical value or cash difference | Supply-demand, basis, and roll risk |
| Option | Nonlinear contingent payoff | Direction, volatility, time, and tail risk |

### 02 / Mechanics And Measurement

#### One Trade Can Serve Different Objectives At The Same Time

Hedgers pay to reduce business or portfolio uncertainty; speculators accept risk for expected return; arbitrageurs compare linked prices while carrying financing, timing, and execution risk; market makers use inventory and capital to absorb short-run imbalances. A role is defined by the current objective and position, not permanently by an institution's name.

Total return combines price change with interim cash flows. Derivatives also require premium, margin funding, daily settlement, fees, and possible physical delivery; a chart's percentage move is not the whole economic result.

- **Holding-period total return**

  ```latex
  R=\frac{P_1-P_0+CF}{P_0}
  ```
  CF is net cash flow received or paid during the period; leveraged products require separate margin and financing checks.

| Participant | Primary Objective | Often-Missed Risk |
| --- | --- | --- |
| Hedger | Reduce an existing exposure | Basis risk and over-hedging |
| Speculator | Accept risk for expected return | Leverage and path dependence |
| Arbitrageur | Trade relative mispricing | Legging, funding, and rule risk |
| Market maker | Quote both sides and manage inventory | Adverse selection and inventory tails |

### 03 / Reading Workflow

#### Read Any Product With Cash-Flow, Risk, And Execution Maps

Do not jump from a product name to a trade conclusion. Build a minimum contract card first, then translate the view into testable risk factors and exit conditions.

- 1. Record legal rights, cash flows, maturity, settlement, multiplier, and currency.
- 2. Mark which directional, volatility, rate, credit, liquidity, basis, and tail risks actually exist.
- 3. Identify whether the current purpose is investment, hedging, speculation, arbitrage, or liquidity provision; one account may hold several roles.
- 4. Test executability with bid-ask, depth, margin, fees, trading hours, and the exit path.

### 04 / Risk Boundary

#### Asset Labels Do Not Replace Suitability, Valuation, Or Risk Budgets

Claims such as bonds are stable, options have limited risk, or arbitrage is riskless are conditional on the exact position, counterparty, financing, and holding path. Correlations can change, liquidity can contract under stress, and legal or settlement rules can alter final cash flows.

- Do not infer maximum loss from an asset label; calculate security by security or leg by leg.
- Do not treat historical average return as a future contractual promise.
- Do not use leverage without understanding settlement, margin, and liquidity.

- Identify cash flows first, risk factors second, and instruments last.
- The same directional view can be expressed through different assets, but path, cost, and tail risk differ.
- Participant labels explain motives; they do not prove the next price direction.
- This lesson teaches market structure and is not an asset-allocation or product recommendation.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- investor-gov-market-basics
- cftc-futures-basics
