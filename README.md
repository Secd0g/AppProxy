<div align="center">

<img src="128x128.png" width="96" height="96" alt="AppProxy icon">

# 🛡️ AppProxy

### 为指定应用单独配置代理

只代理你选择的应用，不接管整个系统。

<p>
  <img src="https://img.shields.io/badge/Windows-10%20%7C%2011-2563eb?logo=windows11&logoColor=white" alt="Windows 10 / 11" />
  <img src="https://img.shields.io/badge/version-0.4.1-6651ce" alt="Version 0.4.1" />
  <img src="https://img.shields.io/badge/engine-native%20relay-22a06b" alt="Native relay engine" />
  <img src="https://img.shields.io/badge/interface-中文%20%2F%20English-f59e0b" alt="Chinese and English" />
</p>

<p>
  <a href="#-快速上手">快速上手</a> ·
  <a href="#-核心功能">核心功能</a> ·
  <a href="#-常见问题">常见问题</a>
</p>

</div>

<br />

> 🎯 **AppProxy 是什么？** 一款面向 Windows 的应用级代理工具。为 ChatGPT、Claude、浏览器或其他桌面应用分别设置 **代理 / 直连** 规则，并从 AppProxy 内按规则启动。它只处理你选择的应用，不接管整个系统网络。

## ✨ 核心功能

| | 功能 | 说明 |
|---|---|---|
| 🧩 | **应用级规则** | 每个应用单独选择代理或直连 |
| 🌐 | **多代理管理** | 配置多个 SOCKS5 代理服务器，每个应用独立中继端口 |
| 📡 | **代理检测** | 测试 SOCKS5 握手、出口 IP、地区和延迟 |
| 🚀 | **按规则启动** | 从 AppProxy 启动应用，自动开启代理引擎，确保新连接使用当前规则 |
| 📊 | **连接监控** | 查看活动连接、进程和实时转发状态 |
| 🪟 | **Windows 原生体验** | 支持 `.exe`、`.lnk`、MSIX/WindowsApps 扫描、开机启动和托盘运行 |
| 🌍 | **双语界面** | 支持中文和 English |

## 🧭 使用前准备

你需要先准备一个可用的 **SOCKS5 代理**，例如 Clash / Mihomo 的本地监听端口。

```text
服务器：127.0.0.1
端口：7897
类型：SOCKS5 (Mixed 端口也兼容)
```

> 💡 AppProxy 只负责应用分流，不提供代理节点、订阅或网络线路。

## 🚀 快速上手

### ① 添加代理服务器

打开 AppProxy，进入 **代理服务器** 页面：

1. 点击 **添加代理**。
2. 填写代理名称、服务器地址和端口。
3. 点击 **测试代理**，确认连接可用。

AppProxy 会显示代理地区、出口 IP 和访问延迟，方便你选择更合适的线路。找不到端口时，可先启动 Clash / Mihomo，再使用自动探测功能。

### ② 添加应用

进入 **应用规则** 页面，任选一种方式：

- 📦 将 `.exe` 程序拖入窗口
- 🔗 将桌面 `.lnk` 快捷方式拖入窗口
- 📁 点击 **添加应用** 浏览文件
- 🔍 点击 **扫描 WindowsApps**，发现 Microsoft Store / Packaged 应用

AppProxy 会自动解析 WindowsApps 应用的真实启动路径。对于 Claude、ChatGPT 等桌面应用，也建议从 AppProxy 重新启动，确保应用拿到当前规则。

### ③ 设置应用动作

| 动作 | 图标 | 作用 |
|---|---:|---|
| **代理** | 🟢 | 通过选定的 SOCKS5 代理访问网络 |
| **直连** | 🔵 | 不经过 AppProxy，直接连接网络 |

### ④ 按规则启动

1. 在应用规则列表中找到目标应用。
2. 点击启动按钮，AppProxy 会自动启动代理引擎并按规则打开应用。

⚠️ 如果应用已经运行，请先完全退出，包括托盘图标和后台进程，再从 AppProxy 启动。已经从开始菜单或桌面打开的进程不会自动获得新规则。

## 🔄 工作方式

```text
┌─────────────────┐       ┌──────────────────┐       ┌────────────────┐
│  选择应用与规则  │  ───▶  │  AppProxy 本地转发  │  ───▶  │ SOCKS5 │
└─────────────────┘       └──────────────────┘       └────────────────┘
          │                         │                         │
          └─────────────── 其他应用保持原有网络行为 ───────────────┘
```

- AppProxy 通过 SOCKS5 协议连接你配置的上游代理。
- 内置中继引擎为每个应用分配独立的本地端口（从 10810 起），通过环境变量和启动参数将代理设置注入目标应用。
- MSIX/Store 应用通过 `shell:AppsFolder` 协议启动，兼容 Windows 10/11 所有版本（含 LTSC）。
- 启动应用时代理引擎自动开启，无需手动操作。
- 只有从 AppProxy 启动且匹配规则的应用使用代理。
- **不会创建 TUN 虚拟网卡**，也不会修改 Windows 系统代理、DNS 或路由表。

## ⚙️ 常用设置

### 🟢 开机启动

在 **设置** 中开启后，AppProxy 会在登录 Windows 后自动打开。代理引擎会在你首次启动应用时自动开启。

### 🌙 轻量模式

降低监控刷新频率，并减少界面动效和阴影，适合长时间运行。

### 📈 网络连接

在 **网络连接** 页面查看应用进程、活动连接和当前代理转发状态。

### 🧹 代理引擎恢复

如果上次异常退出后再次启动提示本地端口被占用，请先完全退出 AppProxy 及其后台进程，再重新启动。AppProxy 会在启动时重新建立本地转发入口，不会修改系统代理设置。

## 🧩 兼容性与限制

- ✅ 对 Chrome、Microsoft Edge、Claude、ChatGPT、Obsidian 及多数 Chromium / Electron 应用支持较好。
- ✅ 支持部分 Microsoft Store / Packaged Electron 应用。
- ⚠️ Store 应用需要完全退出后，再从 AppProxy 重新启动。
- ⚠️ 非 Chromium 且忽略启动参数或自定义代理的应用，可能无法接入。
- ⚠️ 从 AppProxy 外部启动的应用不会自动继承应用规则。
- ✅ AppProxy 不会自动接管系统代理，也不会影响未配置的应用。

## ❓ 常见问题

<details>
<summary><b>测试代理失败怎么办？</b></summary>

确认 Clash / Mihomo 已启动对应端口，并检查地址、端口和代理类型。HTTP-only 端口不能作为 SOCKS5 代理使用。

</details>

<details>
<summary><b>应用没有走代理怎么办？</b></summary>

完全退出应用后，从 AppProxy 重新启动；确认规则动作是 **代理**，并且选择的代理测试通过。同时确认 AppProxy 的代理引擎已经启动。

</details>

<details>
<summary><b>关闭 AppProxy 后连接中断正常吗？</b></summary>

正常。AppProxy 关闭时会停止本地转发组件，需要代理的应用运行期间请保持 AppProxy 开启。

</details>

## 📄 许可证说明

AppProxy 的许可证和第三方组件授权信息以仓库及软件发布包中附带的许可证文件为准。当前版本使用 C++ (WebView2 + Svelte) 构建，内置 SOCKS5 中继引擎。

<br />

<div align="center">

**AppProxy · 为每一个应用，保留选择的权利。**

</div>
