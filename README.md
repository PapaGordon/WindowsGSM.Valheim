<p align="center">
  <img src="Valheim.cs/Valheim.png" alt="Valheim" width="128">
</p>

<h1 align="center">WindowsGSM.Valheim</h1>

<p align="center">
  Run a Valheim dedicated server with WindowsGSM.
</p>

<p align="center">
  <a href="https://github.com/PapaGordon/WindowsGSM/releases/latest"><img src="https://img.shields.io/badge/WindowsGSM-MeFriendos%20latest-38CDD4" alt="Latest MeFriendos WindowsGSM"></a>
  <a href="CHANGELOG.md"><img src="https://img.shields.io/badge/version-0.1.4-8802db" alt="Version 0.1.4"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License"></a>
</p>

This plugin installs and updates the Valheim dedicated server through SteamCMD and runs it from WindowsGSM. It's set up for a server on the normal Steam network, with or without BepInEx mods, and without Crossplay. It's based on [WindowsGSM.Valheim](https://github.com/Sarpendon/WindowsGSM.Valheim) by Sarpendon.

**Using our [MeFriendos WindowsGSM](https://github.com/PapaGordon/WindowsGSM)?** Then you don't need this plugin. Valheim is built in there, with the same code. Just pick **Valheim Dedicated Server** under **Install**. This plugin is for other WindowsGSM builds.

## What it does

- Installs and updates the server (Steam app `896660`). No Steam account needed.
- Passes server name, port and world from WindowsGSM to Valheim.
- Checks before every start that you've set a real password and didn't add `-crossplay` by accident.
- Works with BepInEx mods without any extra launcher.
- Shows the server output in **Embed Console**.
- Stops the server with CTRL+C, so the world gets saved, as Valheim recommends.
- Creates the `save-data` and `logs` folders when needed.

## Install

1. Download the ZIP from the [latest release](https://github.com/PapaGordon/WindowsGSM.Valheim/releases/latest).
2. Copy the whole `Valheim.cs` folder into `<WindowsGSM>\plugins\`.
3. Click **Reload Plugins** or restart WindowsGSM.
4. Pick **Valheim Dedicated Server** and click **Install**.
5. In the start parameters, replace `CHANGE_ME` with your server password. It needs at least 5 characters.
6. Open UDP ports `2456` and `2457` in the Windows firewall and on your router.
7. Start the server.

## Settings

| WindowsGSM field | Default | Passed to Valheim as |
| --- | --- | --- |
| Server Name | | `-name` |
| Server Port | `2456` (UDP) | `-port`. Valheim also uses the next port, `2457`. |
| Map | `Dedicated` | `-world`, the name of your world |

Valheim always allows up to 10 players. **Max Players** in WindowsGSM doesn't change that. Each new Valheim server in WindowsGSM gets ports 2 higher than the previous one.

New servers start with these parameters:

```text
-password "CHANGE_ME" -savedir ".\save-data" -public 1 -saveinterval 1800 -backups 4 -backupshort 7200 -backuplong 43200
```

That means: worlds are saved in `serverfiles\save-data`, the server is listed publicly, it saves every 30 minutes and keeps 4 automatic backups. The server won't start while the password is still `CHANGE_ME`, shorter than 5 characters or missing.

## Steam only, no Crossplay

This plugin is meant for the normal Steam network. Don't add `-crossplay`, the server refuses to start with it. Valheim needs the game port and the one after it, both UDP. With the defaults that's `2456` and `2457`. Valheim has no RCON, so there's no admin port to open.

## Mods with BepInEx

On Windows, BepInEx doesn't need a special launcher. Copy the contents of [BepInExPack Valheim](https://thunderstore.io/c/valheim/p/denikson/BepInExPack_Valheim/) straight into the server folder, so these sit next to `valheim_server.exe`:

```text
BepInEx\
doorstop_config.ini
winhttp.dll
```

BepInEx then loads automatically when the server starts.

If you built your mod list with r2modman or Thunderstore Mod Manager:

1. Test the profile with the same Valheim version as the server.
2. Open the profile folder.
3. Copy the server mods from `BepInEx\plugins`, `BepInEx\config` and, if needed, `BepInEx\patchers` into the same folders on the server.
4. Copy other files only if a mod says it needs them.
5. Leave client-only mods out, unless their description says they work on servers.
6. Start the server and check `BepInEx\LogOutput.log` and the WindowsGSM console.

If a mod opens its own admin port, keep it away from the internet and only allow it from your local network or a VPN.

## Updating

1. Stop the server.
2. Back up `save-data` and your complete BepInEx folder with configs.
3. Click **Update** in WindowsGSM.
4. Check that BepInExPack and all your mods support the new Valheim version.
5. Start the server and look for errors in the console and logs.

The plugin never installs, removes or updates mods. A Valheim update can break single mods even if BepInEx still loads.

## Console and stopping

With **Embed Console** on, the server output appears in WindowsGSM and Valheim's own window stays hidden. WindowsGSM then disables **Toggle Console**. Turn Embed Console off if you want Valheim's window instead. You can't type commands into the embedded console.

`-logFile` would send Valheim's output to a file instead of WindowsGSM. That's why it's not in the default parameters, and the plugin ignores it while Embed Console is on. With Embed Console off, `-logFile` works as usual.

**Stop** sends CTRL+C and gives Valheim 20 seconds to save and close. If that doesn't work, it tries again through the server window and waits 10 more seconds. Only then is the process ended.

## Firewall

The plugin doesn't create or remove firewall rules. Use WindowsGSM's **Auto Firewall** if your build has it, or open UDP `2456` and `2457` yourself (or your own port and the one after it). Router port forwarding is always up to you.

## Troubleshooting

**"Change the default Valheim password placeholder".** Replace `CHANGE_ME` in the start parameters with your password.

**"Valheim requires a server password of at least 5 characters".** Choose a longer password.

**"Remove -crossplay from Server Start Param".** This plugin only supports the Steam network.

**"Server Port must be a number between 1 and 65534".** Valheim also uses the next port, so 65535 doesn't work.

**Embed Console stops after a few Unity lines.** There's probably a `-logFile` in your start parameters. With Embed Console on it's ignored, but remove it anyway to keep things tidy.

**Players can't connect.** Check that the game port and the one after it are open over UDP and forwarded on your router.

**BepInEx doesn't load.** `winhttp.dll`, `doorstop_config.ini` and the `BepInEx` folder have to be in the same folder as `valheim_server.exe`. Then check `BepInEx\LogOutput.log`.

**The server doesn't start after a Valheim update.** Try without mods, or update BepInEx and your mods to versions for the new Valheim.

## Links

- [Releases](https://github.com/PapaGordon/WindowsGSM.Valheim/releases)
- [MeFriendos WindowsGSM](https://github.com/PapaGordon/WindowsGSM)
- [Original plugin by Sarpendon](https://github.com/Sarpendon/WindowsGSM.Valheim)
- [Valheim dedicated server guide](https://valheim.com/support/a-guide-to-dedicated-servers/)
- [BepInExPack Valheim on Thunderstore](https://thunderstore.io/c/valheim/p/denikson/BepInExPack_Valheim/)
- [MeFriendos](https://mefriendos.de)

This is a community plugin. It's not affiliated with or endorsed by Iron Gate, Coffee Stain Publishing, BepInEx, Thunderstore, Sarpendon or the WindowsGSM project. Valheim, BepInEx and mods are not included.

## License

The original plugin and this version are under the [MIT License](LICENSE). The original copyright notice stays in it. You can use, change and share the plugin, also commercially, as long as the copyright and license notice stay with it.
