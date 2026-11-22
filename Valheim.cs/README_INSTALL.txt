WindowsGSM.Valheim 0.1.4
========================

Runs a Valheim dedicated server with WindowsGSM.

If you use MeFriendos WindowsGSM, you don't need this plugin.
Valheim is already built in there.

Install
-------
1. Copy this whole Valheim.cs folder into the "plugins" folder of WindowsGSM.
2. Click "Reload Plugins" or restart WindowsGSM.
3. Pick "Valheim Dedicated Server" and click Install.
   No Steam account needed.
4. In the start parameters, replace CHANGE_ME with your server password
   (at least 5 characters). The server won't start before you do.
5. Open UDP 2456 and 2457 in your firewall and on your router.
6. Start the server.

Good to know
------------
- Server Name, Server Port and Map (world name) are passed to Valheim.
- Don't add -crossplay. This plugin is for the normal Steam network.
- Mods: copy BepInExPack Valheim into the server folder, so BepInEx\,
  doorstop_config.ini and winhttp.dll are next to valheim_server.exe.
- Stop sends CTRL+C so the world gets saved.

Full guide: https://github.com/PapaGordon/WindowsGSM.Valheim

Based on WindowsGSM.Valheim by Sarpendon.
MeFriendos build by PapaGordon. https://mefriendos.de
