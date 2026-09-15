---
title: "已实现波动率与隐含波动率"
title_en: "Realized Versus Implied Volatility"
slug: "realized-vs-implied-volatility"
type: lesson
level: Intermediate
order: 41
track: greeks-and-sensitivities
track_label: "Greeks 与敏感度"
reading_time: "19 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/Greeks 与敏感度"
  - "权限/需登录"
aliases:
  - "已实现波动率与隐含波动率"
  - "Realized Versus Implied Volatility"
  - "realized-vs-implied-volatility"
source_url: "https://tradinghubs.org/docs/trading-knowledge/realized-vs-implied-volatility"
source_file: "Tradinghub-Web/components/site/options-knowledge/supplemental-data.ts"
generated: 2026-09-15
---

# 已实现波动率与隐含波动率

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[greeks-and-sensitivities|Greeks 与敏感度]]
> 上一课：[[rho-rate-sensitivity|Rho：利率敏感度为什么通常排在最后]] ｜ 下一课：[[implied-volatility-surface|隐含波动率 IV 与波动率曲面]]

**中级 · Greeks 与敏感度 · 19 分钟**

> “实际波动了多少”和“期权价格隐含多少”回答的是不同问题。只有统一收益口径、年化方式、期限和事件范围，两者的差值才开始具有解释意义。

区分向后统计的已实现波动率与从期权价格反推的隐含波动率，并用总方差、期限与事件窗口避免把两个不同量直接比较。

### 01 / 向后测量

#### 已实现波动率依赖样本，不是标的的永久属性

常见做法是先计算连续复利收益，再取样本标准差并按一年中的观察期数量年化。日线、小时线或盘中采样会捕捉不同风险；是否包含隔夜、节假日和跳空也会显著改变结果。

滚动窗口越短，指标对近期冲击越敏感但噪声更高；窗口越长，数值更平滑但可能混合多个市场状态。因此报告一个已实现波动率时，应同时报告样本区间、采样频率、年化因子和是否去均值。

- **对数收益**

  ```latex
  r_t=\ln\left(\frac{S_t}{S_{t-1}}\right)
  ```

- **样本已实现波动率**

  ```latex
  \widehat{\sigma}_{\mathrm{RV}}=\sqrt{A}\sqrt{\frac{1}{n-1}\sum_{t=1}^{n}(r_t-\bar r)^2}
  ```

| 选择 | 更敏感于 | 主要盲点 |
| --- | --- | --- |
| 短窗口 | 最新冲击与状态切换。 | 估计噪声和单次跳跃。 |
| 长窗口 | 长期平均活动水平。 | 对新状态反应较慢。 |
| 盘中采样 | 交易时段内路径。 | 隔夜与闭市跳空。 |

### 02 / 向前报价

#### 隐含波动率是模型反解的价格坐标，不是确定预测

隐含波动率是把市场期权价格代入定价模型后反推出的波动率参数。不同执行价、到期日、利率、股息假设和可成交价格会得到不同结果，所以市场不存在一条适用于所有合约的唯一 IV。

跨期限比较时，波动率百分比本身并不直接可加；总方差更适合表示某一到期前累计的不确定性。事件前后期限之间的总方差差值可用于观察某个窗口贡献了多少定价，但它仍混合风险溢价、供需与模型误差。

- IV 上升可能来自期权价格上涨，也可能来自标的、利率或股息输入变化。
- 某一执行价的 IV 不能代表整张波动率曲面。
- 隐含波动率包含市场定价，不等于未来已实现波动率的无偏承诺。

- **总方差**

  ```latex
  w(T)=\sigma_{\mathrm{imp}}(T)^2T
  ```

- **区间隐含方差的简化分解**

  ```latex
  \sigma_{T_1,T_2}^{2}=\frac{w(T_2)-w(T_1)}{T_2-T_1}
  ```

### 03 / 对比流程

#### 先统一期限与口径，再解释 IV 减 RV

比较时先选定同一未来期限，再为历史 RV 选择与该期限相称的窗口和采样频率；随后读取同一到期的 ATM、偏斜和期限结构，而不是只取一个屏幕数字。事件日、周末和闭市时段要单独标记。

IV 高于近期 RV 可能反映未来事件、尾部保险需求或波动风险溢价，也可能只是历史窗口过于平静。IV 低于 RV 也不自动代表期权便宜，因为高 RV 可能来自已过去且不会重复的跳跃。

- 第一步：记录 RV 的窗口、采样频率、年化因子与隔夜处理。
- 第二步：读取匹配到期的 ATM IV、Skew、Term Structure 与总方差。
- 第三步：把事件、风险溢价、供需与模型假设列为竞争解释，而不是只选一个故事。
- IV 与 RV 的差值是研究输入，不是独立的开仓或平仓信号。

## 相关概念

- [[vega-iv-sensitivity|Vega：IV 敏感度与波动率重定价]] — 隐含波动率的变化通过 Vega 转化为持仓损益。
- [[volatility-forecasting|波动率预测：从实现方差到样本外条件预测]] — 比较隐含与已实现波动率本质上是在比较市场预期与预测模型。
- [[dte-window-selection|DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选]] — 已实现波动率的计算窗口必须与所比较的期限一致。
- [[efficient-market-hypothesis|有效市场假说（EMH）]] — 波动率风险溢价是风险补偿还是错价，需要按效率框架判断。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> How much the market moved and how much volatility option prices imply answer different questions. Their difference becomes interpretable only after return convention, annualization, horizon, and event window are aligned.

Distinguish backward-looking realized volatility from implied volatility backed out of option prices, and use total variance, horizon, and event windows to avoid comparing unlike quantities.

### 01 / Backward Measurement

#### Realized Volatility Depends On The Sample; It Is Not A Permanent Asset Property

A common method computes log returns, takes their sample standard deviation, and annualizes by the number of observations in a year. Daily, hourly, and intraday samples capture different risks; including overnight periods, holidays, and gaps can materially change the result.

A shorter rolling window reacts faster to recent shocks but is noisier; a longer window is smoother but may mix several regimes. A realized-volatility figure should therefore disclose sample range, sampling frequency, annualization factor, and whether returns were demeaned.

- **Log return**

  ```latex
  r_t=\ln\left(\frac{S_t}{S_{t-1}}\right)
  ```

- **Sample realized volatility**

  ```latex
  \widehat{\sigma}_{\mathrm{RV}}=\sqrt{A}\sqrt{\frac{1}{n-1}\sum_{t=1}^{n}(r_t-\bar r)^2}
  ```

| Choice | More Sensitive To | Main Blind Spot |
| --- | --- | --- |
| Short window | Recent shocks and regime changes. | Estimation noise and one-off jumps. |
| Long window | Long-run average activity. | Slow response to a new regime. |
| Intraday sampling | The path during trading hours. | Overnight and closed-market gaps. |

### 02 / Forward-Looking Quote

#### Implied Volatility Is A Model-Inverted Price Coordinate, Not A Certain Forecast

Implied volatility is the volatility parameter backed out by placing a market option price into a pricing model. Different strikes, expiries, rate and dividend assumptions, and executable prices produce different results, so there is no single IV that applies to every contract.

Across expiries, volatility percentages are not directly additive; total variance is a more suitable measure of accumulated uncertainty to a horizon. Differences in total variance around an event window can indicate how much pricing sits in that interval, but still mix risk premium, supply and demand, and model error.

- An IV increase may come from higher option prices or from changes in spot, rate, or dividend inputs.
- IV at one strike cannot represent the whole volatility surface.
- Implied volatility embeds market pricing and is not an unbiased promise of future realized volatility.

- **Total variance**

  ```latex
  w(T)=\sigma_{\mathrm{imp}}(T)^2T
  ```

- **Simplified forward-variance decomposition**

  ```latex
  \sigma_{T_1,T_2}^{2}=\frac{w(T_2)-w(T_1)}{T_2-T_1}
  ```

### 03 / Comparison Workflow

#### Align Horizon And Convention Before Interpreting IV Minus RV

Choose a common forward horizon, then select a historical RV window and sampling frequency appropriate to that horizon. Read ATM volatility, skew, and term structure for the matching expiry rather than one screen number. Mark event dates, weekends, and closed-market periods separately.

IV above recent RV may reflect future events, demand for tail insurance, or a volatility risk premium, but it may also mean the historical window was unusually calm. IV below RV does not automatically mean options are cheap because high RV may come from a past jump that will not repeat.

- Step 1: Record the RV window, sampling frequency, annualization factor, and overnight treatment.
- Step 2: Read matching-expiry ATM IV, skew, term structure, and total variance.
- Step 3: Treat events, risk premium, supply and demand, and model assumptions as competing explanations rather than choosing one story.
- The IV-RV gap is a research input, not a standalone entry or exit signal.

## Related Concepts

- [[vega-iv-sensitivity|Vega: IV Sensitivity And Volatility Repricing]] — Changes in implied volatility become position P&L through vega.
- [[volatility-forecasting|Volatility Forecasting: From Realized Variance To Out-Of-Sample Conditional Forecasts]] — Comparing implied with realized volatility compares market expectations with a forecasting model.
- [[dte-window-selection|DTE Windows: How To Choose 0DTE, 1DTE+, And 90D Window]] — The realized-volatility measurement window must match the horizon being compared.
- [[efficient-market-hypothesis|Efficient Market Hypothesis (EMH)]] — Whether the volatility risk premium is compensation or mispricing needs an efficiency frame.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

