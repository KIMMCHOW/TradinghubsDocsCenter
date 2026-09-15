---
title: "隐含波动率 IV 与波动率曲面"
title_en: "Implied Volatility And Volatility Surface"
slug: "implied-volatility-surface"
type: lesson
level: Intermediate
order: 40
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "17 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "隐含波动率 IV 与波动率曲面"
  - "Implied Volatility And Volatility Surface"
  - "implied-volatility-surface"
source_url: "https://tradinghubs.org/docs/trading-knowledge/implied-volatility-surface"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 隐含波动率 IV 与波动率曲面

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[realized-vs-implied-volatility|已实现波动率与隐含波动率]] ｜ 下一课：[[dte-window-selection|DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选]]

**中级 · Greeks 与敏感度 · 17 分钟**

> IV 不是历史波动率本身，而是市场愿意为未来不确定性支付的价格输入。

把 IV 读成市场价格反推的波动率输入，并连接 Expected Move、Skew 和 IV Crush。

### 01 / IV 与 HV

#### IV 是由期权价格反推出来的市场定价

HV / RV 描述过去已经发生的波动，IV 描述市场当前为未来波动付出的价格。两者可以比较，但不能互相替代。

方向判断正确也可能因为 IV 下跌而亏钱，因为期权价格同时受方向、时间和波动率影响。

- **Expected Move**

  ```latex
  \text{Expected Move}=\text{Spot}\times\text{IV}\times\sqrt{\frac{\text{DTE}}{365}}
  ```

### 02 / 曲面

#### 波动率不是单一数字，而是随 Strike 和到期日变化

Vol Smile 和 Skew 描述不同行权价 IV 的差异。期限结构描述不同到期日 IV 的差异。事件风险通常会抬高短期限 IV。

IV Crush 表示事件或不确定性释放后，市场不再愿意为同样的未来波动支付高溢价。

### 03 / 期货传导

#### IV 和 Expected Move 影响市场对波动范围的定价

Expected Move 可以帮助理解市场认为 ES / NQ 在某个期限内可能波动多大。Skew 变化则可能反映下跌尾部风险或上涨追逐风险的重新定价。

- IV 上升或下降会改变 Dealer 的风险管理输入。
- Skew 变陡可能说明保护需求增强。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> IV is not historical volatility itself; it is the price input the market assigns to future uncertainty.

Read IV as the volatility input implied by market prices, then connect expected move, skew, and IV crush.

### 01 / IV And HV

#### IV Is Implied From Option Prices

HV / RV describes volatility that already happened; IV describes the market's current price for future volatility. They can be compared, but one does not replace the other.

A correct directional view can still lose if IV falls, because option price is affected by direction, time, and volatility together.

- **Expected move**

  ```latex
  \text{Expected Move}=\text{Spot}\times\text{IV}\times\sqrt{\frac{\text{DTE}}{365}}
  ```

### 02 / Surface

#### Volatility Is A Surface Across Strike And Expiration

Vol smile and skew describe IV differences across strikes. Term structure describes IV differences across expirations. Event risk often lifts short-dated IV.

IV crush means that after an event or uncertainty passes, the market no longer pays the same high premium for future volatility.

### 03 / Futures Transmission

#### IV And Expected Move Price The Range Of Movement

Expected move helps read how much the market is pricing ES / NQ to move over a horizon. Skew changes can reflect repricing of downside tail risk or upside chase risk.

- Rising or falling IV changes dealer risk-management inputs.
- Steeper skew can indicate stronger protection demand.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

