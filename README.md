<div align="center">
  <img src="src-tauri/icons/128x128.png" width="92" height="92" alt="AppProxy icon">

  # AppProxy

  **让指定应用走代理，让其他流量保持直连。**  
  *Route selected applications through a proxy while keeping everything else direct.*

  ![Windows](https://img.shields.io/badge/Windows-10%20%7C%2011-1674EA?logo=windows&logoColor=white)
  ![Tauri](https://img.shields.io/badge/Tauri-2-24C8DB?logo=tauri&logoColor=white)
  ![Rust](https://img.shields.io/badge/Rust-Backend-000000?logo=rust&logoColor=white)
  ![Svelte](https://img.shields.io/badge/Svelte-5-FF3E00?logo=svelte&logoColor=white)

  [简体中文](#简体中文) · [English](#english) · [开发构建](#开发构建--development)
</div>

---

## 简体中文

AppProxy 是一款轻量的 Windows 按应用网络分流工具。它不接管整个系统代理，而是仅将你指定的应用透明转发到本机 SOCKS5 代理。每个应用都可以独立选择 **代理**、**直连** 或 **阻止联网**。

### ✨ 功能一览

| 功能 | 说明 |
| --- | --- |
| 🎯 按应用分流 | 为每个 Windows 程序单独设置代理、直连或阻止 |
| 🧩 多代理配置 | 添加并编辑多个 SOCKS5 代理服务器 |
| 🖱️ 拖放添加 | 支持 `.exe` 程序和 `.lnk` 桌面快捷方式 |
| 🔍 应用扫描 | 自动发现 ChatGPT、Claude 等常用 AI 应用 |
| 🌍 出口识别 | 显示代理出口国家/地区和真实网站访问延迟 |
| 📈 连接监控 | 查看应用进程数、活跃连接和实时连接趋势 |
| 🛡️ 联网阻止 | 使用 Windows 防火墙阻止指定应用联网 |
| ⚙️ 常用设置 | 支持开机启动、轻量模式和中英文界面 |

> [!IMPORTANT]
> AppProxy 负责“按应用分流”，不提供代理节点、订阅或代理协议。你仍需运行 Clash、Mihomo 或其他提供 SOCKS5/Mixed 端口的代理软件。

### 💻 系统要求

- 64 位 Windows 10 或 Windows 11。
- Clash、Mihomo 或其他可用的 SOCKS5/Mixed 代理服务。
- 推荐使用本机端点，例如 `127.0.0.1:7897`。
- 启动透明代理时需要接受 Windows UAC 管理员权限请求。

### 📦 安装

1. 运行 **`AppProxy_0.1.0_x64-setup.exe`**。
2. 按照安装向导完成安装并打开 AppProxy。
3. 进入 **代理服务器**，填写本机 SOCKS5 地址并点击测速图标。
4. 进入 **应用规则**，拖入或添加目标程序。
5. 为应用选择 **代理**、**直连** 或 **阻止**。
6. 点击右上角 **启动**，并接受 UAC 权限请求。

> [!NOTE]
> 首次启动代理时，AppProxy 会通过 UAC 自动安装随软件附带的 ProxiFyre 服务。仅仅打开 AppProxy 不会自动开启代理。

### 🚦 三种规则

| 规则 | 行为 | 适用场景 |
| --- | --- | --- |
| **代理** | 将应用的新建连接透明转发至所选 SOCKS5 代理 | ChatGPT、Claude 等需要代理的应用 |
| **直连** | 应用连接不经过 AppProxy | 本地服务、国内应用或无需代理的软件 |
| **阻止** | 通过 Windows 防火墙阻止应用联网 | 临时断网、隐私控制或测试 |

### 📊 状态数据怎么看

- **地区**：SOCKS5 代理的互联网出口国家/地区。
- **延迟**：通过该代理实际访问外部轻量测试地址的总响应时间，而非本机端口延迟。
- **活跃连接**：目标应用当前建立的外部 TCP 连接数量。
- **连接趋势**：最近多次刷新中活跃连接数量的变化。
- AppProxy 不抓包、不解密 HTTPS，也不会读取通信内容。

### 💡 使用提示

- 修改规则后，建议完全退出并重新打开目标应用，让它建立新连接。
- 启动前先确认代理服务器测速成功。
- AppProxy 退出后会自动停止 ProxiFyre，并清理由本次会话创建的阻止规则。
- 代理服务已运行时，不要移动或删除 AppProxy 的安装目录。

<details>
<summary><strong>代理显示运行，但应用没有走代理</strong></summary>

1. 确认 SOCKS5 代理测速成功。
2. 完全退出目标应用，包括托盘和后台进程，然后重新打开。
3. 检查应用规则中的关联进程名称。
4. 确认 ProxiFyre 服务未被防火墙或安全软件拦截。
5. 确认 Clash/Mihomo 的 SOCKS5 或 Mixed 端口仍在监听。

</details>

<details>
<summary><strong>为什么需要管理员权限？</strong></summary>

ProxiFyre 需要以 Windows 服务运行，并使用系统网络过滤能力透明重定向指定进程的连接。普通用户权限无法完成这些操作，因此启动和停止引擎时需要 UAC。

</details>

<details>
<summary><strong>为什么还需要 Clash 或 Mihomo？</strong></summary>

AppProxy 只决定“哪个应用走哪个代理”。真正连接代理节点、处理订阅和协议的是 Clash、Mihomo 或其他 SOCKS5 服务。

</details>

---

## English

AppProxy is a lightweight per-application network routing tool for Windows. Instead of taking over the system proxy, it transparently redirects only the applications you select to a local SOCKS5 endpoint. Each application can use **Proxy**, **Direct**, or **Block** independently.

### ✨ Highlights

| Feature | Description |
| --- | --- |
| 🎯 Per-app routing | Assign Proxy, Direct, or Block to individual Windows applications |
| 🧩 Multiple proxies | Add and edit multiple SOCKS5 proxy servers |
| 🖱️ Drag and drop | Supports `.exe` programs and `.lnk` desktop shortcuts |
| 🔍 App discovery | Finds common AI applications such as ChatGPT and Claude |
| 🌍 Exit information | Shows proxy exit country/region and real website latency |
| 📈 Connection monitor | Displays processes, active connections, and live trends |
| 🛡️ Network blocking | Blocks selected applications through Windows Firewall |
| ⚙️ Preferences | Launch at startup, lightweight mode, and Chinese/English UI |

> [!IMPORTANT]
> AppProxy performs per-application routing. It does not provide proxy nodes, subscriptions, or proxy protocol implementations. Clash, Mihomo, or another SOCKS5/Mixed service is still required.

### 💻 Requirements

- 64-bit Windows 10 or Windows 11.
- Clash, Mihomo, or another working SOCKS5/Mixed proxy service.
- A local endpoint such as `127.0.0.1:7897` is recommended.
- Windows UAC approval is required when starting transparent routing.

### 📦 Installation

1. Run **`AppProxy_0.1.0_x64-setup.exe`**.
2. Complete the setup wizard and open AppProxy.
3. Go to **Proxies**, enter the local SOCKS5 endpoint, and click the speed-test icon.
4. Go to **App Rules** and drag in or add the target application.
5. Select **Proxy**, **Direct**, or **Block**.
6. Click **Start** in the top-right corner and approve the UAC prompt.

> [!NOTE]
> On the first proxy start, AppProxy installs its bundled ProxiFyre service through UAC. Opening AppProxy alone does not enable routing.

### 🚦 Rule Types

| Rule | Behavior | Typical use |
| --- | --- | --- |
| **Proxy** | Redirects new application connections to the selected SOCKS5 proxy | ChatGPT, Claude, and other proxied applications |
| **Direct** | Leaves application connections outside AppProxy | Local services or applications that do not need a proxy |
| **Block** | Blocks application networking through Windows Firewall | Temporary offline mode, privacy control, or testing |

### 📊 Understanding the Data

- **Region**: the Internet exit country/region of the SOCKS5 proxy.
- **Latency**: total response time to a lightweight external endpoint through the proxy, not latency to the local port.
- **Active connections**: current external TCP connections created by the target application.
- **Connection trend**: changes in active connection counts across recent refreshes.
- AppProxy does not capture packets, decrypt HTTPS, or read communication content.

### 💡 Usage Tips

- After changing a rule, fully close and reopen the target application so it creates new connections.
- Verify the proxy with the speed-test button before starting the engine.
- AppProxy stops ProxiFyre and removes session block rules when the application exits.
- Do not move or delete the AppProxy installation directory while its service is running.

<details>
<summary><strong>The engine is running, but the application is not proxied</strong></summary>

1. Confirm that the SOCKS5 speed test succeeds.
2. Fully close the target application, including tray and background processes, then reopen it.
3. Check the associated process names in the application rule.
4. Make sure ProxiFyre is not blocked by firewall or security software.
5. Confirm that the Clash/Mihomo SOCKS5 or Mixed port is still listening.

</details>

<details>
<summary><strong>Why are administrator privileges required?</strong></summary>

ProxiFyre runs as a Windows service and uses system network filtering to transparently redirect selected processes. These operations require UAC elevation.

</details>

<details>
<summary><strong>Why is Clash or Mihomo still required?</strong></summary>

AppProxy decides which application uses which proxy. Clash, Mihomo, or another SOCKS5 service handles proxy nodes, subscriptions, and the actual Internet connection.

</details>

---

## 开发构建 / Development

### 技术栈 / Stack

`Tauri 2` · `Rust` · `Svelte 5` · `TypeScript` · `ProxiFyre`

```powershell
# 安装依赖 / Install dependencies
pnpm install

# 开发运行 / Development
pnpm tauri dev

# 构建 NSIS 安装包 / Build the NSIS installer
pnpm tauri build
```

安装包输出位置 / Installer output:

```text
src-tauri/target/release/bundle/nsis/
```

### 第三方组件 / Third-party Component

AppProxy bundles [ProxiFyre](https://github.com/wiresock/proxifyre) as its transparent per-application routing engine. ProxiFyre is distributed under the **AGPL-3.0** license. Review its license and dependency requirements before redistributing AppProxy, especially for commercial or closed-source use.

---

<div align="center">
  <sub>Built for focused, transparent per-application routing on Windows.</sub>
</div>
