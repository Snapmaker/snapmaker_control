# Snapmaker Control

**English** | [简体中文](README.zh-CN.md)

[![Latest release](https://img.shields.io/github/v/release/Snapmaker/snapmaker_control)](https://github.com/Snapmaker/snapmaker_control/releases/latest)
![Platforms](https://img.shields.io/badge/platform-macOS%20%7C%20Windows%20%7C%20Linux-lightgrey)

Snapmaker Control is the device connection and control program behind
**[Snapmaker Orca](https://github.com/Snapmaker/OrcaSlicer)**. It runs in the background, talks to your
printers, and serves the device pages shown inside Snapmaker Orca.

It also runs **on its own**: start it without Snapmaker Orca and use it in your web browser
as a standalone controller for the **Snapmaker U1**.

> This repository is the official distribution channel for Snapmaker Control binaries.
> It contains release packages, the license and third-party notices — not source code.

## Features

**Connect**
- Find Snapmaker U1 printers on your local network automatically, or add one by IP address
- Bind a printer with its PIN code; connect over your local network or remotely through your Snapmaker account
- Manage your printers: rename, remove or unbind, see connection status at a glance, and get notified when new firmware is available

**Live view**
- Watch the printer's camera live and switch the chamber light on or off
- Browse, preview, batch-download and delete timelapse videos

**Control**
- Set the nozzle temperature (per extruder) and the heated-bed temperature
- Control the chamber light, the cooling and chamber fans, and the air purifier (when installed)
- Adjust print speed while printing
- When idle: move the X/Y/Z axes, home, extrude or retract filament, pick or park a print head, raise or lower the bed

**Print jobs**
- See the current print with thumbnail, progress and remaining time
- Pause, resume or cancel a print
- Browse files on the printer's internal storage or USB drive and start a print
- Get alerted when the printer reports a fault

**Filament**
- See up to 4 filament slots and set each slot's color, brand and material

**AI monitoring**
- Turn print defect detection on or off and adjust its settings

**Home and account**
- Model recommendations from the Snapmaker model station, your printers, recent files and print history
- Sign in, register, or sign in with a third-party account

> Sending sliced files from the slicer and opening models from the model station require Snapmaker Orca.

## Download

Get the latest version from the [Releases](https://github.com/Snapmaker/snapmaker_control/releases/latest) page.

| Platform | Package |
|---|---|
| macOS (Apple silicon) | `snapmaker_control-<version>-macos-arm64.zip` |
| macOS (Intel) | `snapmaker_control-<version>-macos-x64.zip` |
| Windows (x64) | `snapmaker_control-<version>-windows-x64.zip` |
| Windows (ARM64) | `snapmaker_control-<version>-windows-arm64.zip` |
| Linux (x64) | `snapmaker_control-<version>-linux-x64.tar.gz` |
| Linux (arm64) | `snapmaker_control-<version>-linux-arm64.tar.gz` |

The macOS builds are signed with Snapmaker's Developer ID and notarized by Apple.
The Windows builds are signed with Snapmaker's code-signing certificate.

## Run it standalone

1. Download the package for your system and extract it.
   Keep the program and the `web` folder next to each other — the program will not start the web pages without it.
   ```
   snapmaker_control_<os>_<arch>[.exe]
   web/
   ```
2. Start the program:
   - **Windows / macOS**: double-click `snapmaker_control_…`.
   - **Linux**: run it from a terminal, e.g. `./snapmaker_control_linux_x64`.

   Your default browser opens the **Home** and **Device Control** pages automatically.

To stop the program, close the window it runs in (or press `Ctrl+C` in the terminal).

The web pages are served only to this computer (`127.0.0.1`); other devices on your network cannot open them.

### First run notes

- **Windows**: a Windows Defender Firewall prompt may appear the first time. Click **Allow** —
  the program uses mDNS to find printers on your local network. If you clicked **Cancel**,
  printers on your network will not show up until you allow
  `snapmaker_control_windows_*.exe` in *Windows Security → Firewall & network protection → Allow an app through firewall*.
- **macOS**: if macOS asks whether to allow incoming network connections or local network access, click **Allow** for the same reason.

## Use with Snapmaker Orca

Snapmaker Orca ships with Snapmaker Control and starts it for you. Nothing needs to be installed separately.

## Verify your download

Each release includes a `SHA256SUMS` file:

```bash
# macOS / Linux
shasum -a 256 -c SHA256SUMS --ignore-missing
```

```powershell
# Windows (PowerShell)
Get-FileHash .\snapmaker_control-<version>-windows-x64.zip -Algorithm SHA256
```

## Data and logs

Settings, the device list and logs are stored per user:

| OS | Location |
|---|---|
| Windows | `%APPDATA%\Snapmaker_Orca\snapmaker_control\` |
| macOS | `~/Library/Application Support/Snapmaker_Orca/snapmaker_control/` |
| Linux | `$XDG_CONFIG_HOME/Snapmaker_Orca/snapmaker_control/` (default `~/.config/…`) |

When reporting a problem, please attach the latest file from the `data/log/` folder there.

To uninstall, delete the extracted folder and, optionally, the data folder above.

## Command line

```bash
snapmaker_control --version     # print the version
snapmaker_control --help        # list all options
snapmaker_control --locale=zh-CN  # interface language and cloud region (default en-US)
```

## Feedback

Please report problems through [GitHub Issues](https://github.com/Snapmaker/snapmaker_control/issues).
Include your OS, the Snapmaker Control version (`--version`) and the log file.

## License

Snapmaker Control is proprietary software © Shenzhen Snapmaker Technologies Co., Ltd.,
distributed under the terms in [LICENSE.txt](LICENSE.txt).
Third-party components and their licenses are listed in [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt).
Snapmaker Orca is licensed separately under the GNU AGPL-3.0.
