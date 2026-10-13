# Snapmaker Control

[English](README.md) | **简体中文**

[![Latest release](https://img.shields.io/github/v/release/Snapmaker/snapmaker_control)](https://github.com/Snapmaker/snapmaker_control/releases/latest)
![Platforms](https://img.shields.io/badge/platform-macOS%20%7C%20Windows%20%7C%20Linux-lightgrey)

Snapmaker Control 是 **[Snapmaker Orca](https://github.com/Snapmaker/OrcaSlicer)** 的设备连接与控制程序。
它在后台运行，负责和打印机通信，并提供 Snapmaker Orca 里显示的设备页面。

它也可以**独立运行**：不打开 Snapmaker Orca，直接在浏览器里使用，作为一个独立控制
**Snapmaker U1** 的程序。

> 本仓库是 Snapmaker Control 可执行程序的官方分发渠道，
> 只包含发布包、许可协议和第三方声明，不包含源代码。

## 功能

**连接**
- 自动发现局域网里的 Snapmaker U1，也可以输入 IP 地址添加
- 通过 PIN 码绑定打印机；可在局域网内直连，也可通过 Snapmaker 账号远程连接
- 管理打印机：重命名、移除、解绑，一眼看清连接状态，有新固件时提醒

**实时画面**
- 实时查看打印机摄像头画面，可开关腔内灯
- 浏览、预览、批量下载和删除延时摄影视频

**控制**
- 设置喷嘴温度（多喷头分别设置）和热床温度
- 控制腔内灯、冷却风扇与腔体风扇，以及空气净化器（已安装时）
- 打印中调整打印速度
- 空闲时：移动 X/Y/Z 轴、回零、进料或退料、取放打印头、升降热床

**打印任务**
- 查看当前打印的缩略图、进度和剩余时间
- 暂停、继续或取消打印
- 浏览打印机内部存储和 U 盘中的文件，直接开始打印
- 打印机报告故障时弹出提醒

**耗材**
- 查看最多 4 个料槽，设置每个料槽的颜色、品牌和材料

**AI 监测**
- 开启或关闭打印缺陷检测，并调整检测设置

**首页与账号**
- 模型广场推荐、我的设备、最近文件和打印历史
- 登录、注册，或使用第三方账号登录

> 从切片软件发送文件、从模型广场打开模型需要配合 Snapmaker Orca 使用。

## 下载

在 [Releases](https://github.com/Snapmaker/snapmaker_control/releases/latest) 页面下载最新版本。

| 平台 | 安装包 |
|---|---|
| macOS（Apple 芯片） | `snapmaker_control-<版本>-macos-arm64.zip` |
| macOS（Intel） | `snapmaker_control-<版本>-macos-x64.zip` |
| Windows（x64） | `snapmaker_control-<版本>-windows-x64.zip` |
| Windows（ARM64） | `snapmaker_control-<版本>-windows-arm64.zip` |
| Linux（x64） | `snapmaker_control-<版本>-linux-x64.tar.gz` |
| Linux（arm64） | `snapmaker_control-<版本>-linux-arm64.tar.gz` |

macOS 版本使用 Snapmaker 的 Developer ID 签名并经过 Apple 公证；
Windows 版本使用 Snapmaker 的代码签名证书签名。

## 独立运行

1. 下载对应系统的安装包并解压。
   程序和 `web` 文件夹必须放在同一目录下，缺少 `web` 文件夹将无法打开网页。
   ```
   snapmaker_control_<系统>_<架构>[.exe]
   web/
   ```
2. 启动程序：
   - **Windows / macOS**：双击 `snapmaker_control_…`。
   - **Linux**：在终端中运行，例如 `./snapmaker_control_linux_x64`。

   默认浏览器会自动打开「首页」和「设备控制」页面。

关闭程序运行的窗口（或在终端中按 `Ctrl+C`）即可退出。

网页只对本机（`127.0.0.1`）开放，局域网里的其他设备无法访问。

### 首次运行

- **Windows**：首次运行时可能弹出 Windows Defender 防火墙提示，请点击**允许**——
  程序通过 mDNS 在局域网中发现打印机。如果点了**取消**，会搜不到局域网里的打印机，
  需要到「Windows 安全中心 → 防火墙和网络保护 → 允许应用通过防火墙」中放行
  `snapmaker_control_windows_*.exe`。
- **macOS**：如果系统询问是否允许接入网络连接或访问本地网络，请点击**允许**，原因同上。

## 配合 Snapmaker Orca 使用

Snapmaker Orca 已内置 Snapmaker Control，并会自动启动它，无需单独安装。

## 校验下载文件

每个版本都附带 `SHA256SUMS` 文件：

```bash
# macOS / Linux
shasum -a 256 -c SHA256SUMS --ignore-missing
```

```powershell
# Windows（PowerShell）
Get-FileHash .\snapmaker_control-<版本>-windows-x64.zip -Algorithm SHA256
```

## 数据与日志

设置、设备列表和日志按用户保存在：

| 系统 | 位置 |
|---|---|
| Windows | `%APPDATA%\Snapmaker_Orca\snapmaker_control\` |
| macOS | `~/Library/Application Support/Snapmaker_Orca/snapmaker_control/` |
| Linux | `$XDG_CONFIG_HOME/Snapmaker_Orca/snapmaker_control/`（默认 `~/.config/…`） |

反馈问题时，请附上该目录下 `data/log/` 中最新的日志文件。

卸载时删除解压出的文件夹即可；如需清除数据，再删除上面的数据目录。

## 命令行

```bash
snapmaker_control --version       # 显示版本号
snapmaker_control --help          # 查看全部参数
snapmaker_control --locale=zh-CN  # 界面语言与云区域（默认 en-US）
```

## 问题反馈

请通过 [GitHub Issues](https://github.com/Snapmaker/snapmaker_control/issues) 反馈问题，
并附上操作系统、Snapmaker Control 版本号（`--version`）和日志文件。

## 许可

Snapmaker Control 是深圳快造科技有限公司（Shenzhen Snapmaker Technologies Co., Ltd.）的专有软件，
依据 [LICENSE.txt](LICENSE.txt) 中的条款分发。
第三方组件及其许可见 [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt)。
Snapmaker Orca 另行依据 GNU AGPL-3.0 授权。
