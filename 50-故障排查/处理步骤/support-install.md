---
title: "安装问题处理步骤"
title_en: "Installation Issue Steps"
type: support-topic
access: signin
tags:
  - "文档中心"
  - "故障排查"
  - "权限/需登录"
aliases:
  - "安装问题"
  - "Installation issue"
  - "安装问题处理步骤"
source_url: "https://tradinghubs.org/docs/troubleshooting/installation"
generated: 2026-09-15
---

# 安装问题处理步骤

> [!info] 导航 / Navigation
> [[文档中心]] · [[troubleshoot-options-level-pro|Options Level Pro 错误码]]

**确认 DLL 类型、ATAS 目录、隐藏 AppData、版本和启用状态。**

Risk Manager、Options Level、Options Level Pro 和 Rithmic Registration Tool 都需要先确认平台版本、产品版本和安装路径；完整图文步骤请先看集中安装教程。

## 处理步骤

1. 先打开集中安装教程：`/docs/getting-started/install-update`，按文件资源管理器步骤确认隐藏的 AppData 是否能看到。
2. 关闭 ATAS 后再复制 DLL，避免旧文件仍被占用。
3. Risk Manager 放入 `%AppData%\ATAS\Strategies\`；Options Level 和 Options Level Pro 放入 `%AppData%\ATAS\Indicators\`；Rithmic Registration Tool 使用 Windows x64 版本。
4. 选择与你 ATAS 文件名匹配的 DLL；X 与 8.x 内容完全相同，7.x 为独立构建。
5. 重新启动 ATAS 后，在 Chart Strategies 或 Indicators 里添加产品并确认已启用。

---

## English

For Risk Manager, Options Level, Options Level Pro, and Rithmic Registration Tool, confirm the platform version, product version, and setup path first; use the central setup guide for the full walkthrough.

1. Open the central setup guide first: `/docs/getting-started/install-update`, then follow the File Explorer steps to confirm hidden AppData is visible.
2. Close ATAS before copying the DLL so the old file is not locked.
3. Place Risk Manager in `%AppData%\ATAS\Strategies\`; place Options Level and Options Level Pro in `%AppData%\ATAS\Indicators\`; use the Windows x64 version of Rithmic Registration Tool.
4. Choose the DLL name matching ATAS; X and 8.x are byte-identical, while 7.x remains a separate build.
5. Restart ATAS, add the product from Chart Strategies or Indicators, and confirm it is enabled.
