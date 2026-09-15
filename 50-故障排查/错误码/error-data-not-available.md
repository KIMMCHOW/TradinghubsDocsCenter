---
title: "当前品种没有可用数据"
title_en: "DATA_NOT_AVAILABLE"
type: error-code
code: "DATA_NOT_AVAILABLE"
access: public
tags:
  - "文档中心"
  - "故障排查"
  - "错误码"
  - "权限/公开"
aliases:
  - "DATA_NOT_AVAILABLE"
  - "当前品种没有可用数据"
  - "data-not-available"
source_url: "https://tradinghubs.org/docs/troubleshooting/options-level-pro/data-not-available"
generated: 2026-09-15
---

# 当前品种没有可用数据

> [!info] 导航 / Navigation
> [[文档中心]] · [[setup-options-level-pro|Options Level Pro 安装激活]]

**错误码 DATA_NOT_AVAILABLE**

错误码：`DATA_NOT_AVAILABLE`

当前图表品种可能不在插件支持列表中，或者当前交易日的数据尚未生成。

## 处理步骤

1. 检查当前合约对应的基础品种。
2. 确认图表品种是否在支持范围内：静态线支持 ES、MES、NQ、MNQ、RTY、M2K、GC、MGC；动态热图支持 ES、MES、NQ、MNQ、RTY、M2K、YM、MYM、GC、MGC、SI、SIL、CL、MCL。
3. 检查当前数据更新时间。
4. 数据更新后重新加载指标。

## 相关链接

- 安装与读图文档：/docs/getting-started/options-level-pro
- 支持中心：/docs/troubleshooting/options-level-pro
