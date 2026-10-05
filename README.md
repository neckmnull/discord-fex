<div align="center">

# Discord Fex

**A ready-to-use Windows bundle powered by `zapret` and WinDivert, with presets for Discord, YouTube, and other services.**

[![Windows](https://img.shields.io/badge/Windows-7%2F10%2F11-0078D4?logo=windows&logoColor=white)](#system-requirements)
[![zapret](https://img.shields.io/badge/zapret-win--bundle-6A5ACD)](https://github.com/bol-van/zapret-win-bundle)
[![Version](https://img.shields.io/badge/DiscordFix-9.3.0-5865F2?logo=discord&logoColor=white)](https://github.com/neckmnull/discord-fex/releases/latest)
[![Release](https://img.shields.io/github/v/release/neckmnull/discord-fex?display_name=tag&sort=semver)](https://github.com/neckmnull/discord-fex/releases/latest)

[Quick start](#quick-start) · [Presets](#main-presets) · [Windows service](#installing-as-a-windows-service) · [Troubleshooting](#troubleshooting) · [Security](#security)

</div>

> [!IMPORTANT]
> Extract the entire archive into a separate folder before running anything. Do not launch files directly from a ZIP archive.

## About

Discord Fex combines the Windows version of [zapret](https://github.com/bol-van/zapret), the [WinDivert](https://github.com/basil00/WinDivert) driver, domain lists, and ready-made DPI desynchronization strategies. The bundle includes presets for Discord, YouTube, Telegram, Twitch, Spotify, Steam, and other services.

This project is not a VPN or proxy. `winws.exe` processes selected network traffic locally through WinDivert. Strategy effectiveness depends on the ISP and current network conditions, so no single preset is guaranteed to work everywhere.

### Features

- ready-made profiles for Discord, YouTube, and combined use;
- alternative strategies for different ISPs;
- automatic preset discovery;
- installation of a selected strategy as a Windows service;
- game mode and domain-list management;
- `blockcheck` and built-in network diagnostics;
- archived presets from previous versions.

## System requirements

- Windows 10 or Windows 11; a separate installation script for Windows 7 is available under `bin/win7`;
- administrator privileges to load WinDivert and install a service;
- a fully extracted local copy of the repository;
- no conflicting network filtering software running at the same time, such as another zapret bundle, certain VPN clients, WARP, or similar tools.

## Quick start

1. Download the bundle from the [latest release](https://github.com/neckmnull/discord-fex/releases/latest), use **Code → Download ZIP**, or clone the repository:

   ```powershell
   git clone https://github.com/neckmnull/discord-fex.git
   cd discord-fex
   ```

2. If you downloaded an archive, extract it completely.
3. Close other zapret instances, VPN/WARP clients, and network-filtering applications.
4. Open the `pre-configs` directory.
5. Run the required BAT file as administrator:
   - `DiscordFix.bat` — Discord, including voice channels;
   - `YoutubeFix.bat` — YouTube;
   - `UltimateFix.bat` — combined configuration.
6. If the default profile does not work, try an `ALT` variant or an ISP-specific preset.

> [!TIP]
> Do not move individual files within the bundle. The BAT scripts use relative paths to `bin` and `lists`.

## Main presets

| File or group | Purpose |
| --- | --- |
| `DiscordFix*.bat` | Discord, including voice traffic |
| `YoutubeFix*.bat` | YouTube and Google Video |
| `UltimateFix*.bat` | Discord, YouTube, and an extended domain list |
| `general*.bat` | General-purpose strategies for custom lists |
| `discord-optimized.bat` | Optimized Discord profile |
| `discord-voice-only.bat` | Discord voice traffic only |
| `gaming.bat` | Gaming profile |
| `youtube-optimized.bat` | Optimized YouTube profile |
| `pre-configs/6.0` | Version 6.0 profiles for systems where newer strategies do not work |
| `pre-configs/_old` | Obsolete profiles, retained for troubleshooting only |

Results vary by ISP. Start with the profile without a suffix, then test `ALT` variants and profiles named after your provider.

## Installing as a Windows service

To run a strategy in the background:

1. run `service.bat` as administrator;
2. select **Install as Service** and choose a configuration;
3. verify the result with **Check Status**.

Use **Remove Services** in the same menu to uninstall it. The root directory also contains `Установить как службу в АВТОЗАПУСК v2.exe`, a graphical utility based on [bat_autorunner](https://github.com/Priler/bat_autorunner).

## Additional tools

Some bundled filenames are in Russian because they are retained from their upstream distributions. Renaming them is not recommended.

| Tool | Purpose |
| --- | --- |
| `service.bat` | Manages the service, list updates, tests, and the Discord cache |
| `blockcheck.cmd` | Runs the `blockcheck` strategy discovery tool |
| `switch_game_mode.cmd` | Enables or disables the gaming port range |
| `АВТО-ПОИСК пре-конфига*.exe` | Automatically tests bundled presets |
| `НАСТРОИТЬ список доменов.exe` | Builds a custom domain selection |
| `ОБНОВИТЬ сборку.exe` | Checks for bundle updates |
| `utils/test zapret.ps1` | Runs network tests and stores results locally |

## Troubleshooting

### The window opens and immediately closes

1. Make sure the archive was fully extracted.
2. Confirm that `bin/winws.exe`, `bin/WinDivert.dll`, and `bin/WinDivert64.sys` exist.
3. Run `service.bat` and select **Run Diagnostics**.
4. Check whether another service or copy of `winws.exe` is already running.
5. Review antivirus notifications and verify a suspicious file by hash before adding an exclusion.

### Discord works, but voice channels do not

- use `DiscordFix.bat` or `UltimateFix.bat`, not a TCP-only profile;
- select **Update hosts file (for Discord voice)** in `service.bat`;
- confirm that UDP is not blocked by the router, VPN, or a third-party firewall.

### None of the bundled strategies work

1. Run `АВТО-ПОИСК пре-конфига (бета v2).exe`.
2. Run `blockcheck.cmd` and save the working parameters.
3. Try the profiles under `pre-configs/6.0`.
4. Consult the [zapret documentation](https://github.com/bol-van/zapret/tree/master/docs).

## Repository structure

```text
discord-fex/
├── bin/            # winws, WinDivert, blockcheck, Cygwin, and support files
├── lists/          # domain lists, IP lists, and WinDivert filters
├── pre-configs/    # ready-made BAT configurations
├── utils/          # tests and supporting data
├── service.bat     # service management and diagnostics
├── blockcheck.cmd  # strategy discovery
└── README.md
```

## Security

> [!WARNING]
> This project changes how network traffic is processed and loads the WinDivert system driver. Run it only if you understand the role of these components.

- Some bundled EXE files may not have a digital signature. Verify their source and SHA-256 hash before running them.
- Do not disable Windows security entirely. If a file is detected, compare it with the corresponding upstream project and analyze it with multiple tools first.
- The file `Запустить майнер.exe` is described by the original bundle documentation as the [AlbanianVirus](https://github.com/Priler/AlbanianVirus) joke program. It is **not required** for zapret to work.
- Review diagnostic reports before sharing them because they may contain information about your network.
- See [SECURITY.md](SECURITY.md) for the complete policy.

## Third-party components

This bundle contains material from several independent projects:

- [bol-van/zapret](https://github.com/bol-van/zapret)
- [bol-van/zapret-win-bundle](https://github.com/bol-van/zapret-win-bundle)
- [basil00/WinDivert](https://github.com/basil00/WinDivert)
- [Priler/bat_autorunner](https://github.com/Priler/bat_autorunner)
- [Priler/zapret_preconfigs_tester](https://github.com/Priler/zapret_preconfigs_tester)
- [Priler/zapret_domains_selector](https://github.com/Priler/zapret_domains_selector)
- [Flowseal/zapret-discord-youtube](https://github.com/Flowseal/zapret-discord-youtube)
- [Priler/discordfix_autoupdate](https://github.com/Priler/discordfix_autoupdate)
- [V3nilla/IPSets-For-Bypass-in-Russia](https://github.com/V3nilla/IPSets-For-Bypass-in-Russia)

See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for attribution and licensing notes. The original extended instructions remain available in [`2. ПРОЧТИ_МЕНЯ.txt`](2.%20ПРОЧТИ_МЕНЯ.txt).

## Legal notice

Use this project only in accordance with applicable law and the rules of your network. The repository is provided “as is,” without any guarantee that a particular service will be available. Rights to third-party components remain with their respective authors; determine the license for each component from its upstream project.