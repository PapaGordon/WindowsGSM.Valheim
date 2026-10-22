MeFriendos WindowsGSM Valheim Plugin 0.1.3
==========================================

INSTALL
-------
1. Copy the complete Valheim.cs folder into:
   <WindowsGSM>\plugins\Valheim.cs

2. Reload plugins or restart WindowsGSM.

3. Install "Valheim Dedicated Server".

4. Change the default password in Server Start Param.
   The plugin intentionally refuses to start with CHANGE_ME.

5. Do not add -crossplay. This MeFriendos build uses the Steam backend.

6. Open/forward only the required Valheim game ports for the configured
   game port and game port +1. Defaults:

   UDP 2456-2457

   Valheim has no built-in RCON port.

DEFAULT PARAMETERS
------------------
-password "CHANGE_ME" -savedir ".\save-data" -public 1 -saveinterval 1800 -backups 4 -backupshort 7200 -backuplong 43200

EMBEDDED CONSOLE
----------------
Version 0.1.1 removes -logFile from the default parameters so Valheim's live
runtime output remains available to the WindowsGSM embedded console.

If an existing 0.1.0 server still has -logFile in Server Start Param, the
plugin filters that argument from the actual Valheim launch command while
Embed Console is enabled. The saved WindowsGSM configuration is not modified.

When Embed Console is disabled, a manually configured -logFile argument is
left untouched and can still be used normally.

BEPINEX / MODDED SERVER
-----------------------
For Windows, install the current BepInExPack_Valheim contents directly into
Valheim's serverfiles root. The following must be beside valheim_server.exe:

   BepInEx\
   doorstop_config.ini
   winhttp.dll

No special Windows launch wrapper is needed. BepInEx loads through Doorstop
when WindowsGSM starts valheim_server.exe.

For r2modman / Thunderstore profiles, copy only server-compatible mod files
and configuration into the matching BepInEx folders on the dedicated server.
Always check each mod's server requirements.

FIREWALL
--------
Firewall management follows WindowsGSM's per-server Auto Firewall setting.
The plugin does not create, remove or inspect firewall rules and does not block startup for a plugin firewall check.

Use MeFriendos WindowsGSM v1.25.3.0 with Auto Firewall:
https://github.com/PapaGordon/WindowsGSM/releases/tag/v1.25.3.0
For manual port rules, turn Auto Firewall off for this server in WindowsGSM and configure the required ports yourself. Router forwarding remains separate.

SHUTDOWN
--------
Valheim should be stopped with CTRL+C. The plugin attempts CTRL+C first and
uses forced termination only as a final fallback.

PROJECT
-------
https://github.com/PapaGordon/WindowsGSM.Valheim-MeFriendos
