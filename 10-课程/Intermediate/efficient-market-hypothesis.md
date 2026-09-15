---
title: "有效市场假说（EMH）"
title_en: "Efficient Market Hypothesis (EMH)"
slug: "efficient-market-hypothesis"
type: lesson
level: Intermediate
order: 22
track: markets-macro-and-behavior
track_label: "市场、宏观与行为"
reading_time: "24 分钟"
access: signin
tags:
  - "文档中心"
  - "课程"
  - "等级/中级"
  - "主题/市场、宏观与行为"
  - "权限/需登录"
aliases:
  - "有效市场假说（EMH）"
  - "Efficient Market Hypothesis (EMH)"
  - "efficient-market-hypothesis"
source_url: "https://tradinghubs.org/docs/trading-knowledge/efficient-market-hypothesis"
source_file: "Tradinghub-Web/components/site/options-knowledge/market-theory-data.ts"
generated: 2026-09-15
---

# 有效市场假说（EMH）

> [!info] 导航 / Navigation
> [[文档中心]] · [[level-intermediate|中级]] · [[markets-macro-and-behavior|市场、宏观与行为]]
> 上一课：[[skewness-kurtosis-fat-tails|偏度、峰度与肥尾风险]] ｜ 下一课：[[random-walk-hypothesis|随机游走假说]]

**中级 · 市场、宏观与行为 · 24 分钟**

> EMH 讨论的不是“价格是否永远正确”，而是在给定信息集、资产定价模型与交易成本下，投资者能否系统性地获得异常的风险调整收益。

系统学习有效市场假说的定义、Bachelier–Samuelson–Fama 的思想脉络、弱式／半强式／强式三种形式、超额收益与联合假设问题，以及它对订单流、期权定价与行为金融争论的含义。

### 01 / 概念边界

#### 效率是关于信息集的命题，不是关于价格正确性的判断

有效市场假说（Efficient Market Hypothesis，EMH）主张：资产价格已经反映了某一信息集内的信息。此处的“效率”既不表示价格等于内在价值，也不表示价格不再波动，而是表示在给定信息集下，利用该信息集系统性获取异常风险调整收益的空间被压缩。

因此 EMH 只有在三个要素同时被说明时才可操作：所讨论的信息集是什么、用哪个资产定价模型定义预期收益、以及交易成本与容量约束有多大。缺少任何一项，“市场是否有效”都无法被检验，只能停留在口号层面。

学术传统把信息集由窄到宽分成三种形式：弱式只涉及历史价格与收益，半强式加入全部公开信息，强式再加入私有信息。三种形式是三个强度不同的命题，而不是同一结论的三档置信度；经验研究通常认为弱式与半强式在多数流动市场中相当接近成立，而强式被普遍视为过强。

> [!question] 常见误解：EMH 等于“没有人能从交易中赚钱”
> EMH 并不主张价格永远“正确”。它讨论的是：可用信息能否被系统性地用于获取异常的风险调整收益。个别交易者赚钱、某段时期出现大幅错价、某个策略在若干年内有效，都可以与 EMH 相容；EMH 约束的是在成本、风险与容量之后仍然稳定存在的超额收益。

| 形式 | 已反映的信息 | 主要含义 |
| --- | --- | --- |
| 弱式 | 历史市场数据：价格、历史收益与交易信息 | 历史价格形态不应系统性地产生 alpha。 |
| 半强式 | 全部公开信息：财报、宏观数据、新闻、公司公告 | 公开信息应被迅速纳入价格。 |
| 强式 | 公开信息与私有信息 | 即使私有信息也不应产生持续的异常收益。 |

### 02 / 机制与度量

#### 从随机游走到联合假设：理论如何被系统化

Bachelier（1900）在《Théorie de la spéculation》中首次用随机过程描述投机价格，比现代金融学早了几十年。他的核心洞见是：如果价格已经反映当前预期，后续变动就来自尚未发生的信息，因而在统计上不可预测。这为后来把效率与随机游走联系起来的传统提供了数学起点。

Samuelson（1965）证明了“被正确预期的价格随机波动”：一旦预期被纳入价格，价格变化就由新信息驱动，因此不可预测。这一步把效率从“价格是否准确”重新定位为“价格变化能否被既有信息预测”，并把它与鞅式（martingale-like）行为联系起来。Fama（1965）随后整理了早期关于股价随机游走行为的经验证据。

Fama（1970）是 EMH 的系统化文献：它把有效市场定义为价格充分反映可得信息的市场，把大量检验归入弱式、半强式与强式三种信息集，并认为当时的证据大体支持效率。Fama（1991）重新评估证据时强调了一个方法论点：任何效率检验都同时依赖一个资产定价模型，因此检验结果也受模型设定影响。

Grossman 与 Stiglitz（1980）指出了理论上的张力：如果价格已经完全反映所有信息，那么搜集信息的回报为零，也就没有人有动机去搜集信息。因此完全信息有效的市场在均衡中难以成立，市场更可能停留在“信息有效、但仍有回报补偿信息成本”的状态。这解释了为什么现实中效率与大量专业研究支出会同时存在。

> [!note] 联合假设问题（The Joint Hypothesis Problem）
> 检验效率必须同时使用一个资产定价模型来定义“预期收益”。因此观测到异常收益时至少有两种解释：市场没有把信息充分计入价格，或所选模型错误地设定了风险与预期收益的关系，例如遗漏风险因子或使用了错误的基准。简单例子：某组股票长期跑赢市场模型预测，若它们同时承担了模型未包含的困境风险，那么“异常”可能只是未被正确定价的风险补偿，而不必然是错价。这也是现代研究把异象表述为对某个模型的挑战，而不是对“市场无效”的最终证明的原因。

- **超额收益（Abnormal Return）**

  ```latex
  AR_t=R_t-E(R_t)
  ```
  AR_t 为超额收益，R_t 为实际收益，E(R_t) 为所选资产定价模型给出的预期收益。EMH 的核心问题是 AR_t 能否被系统性地预测与获取。

- **效率的信息集条件**

  ```latex
  E\left(R_{t+1}\mid I_t\right)=E\left(R_{t+1}\right)
  ```
  I_t 为信息集。该式表示：给定 I_t 的条件预期收益不优于无条件预期收益，即信息集对下一期收益没有预测力。

- **联合假设下的市场模型**

  ```latex
  R_t=\alpha+\beta R_{m,t}+\varepsilon_t
  ```
  R_m 为市场组合收益。检验中把 α 视为异常收益：若 α 显著不为零，既可能是市场无效，也可能是该模型遗漏了风险因子。

### 03 / 阅读流程

#### 把“有没有 edge”改写成信息集、成本、风险与容量

Alpha 是经风险调整、扣除成本之后仍然存在的超额收益。EMH 并不否认风险承担的补偿：承担衰退风险、流动性风险或波动率风险的投资者理应获得溢价。EMH 约束的是在同样的风险暴露与成本假设下，是否存在可以重复获取、且无法被风险解释的额外收益。

更准确的问题因此是：哪些信息已经被定价、它以多快速度被纳入价格、以及是什么阻止了套利把剩余 edge 消除？这三个问题分别对应信息集、价格发现速度与套利限制，也正是市场微观结构研究的核心对象。

关于订单流：订单流与弱式效率并不直接冲突，因为两者讨论的信息集不同。弱式效率针对的是历史价格、收益与成交量形态；订单流数据描述的是实时的流动性、主动成交方向、挂单与仓位结构。Glosten 与 Milgrom（1985）一类模型表明，做市商面对知情交易者时必须让价格随订单流调整，因此订单流本身是价格发现机制的一部分，而不是对效率的反例。这类信息是否构成 edge，仍取决于竞争强度、延迟、成本与容量。

关于期权：隐含波动率是把市场对未来波动的预期编码进价格的直接渠道，因此期权价格通常已经包含大量公开信息与仓位信息。Gamma 敞口与做市商对冲描述的是信息如何转化为期货订单流，而不是一个新的定价漏洞。与此同时，波动率风险溢价是一个被广泛记录的实证现象，把它读作风险补偿与结构性供需，通常比读作可以无成本套利的错价更符合证据。

> [!tip] 本课的核心问题
> 哪些信息已经被定价、它以多快速度被纳入价格、以及是什么阻止了套利把剩余 edge 消除？把这三个问题回答清楚，比抽象争论“市场是否有效”更有实际意义。

- 信息优势：掌握其他人尚未获得或尚未处理的信息；其可持续性取决于信息获取成本与法律边界。
- 速度优势：对同一信息更早行动；随着基础设施普及，这类优势衰减最快。
- 分析优势：从同样的公开数据中提取更准确的推断，例如更好的现金流或波动率估计。
- 结构性优势：由制度、授权、资金期限或风险承担能力形成的准入差异，通常最难被复制。
- 行为优势：利用其他参与者在参考点、损失厌恶或注意力上的系统性偏差，同时承担偏差长期不修正的融资风险。
- 执行优势：以更低的价差、冲击与融资成本实现同一想法；在效率较高的市场中，这往往就是决定性的边际。

| 领域 | 与 EMH 的关系 | 关键区分 |
| --- | --- | --- |
| 订单流 | 不构成对弱式效率的反例；它属于更细的信息集。 | 历史价格形态，与实时流动性、主动成交和仓位结构之间的区别。 |
| 期权与波动率 | 隐含波动率已经是定价输入，而不是免费信息。 | 风险补偿（如波动率风险溢价）与可无成本套利错价之间的区别。 |

### 04 / 风险边界

#### 挑战、批评与失效条件

自 Fama（1970）以来，文献记录了大量难以用最简模型解释的现象，通常称为异象（anomalies）：动量、价值效应、盈余公告后漂移、过度波动、泡沫与系统性行为偏差。Jensen（1978）在早期综述中已经指出，这些证据要求更精细地定义“信息”与“效率”，而不是简单推翻效率概念。

行为金融提供了一条解释路径：参考点、损失厌恶、过度自信与有限注意力可能让价格偏离基本价值。但行为解释必须同时回答为什么偏离没有被套利消除。Shleifer 与 Vishny（1997）给出的答案是套利本身有成本与代理约束：套利者面对资金期限、追加保证金风险与资本撤离，因此错误定价可以在套利者无法坚持的期限内继续扩大。

现代金融学的处理方式不是二选一。更常见的表述是：市场可以在高度有效的同时并非完美有效；效率会随市场、时期与信息集变化；套利存在成本与约束；并且部分异象可能是风险溢价而非纯粹错价。Malkiel（2003）在批评综述中指出，随着已知异象被公开，其中一部分随后减弱或消失，这与效率的自我修正相容，但不能证明所有异象都会消失。

> [!question] 常见误解：发现异象就等于证明市场无效
> 异常收益本身无法区分两种解释：市场没有充分定价，或所用资产定价模型遗漏了风险因子。这正是联合假设问题。因此更严谨的表述是“在该模型下存在尚未解释的异常收益”，而不是“市场已被证明无效”。

- 动量：Jegadeesh 与 Titman（1993）报告买入过去赢家、卖出过去输家的策略在其样本内取得了显著收益，直接挑战“历史收益无预测力”的强表述。
- 价值效应：Basu（1977）发现低市盈率股票组合的表现优于高市盈率组合；Fama 与 French（1992）随后表明，此类差异与规模及账面市值比等特征相关。
- 盈余公告后漂移：Bernard 与 Thomas（1990）记录价格对盈利信息的调整并不在公告日一次性完成，而是持续一段时间。
- 过度波动与泡沫：Shiller（1981）指出股价波动幅度难以由后续股息变化解释，这一论证成为“价格可能偏离基本价值”的经典经验依据。
- 限制套利：即使识别出错价，资金期限、风险限额、借券成本与资本撤离都可能使套利无法推进到价格修正。
- 度量与方法争议：异象对样本期、数据挖掘、交易成本与基准模型高度敏感，因此“已记录的异象”与“可交易的错价”必须分开对待。

- 先声明信息集：你使用的是历史价格、公开信息、订单流还是私有研究？不同答案对应不同的效率形式。
- 写出预期收益模型：超额收益的定义依赖一个基准，任何 alpha 声明都必须同时给出该基准。
- 扣除全部成本：手续费、价差、冲击成本、借券成本与融资成本都要进入判断，再检验剩余收益是否仍然显著。
- 评估容量与期限：策略能承载多少资金、需要多长持有期，以及资金能否承受该期限内的回撤。
- 提前写明失效条件：当竞争加剧、市场结构改变或成本上升时 edge 会衰减，因此必须先确定什么证据会让观点失效。

## 相关概念

- [[random-walk-hypothesis|随机游走假说]] — 价格变化不可预测的统计表述；与弱式效率关系最直接，但两者并不等价。
- [[market-efficiency-information-signaling|市场效率、信息不对称与信号]] — 同一主题的应用侧：信号、噪声、贝叶斯更新与事件后的价格接受过程。
- [[price-discovery-market-clearing|价格发现与市场出清]] — 信息进入价格的具体场所：订单簿、边际成交与不断移动的暂时平衡。
- [[market-making-inventory-adverse-selection|做市库存与逆向选择：价差收入不是免费收益]] — 市场微观结构对效率的标准回答：存在知情交易者时，价差必须补偿逆向选择风险。
- [[no-arbitrage-and-synthetics|无套利边界与合成头寸]] — 套利既是效率的执行机制，也是限制套利成本的来源。
- [[anchoring-framing-trading-decisions|锚定、框架与交易决策]] — 行为金融挑战 EMH 的入口：参考点与框架如何制造可重复的定价偏差。
- [[expectations-feedback-path-dependence|预期、反馈与路径依赖]] — 异象与泡沫的动力学解释：自我强化过程如何让错价在短期扩大。
- [[sharpe-ratio|Sharpe Ratio：单位总波动的超额收益]] — 把「异常收益」变成可计算量：必须先定义风险，超额收益才有意义。
- [[realized-vs-implied-volatility|已实现波动率与隐含波动率]] — 波动率风险溢价的观察窗口：价格是否已经反映预期波动。
- [[gamma-exposure-gex|GEX / vGEX：Gamma Exposure 怎么看]] — 讨论结构性对冲流是否构成可持续 edge 的入口，并区分传导机制与方向预测。
- 市场异象（规划中） — 动量、价值与盈余公告后漂移等已记录异象需要独立知识点承接，目前尚未成课。

> [!warning] 风险说明
> 本内容仅用于学习金融市场、风险管理与衍生品机制，不构成投资、交易、税务或法律建议。模型、指标与历史样本都可能失效；采取任何行动前，请核对当前合约规则、数据口径、成本与自身风险承受能力。

---

## English

> EMH does not ask whether prices are always correct. It asks whether investors can systematically earn abnormal risk-adjusted returns from a stated information set once risk and cost are accounted for.

Study the definition of the efficient market hypothesis, the Bachelier–Samuelson–Fama lineage, the weak, semi-strong and strong forms, abnormal return and the joint hypothesis problem, and what the hypothesis implies for order flow, options, and the behavioral-finance debate.

### 01 / Concept Boundary

#### Efficiency Is A Statement About An Information Set, Not About Price Correctness

The efficient market hypothesis (EMH) asserts that asset prices already reflect the information in a stated information set. Efficiency here does not mean the price equals intrinsic value, and it does not mean prices stop moving. It means the room to earn abnormal risk-adjusted returns systematically from that information set is compressed.

EMH therefore becomes operational only when three elements are stated together: which information set is meant, which asset-pricing model defines expected return, and how large the trading-cost and capacity constraints are. Without all three, "is the market efficient" cannot be tested and remains a slogan.

The academic tradition orders information sets from narrow to wide: weak form covers historical prices and returns, semi-strong form adds all public information, and strong form adds private information. These are three propositions of different strength, not three confidence levels of one conclusion. Empirical work generally places weak and semi-strong efficiency close to holding in liquid markets, while strong form is widely regarded as too strong.

> [!question] Common Misconception: EMH Means Nobody Can Make Money Trading
> EMH does not claim that prices are always "correct." It concerns whether available information can be systematically exploited to earn abnormal risk-adjusted returns. Individual traders making money, large mispricing in some periods, or a strategy working for years can all be compatible with EMH; what EMH constrains is an excess return that persists after cost, risk, and capacity.

| Form | Information Reflected | Main Implication |
| --- | --- | --- |
| Weak | Historical market data: prices, historical returns, and trading information | Historical price patterns should not systematically generate alpha. |
| Semi-strong | All public information: financial statements, macroeconomic data, news, and corporate announcements | Public information should be rapidly incorporated into prices. |
| Strong | Public and private information | Even private information should not generate persistent abnormal returns. |

### 02 / Mechanics And Measurement

#### From The Random Walk To The Joint Hypothesis: How The Theory Was Systematized

Bachelier (1900), in Théorie de la spéculation, described speculative prices with a random process decades before modern finance. His central insight was that if a price already reflects current expectations, later changes come from information that has not yet arrived and are therefore statistically unpredictable. That gave the later efficiency tradition its mathematical starting point.

Samuelson (1965) proved that properly anticipated prices fluctuate randomly: once expectations are embedded in price, price changes are driven by new information and are therefore unpredictable. That reframed efficiency away from price accuracy and toward the predictability of price changes, and linked it to martingale-like behaviour. Fama (1965) then organized the early empirical evidence on the random-walk behaviour of stock prices.

Fama (1970) is the systematizing paper for EMH: it defined an efficient market as one in which prices fully reflect available information, grouped a large body of tests into the weak, semi-strong, and strong information sets, and read the evidence of the time as broadly supportive. Fama (1991) reassessed that evidence and stressed a methodological point: every efficiency test also relies on an asset-pricing model, so the result depends on the model specification as well.

Grossman and Stiglitz (1980) identified the theoretical tension: if prices already reflected all information, the return to gathering information would be zero and nobody would have an incentive to gather it. A fully informationally efficient market is therefore difficult to sustain in equilibrium; markets more plausibly settle into a state that is informationally efficient while still paying a return that compensates information cost. That is why real markets show efficiency and heavy professional research spending at the same time.

> [!note] The Joint Hypothesis Problem
> Testing efficiency requires an asset-pricing model to define expected return. Observing abnormal return therefore has at least two explanations: the market failed to incorporate information, or the chosen model mis-specified the relationship between risk and expected return, for example by omitting a risk factor or using the wrong benchmark. A simple example: if a group of stocks beats a market-model prediction for years while carrying distress risk the model omits, the "anomaly" may be compensation for unpriced risk rather than mispricing. This is why modern work treats anomalies as challenges to a specific model rather than as final proof that markets are inefficient.

- **Abnormal return**

  ```latex
  AR_t=R_t-E(R_t)
  ```
  AR_t is the abnormal return, R_t the realised return, and E(R_t) the expected return under the selected asset-pricing model. The central question of EMH is whether AR_t can be systematically predicted and captured.

- **Efficiency condition on an information set**

  ```latex
  E\left(R_{t+1}\mid I_t\right)=E\left(R_{t+1}\right)
  ```
  I_t is the information set. The expression states that the expected return conditional on I_t is no better than the unconditional expectation, so the information set has no forecasting power for the next period.

- **Market model under the joint hypothesis**

  ```latex
  R_t=\alpha+\beta R_{m,t}+\varepsilon_t
  ```
  R_m is the market-portfolio return. In tests, α is read as the abnormal return: a significant non-zero α may indicate inefficiency, or it may indicate that the model omits a relevant risk factor.

### 03 / Reading Workflow

#### Rewrite Whether An Edge Exists As Information Set, Cost, Risk, And Capacity

Alpha is the excess return that survives after risk adjustment and cost. EMH does not deny compensation for risk bearing: investors who carry recession risk, liquidity risk, or volatility risk should be paid a premium. What EMH constrains is whether an extra, repeatable return that risk cannot explain exists under the same exposure and cost assumptions.

The sharper question is therefore: what information is already priced in, how quickly is it incorporated, and what prevents arbitrage from eliminating the remaining edge? Those three questions map onto the information set, the speed of price discovery, and limits to arbitrage, which is precisely what market-microstructure research studies.

On order flow: order flow does not directly contradict weak-form efficiency, because the two describe different information sets. Weak-form efficiency concerns historical prices, returns, and volume patterns, while order-flow data describes real-time liquidity, aggressive trade direction, resting orders, and positioning. Models in the Glosten and Milgrom (1985) tradition show that a market maker facing informed traders must let price move with order flow, so order flow is part of the price-discovery mechanism rather than a counterexample to efficiency. Whether such information constitutes an edge still depends on competition, latency, cost, and capacity.

On options: implied volatility is the direct channel through which the market's expectation of future volatility is encoded in price, so option prices normally already contain substantial public and positioning information. Gamma exposure and dealer hedging describe how that information becomes futures order flow rather than a new pricing loophole. At the same time, the volatility risk premium is a widely documented empirical phenomenon, and reading it as risk compensation plus structural supply-demand is usually better supported than reading it as costlessly arbitrageable mispricing.

> [!tip] The Central Question Of This Lesson
> What information is already priced in, how quickly is it incorporated, and what prevents arbitrage from eliminating the remaining edge? Answering those three questions is more useful than arguing in the abstract about whether markets are efficient.

- Information advantage: holding information others have not obtained or processed; durability depends on acquisition cost and legal boundaries.
- Speed advantage: acting on the same information earlier; this decays fastest as infrastructure spreads.
- Analytical advantage: extracting a better inference from the same public data, for example a better cash-flow or volatility estimate.
- Structural advantage: access created by mandate, regulation, funding horizon, or risk-bearing capacity, which is usually hardest to replicate.
- Behavioral advantage: exploiting systematic bias in other participants' reference points, loss aversion, or attention, while bearing the funding risk that the bias persists.
- Execution advantage: implementing the same idea with lower spread, impact, and funding cost; in relatively efficient markets this is often the decisive margin.

| Area | Relationship To EMH | Key Distinction |
| --- | --- | --- |
| Order flow | Not a counterexample to weak-form efficiency; it is a finer information set. | Historical price patterns versus real-time liquidity, aggressive trading, and positioning. |
| Options and volatility | Implied volatility is already a pricing input, not free information. | Risk compensation such as the volatility risk premium versus costlessly arbitrageable mispricing. |

### 04 / Risk Boundary

#### Challenges, Criticism, And Failure Conditions

Since Fama (1970), the literature has documented many patterns that the simplest models do not explain, usually called anomalies: momentum, the value effect, post-earnings-announcement drift, excess volatility, bubbles, and systematic behavioral bias. Jensen (1978), in an early survey, already argued that such evidence demands more careful definitions of information and efficiency rather than a simple rejection of the concept.

Behavioral finance offers one explanatory path: reference points, loss aversion, overconfidence, and limited attention can push price away from fundamental value. A behavioral explanation must also answer why the deviation is not arbitraged away. Shleifer and Vishny (1997) answered that arbitrage itself carries costs and agency constraints: arbitrageurs face funding horizons, margin risk, and capital withdrawal, so mispricing can keep widening beyond the horizon an arbitrageur can survive.

Modern finance does not treat this as a binary. The more common formulation is that markets can be highly efficient without being perfectly efficient; efficiency can vary across markets, periods, and information sets; arbitrage has costs and constraints; and some anomalies may represent risk premia rather than pure mispricing. Malkiel (2003), reviewing the critics, noted that some documented anomalies weakened or disappeared after becoming public, which is consistent with self-correction but does not prove that every anomaly will vanish.

> [!question] Common Misconception: An Anomaly Proves Inefficiency
> Abnormal return alone cannot distinguish two explanations: the market mispriced the information, or the asset-pricing model omitted a relevant risk factor. That is the joint hypothesis problem. The more careful statement is therefore that an unexplained abnormal return exists under this model, not that the market has been proven inefficient.

- Momentum: Jegadeesh and Titman (1993) reported significant returns to buying past winners and selling past losers within their sample, challenging a strong reading that historical returns have no predictive power.
- Value effect: Basu (1977) found that low price-earnings portfolios outperformed high price-earnings portfolios, and Fama and French (1992) later showed such differences relate to characteristics such as size and book-to-market.
- Post-earnings-announcement drift: Bernard and Thomas (1990) documented that price adjustment to earnings information is not completed on the announcement day but continues for a period.
- Excess volatility and bubbles: Shiller (1981) argued that stock-price volatility is difficult to justify by subsequent dividend changes, a classic empirical argument that price can depart from fundamental value.
- Limits to arbitrage: even when mispricing is identified, funding horizon, risk limits, borrow cost, and capital withdrawal can prevent arbitrage from being carried to the point of correction.
- Measurement and methodology debate: anomalies are highly sensitive to sample period, data mining, trading costs, and the benchmark model, so a documented anomaly must be kept separate from a tradable mispricing.

- State the information set first: historical prices, public information, order flow, or proprietary research? Each maps to a different form of efficiency.
- Write down the expected-return model: abnormal return depends on a benchmark, so every alpha claim must name it.
- Deduct total cost: fees, spread, market impact, borrow cost, and funding cost all belong in the judgement before asking whether the residual return is still significant.
- Assess capacity and horizon: how much capital the strategy can absorb, how long it must be held, and whether the funding can survive the drawdown inside that horizon.
- Record the failure condition in advance: edge decays as competition, structure, or cost changes, so decide beforehand what evidence would falsify the view.

## Related Concepts

- [[random-walk-hypothesis|Random Walk Hypothesis]] — The statistical statement that price changes are unpredictable; closest to weak-form efficiency without being identical to it.
- [[market-efficiency-information-signaling|Market Efficiency, Information Asymmetry, And Signals]] — The applied half of the same subject: signals, noise, Bayesian updating, and post-event acceptance.
- [[price-discovery-market-clearing|Price Discovery And Market Clearing]] — Where information actually enters price: the order book, marginal trades, and a shifting temporary balance.
- [[market-making-inventory-adverse-selection|Market-Making Inventory And Adverse Selection: Spread Capture Is Not Free Return]] — The standard microstructure answer on efficiency: with informed traders, the spread must compensate adverse selection.
- [[no-arbitrage-and-synthetics|No-Arbitrage Bounds And Synthetic Positions]] — Arbitrage is both the enforcement mechanism of efficiency and the source of the costs that limit it.
- [[anchoring-framing-trading-decisions|Anchoring, Framing, And Trading Decisions]] — The entry point of the behavioral challenge to EMH: how reference points and framing create repeatable pricing bias.
- [[expectations-feedback-path-dependence|Expectations, Feedback, And Path Dependence]] — A dynamic reading of anomalies and bubbles: how self-reinforcing processes widen mispricing in the short run.
- [[sharpe-ratio|Sharpe Ratio: Excess Return Per Unit Of Total Volatility]] — Turns abnormal return into a measurable quantity: risk must be defined before excess return means anything.
- [[realized-vs-implied-volatility|Realized Versus Implied Volatility]] — The observation window for the volatility risk premium: whether price already reflects expected volatility.
- [[gamma-exposure-gex|GEX / vGEX: How To Read Gamma Exposure]] — The entry point for asking whether structural hedging flow is a durable edge, and for separating transmission from direction.
- Market Anomalies (planned) — Documented anomalies such as momentum, value, and post-earnings drift need a dedicated knowledge point that has not been written yet.

> [!warning] Risk disclosure
> This content is for learning about financial markets, risk management, and derivatives mechanics only. It is not investment, trading, tax, or legal advice. Models, indicators, and historical samples can fail; verify current contract rules, data conventions, costs, and your own risk capacity before taking action.

## References

- bachelier-1900-theorie-speculation
- samuelson-1965-anticipated-prices
- fama-1965-random-walks
- fama-1970-efficient-capital-markets
- fama-1991-efficient-capital-markets-ii
- grossman-stiglitz-1980-informationally-efficient-markets
- shiller-1981-excess-volatility
- basu-1977-price-earnings-ratios
- fama-french-1992-cross-section
- bernard-thomas-1990-earnings-drift
- jegadeesh-titman-1993-momentum
- shleifer-vishny-1997-limits-of-arbitrage
- jensen-1978-anomalous-evidence
- malkiel-2003-efficient-market-hypothesis-critics
- nobel-2013-asset-price-predictability
