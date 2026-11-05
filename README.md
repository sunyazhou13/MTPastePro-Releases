# PastePro

一款常驻菜单栏的 macOS 剪贴板管理器。免费、无订阅、无账号，所有数据只留在本机。

> 本仓库仅用于**分发构建产物与发布说明**，源码仓库暂不公开。

## 下载

**[下载最新版 PastePro-1.0.0.dmg](https://github.com/sunyazhou13/MTPastePro-Releases/releases/latest/download/PastePro-1.0.0.dmg)**

也可以到 [Releases 页面](https://github.com/sunyazhou13/MTPastePro-Releases/releases) 查看所有版本与完整发布说明。

| 项 | 值 |
|---|---|
| 版本 | 1.0.0 (build 3) |
| 系统要求 | macOS 14.0 (Sonoma) 或更高，Apple Silicon / Intel（Universal 2） |
| 文件大小 | 8,170,496 B ≈ 7.8 MB |
| SHA-256 | `01accbb34797882034b29ca215d9842a0c90fffa93dd874e6df929813eb2ba67` |

> **2026-11-05 更新（同版本 1.0.0 / build 3）**：DMG 已重新打包覆盖，**下载链接不变**。
> 修掉方向切换整屏跳页、删除卡片滚回页首、打开面板滑回开头三个体验问题；
> 外观 Tab 新增「记住上次操作的位置」开关（默认关闭）与高清 App 图标预览。
> Windows / Linux Electron 版 0.1.0 未变动。

## 🖥 Windows / Linux（实验性）

另有一套 **Electron 跨平台版 0.1.0**，由独立项目 `MTPasteProUniform` 构建，目标是三平台 UI / 交互一致。
⚠️ 它与上面的 macOS 原生版 **1.0.0 不是同一套实现**：采用 Electron + JSON 存储，
**暂不含** SQLCipher 加密、WCDB / MMKV、图钉板等能力，功能仍在迭代。

完整说明与 SHA-256 见 [v1.0.0 Release 正文](https://github.com/sunyazhou13/MTPastePro-Releases/releases/tag/v1.0.0)。

| 平台 | 下载 |
|:---|:---|
| Windows x64 | [NSIS 安装版](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-win-x64-setup.exe) · [免安装 zip](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-win-x64.zip) |
| Linux x86_64 | [AppImage](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-linux-x86_64.AppImage) · [deb](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-linux-amd64.deb) |
| Linux arm64 | [AppImage](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-linux-arm64.AppImage) · [deb](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-linux-arm64.deb) |

> Linux 上「选中即粘贴」会自动在 `xdotool` / 内置 XTEST 注入 / `wtype` / `ydotool` 之间挑可用的；
> 纯 Wayland 或工具全缺时仍可复制后手动粘贴。

## 安装

1. 打开 DMG，把 `PastePro.app` 拖进「应用程序」。
2. 首次使用需在「系统设置 → 隐私与安全性 → 辅助功能」中勾选 PastePro，否则「选中即粘贴」无法发出 ⌘V。
3. 默认热键 **⇧⌘V** 唤起面板（被占用时自动回退 ⌥⌘V / ⌃⌘V / ⌃⌥⌘V），可在设置里改。

> ⚠️ **关于签名**：本版本为 ad-hoc 签名，未经 Developer ID 签名与 Apple 公证，Gatekeeper 会提示「已损坏，无法打开」。任选一种方式处理：
> - 终端执行 `xattr -cr /Applications/PastePro.app` 后重新打开；
> - 或在「系统设置 → 隐私与安全性」里点「仍要打开」。
>
> 这是分发方式限制，不是文件损坏。

## 主要功能

- 自动记录 **文本 / 富文本 / 链接 / 图片 / 文件 / 颜色** 六类剪贴板内容，SHA256 去重，历史上限默认 500 条
- 底部通栏面板：搜索、卡片流、来源 App 图标、内容主色头带、毛玻璃背景
- 键盘翻卡（← → ↑ ↓ / 滚轮 / 触控板横滑）、⌘1–⌘9 快贴、⌘A 多选、空格 Quick Look、**长按 ⌫ / ⌦ 连续删除**
- 多图钉板（新建 / 重命名 / 7 色标记 / 排序 / 固定）、回收站与删除撤销
- 设置页五个 Tab，全局热键自定义 + 冲突检测
- 数据库 SQLCipher 加密（WCDB.swift ORM），设置走 MMKV，全程无网络请求、无遥测

## 已知限制

- 剪贴板变更采用 0.3s 轮询，非事件驱动，极端情况下有极短延迟
- 「选中即粘贴」依赖辅助功能权限，部分安全输入框可能拒绝模拟 ⌘V
- 尚未实现：条目编辑与大图预览窗口、Paste Stack 粘贴栈、隐私忽略规则配置页
- 明确不做：iCloud 同步、小组件、共享图钉板、智能建议，以及任何付费 / 许可 / 试用模块

## 反馈

问题与建议欢迎开 [Issue](https://github.com/sunyazhou13/MTPastePro-Releases/issues)。

---

© 2026 sunyazhou
