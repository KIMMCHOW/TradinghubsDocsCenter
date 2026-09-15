---
title: "单腿盈亏结构"
title_en: "Single-Leg Payoff Structure"
slug: "single-leg-payoff"
type: lesson
level: Beginner
order: 10
track: options-foundations
track_label: "期权基础与合约"
reading_time: "14 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/初级"
  - "主题/期权基础与合约"
  - "权限/需登录"
aliases:
  - "单腿盈亏结构"
  - "Single-Leg Payoff Structure"
  - "single-leg-payoff"
source_url: "https://tradinghubs.org/docs/trading-knowledge/single-leg-payoff"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# 单腿盈亏结构

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-beginner|初级]] · [[options-foundations|期权基础与合约]]
> 上一课：[[option-value-moneyness-put-call-parity|期权价值、价内价外与 Put-Call Parity]] ｜ 下一课：[[exercise-assignment-settlement-pin-risk|行权、指派、结算与 Pin Risk]]

**初级 · 期权基础与合约 · 14 分钟**

> 单腿期权不是策略推荐，而是最基础的风险形状。先看清曲线，再谈它可能如何改变对冲压力。

比较 Long Call、Long Put、Short Call、Short Put 的到期盈亏和尾部风险。

### 01 / 四种形状

#### 买方风险有限，卖方可能承担尾部风险

Long Call 和 Long Put 的最大亏损通常是支付的 Premium。它们需要价格、时间和 IV 共同配合，方向看对也可能被时间和波动率变化抵消。

Short Call 和 Short Put 收取 Premium，但风险不对称。卖方结构的风险重点不是“胜率”，而是尾部行情中亏损如何扩张。

- **Long Call PnL**

  ```latex
  \max(S-K,0)-P
  ```

- **Long Put PnL**

  ```latex
  \max(K-S,0)-P
  ```

- **Short Call PnL**

  ```latex
  P-\max(S-K,0)
  ```

- **Short Put PnL**

  ```latex
  P-\max(K-S,0)
  ```

### 02 / Break-even

#### Break-even 是曲线转正位置，不是入场条件

Long Call 的 break-even 通常是 Strike + Premium；Long Put 的 break-even 通常是 Strike - Premium。卖方结构方向相反。

到期盈亏图不包含路径、滑点、提前平仓、IV 变化和流动性，因此只能说明静态终点风险。

| 结构 | 最大亏损 | 最大盈利 |
| --- | --- | --- |
| Long Call | Premium | 理论上随上涨扩大 |
| Long Put | Premium | 随下跌扩大但受标的零价限制 |
| Short Call | 理论上无上限 | Premium |
| Short Put | Strike - Premium 的下方风险 | Premium |

### 03 / 对冲传导

#### 单腿结构会映射成 Delta 暴露

当大量单腿仓位集中在某些 Strike 附近，Dealer 可能需要根据价格移动动态调整 Delta hedge。这条链路会把期权市场传导到 ES / NQ 期货。

- 接近 Strike 时，对冲需求可能变得更敏感。
- 卖方仓位密集区可能带来不同的 Gamma 环境。
- 这解释市场现象，不构成做多或做空建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Single-leg options are not strategy recommendations; they are the base risk shapes. Read the curve before discussing hedging pressure.

Compare expiration payoff and tail risk for long calls, long puts, short calls, and short puts.

### 01 / Four Shapes

#### Buyers Have Limited Loss; Sellers May Carry Tail Risk

Long calls and long puts usually cap loss at the premium paid. They need price, time, and IV to align; correct direction can still be offset by time and volatility changes.

Short calls and short puts collect premium, but the risk is asymmetric. The key risk is not win rate; it is how loss expands in tail moves.

- **Long Call PnL**

  ```latex
  \max(S-K,0)-P
  ```

- **Long Put PnL**

  ```latex
  \max(K-S,0)-P
  ```

- **Short Call PnL**

  ```latex
  P-\max(S-K,0)
  ```

- **Short Put PnL**

  ```latex
  P-\max(K-S,0)
  ```

### 02 / Break-even

#### Break-even Is Where The Curve Turns Positive, Not An Entry Rule

A long call usually breaks even at strike plus premium; a long put usually breaks even at strike minus premium. Short structures reverse the exposure.

An expiration payoff chart excludes path, slippage, early exit, IV change, and liquidity, so it only describes static terminal risk.

| Structure | Max loss | Max profit |
| --- | --- | --- |
| Long Call | Premium | Theoretically expands with upside |
| Long Put | Premium | Expands with downside, bounded by zero spot |
| Short Call | Theoretically unlimited | Premium |
| Short Put | Downside risk below strike less premium | Premium |

### 03 / Hedging Transmission

#### Single Legs Map Into Delta Exposure

When many single-leg positions cluster around strikes, dealers may need to adjust delta hedges as price moves. That connects the options market to ES / NQ futures.

- Near a strike, hedging demand can become more sensitive.
- Dense short-option areas can create different gamma regimes.
- This explains market behavior; it is not a long or short recommendation.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

