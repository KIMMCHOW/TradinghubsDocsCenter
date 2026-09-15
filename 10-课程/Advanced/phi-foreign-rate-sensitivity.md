---
title: "Foreign Rho / Phi：外币利率与持有收益敏感度"
title_en: "Foreign Rho / Phi: Foreign-Rate And Carry Sensitivity"
slug: "phi-foreign-rate-sensitivity"
type: lesson
level: Advanced
order: 70
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "22 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "Foreign Rho / Phi：外币利率与持有收益敏感度"
  - "Foreign Rho / Phi: Foreign-Rate And Carry Sensitivity"
  - "phi-foreign-rate-sensitivity"
source_url: "https://tradinghubs.org/docs/trading-knowledge/phi-foreign-rate-sensitivity"
source_file: "Tradinghub-Web/components/site/options-knowledge/expanded-options-data.ts"
generated: 2026-09-15
---

# Foreign Rho / Phi：外币利率与持有收益敏感度

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[lambda-option-elasticity|Lambda：把 Delta 转成价格弹性]] ｜ 下一课：[[vanna-cross-sensitivity|Vanna：Delta 与波动率的交叉敏感度]]

**高级 · Greeks 与敏感度 · 22 分钟**

> Phi 没有跨系统统一的字段含义。本课优先使用 Foreign Rho（ρf）表示 FX 模型的国外利率敏感度，并注明部分系统把它称为 Phi；股票期权总览则把对连续股息率 q 的敏感度写成 Phi_q。Garman–Kohlhagen 中 q 与 rf 在数学折现项上对应，但字段、标的与报价币种仍必须明确。

在明确国内币、国外币与单位口径后，用 ρf（部分系统称 Phi）衡量 FX 期权对国外无风险利率的局部敏感度，并与股票期权的 Phi_q 股息率口径分开。

### 01 / 概念边界

#### 先固定 Foreign Rho / Phi 的变量与报价币种

对于以国内币计价、单位国外币标的的 FX 期权，设国内连续复利率为 rd、国外连续复利率为 rf。本课的 Foreign Rho 为保持 S、波动率、rd 与期限不变时，期权价值对 rf 的偏导；若数据系统把它命名为 Phi，也必须保留 ρf 下标。它是局部模型敏感度，不是央行路径预测。

股票期权中的连续股息率 q 在数学上对应 FX 模型里的 rf 折现角色，因此两者的解析导数形式可映射；但 ∂V/∂q 应写成 Phi_q 或 dividend-yield sensitivity，不能在没有元数据时冒充 FX ρf。离散股息、借券费、便利收益和期货基差也不是一个可随意互换的单一利率。

- **本课的 Foreign Rho（部分系统称 Phi）**

  ```latex
  \rho_f=\frac{\partial V}{\partial r_f}
  ```

- **带国内外利率的欧式 FX Call**

  ```latex
  C=S_0e^{-r_fT}N(d_1)-Ke^{-r_dT}N(d_2)
  ```

| 字段口径 | 扰动变量 | 读取前必须确认 |
| --- | --- | --- |
| FX Foreign Rho / ρf（有时称 Phi） | 国外无风险利率 rf | 货币对方向与国内/国外币 |
| Equity Phi_q | 连续股息率 q | 连续还是离散股息模型 |
| Rho / ρd | 国内无风险利率 rd | 输出是每 1、每 1% 还是每 bp |

### 02 / 机制与度量

#### 国外利率通过现值化的标的项改变价值

在 Garman–Kohlhagen 形式下，Long Call 的国外利率敏感度为负，Long Put 为正，因为 rf 上升会降低现值化的国外资产项。该符号依赖本课的报价方向与偏导定义；若平台反转货币对、输出 short position 或采用不同正负口径，屏幕符号可能相反。

解析导数通常以利率小数变化 1.00 为单位。若界面要显示利率上升 1 个百分点的价值变化，应乘 0.01；显示 1 bp 则乘 0.0001。价格是每单位标的还是整份合约，还要再纳入数量与合约乘数。

- 利率曲线应匹配每条腿的币种、期限、抵押与贴现约定。
- Call 与 Put 的 Foreign Rho 不应脱离货币对方向和 position side 单独比较。
- 长期限通常更敏感，但远期点、波动率曲面和交叉货币基差可能同时变化。

- **FX Call 的 Foreign Rho**

  ```latex
  \rho_{f,C}=-T S_0e^{-r_fT}N(d_1)
  ```

- **FX Put 的 Foreign Rho**

  ```latex
  \rho_{f,P}=+T S_0e^{-r_fT}N(-d_1)
  ```

- **屏幕单位换算**

  ```latex
  \rho_{f,1\%}=0.01\,\frac{\partial V}{\partial r_f},\qquad \rho_{f,1bp}=0.0001\,\frac{\partial V}{\partial r_f}
  ```

### 03 / 阅读流程

#### 用元数据、平移冲击和有限差分核验 Foreign Rho / Phi

读取平台 Phi 前，先写出货币对“1 单位国外币值多少国内币”、期权方向、position side、估值币种、利率曲线和输出单位。然后只平移 rf 一个很小的 ε，保持其他输入不变，用中央有限差分验证解析或平台值。

真实情景还应把 rd、rf、现货、远期点和 IV 联合重估，因为宏观事件很少只移动一条曲线。先用单变量冲击诊断字段，再用相关情景估算损益，这两个目的不能混在一起。

- 步骤 1：确认报价币、标的币及国内/国外利率的角色。
- 步骤 2：确认数值按 1.00、1 个百分点或 1 bp 输出，并统一合约乘数。
- 步骤 3：用小 ε 有限差分核验符号和量级。
- 步骤 4：再运行 Spot × rd × rf × IV 联合压力情景。

- **中央有限差分检查**

  ```latex
  \rho_f\approx\frac{V(r_f+\varepsilon)-V(r_f-\varepsilon)}{2\varepsilon}
  ```

### 04 / 风险边界

#### Foreign Rho / Phi 隔离的是偏导，不隔离现实世界

Phi 的解析值依赖平滑曲线、模型形式和固定其他变量的假设。政策冲击可能同时改变现货、远期、基差、偏斜和流动性；长期或受资本管制的货币对还可能偏离简单模型。大冲击应完整重估，而不是线性外推。

若数据源没有明确 Phi 字段定义，应把该值标为“口径待确认”，不能依据经验猜测。错误交换 rd 与 rf、百分点与 bp，都会造成符号或倍数级错误。

- 先读字段定义，再读数值；未知口径不进入组合汇总。
- 分别保存 ρd、ρf 或股息率敏感度，不用一个“rate Greek”覆盖全部 carry 风险。
- 单变量 Foreign Rho 用于诊断，联合宏观情景用于评估真实损益。
- 本课解释计量方法，不预测利率或货币方向，也不构成交易建议。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Phi is not a universally standardized field name. This lesson prefers foreign rho (ρf) for FX foreign-rate sensitivity and notes that some systems call it phi; the equity-options overview writes continuous-dividend-yield sensitivity as Phi_q. In Garman–Kohlhagen, q and rf occupy corresponding mathematical discount terms, but field identity, instrument, and quote currency must still be explicit.

Measure an FX option's local foreign-rate sensitivity with ρf (called phi by some systems) only after fixing domestic currency, foreign currency, and units, and keep it separate from the equity-option Phi_q dividend-yield convention.

### 01 / Concept Boundary

#### Fix The Foreign-Rho / Phi Variable And Quote Currency First

For an FX option quoted in domestic currency per unit of foreign currency, let rd be the domestic continuously compounded rate and rf the foreign rate. Foreign rho here is the partial derivative with respect to rf while S, volatility, rd, and maturity are held fixed; if a data system calls it phi, the ρf subscript must remain explicit. It is a local model sensitivity, not a central-bank forecast.

Continuous equity dividend yield q maps mathematically to the rf discounting role in an FX model, so their analytical derivative forms can correspond. But ∂V/∂q should be labeled Phi_q or dividend-yield sensitivity, not treated as FX ρf without metadata. Discrete dividends, borrow fees, convenience yield, and futures basis are not one interchangeable rate.

- **Foreign rho here (called phi by some systems)**

  ```latex
  \rho_f=\frac{\partial V}{\partial r_f}
  ```

- **European FX call with domestic and foreign rates**

  ```latex
  C=S_0e^{-r_fT}N(d_1)-Ke^{-r_dT}N(d_2)
  ```

| Field convention | Shocked variable | Confirm before reading |
| --- | --- | --- |
| FX foreign rho / ρf (sometimes phi) | Foreign risk-free rate rf | Pair direction and domestic/foreign currency |
| Equity Phi_q | Continuous dividend yield q | Continuous or discrete dividend model |
| Rho / ρd | Domestic risk-free rate rd | Output per 1.00, 1%, or basis point |

### 02 / Mechanics And Measurement

#### The Foreign Rate Acts Through The Discounted Spot Leg

Under the Garman–Kohlhagen form, a long call has negative foreign-rate sensitivity and a long put positive sensitivity because a higher rf reduces the discounted foreign-asset leg. This sign depends on this lesson's quote direction and derivative convention; reversing the pair, reporting a short position, or using another sign convention can reverse the displayed sign.

Analytical derivatives are commonly expressed for a 1.00 change in the rate decimal. A display per one percentage-point move multiplies by 0.01; a display per one basis point multiplies by 0.0001. Whether price is per unit of underlying or per contract then determines quantity and multiplier scaling.

- Rate curves should match each leg's currency, maturity, collateral, and discount convention.
- Do not compare call and put foreign rho without pair direction and position side.
- Longer maturities are often more sensitive, while forward points, the volatility surface, and cross-currency basis may move together.

- **Foreign rho for an FX call**

  ```latex
  \rho_{f,C}=-T S_0e^{-r_fT}N(d_1)
  ```

- **Foreign rho for an FX put**

  ```latex
  \rho_{f,P}=+T S_0e^{-r_fT}N(-d_1)
  ```

- **Display-unit conversion**

  ```latex
  \rho_{f,1\%}=0.01\,\frac{\partial V}{\partial r_f},\qquad \rho_{f,1bp}=0.0001\,\frac{\partial V}{\partial r_f}
  ```

### 03 / Reading Workflow

#### Validate Foreign Rho / Phi With Metadata, Parallel Shocks, And Finite Differences

Before reading platform phi, write the pair as domestic currency per one unit of foreign currency, option side, position side, valuation currency, rate curves, and output unit. Then shift only rf by a small ε while holding all other inputs fixed and validate the analytical or platform value with a central finite difference.

A realistic scenario should jointly revalue rd, rf, spot, forward points, and IV because macro events rarely move only one curve. Use a one-variable shock to diagnose the field, then correlated scenarios for P&L; the two purposes should not be mixed.

- Step 1: Confirm quote currency, base currency, and domestic/foreign rate roles.
- Step 2: Confirm whether output is per 1.00, percentage point, or basis point, then align multipliers.
- Step 3: Use a small-ε finite difference to verify sign and magnitude.
- Step 4: Then run joint spot-by-rd-by-rf-by-IV stress scenarios.

- **Central finite-difference check**

  ```latex
  \rho_f\approx\frac{V(r_f+\varepsilon)-V(r_f-\varepsilon)}{2\varepsilon}
  ```

### 04 / Risk Boundary

#### Foreign Rho / Phi Isolates A Partial Derivative, Not The Real World

Analytical phi depends on smooth curves, model form, and the assumption that other inputs stay fixed. Policy shocks may move spot, forwards, basis, skew, and liquidity together; long-dated or controlled currency pairs may also depart from the simple model. Large shocks require full repricing rather than linear extrapolation.

If a data source does not define its phi field, mark the value as convention unconfirmed rather than guessing from habit. Swapping rd and rf, or percentage points and basis points, can create sign or orders-of-magnitude errors.

- Read the field definition before the value; unknown conventions do not enter portfolio aggregation.
- Store ρd, ρf, and dividend-yield sensitivity separately rather than hiding all carry risk in one rate Greek.
- Use one-variable foreign rho for diagnostics and joint macro scenarios for realistic P&L.
- This lesson explains measurement; it forecasts neither rates nor currencies and is not trading advice.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- cme-greeks
- occ-options-disclosure
