---
title: "Flow：期权成交分类怎么读"
title_en: "Flow: How To Read Classified Options Trading"
slug: "options-flow-direction"
type: lesson
level: Intermediate
order: 43
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "12 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "Flow：期权成交分类怎么读"
  - "Flow: How To Read Classified Options Trading"
  - "options-flow-direction"
source_url: "https://tradinghubs.org/docs/trading-knowledge/options-flow-direction"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# Flow：期权成交分类怎么读

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[market-maker-flow|做市商对冲：Delta 中性与 Gamma 再平衡]] ｜ 下一课：[[gamma-exposure-gex|GEX / vGEX：Gamma Exposure 怎么看]]

**中级 · 做市商定位与期权敞口 · 12 分钟**

> Flow 来自当天真实成交，但 Buy / Sell 标签通常是主动侧分类，不是完整交易意图。它不是做市商库存，也不自动回答开仓、平仓或多腿组合最终偏向哪一侧。

区分 Call Buy、Put Buy、Call Sell、Put Sell 的成交分类，并在不知道开平仓、多腿意图与最终对手方时保持边界。

### 01 / 四类成交

#### Call Buy、Put Buy、Call Sell、Put Sell 要分开看

在单腿、主动成交且方向未被其他腿抵消的简化情形下，Call Buy 与 Put Sell 可归为偏多分类，Put Buy 与 Call Sell 可归为偏空分类。真实成交可能是平仓、对冲或组合的一条腿，所以该标签描述分类倾向，不代表账户意图或期货必然方向。

Flow 应与价格位置、期货成交和之后的 OI 更新一起核对。与 GEX、vGEX、DEX 比较前，还要确认这些指标是否使用兼容的有符号口径，避免把绝对量称为同向或背离。

- F_bullish class 与 F_bearish class 必须使用同一单位和互斥分类。
- Ratio 与 Net Flow 都是成交分类统计，不是开仓方向或 dealer 库存。

- **分类 Flow Ratio**

  ```latex
  R_F=\frac{F_{\mathrm{bullish\ class}}}{F_{\mathrm{bullish\ class}}+F_{\mathrm{bearish\ class}}},\quad \text{denominator}>0
  ```

- **净分类 Flow**

  ```latex
  F_{\mathrm{net\ class}}=F_{\mathrm{bullish\ class}}-F_{\mathrm{bearish\ class}}
  ```

### 02 / 确认与冲突

#### 兼容口径下的 Flow 只能增加证据，不能证明结构

如果价格接近某个 OI / GEX 集中区，同时分类 Flow 与期货价格都向该区域延续，可说当天活动正在测试该位置。若分类 Flow 与最近仓位快照不同，只能记录为观察层不一致；等待价格接受和下一次 OI 更新后，才能讨论结构是否迁移。

| Flow 状态 | 结构状态 | 读法 |
| --- | --- | --- |
| Flow 偏多 | 价格接近上方 GEX | 测试上方结构。 |
| Flow 偏空 | 价格接近下方 GEX | 测试下方结构。 |
| Flow 与 GEX 背离 | Volume 放大 | 记录为活动与快照不一致，等待价格和 OI 更新。 |

### 03 / 期货传导

#### Flow 是“今天有没有人推动”的线索

OI 快照告诉你最近哪里有未平仓合约，绝对 GEX 告诉你哪里 Gamma 敏感，Flow 告诉你当天成交主动侧如何分类。只有价格与成交持续确认后，才能把三者组合成市场状态假设。

- Flow 要和 Volume 一起看，只有方向没有参与度是不够的。
- Flow 是日内信息，不应替代中期仓位结构。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Flow comes from real same-session trades, but buy-sell labels usually describe aggressor-side classification rather than complete intent. It is not dealer inventory and does not automatically reveal whether opening, closing, or multi-leg packages are ultimately directional.

Separate call-buy, put-buy, call-sell, and put-sell classifications while preserving the boundary around unknown opening, closing, multi-leg intent, and final counterparty.

### 01 / Four Trade Types

#### Call Buy, Put Buy, Call Sell, And Put Sell Must Be Separated

In a simplified single-leg aggressor trade whose direction is not offset elsewhere, call buys and put sells can be classified as bullish-leaning, while put buys and call sells can be classified as bearish-leaning. A real trade may be closing, hedging, or one leg of a package, so the label describes classification rather than account intent or guaranteed futures direction.

Check flow against price location, futures participation, and the later OI update. Before comparing it with GEX, vGEX, or DEX, confirm compatible signed conventions so magnitude-only values are not called aligned or divergent.

- Bullish-class and bearish-class flow must use the same units and mutually exclusive classification.
- Both the ratio and net flow are trade-classification statistics, not opening direction or dealer inventory.

- **Classified flow ratio**

  ```latex
  R_F=\frac{F_{\mathrm{bullish\ class}}}{F_{\mathrm{bullish\ class}}+F_{\mathrm{bearish\ class}}},\quad \text{denominator}>0
  ```

- **Net classified flow**

  ```latex
  F_{\mathrm{net\ class}}=F_{\mathrm{bullish\ class}}-F_{\mathrm{bearish\ class}}
  ```

### 02 / Confirmation And Conflict

#### Compatible Flow Adds Evidence; It Does Not Prove Structure

If price approaches an OI or GEX cluster while classified flow and futures price both persist toward it, same-session activity is testing that area. If classified flow differs from the latest positioning snapshot, record disagreement between observation layers; wait for price acceptance and the next OI update before calling structural migration.

| Flow State | Structure State | Reading |
| --- | --- | --- |
| Bullish flow | Price near upper GEX | Testing upper structure. |
| Bearish flow | Price near lower GEX | Testing lower structure. |
| Flow diverges from GEX | Volume expands | Record activity-versus-snapshot disagreement and wait for price and OI updates. |

### 03 / Futures Transmission

#### Flow Shows Whether Someone Is Pushing Today

The OI snapshot shows where contracts were recently open, magnitude GEX shows where gamma sensitivity sits, and flow shows how same-session aggressor trades are classified. Combine them into a regime hypothesis only after persistent price and participation confirmation.

- Read flow with volume; direction without participation is not enough.
- Flow is intraday information and should not replace medium-term positioning structure.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

