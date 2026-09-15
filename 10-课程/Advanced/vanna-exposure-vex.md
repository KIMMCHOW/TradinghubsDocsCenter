---
title: "VEX：Vanna Exposure 怎么看"
title_en: "VEX: How To Read Vanna Exposure"
slug: "vanna-exposure-vex"
type: lesson
level: Advanced
order: 78
track: dealer-positioning-and-exposure
track_label: "做市商定位与期权敞口"
reading_time: "14 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/高级"
  - "主题/做市商定位与期权敞口"
  - "权限/需登录"
aliases:
  - "VEX：Vanna Exposure 怎么看"
  - "VEX: How To Read Vanna Exposure"
  - "vanna-exposure-vex"
source_url: "https://tradinghubs.org/docs/trading-knowledge/vanna-exposure-vex"
source_file: "Tradinghub-Web/components/site/options-knowledge/data.ts"
generated: 2026-09-15
---

# VEX：Vanna Exposure 怎么看

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-advanced|高级]] · [[dealer-positioning-and-exposure|做市商定位与期权敞口]]
> 上一课：[[zomma-gamma-volatility-drift|Zomma：Gamma 随波动率的变化]] ｜ 下一课：[[charm-exposure-chex|CHEX：Charm Exposure 怎么看]]

**高级 · 做市商定位与期权敞口 · 14 分钟**

> 有时期货价格还没动，但 IV 已经在动。VEX 把“波动率变化会改变 Delta”这条模型路径单独拆出来；页面符号本身不证明 dealer 库存或之后一定发生对冲。

理解 Vanna 如何描述 Delta 对 IV 变化的敏感度，并用 ODV 预计算 VEX 定位波动率路径的模型敏感区。

### 01 / 定义

#### 先分清 Vanna 概念与页面预计算 VEX

Vanna 衡量 Delta 对隐含波动率变化的敏感度，理论上必须先区分按波动率小数 1.00 还是按 1 个 IV 点缩放。一般 Vanna 暴露与 Vanna、某种仓位度量和合约乘数成比例；ODV 页面则直接展示已包含其模型缩放、符号和聚合的预计算 VEX，不能用 OI 或固定乘数复算。

在本课的产品读法里，正负号、OI 与 Volume 都不能单独证明做市商库存、持仓归属或对冲方向；K / M / B 仅为紧凑显示缩写，不是美元、股数、合约数或每点冲击的经济单位。只可在同一标的、同一指标、同一 DTE 窗口和同一数据快照内比较分布。0DTE、1DTE+ 与 90D Window 均为独立预计算值，90D Window 不等于前两者相加。

- Vanna 的正负会随 Call / Put、价内外程度和模型约定变化，不能默认 Put 一律取相反号。
- K / M / B 只是显示缩写，不声明美元、股数、合约数或每 1 个 IV 点的经济单位。

- **每 1 个 IV 点的 Vanna**

  ```latex
  \mathrm{Vanna}_{1\mathrm{pt}}=0.01\,\frac{\partial\Delta}{\partial\sigma}
  ```

- **一般概念关系，不能复算页面**

  ```latex
  \text{Vanna exposure}\;\propto\;\mathrm{Vanna}\times\text{position measure}\times\text{contract multiplier}
  ```

- **同一视图的相对条宽**

  ```latex
  w_i=\frac{|x_i|}{\max_j|x_j|},\quad \max_j|x_j|>0
  ```

### 02 / IV 路径

#### IV 变化也可能改变对冲需求

价格变化会通过 Gamma 改变 Delta；IV 变化则可以通过 Vanna 改变 Delta。事件前 IV 抬升或事件后 IV crush 与 VEX 热点重合时，只能确认模型敏感路径值得观察；实际标的或期货对冲仍需独立的持仓归属与成交证据。

| 现象 | VEX 含义 | 下一步 |
| --- | --- | --- |
| IV 抬升，VEX 集中 | IV 变化与模型敏感区重合。 | 检查价格、Flow 与成交是否出现独立确认。 |
| IV crush，VEX 高 | 事件后模型 Delta 对 IV 回落较敏感。 | 观察实际价格与成交，不预设对冲方向。 |
| GEX 与 VEX 同区 | 两个指标各自的热点位置重合。 | 只比较位置，不比较跨指标绝对值，也不是交易信号。 |

### 03 / 期货传导

#### VEX 让你看到价格未动时的波动率压力

当期货价格暂时横住，但 IV、Flow 和 VEX 已经发生变化时，期权市场可能比期货主图更早反映风险定价。

- VEX 应和 IV、Flow、GEX 一起看。
- 事件日前后和 IV 快速变化时，优先检查 VEX 热点与实际价格反应是否重合。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> Sometimes futures price has not moved yet, but IV already has. VEX isolates the modeled path through which volatility changes delta; its displayed sign does not establish dealer inventory or guarantee later hedging.

Understand how vanna describes delta sensitivity to IV changes, then use ODV's precomputed VEX to locate modeled sensitivity along the volatility path.

### 01 / Definition

#### Separate Vanna Theory From Precomputed VEX

Vanna measures delta sensitivity to implied volatility, and theory must distinguish a derivative per 1.00 volatility from one scaled per IV point. Conceptually, vanna exposure is proportional to vanna, a position measure, and a contract multiplier. ODV directly displays precomputed VEX with its model scaling, signs, and aggregation already embedded, so OI or a fixed multiplier cannot reproduce it.

In this product reading, signs, OI, and volume do not establish dealer inventory, ownership, or hedge direction. K / M / B are compact display suffixes, not economic units such as dollars, shares, contracts, or a per-point shock. Compare distributions only within the same symbol, metric, DTE window, and snapshot. 0DTE, 1DTE+, and 90D Window are independent precomputed values; 90D Window is not the sum of the first two.

- Vanna sign varies with call-put side, moneyness, and model convention; do not assume puts always take the opposite sign.
- K, M, and B are display suffixes; they do not declare dollars, shares, contracts, or an economic unit per IV point.

- **Vanna per one IV point**

  ```latex
  \mathrm{Vanna}_{1\mathrm{pt}}=0.01\,\frac{\partial\Delta}{\partial\sigma}
  ```

- **General concept; not a page-reproduction formula**

  ```latex
  \text{Vanna exposure}\;\propto\;\mathrm{Vanna}\times\text{position measure}\times\text{contract multiplier}
  ```

- **Relative bar width within one view**

  ```latex
  w_i=\frac{|x_i|}{\max_j|x_j|},\quad \max_j|x_j|>0
  ```

### 02 / IV Path

#### IV Changes Can Also Change Hedge Demand

Price changes alter delta through gamma, while IV changes can alter delta through vanna. When pre-event IV expansion or post-event IV crush overlaps a VEX hotspot, it identifies a modeled sensitivity path worth watching. Actual underlying or futures hedging still requires independent ownership and transaction evidence.

| Observation | VEX Meaning | Next Step |
| --- | --- | --- |
| IV rises, VEX clusters | The IV move overlaps a modeled sensitivity area. | Check price, flow, and participation for independent confirmation. |
| IV crush, high VEX | Modeled delta is sensitive to the post-event IV decline. | Observe actual price and participation without presuming hedge direction. |
| GEX and VEX cluster together | Hotspot locations from the two metrics overlap. | Compare location only, not raw cross-metric magnitude; it is not a trade signal. |

### 03 / Futures Transmission

#### VEX Shows Volatility Pressure Before Price Moves

When futures price is still holding but IV, flow, and VEX are already changing, the options market may be pricing risk before the futures chart shows it.

- Read VEX with IV, flow, and GEX.
- Around events and rapid IV changes, prioritize checking whether VEX hotspots overlap actual price reaction.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

