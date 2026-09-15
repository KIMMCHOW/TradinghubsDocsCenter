---
title: "自动更新失败"
title_en: "UPDATE_FAILED"
type: error-code
code: "UPDATE_FAILED"
access: public
tags:
  - "文档中心"
  - "故障排查"
  - "错误码"
  - "权限/公开"
aliases:
  - "UPDATE_FAILED"
  - "自动更新失败"
  - "update-failed"
source_url: "https://tradinghubs.org/docs/troubleshooting/options-level-pro/update-failed"
generated: 2026-09-15
---

# 自动更新失败

> [!info] 导航 / Navigation
> [[文档中心]] · [[setup-options-level-pro|Options Level Pro 安装激活]]

**错误码 UPDATE_FAILED**

错误码：`UPDATE_FAILED`

指标检测到新版本，但未能完成自动更新。常见原因是 DLL 被 ATAS 占用，或安装目录没有写入权限。

## 处理步骤

1. 完全退出 ATAS。
2. 检查 DLL 文件是否被其他程序占用。
3. 检查安装目录是否具有写入权限。
4. 前往下载页面手动安装最新版本。

## 相关链接

- 下载最新版本：/download/options-level-pro
- 安装与更新文档：/docs/getting-started/options-level-pro
