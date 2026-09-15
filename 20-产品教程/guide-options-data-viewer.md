---
title: "Options Data Viewer"
title_en: "Options Data Viewer"
type: document
access: signin
tags:
  - "文档中心"
  - "权限/需登录"
aliases:
  - "Options Data Viewer"
  - "guide-options-data-viewer"
source_url: "https://tradinghubs.org/docs/products/options-data-viewer"
source_files:
  - "Tradinghub-Web/app/docs/products/options-data-viewer/page.tsx"
  - "Tradinghub-Web/components/site/OptionsDataViewerGuideClient.tsx"
generated: 2026-09-15
extraction: mechanical
---

# Options Data Viewer

> [!info] 导航 / Navigation
> [[文档中心]]

**需登录 / Sign-in required**

> Use Data Dashboard and Greeks Profile in a repeatable workflow with linked standalone knowledge lessons.

## Options Data Viewer 产品教程

先用 Data Dashboard 建立整体判断，再用 Greeks Profile 定位具体行权价和到期窗口。本教程讲产品操作路径，独立知识点继续在对应课程中学习。

打开数据看板

查看知识课程

使用边界

本页不构成投资建议、交易建议或收益承诺。期货、期权、ETF、股票和指数交易都可能产生亏损。

## 先学独立知识点

每个核心概念都应单独理解，再回到产品界面组合使用。

### 先学独立知识点

- **做市商对冲** — Delta 中性与 Gamma 再平衡 — 为什么期权成交可能变成标的、ETF 或期货上的对冲流
- **OI** — 期权仓位账本 — 哪里有大量尚未平掉的期权仓位
- **GEX / vGEX** — Gamma Exposure 与成交量加权读法 — 存量 Gamma 结构在哪里，当天成交是否正在改变它
- **DEX** — Delta Exposure — 方向暴露集中在哪些区域
- **VEX** — Vanna Exposure — IV 变化可能在哪里触发 Delta 再平衡
- **CHEX** — Charm Exposure — 时间衰减可能在哪里触发 Delta 再平衡
- **Flow** — 真实期权成交方向 — 当天真实成交正在偏向哪一侧
- **Volume** — 期权参与强度 — 当天是否真的有足够参与度
- **IV** — 隐含波动率与波动率曲面 — 市场是否已经为未来波动、事件或方向压力付费
- **DTE** — 0DTE、Next DTE 与 90 Days — 当前读法属于日内、隔夜还是中期结构
- **Aggregate Data** — 总量结构 — 整体环境更偏吸收、冲击还是重新定价
- **组合读法** — 趋势延续、吸附与波动放大 — 多个指标组合后更接近哪种盘面状态
- **10 分钟流程** — 固定顺序读盘 — 如何按固定顺序完成一次 ODV 读盘

## 两个核心视图

### 核心视图

- **Data Dashboard** — 汇总关键价位、GEX/OI、Flow、Volume、IV 和盘中状态 — 判断当前期货盘面背后的期权结构更像吸附、冲击还是波动放大
- **Greeks Profile** — 按行权价和 DTE 窗口拆分 OI、GEX、DEX、VEX、CHEX — 定位具体哪些价位和到期窗口附近有风险集中

### Data Dashboard 读取顺序

- 确认 ticker、期货价格或参考标的价格，以及数据更新时间。
- 查看 Key Levels，先标出当前价格上下方最近的结构价位。
- 查看 OI，确认哪些行权价是仓位账本的重心。
- 查看 GEX / vGEX，判断环境更偏吸收还是放大波动，以及当天成交是否正在改变结构。
- 查看 Flow 和 Volume，确认真实成交是否正在强化或冲击结构。
- 查看 IV，判断期权市场是否已经提前定价风险。
- 切到 Greeks Profile，检查多种 Greeks 是否集中在同一区域。

### Greeks Profile 读取顺序

- 先看 OI，确认行权价附近是否有足够仓位基础。
- 再看 GEX，判断该区域是否对价格变化敏感。
- 再看 DEX，确认方向暴露是否也集中在同一区域。
- 在 0DTE 或临近到期窗口，再看 VEX / CHEX，观察 IV 变化或时间衰减是否可能触发新的 Delta 再平衡。
- 最后回到期货主图，观察价格在这些区域附近是吸收、停顿、穿越还是加速。

## 三种常见使用场景

### 常见使用场景

- **价格接近大仓位区** — 先看 OI 和 Key Levels — 再确认 GEX / DEX 是否同区集中，Flow 是否放大
- **突破前后波动变快** — 先看 Total Net GEX、vGEX 和 Zero Gamma — 再确认是否进入负 GEX 或高敏感区域，以及当天成交是否同向
- **事件日前后** — 先看 IV、VEX 和 Flow — 再确认 IV 是否提前定价，Greeks Profile 是否出现集中风险

## 风险边界

### 使用边界

- 不要把 GEX 当成方向预测。
- 不要把 OI 当成支撑阻力本身。
- 不要把 DEX 当成直接开仓指令。
- 不要只看 Data Dashboard，而不回到 Greeks Profile 验证具体行权价。
- 不要只看期权结构，忽略期货成交、盘口、宏观事件和自己的风控。

Options Data Viewer 是期货交易系统里的期权结构层。最终交易决策仍要回到你的策略、执行和风险控制。

## 相关课程

- [[market-maker-flow|做市商对冲：Delta 中性与 Gamma 再平衡]]
- [[open-interest-oi|OI 未平仓量：期权仓位账本]]
- [[gamma-exposure-gex|GEX / vGEX：Gamma Exposure 怎么看]]
- [[delta-exposure-dex|DEX：Delta Exposure 怎么看]]
- [[vanna-exposure-vex|VEX：Vanna Exposure 怎么看]]
- [[charm-exposure-chex|CHEX：Charm Exposure 怎么看]]
- [[options-flow-direction|Flow：期权成交分类怎么读]]
- [[options-volume-participation|Volume：期权参与强度怎么读]]
- [[implied-volatility-surface|隐含波动率 IV 与波动率曲面]]
- [[dte-window-selection|DTE 窗口：0DTE、1DTE+ 与 90D Window 怎么选]]
- [[aggregate-options-data|Aggregate Data：总量结构怎么读]]
- [[combined-odv-reads|组合读法：趋势延续、吸附与波动放大]]
- [[odv-10-minute-reading-routine|ODV 10 分钟读盘流程]]

> [!note] 生成方式
> 本笔记由 `app/docs/products/options-data-viewer/page.tsx`, `components/site/OptionsDataViewerGuideClient.tsx` 机械提取生成（页面为 React 渲染，非 Markdown 源）；权威版本以站点页面为准：https://tradinghubs.org/docs/products/options-data-viewer

---

## English

## Options Data Viewer Product Guide

Build the overall picture in Data Dashboard, then use Greeks Profile to locate exact strikes and expiry windows. This guide covers the product workflow while standalone concepts remain in their dedicated lessons.

Open dashboard

Browse knowledge lessons

Usage boundary

This page is not investment advice, trading advice, or a promise of results. Futures, options, ETFs, stocks, and indexes can lose money.

## Learn each concept separately first

Understand each core concept separately, then combine them on the product screens.

### Concepts To Learn First

- **Market-maker hedging** — Delta neutrality and gamma rebalancing — Why options trading can become hedge flow in the underlying, ETF, or futures
- **OI** — The options position ledger — Where large standing option positions exist
- **GEX / vGEX** — Gamma exposure and its volume-weighted read — Where standing gamma sits and whether current-session volume is changing it
- **DEX** — Delta exposure — Where directional exposure is concentrated
- **VEX** — Vanna exposure — Where IV changes may trigger delta rebalancing
- **CHEX** — Charm exposure — Where time decay may trigger delta rebalancing
- **Flow** — Real options trading direction — Which side current-session trading is leaning toward
- **Volume** — Options participation strength — Whether current-session participation is strong enough to matter
- **IV** — Implied volatility and the volatility surface — Whether the options market has already priced future volatility, events, or directional stress
- **DTE** — 0DTE, next DTE, and 90 days — Whether the read belongs to intraday, overnight, or medium-term structure
- **Aggregate Data** — Total structure — Whether the environment leans toward absorption, pressure, or repricing
- **Combined reads** — Trend continuation, pinning, and volatility expansion — Which market state multiple metrics point to together
- **10-minute routine** — A fixed-order reading routine — How to complete one ODV read in a repeatable order

## Two core views

### Core Views

- **Data Dashboard** — Summarizes key levels, GEX/OI, flow, volume, IV, and intraday state — Judge whether the options structure is more likely to pin, pressure, or amplify current futures movement
- **Greeks Profile** — Breaks OI, GEX, DEX, VEX, and CHEX down by strike and DTE window — Locate the exact strikes and expiry windows carrying concentrated risk

### Data Dashboard Reading Order

- Confirm ticker, futures price or reference price, and data freshness.
- Read Key Levels and mark the nearest structural levels above and below current price.
- Read OI to locate the position-ledger center of gravity.
- Read GEX / vGEX to judge whether the environment absorbs or amplifies volatility and whether current-session trading is changing the structure.
- Read Flow and Volume to check whether live trading is reinforcing or attacking the structure.
- Read IV to judge whether the options market has already priced risk.
- Move to Greeks Profile and check whether several Greeks cluster in the same area.

### Greeks Profile Reading Order

- Start with OI to confirm whether a strike has enough standing positioning.
- Read GEX to judge whether that area is sensitive to price movement.
- Read DEX to confirm whether directional exposure also clusters there.
- In 0DTE or near-expiry windows, read VEX / CHEX for delta rebalancing that may follow IV changes or time decay.
- Return to the futures chart and watch whether price absorbs, pauses, breaks, or accelerates near those areas.

## Three common use cases

### Common Use Cases

- **Price approaches a large-position area** — Read OI and Key Levels first — Then confirm whether GEX / DEX cluster nearby and flow expands
- **Volatility speeds up around a break** — Read Total Net GEX, vGEX, and Zero Gamma first — Then confirm negative GEX or high-sensitivity conditions and whether current-session trading aligns
- **Event-day or pre-event trading** — Read IV, VEX, and Flow first — Then confirm whether IV priced risk early and Greeks Profile shows concentrated exposure

## Risk boundaries

### Usage Boundaries

- Do not treat GEX as a directional forecast.
- Do not treat OI as support or resistance by itself.
- Do not treat DEX as a direct entry instruction.
- Do not read only Data Dashboard without confirming exact strikes in Greeks Profile.
- Do not read options structure while ignoring futures prints, order-book behavior, macro events, and your own risk controls.

Options Data Viewer is the options-structure layer in a futures trading system. Final decisions still belong to your strategy, execution, and risk control.

