---
title: "授权失败：当前授权已绑定其他设备"
title_en: "DEVICE_LIMIT_REACHED"
type: error-code
code: "DEVICE_LIMIT_REACHED"
access: public
tags:
  - "文档中心"
  - "故障排查"
  - "错误码"
  - "权限/公开"
aliases:
  - "DEVICE_LIMIT_REACHED"
  - "授权失败：当前授权已绑定其他设备"
  - "device-limit-reached"
source_url: "https://tradinghubs.org/docs/troubleshooting/options-level-pro/device-limit-reached"
generated: 2026-09-15
---

# 授权失败：当前授权已绑定其他设备

> [!info] 导航 / Navigation
> [[文档中心]] · [[setup-options-level-pro|Options Level Pro 安装激活]]

**错误码 DEVICE_LIMIT_REACHED**

错误码：`DEVICE_LIMIT_REACHED`

当前授权已经绑定在另一台设备上。请先让旧设备上的 ATAS 完全退出并确认没有在运行，再到账户“设备解绑”页解除旧设备绑定，否则两台设备会互相抢占绑定位。

## 处理步骤

1. 完全退出旧设备上的 ATAS，确认 Options Level Pro 没有在运行。
2. 登录 TradingHub。
3. 进入“设备解绑”页。
4. 找到 Options Level Pro 授权并点击“解绑设备”。
5. 回到新设备上的 ATAS 重新加载指标完成激活。

## 相关链接

- 设备解绑：/account/login?next=%2Faccount%2Fdevices
- 设备绑定说明：/account/login?next=%2Fdocs%2Faccount-and-license%2Fdevice-binding
