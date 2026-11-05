# Snapmaker Orca Control Log 

If you experience problems with device connection, print control or file downloads, follow this guide to collect your logs and send them to Snapmaker Support.
遇到设备连接、打印控制或文件下载异常时，请按本指南打包日志并发送给售后。

> It takes about 3 minutes and uses only built-in system tools. No software installation is required.
> 💡 全程约 3 分钟，只使用系统自带工具，无需安装任何软件。

- [English](#english)
- [中文版](#中文版)

---

## English

### 1. Before you start

1. Note the date and approximate time the problem occurred
2. If the problem can be reproduced, reproduce it once more before collecting the logs so they contain the latest information.
3. Close all Snapmaker Orca windows and wait about 5 seconds. The software writes any remaining log entries to disk when it exits.

### 2. Collect the logs

The logs are stored in the folder below. **Only the log folder needs to be compressed.**

| OS | Log folder |
| --- | --- |
| Windows | `%APPDATA%\Snapmaker_Orca\snapmaker_control\data\log` |
| macOS | `~/Library/Application Support/Snapmaker_Orca/snapmaker_control/data/log` |
| Linux | `~/.config/Snapmaker_Orca/snapmaker_control/data/log` |

When you open the data folder (the parent of log), you will usually see:

| Name | Description | Send it? |
| --- | --- | --- |
| `log` | Runtime logs | **Yes** |
| `hive` | Local app data, including sign-in information | No. Do not send it. |
| Other files or folders | Runtime state files, etc. | No |

Common files in the log folder:

- Dated files such as `snapmaker_control_2026-11-05.log`: the log for that day.
- Files ending in `.log.gz`: logs from previous days, compressed automatically and kept for up to 7 days.
- `startup_error.txt`: appears only if the software failed to start.

Follow the section for your operating system below.

#### 2.1 Windows

**Option 1: File Explorer (recommended)**

1. Press **Win + R** (the Win key has the Windows logo) to open the Run dialog.
2. Copy the path below, paste it into the Open box and click **OK**:

   ```text
   %APPDATA%\Snapmaker_Orca\snapmaker_control\data
   ```

3. The data folder opens. Check that it contains a log folder. If Windows says it cannot find the path, go to [section 4](#4-fallback-log-folder-not-found).
4. Right-click the log folder:
   - Windows 11: select **Compress to ZIP file**; on some versions, **Compress to… → ZIP File**.
   - Windows 10: select **Send to → Compressed (zipped) folder**.
5. `log.zip` is created in the same folder. Drag it to your Desktop so it is easy to find.

**Option 2: PowerShell**

1. Right-click the Start button on the taskbar and select **Terminal** or **Windows PowerShell**.
2. Copy the command below, paste it into the window and press Enter:

   ```powershell
   Compress-Archive -Path "$env:APPDATA\Snapmaker_Orca\snapmaker_control\data\log" -DestinationPath "$([Environment]::GetFolderPath('Desktop'))\snapmaker_log.zip" -Force
   ```

3. If no red error appears, it worked: `snapmaker_log.zip` is on your Desktop.
4. If a red error says the path does not exist, go to [section 4](#4-fallback-log-folder-not-found). If it says the file is being used by another process, make sure Snapmaker Orca is closed and try again.

#### 2.2 macOS

macOS includes the zip tool. No software installation is required.

**Option 1: Terminal (recommended)**

1. Press **Command + Space** to open Spotlight, type "Terminal" and press Return.
2. Copy the command below, paste it into the Terminal window and press Return:

   ```bash
   rm -f ~/Desktop/snapmaker_log.zip && cd "$HOME/Library/Application Support/Snapmaker_Orca/snapmaker_control/data" && zip -r -q ~/Desktop/snapmaker_log.zip log -x "*.DS_Store" && open -R ~/Desktop/snapmaker_log.zip
   ```

3. If macOS asks whether "Terminal" may access files in your Desktop folder, click **Allow**.
4. When the command succeeds, a Finder window opens with `snapmaker_log.zip` on your Desktop selected.
5. If Terminal shows `No such file or directory`, there are no logs in the default location. Go to [section 4](#4-fallback-log-folder-not-found).

**Option 2: Finder**

1. Click the **Finder** icon in the Dock.
2. In the menu bar at the top of the screen, choose **Go → Go to Folder…** (shortcut **Shift + Command + G**).
3. Paste the path below and press Return:

   ```text
   ~/Library/Application Support/Snapmaker_Orca/snapmaker_control/data
   ```

4. Check that the window contains a log folder. If the folder cannot be found, go to [section 4](#4-fallback-log-folder-not-found).
5. Control-click the log folder (or tap with two fingers on the trackpad) and choose **Compress "log"**.
6. `log.zip` is created in the same folder. Drag it to your Desktop so it is easy to find.

#### 2.3 Linux

**Option 1: Terminal (recommended)**

1. Press **Ctrl + Alt + T** to open a terminal, or search for "Terminal" in your applications.
2. Copy the command below, paste it into the terminal (paste shortcut: **Ctrl + Shift + V**) and press Enter:

   ```bash
   cd "${XDG_CONFIG_HOME:-$HOME/.config}/Snapmaker_Orca/snapmaker_control/data" && tar -czf ~/snapmaker_log.tar.gz log
   ```

3. No output means it worked: `snapmaker_log.tar.gz` is in your home folder.
4. If it shows `No such file or directory`, go to [section 4](#4-fallback-log-folder-not-found).

**Option 2: File manager**

1. Open Files (your file manager) and press **Ctrl + L** to show the location bar.
2. Enter the path below and press Enter (if you have set `XDG_CONFIG_HOME`, replace `~/.config` with that folder):

   ```text
   ~/.config/Snapmaker_Orca/snapmaker_control/data
   ```

3. Right-click the log folder, select **Compress…**, choose `.zip` and click **Create**.
4. `log.zip` is created in the same folder.

### 3. Send to Support

1. Attach the archive created in section 2 (`log.zip`, `snapmaker_log.zip` or `snapmaker_log.tar.gz`) to your message to Support.
2. Include the following information in the message (you can copy it):

   ```text
   Operating system and version: (e.g. Windows 11 / macOS 15 / Ubuntu 24.04)
   Snapmaker Orca version: (see Help → About)
   Printer model:
   Time the problem occurred: (date + time)
   Description and steps to reproduce:
   ```

3. If an error message appeared, attach a screenshot as well.

### 4. Fallback: log folder not found

> ⚠️ Follow this section only if section 2 reported that the path does not exist, or the data folder has no log folder. If you already collected the logs in section 2, skip this section.

There are usually two reasons the log folder cannot be found:

- **No logs have been created yet**: the Snapmaker Orca device features have never run on this computer. Open Snapmaker Orca, go to the device page, reproduce the problem once, then repeat section 2.
- **Your user folder is not writable**: because of restricted permissions or a company security policy, the software writes its logs to the system temporary folder instead. Collect them from there as described below.

> ⚠️ The system temporary folder may be cleared when the computer restarts. Complete the steps below before restarting.

| OS | Logs in the temporary folder | Startup error file (may not exist) |
| --- | --- | --- |
| Windows | `%TEMP%\Snapmaker_Orca\snapmaker_control\data\log` | `%TEMP%\snapmaker_control_startup_error.txt` |
| macOS | `$TMPDIR/Snapmaker_Orca/snapmaker_control/data/log` | `$TMPDIR/snapmaker_control_startup_error.txt` |
| Linux | `/tmp/Snapmaker_Orca/snapmaker_control/data/log` | `/tmp/snapmaker_control_startup_error.txt` |

#### 4.1 Windows

1. Press **Win + R**, paste the path below and click **OK**:

   ```text
   %TEMP%\Snapmaker_Orca\snapmaker_control\data
   ```

2. Right-click the log folder and compress it as in section 2 to get `log.zip`.
3. Press **Win + R** again, enter `%TEMP%` and click **OK**. Look for `snapmaker_control_startup_error.txt` in the folder that opens. If it exists, send it together with `log.zip`.

#### 4.2 macOS

1. Open Terminal, paste the command below and press Return:

   ```bash
   rm -f ~/Desktop/snapmaker_log_temp.zip && cd "$TMPDIR" && zip -r -q ~/Desktop/snapmaker_log_temp.zip Snapmaker_Orca/snapmaker_control/data/log $(ls snapmaker_control_startup_error.txt 2>/dev/null) -x "*.DS_Store" && open -R ~/Desktop/snapmaker_log_temp.zip
   ```

2. `snapmaker_log_temp.zip` is created on your Desktop. The startup error file is included automatically if it exists.

#### 4.3 Linux

1. Open a terminal, paste the command below and press Enter:

   ```bash
   cd "${TMPDIR:-/tmp}" && tar -czf ~/snapmaker_log_temp.tar.gz Snapmaker_Orca/snapmaker_control/data/log $(ls snapmaker_control_startup_error.txt 2>/dev/null)
   ```

2. `snapmaker_log_temp.tar.gz` is created in your home folder. The startup error file is included automatically if it exists.

Send the archive to Support as described in section 3. If no logs can be found in either the default location or the temporary folder, contact Support directly, list the paths you tried, and attach screenshots of the error messages.

---

## 中文版

### 一、提交前准备

1. 记下问题发生的日期和大致时间
2. 如果问题可以重现，请在打包前再操作一次，让日志记录下最新的情况。
3. 关闭 Snapmaker Orca 的所有窗口，等待约 5 秒。软件退出时会把剩余日志写入文件。

### 二、打包日志

日志保存在以下文件夹中，**只需打包 log 文件夹**：

| 系统 | 日志文件夹 |
| --- | --- |
| Windows | `%APPDATA%\Snapmaker_Orca\snapmaker_control\data\log` |
| macOS | `~/Library/Application Support/Snapmaker_Orca/snapmaker_control/data/log` |
| Linux | `~/.config/Snapmaker_Orca/snapmaker_control/data/log` |

打开 log 的上一级 data 文件夹后，通常会看到以下内容：

| 名称 | 说明 | 是否需要发送 |
| --- | --- | --- |
| `log` | 运行日志 | **需要** |
| `hive` | 软件本地数据，包含登录信息 | 不需要，请勿发送 |
| 其他文件或文件夹 | 运行状态文件等 | 不需要 |

log 文件夹中常见的文件：

- `snapmaker_control_2026-11-05.log` 这类带日期的文件：当天的日志。
- 以 `.log.gz` 结尾的文件：前几天的日志，已自动压缩，最多保留 7 天。
- `startup_error.txt`：只在软件启动失败时出现。

请根据您的电脑系统，选择下面对应的一节操作。

#### （一）Windows

**方式一：文件资源管理器（推荐）**

1. 按键盘上的 **Win + R**（Win 键即带 Windows 徽标的键），打开“运行”窗口。
2. 复制下面的路径，粘贴到“打开”输入框中，点击 **确定**：

   ```text
   %APPDATA%\Snapmaker_Orca\snapmaker_control\data
   ```

3. 系统会打开 data 文件夹，请确认其中有 log 文件夹。如果提示“Windows 找不到…”，请跳到[第四节](#四备用步骤找不到日志文件夹时)。
4. 右键单击 log 文件夹：
   - Windows 11：选择 **压缩为 ZIP 文件**；部分版本显示为 **压缩为… → ZIP 文件**。
   - Windows 10：选择 **发送到 → 压缩(zipped)文件夹**。
5. 同一文件夹中会生成 `log.zip`，将它拖到桌面，便于稍后发送。

**方式二：PowerShell**

1. 右键单击任务栏上的“开始”按钮，选择 **终端** 或 **Windows PowerShell**。
2. 复制以下命令，粘贴到窗口中，按回车：

   ```powershell
   Compress-Archive -Path "$env:APPDATA\Snapmaker_Orca\snapmaker_control\data\log" -DestinationPath "$([Environment]::GetFolderPath('Desktop'))\snapmaker_log.zip" -Force
   ```

3. 没有出现红色报错即表示成功，桌面会生成 `snapmaker_log.zip`。
4. 如果红色报错提示路径不存在，请跳到[第四节](#四备用步骤找不到日志文件夹时)；如果提示文件正被另一进程使用，请确认已关闭 Snapmaker Orca 后重试。

#### （二）macOS

macOS 自带 zip 压缩工具，无需安装任何软件。

**方式一：终端（推荐）**

1. 按 **Command + 空格** 打开“聚焦搜索”，输入“终端”，按回车打开。
2. 复制以下命令，粘贴到终端窗口中，按回车：

   ```bash
   rm -f ~/Desktop/snapmaker_log.zip && cd "$HOME/Library/Application Support/Snapmaker_Orca/snapmaker_control/data" && zip -r -q ~/Desktop/snapmaker_log.zip log -x "*.DS_Store" && open -R ~/Desktop/snapmaker_log.zip
   ```

3. 如果弹出“‘终端’想访问‘桌面’文件夹中的文件”，点击 **允许**。
4. 命令执行成功后，会自动打开访达窗口并选中桌面上的 `snapmaker_log.zip`。
5. 如果终端提示 `No such file or directory`，说明默认位置没有日志，请跳到[第四节](#四备用步骤找不到日志文件夹时)。

**方式二：访达（Finder）**

1. 点击程序坞中的 **访达** 图标。
2. 在屏幕顶部菜单栏选择 **前往 → 前往文件夹…**（快捷键 **Shift + Command + G**）。
3. 粘贴以下路径，按回车：

   ```text
   ~/Library/Application Support/Snapmaker_Orca/snapmaker_control/data
   ```

4. 确认窗口中有 log 文件夹。如果提示找不到该文件夹，请跳到[第四节](#四备用步骤找不到日志文件夹时)。
5. 按住 Control 键单击 log 文件夹（或在触控板上双指点按），选择 **压缩“log”**。
6. 同一文件夹中会生成 `log.zip`，将它拖到桌面，便于稍后发送。

#### （三）Linux

**方式一：终端（推荐）**

1. 按 **Ctrl + Alt + T** 打开终端，或在应用列表中搜索“终端 / Terminal”。
2. 复制以下命令，粘贴到终端中（终端内粘贴快捷键为 **Ctrl + Shift + V**），按回车：

   ```bash
   cd "${XDG_CONFIG_HOME:-$HOME/.config}/Snapmaker_Orca/snapmaker_control/data" && tar -czf ~/snapmaker_log.tar.gz log
   ```

3. 执行后没有任何输出即表示成功，个人主目录（Home）中会生成 `snapmaker_log.tar.gz`。
4. 如果提示 `No such file or directory`，请跳到[第四节](#四备用步骤找不到日志文件夹时)。

**方式二：文件管理器**

1. 打开“文件”（文件管理器），按 **Ctrl + L** 显示地址栏。
2. 输入以下路径，按回车（如果您设置过 `XDG_CONFIG_HOME`，请将 `~/.config` 替换为该目录）：

   ```text
   ~/.config/Snapmaker_Orca/snapmaker_control/data
   ```

3. 右键单击 log 文件夹，选择 **压缩…**，格式选择 `.zip`，点击 **创建**。
4. 同一文件夹中会生成 `log.zip`。

### 三、发送给售后

1. 将第二节生成的压缩包（`log.zip`、`snapmaker_log.zip` 或 `snapmaker_log.tar.gz`）作为附件发送给售后。
2. 同时在正文中填写以下信息（可直接复制）：

   ```text
   操作系统及版本：（例如 Windows 11 / macOS 15 / Ubuntu 24.04）
   Snapmaker Orca 版本：（菜单“帮助 → 关于”中查看）
   打印机型号：
   问题发生时间：（日期 + 时分）
   问题描述及复现步骤：
   ```

3. 如果出现过报错弹窗，请截图一并发送。

### 四、备用步骤：找不到日志文件夹时

> ⚠️ 仅当第二节提示路径不存在，或 data 文件夹中没有 log 文件夹时，才需要执行本节。已在第二节成功打包的，请忽略本节。

找不到日志文件夹，通常有以下两种原因：

- **本机尚未生成日志**：Snapmaker Orca 的设备功能从未在这台电脑上运行过。请打开 Snapmaker Orca，进入设备页面重现一次问题，然后回到第二节重新操作。
- **用户文件夹无法写入**：因权限受限或公司电脑安全策略等原因，软件改为把日志写到系统临时文件夹。请按下文从临时文件夹打包。

> ⚠️ 系统临时文件夹可能在电脑重启后被清空，请在重启前完成以下操作。

| 系统 | 临时文件夹中的日志 | 启动错误文件（可能没有） |
| --- | --- | --- |
| Windows | `%TEMP%\Snapmaker_Orca\snapmaker_control\data\log` | `%TEMP%\snapmaker_control_startup_error.txt` |
| macOS | `$TMPDIR/Snapmaker_Orca/snapmaker_control/data/log` | `$TMPDIR/snapmaker_control_startup_error.txt` |
| Linux | `/tmp/Snapmaker_Orca/snapmaker_control/data/log` | `/tmp/snapmaker_control_startup_error.txt` |

#### （一）Windows

1. 按 **Win + R**，粘贴以下路径，点击 **确定**：

   ```text
   %TEMP%\Snapmaker_Orca\snapmaker_control\data
   ```

2. 按第二节的方法右键压缩 log 文件夹，得到 `log.zip`。
3. 再按 **Win + R**，输入 `%TEMP%`，点击 **确定**。在打开的文件夹中查找 `snapmaker_control_startup_error.txt`，如果存在，与 `log.zip` 一并发送。

#### （二）macOS

1. 打开“终端”，粘贴以下命令，按回车：

   ```bash
   rm -f ~/Desktop/snapmaker_log_temp.zip && cd "$TMPDIR" && zip -r -q ~/Desktop/snapmaker_log_temp.zip Snapmaker_Orca/snapmaker_control/data/log $(ls snapmaker_control_startup_error.txt 2>/dev/null) -x "*.DS_Store" && open -R ~/Desktop/snapmaker_log_temp.zip
   ```

2. 桌面会生成 `snapmaker_log_temp.zip`，启动错误文件如果存在会自动包含在内。

#### （三）Linux

1. 打开终端，粘贴以下命令，按回车：

   ```bash
   cd "${TMPDIR:-/tmp}" && tar -czf ~/snapmaker_log_temp.tar.gz Snapmaker_Orca/snapmaker_control/data/log $(ls snapmaker_control_startup_error.txt 2>/dev/null)
   ```

2. 个人主目录中会生成 `snapmaker_log_temp.tar.gz`，启动错误文件如果存在会自动包含在内。

按第三节的要求将压缩包发送给售后。如果默认位置和临时文件夹都找不到日志，请直接联系售后，并说明已尝试的路径，附上报错提示的截图。
