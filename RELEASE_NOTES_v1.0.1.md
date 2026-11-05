# PastePro v1.0.1

1.0.0 之后的第一个维护版本：修掉卡片流的几处交互问题，并补上「记住上次操作的位置」开关。
一款常驻菜单栏的 macOS 剪贴板管理器，交互参考 Paste，**完全免费、无订阅、无内购、无账号**。

> 所有数据只留在本机，无网络请求、无遥测。

**📦 下载**：[PastePro-1.0.1.dmg](https://github.com/sunyazhou13/MTPastePro-Releases/releases/latest/download/PastePro-1.0.1.dmg)

## ✨ 本次更新（相对 1.0.0）

- **卡片流翻页**：修掉「往右翻十几张后按 ← 会整屏跳一页」的问题 ——
  只在目标卡越出可视区时才滚动，视口内移动一律不滚，方向切换不再贴边跳页。
- **删除补位**：删中间卡片时后面的卡原地前移补位，选框不再滚到页首、也不会往后跳；
  删最后一张且列表够一屏时，左侧卡片带动画右移补位；列表不足一屏时选框往前移一位
  选中前一张。长按 ⌫ / ⌦ 连续删仍可用。
- **打开面板**：不再有「从上次位置滑回开头」的动画。外观 Tab 新增
  **「记住上次操作的位置」** 开关（默认关闭；开启后按卡片 id 恢复上次位置，
  历史增删不会错位）。
- **外观 Tab**：卡片倾斜强度预览换成 1024×1024 高清 App 图标。

> Windows / Linux Electron 版仍是 **0.1.0**，本次未改动，安装包继续挂在
> [v1.0.0 Release](https://github.com/sunyazhou13/MTPastePro-Releases/releases/tag/v1.0.0) 下
> （见下方表格）。两条产品线版本号互相独立。

## ✨ 功能

### 核心
- 菜单栏常驻（无 Dock 图标），0.3s 轮询监听剪贴板，自动收录 **文本 / 富文本 / 链接 / 图片 / 文件 / 颜色** 六类内容。
- SHA256 内容去重（相同内容只刷新时间），历史容量上限默认 500 条，仅裁剪未固定项。
- 底部通栏面板：搜索、卡片流、来源 App 图标、内容主色头带、毛玻璃背景、点击面板外收起。
- 选中即写回系统剪贴板并自动模拟 ⌘V 粘贴（需辅助功能权限，首次会引导）。
- 单实例保护、回收站与删除撤销、历史容量可在设置里调整。

### 键盘与导航
- 面板打开即聚焦卡片，← → ↑ ↓ / 鼠标滚轮 / 触控板横滑均「一格一张」翻卡，选中态高亮并自动居中。
- **长按 ⌫ / ⌦ 连续删除**：按住不松即从当前卡片逐张往下删，不用一下一下敲。
- ⌘1–⌘9 快贴、↵ 粘贴、⌘A 多选、空格 Quick Look 预览、esc 收起。

### 图钉板（Pinboard）
- 多板新建 / 重命名 / 删除 / 7 色标记 / 板内排序 / 固定与取消，chip 带条目计数。
- 顶栏三段式布局，板切换带交叉淡化；旧版 `pinned` 数据自动迁入「收藏」板。

### 快捷键与设置
- 默认 **⇧⌘V** 唤起面板，若被其他 App（如 Paste）占用会检测冲突并依次回退 ⌥⌘V / ⌃⌘V / ⌃⌥⌘V，可在设置页自定义。
- 设置页五个 Tab：通用 / 快捷键 / 规则 / 按键说明 / 外观（含「记住上次操作的位置」开关）；冲突检测覆盖系统符号热键与常见第三方工具。

## 🔐 隐私与数据
- 剪贴板历史数据库使用 **SQLCipher 加密**（WCDB.swift ORM 存储），设置走 MMKV。
- 一次性完成旧明文库 → 加密库迁移，任何一步失败自动回退明文，**不会损坏历史**。
- 数据目录：`~/Library/Application Support/Paste Pro/`。图片按文件引用不入库。
- 不开启 App Sandbox（辅助功能授权与沙盒互斥）。

## 📦 安装
1. 下载 `PastePro-1.0.1.dmg`，打开后把 `PastePro.app` 拖进「应用程序」。
2. 首次使用时，在「系统设置 → 隐私与安全性 → 辅助功能」中勾选 PastePro，否则「选中即粘贴」无法发出 ⌘V。
3. 要求 **macOS 14.0 (Sonoma) 或更高**，Apple Silicon / Intel 通用（Universal 2）。

> ⚠️ **关于签名**：本版本为 ad-hoc 签名，**未使用 Developer ID 签名、未经 Apple 公证**。
> Gatekeeper 会提示「Apple 无法验证」或「已损坏，无法打开」。任选一种方式处理：
> - 终端执行 `xattr -cr /Applications/PastePro.app` 后重新打开；
> - 或「系统设置 → 隐私与安全性」里点「仍要打开」。
>
> 这是分发方式限制，不是文件损坏。后续拿到 Developer ID 证书并公证后会更新安装包。

## 🖥 Windows / Linux（Electron 跨平台版 0.1.0）

> ⚠️ **这是另一条产品线，不是同一个版本号。** 下面的安装包来自独立的 Electron 跨平台项目
> （`MTPasteProUniform`），版本 **0.1.0**；上面的 macOS 原生版是 **1.0.1**。Electron 版采用
> Electron + JSON 本地存储，目标是三平台 UI / 交互一致，**尚不包含**原生版的 SQLCipher 加密、
> WCDB / MMKV 存储、图钉板等能力，属于实验性版本，功能仍在迭代。macOS 用户请用上面的
> `PastePro-1.0.1.dmg`。
>
> 本次 1.0.1 只更新 macOS 原生版，以下 6 个安装包仍挂在
> [v1.0.0](https://github.com/sunyazhou13/MTPastePro-Releases/releases/tag/v1.0.0) 下，链接保持不变。

| 平台 | 文件 | 大小 |
|:---|:---|:---|
| Windows x64 | [NSIS 安装版 `.exe`](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-win-x64-setup.exe) | 124.7 MB |
| Windows x64 | [免安装绿色版 `.zip`](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-win-x64.zip) | 157.1 MB |
| Linux x86_64 | [AppImage](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-linux-x86_64.AppImage)（`chmod +x` 后直接运行） | 129.6 MB |
| Linux x86_64 | [Debian / Ubuntu `.deb`](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-linux-amd64.deb) | 104.7 MB |
| Linux arm64 | [AppImage](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-linux-arm64.AppImage) | 130.9 MB |
| Linux arm64 | [`.deb`](https://github.com/sunyazhou13/MTPastePro-Releases/releases/download/v1.0.0/PastePro-0.1.0-linux-arm64.deb)（RK3576 / Debian 13 开发板已实测） | 99.5 MB |

**SHA-256**

```
88dd1897fb15a522091ff91ff80e87be4692261e0a46b02e67d308e011dc1b4c  PastePro-0.1.0-win-x64-setup.exe
4b07ad320296b8cb8df01ca749c1fbb571ba416bf3723c96a04422339fc2db78  PastePro-0.1.0-win-x64.zip
2f8333e5ab235084c7640cd1641712fdaa2b3358a574b1e9f0487ccc1445240c  PastePro-0.1.0-linux-x86_64.AppImage
7162eeaadaadabcfe598fea466b0514eef7f42891711a6efe39003f7d0f5191c  PastePro-0.1.0-linux-amd64.deb
fb0ee53f97c21e30ea151257ebb8d28d3d3b224161cb61af302661043cc6bbad  PastePro-0.1.0-linux-arm64.AppImage
7a786bf004d435e47b32302ff43776f52e486d2f742c11d65f8272138fcaf7eb  PastePro-0.1.0-linux-arm64.deb
```

**Linux 使用提示**：「选中即粘贴」会按 `xdotool` → 内置 `x11-inject.py`（python3 + libXtst，零安装）→
`wtype` → `ydotool` 依次探测；X11 下剪贴板写入还有内置 `clip-set.py` 兜底，解决 Chromium 失焦后
拒发剪贴板的问题。**纯 Wayland 会话下 XTEST 不生效**，需 `wtype` / `ydotool`；这些工具全不可用时
仍可复制内容后手动粘贴。deb 安装时会自动修 `chrome-sandbox` 的 setuid 权限。

## ⌨️ 快捷键速查

| 动作 | 快捷键 |
|---|---|
| 唤起 / 收起面板 | ⇧⌘V（占用时自动回退） |
| 快贴第 1–9 条 | ⌘1 – ⌘9 |
| 粘贴选中项 | ↵ |
| 翻卡 | ← → ↑ ↓ / 滚轮 / 触控板横滑 |
| 连续删除 | 长按 ⌫ 或 ⌦ |
| 多选 / 全选 | ⌘A |
| 搜索 | 面板内直接敲字 |
| Quick Look | 空格 |
| 关闭面板 | esc |

## 🧪 质量
- 测试代码为 `PasteProUITests`（XCTest Unit Test），覆盖纯逻辑断言 + SQLCipher 加密迁移 + 回收站端到端（真实读写 DB）。
- 测试在临时数据目录运行，不污染真实历史。
- 发布前验证：`xcodebuild build` 通过，`codesign --verify --deep --strict` 通过。

## ⚠️ 已知限制
- 剪贴板变更采用轮询（0.3s），非事件驱动，极端情况下有极短延迟。
- 自动粘贴依赖辅助功能权限；部分全屏/安全输入框可能拒绝模拟 ⌘V。
- 尚未实现：条目编辑与大图预览窗口、Paste Stack 粘贴栈、隐私忽略规则配置页（列入后续版本）。
- 明确不做：iCloud 同步、小组件、共享图钉板、智能建议，以及任何付费 / 许可 / 试用模块。

## 系统要求与校验
| 项 | 值 |
|:---|:---|
| 版本 | 1.0.1 (build 4) |
| 系统 / 架构 | macOS 14.0+，Universal 2（arm64 + x86_64） |
| 安装包 | `PastePro-1.0.1.dmg`（8,171,520 B ≈ 7.8 MB） |
| SHA-256 | `417f824c0529d8ca6d4bebb1975dacdd38b4a42ffab2851f4f226c6366429163` |

---

源码仓库暂不公开，本仓库仅用于分发构建产物。问题反馈欢迎开 Issue。
