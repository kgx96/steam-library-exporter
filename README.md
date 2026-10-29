# Steam Library Exporter

Export every game you own on Steam to a **TXT** list or a **CSV** spreadsheet, with hours played and last-played dates. Windows app with a simple window, and a command-line mode for scripts.

**By KGX PRODUCTIONS**

---

## Download

Get **`SteamLibraryExporter.exe`** from the [Releases](../../releases) page. It is a single file with nothing to install. Put it in any folder and run it.

**Requirements**

- Windows 10 or 11 (64-bit)
- Microsoft Edge (built into Windows) or Google Chrome. The program's window is shown through it.
- A Steam Web API key (free; see below)
- Your Steam profile's **Game details** set to **Public**

## Getting an API key

1. Go to https://steamcommunity.com/dev/apikey and sign in.
2. Enter any domain name (for example `localhost`), agree, and register.
3. Copy the 32-character key.

Treat the key like a password. You can revoke it on the same page at any time.

## Using the app

Double-click `SteamLibraryExporter.exe`.

1. **Steam Web API key**: paste your key. Tick **Remember key on this PC** if you don't want to paste it every time.
2. **Steam profile**: any of these work:
   - SteamID64: `76561198000000000`
   - Profile URL: `https://steamcommunity.com/profiles/76561198000000000`
   - Custom URL: `https://steamcommunity.com/id/yourname` or just `yourname`
3. **Output**: pick the folder and file name (**Browse…** opens the Windows Save dialog), choose **TXT**, **CSV**, or both, and choose the sort order.
4. Click **EXPORT**.

After exporting you can:

- **Rename file…**: rename the exported file(s). The extension is kept, and the TXT and CSV are renamed together.
- **Open folder**: open the folder with the file selected.
- **Filter games**: search the list shown in the window.

Your settings are remembered for next time. Closing the window exits the program.

### Output formats

**TXT**
```
Steam library for 76561198000000000
Owned games: 412   Total hours: 3021.4

AppID         Hours  Name
---------- --------  ----------------------------------------
105600        500.0  Terraria
427410        102.1  Abiotic Factor
```

**CSV** columns: `AppID, Name, HoursPlayed, LastPlayed, StoreURL`. The file is UTF-8 with BOM, so Excel shows non-English game names correctly.

## Command-line mode

Pass any arguments and the program runs in the console instead of opening a window.

```
SteamLibraryExporter.exe --key <API_KEY> --user <SteamID64 | profile URL | custom name> [options]
```

| Option | Default | Description |
|---|---|---|
| `--key` | | Steam Web API key. If omitted, the `STEAM_API_KEY` environment variable is used. |
| `--user` | *(required)* | SteamID64, profile URL, or custom URL name |
| `--out` | `owned_games` | Output path **without extension** (folder + base name) |
| `--format` | `txt` | `txt`, `csv`, or `both` |
| `--sort` | `name` | `name` or `hours` |
| `--version` | | Print the version |
| `--help` | | Show help |

Examples:
```
SteamLibraryExporter.exe --key XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX --user 76561198000000000
SteamLibraryExporter.exe --user yourname --format both --sort hours --out "D:\Exports\my_games"
```

Exit codes: `0` success, `1` bad arguments, `2` Steam/API error, `3` file write error.

## Privacy and security

- Your API key is sent only to Valve's official API (`api.steampowered.com`). Nothing is sent anywhere else, and there is no telemetry.
- The window is a local page served by the program itself on `127.0.0.1` (your own PC only). Each launch uses a random access token, so other programs and websites can't use it.
- **Remember key** stores the key encrypted with Windows DPAPI, readable only by your Windows user account. Without the tick, the key is never saved.
- Settings are stored in `%APPDATA%\KGX\Steam Library Exporter\config.json`. Delete that folder to reset everything.

## Troubleshooting

| Message | Fix |
|---|---|
| *Steam returned no game data* | Steam → Profile → Edit Profile → Privacy Settings → set **Game details** to **Public**. |
| *Steam rejected the API key* | The key is wrong or revoked. Generate a new one. |
| *No Steam profile found for custom URL* | Check the custom URL name, or use your SteamID64. |
| *Windows protected your PC* (SmartScreen) | The exe isn't code-signed. Click **More info → Run anyway**. |
| Antivirus flags the exe | A known false positive with unsigned programs. Download only from this repository's Releases. |
| The window doesn't open | Install or repair Microsoft Edge, or run the program from Command Prompt to see the local address and open it in any browser. |

## License

Free to download and use. Source code is not published. See [LICENSE](LICENSE).

Not affiliated with or endorsed by Valve Corporation. Steam and the Steam logo are trademarks of Valve Corporation.

© KGX PRODUCTIONS 2026
