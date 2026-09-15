---
title: "二叉树与风险中性定价"
title_en: "Binomial Trees And Risk-Neutral Pricing"
slug: "binomial-risk-neutral-pricing"
type: lesson
level: Advanced
order: 57
track: structures-pricing-and-volatility
track_label: "结构、定价与波动率"
reading_time: "22 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/结构、定价与波动率"
  - "权限/需登录"
aliases:
  - "二叉树与风险中性定价"
  - "Binomial Trees And Risk-Neutral Pricing"
  - "binomial-risk-neutral-pricing"
source_url: "https://tradinghubs.org/docs/trading-knowledge/binomial-risk-neutral-pricing"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# 二叉树与风险中性定价

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[structures-pricing-and-volatility|结构、定价与波动率]]
> 上一课：[[model-assumptions-and-model-risk|模型假设与模型风险：从公式正确到决策可靠]] ｜ 下一课：[[bsm-pricing-model|Black-Scholes-Merton Pricing Model]]

**高级 · 结构、定价与波动率 · 22 分钟**

> 二叉树的重点不是猜下一步上涨还是下跌，而是把未来状态离散化，并在每个节点寻找能复制下一期现金流的标的与现金组合。含连续收益率 q 时，标的腿必须按预付远期或股息再投资后的实际持股统一计量。

从一期复制组合推导 Delta 与风险中性概率，再用向后递推理解多期、美式提前行权和离散现金流如何进入期权价格。

### 01 / 一期复制

#### 先用两个未来状态解出 Delta 与现金腿

设上涨与下跌节点是一期末除息后的标的价格，期权终值分别为 V(u) 与 V(d)。先解出一期末需要交付的标的等价数量 h(T)，再配合到期现金 B(T)，使复制组合在两个状态都等于期权终值。该标的腿今天按预付远期价值计价。

若用实际股票实施并把股息持续再投资，今天的持股 Delta 应按收益率 q 折减，期末再增长为 h(T) 股；若直接把 h(T) 乘以现货价作为今天的成本，就会漏掉 q 的持有收益，并与下一节的风险中性权重不一致。

- **上下状态**

  ```latex
  S_u=uS_0,\qquad S_d=dS_0
  ```

- **期末标的等价数量**

  ```latex
  h_T=\frac{V_u-V_d}{S_u-S_d}
  ```

- **期初实际持股 Delta**

  ```latex
  \Delta_0=e^{-q\Delta t}h_T
  ```

- **现金腿到期额**

  ```latex
  B_T=\frac{S_uV_d-S_dV_u}{S_u-S_d}
  ```

- **与 q 一致的一期价值**

  ```latex
  V_0=h_TS_0e^{-q\Delta t}+B_Te^{-r\Delta t}=\Delta_0S_0+B_Te^{-r\Delta t}
  ```

### 02 / 向后递推

#### 风险中性概率是定价权重，不是市场上涨预测

把复制公式整理后，可以用风险中性概率加权上下状态，再按无风险利率折现。该概率使模型中的标的预期增长与持有收益一致；它由无套利关系确定，不应解读为主观或真实世界的上涨胜率。

多期树从到期节点开始，把每个父节点的下一期价值折现回来。欧式期权只使用继续持有价值；美式期权则在每个节点比较立即行权与继续持有，取较大者，因此可显式表达提前行权边界。

- **含连续收益率的风险中性权重**

  ```latex
  p^*=\frac{e^{(r-q)\Delta t}-d}{u-d}
  ```

- **一期无套利条件**

  ```latex
  d<e^{(r-q)\Delta t}<u
  ```

- **欧式节点递推**

  ```latex
  V=e^{-r\Delta t}\left(p^*V_u+(1-p^*)V_d\right)
  ```

- **美式节点递推**

  ```latex
  V=\max\left(\text{Intrinsic},\ e^{-r\Delta t}\left[p^*V_u+(1-p^*)V_d\right]\right)
  ```

| 输入 | 模型作用 | 需要警惕 |
| --- | --- | --- |
| 步长 | 控制时间离散精度。 | 步数少可能导致价格振荡。 |
| u 与 d | 定义单步价格状态。 | 参数化方法会影响收敛。 |
| 现金流 | 调整节点价格与持有收益。 | 离散股息需落在正确时间点。 |

### 03 / 模型使用

#### 树的答案取决于节点设计与输入质量

使用前先确认标的过程、波动率输入、收益率、利率、股息、期权风格和结算。增加步数时检查价格是否稳定收敛，并用简单欧式情形与另一种成熟模型交叉核对，而不是只相信一次计算。

真实市场可能存在波动率偏斜、跳跃、随机波动率、交易成本和无法连续对冲等现象。二叉树可通过扩展处理部分特征，但节点更多不等于假设自动正确；模型价格应与可成交报价和情景分析并列阅读。

- 第一步：明确树的时间步长、上涨/下跌参数、利率、收益率和现金流。
- 第二步：从到期现金流向后递推，并对美式节点比较行权与继续持有。
- 第三步：做步数收敛、输入扰动和报价差异检查。
- 模型用于组织假设与情景，不提供“理论价必然回归”的交易结论。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> The point of a binomial tree is not to guess whether the next move is up or down. It discretizes future states and finds an underlying-plus-cash portfolio at each node that replicates the next-step cash flows. With continuous yield q, the underlying leg must be measured consistently as a prepaid forward or as actual shares with dividends reinvested.

Derive delta and the risk-neutral probability from a one-period replicating portfolio, then use backward induction to understand multi-step pricing, American exercise, and discrete cash flows.

### 01 / One-Period Replication

#### Use Two Future States To Solve For Delta And The Cash Leg

Let the up and down nodes be ex-dividend underlying prices at the end of one step, with option values V(u) and V(d). First solve for the terminal share-equivalent quantity h(T) and terminal cash B(T) so that the portfolio matches both states. The underlying leg is priced today at its prepaid-forward value.

If replication uses actual shares and continuously reinvests dividends, today's stock delta is reduced for yield q and grows to h(T) shares at the step end. Multiplying h(T) directly by today's spot would omit the q carry and conflict with the next section's risk-neutral weight.

- **Up and down states**

  ```latex
  S_u=uS_0,\qquad S_d=dS_0
  ```

- **Terminal share-equivalent quantity**

  ```latex
  h_T=\frac{V_u-V_d}{S_u-S_d}
  ```

- **Actual stock delta at the step start**

  ```latex
  \Delta_0=e^{-q\Delta t}h_T
  ```

- **Terminal amount of the cash leg**

  ```latex
  B_T=\frac{S_uV_d-S_dV_u}{S_u-S_d}
  ```

- **One-period value consistent with q**

  ```latex
  V_0=h_TS_0e^{-q\Delta t}+B_Te^{-r\Delta t}=\Delta_0S_0+B_Te^{-r\Delta t}
  ```

### 02 / Backward Induction

#### Risk-Neutral Probability Is A Pricing Weight, Not An Up-Move Forecast

Rearranging the replication equations produces a risk-neutral probability that weights the up and down states before risk-free discounting. It aligns expected growth in the model with carry and is fixed by no-arbitrage, not by a subjective or real-world forecast of an up move.

A multi-step tree starts at terminal nodes and discounts each pair of next-step values back to its parent. A European option uses continuation value only; an American option compares immediate exercise with continuation at every node and takes the larger, explicitly representing an early-exercise boundary.

- **Risk-neutral weight with continuous yield**

  ```latex
  p^*=\frac{e^{(r-q)\Delta t}-d}{u-d}
  ```

- **One-step no-arbitrage condition**

  ```latex
  d<e^{(r-q)\Delta t}<u
  ```

- **European node recursion**

  ```latex
  V=e^{-r\Delta t}\left(p^*V_u+(1-p^*)V_d\right)
  ```

- **American node recursion**

  ```latex
  V=\max\left(\text{Intrinsic},\ e^{-r\Delta t}\left[p^*V_u+(1-p^*)V_d\right]\right)
  ```

| Input | Role In The Model | Caution |
| --- | --- | --- |
| Step size | Controls time discretization. | Too few steps can produce oscillation. |
| u and d | Define one-step price states. | Parameterization affects convergence. |
| Cash flows | Adjust node prices and carry. | Discrete dividends must occur at the correct node time. |

### 03 / Model Use

#### A Tree's Answer Depends On Node Design And Input Quality

Before use, confirm the underlying process, volatility input, yield, rates, dividends, exercise style, and settlement. Increase the step count and check for stable convergence, then cross-check a simple European case against another established model instead of trusting one calculation.

Real markets may feature skew, jumps, stochastic volatility, transaction costs, and discontinuous hedging. Trees can be extended to represent some features, but more nodes do not make assumptions automatically correct; model value should be read alongside executable quotes and scenario analysis.

- Step 1: State the time step, up/down parameters, rate, yield, and cash flows.
- Step 2: Work backward from terminal cash flows and compare exercise with continuation at American nodes.
- Step 3: Check step convergence, input perturbations, and differences from market quotes.
- The model organizes assumptions and scenarios; it does not imply that market price must converge to a theoretical value.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

