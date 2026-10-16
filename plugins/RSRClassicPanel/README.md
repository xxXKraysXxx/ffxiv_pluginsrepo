# RSR Classic Panel

A companion Dalamud plugin that restores the Rotation Solver Reborn **7.5.6.13 control panel** and **Lifestream's pre-badge travel overlay** while using the installed plugins' current logic. Keep RSR and Lifestream updated normally.

Requires **Dalamud API 15** and .NET 10. Each integration works independently with its original plugin installed. Contracts were checked against **RSR 7.5.6.21, 7.5.6.24 and 7.5.7.2**, and **Lifestream 2.6.0.6**. Older Lifestream versions that already use the classic overlay keep their own UI. Future upstream changes may require updating this companion plugin.

## Install

Add this custom plugin repository under `/xlsettings` → Experimental → Custom Plugin Repositories:

```text
https://raw.githubusercontent.com/xxXKraysXxx/ffxiv_pluginsrepo/refs/heads/main/plug_repos.json
```

Open `/xlplugins`, find **RSR Classic Panel**, and install it. In RSR's own settings, disable **Show Control Window** to avoid two panels.

## Use

- `/rsrclassic`: show/hide the panel.
- `/rsrclassic config`: configure RSR appearance and toggle the Lifestream replacement.
- `/rsrclassic show` / `/rsrclassic hide`: explicitly show or hide it.
- `/rsrclassic retry`: reconnect after an RSR update or a connection error.
- Click **Targeting:** to cycle through the targeting modes configured in RSR, preserving Auto/Manual/Off. Modes controlled by another plugin, such as AutoDuty, still follow RSR's overrides.
- Click **AoE:** to cycle Off/Cleave/Full; click **Burst** to toggle automatic burst.

The original RSR control layout, game icons, cooldown frames, charge indicators, special-state highlights/countdowns and action-click behavior are carried over from the pre-Material panel. The full RSR settings interface and the removed cooldown window are outside this addon's scope.

## Lifestream

**Enabled by default**, including when updating from an older version of this addon. Disable **Replace Lifestream badges with the classic overlay** in `/rsrclassic config` to restore Lifestream's normal UI.

- `/rsrclassic lifestream on` / `/rsrclassic lifestream off`: explicitly enable or disable replacement.
- `/rsrclassic lifestream`: toggle replacement.
- `/rsrclassic retry`: reconnect both integrations after an update or connection error.

Restores the old side-by-side aethernet, world-visit, housing-ward and instance columns. Residential destinations retain their main/subdivision columns; custom aethernet zones work too. Uses Lifestream's current aethernet renderer, context menus, favorites, renames, position and button-size settings. World and ward buttons call its current travel routines, including post-world aethernet teleports when configured for overlay clicks.

The new badge overlay is hidden while replacement is enabled. Turning replacement off or unloading this addon restores the original window and badges. Lifestream settings are not overwritten. If adapter binding or drawing fails, replacement stops and the original UI is restored. Lifestream's address book, settings, world-selection window and travel engine continue to work as provided by Lifestream. `/rsrclassic show` and `hide` only affect the RSR panel.

## Build

Install the .NET 10 SDK and have Dalamud API 15 libraries available locally. From this folder:

```powershell
.\build.ps1
# Or specify the folder containing Dalamud.dll:
.\build.ps1 -DalamudLibPath 'C:\path\to\Dalamud'
```

This project does not bundle or reference RSR, Lifestream, BadgeOverlay or ECommons DLLs. Adapters locate the live plugin assemblies and use their current state, renderers and actions. RSR and Lifestream failures are handled independently.

## Validation

Release compilation completed without warnings. The source bundle includes tests for RSR action execution/queuing, targeting cycling, settings, visibility and failure handling; Lifestream column selection, travel calls, secondary teleport timing, badge suppression and restoration; and window registration, repeated toggles, partial failures and unload cleanup. Tests cover both RSR action-queue signatures and bind all Lifestream adapter members against the shipped 2.6.0.6 binaries. These checks do not replace in-game visual and interaction testing.

```powershell
dotnet run --project ../RSRClassicPanel.Tests -c Release -p:DalamudLibPath='C:\path\to\Dalamud' -- 'C:\path\to\Lifestream-2.6.0.6' 'C:\path\to\Lifestream-2.5.4.23'
```

With both reference versions available, the suite runs 75 checks. Without binary folders it runs the executable behavior and lifecycle checks only.

## License and attribution

LGPL-3.0-or-later. Legacy renderer code is adapted from [RotationSolverReborn](https://github.com/FFXIV-CombatReborn/RotationSolverReborn/tree/7.5.6.13), copyright its contributors. `COPYING` and `COPYING.LESSER` contain the license texts. Source modifications include the standalone adapter, plugin lifecycle, panel settings and clickable targeting cycling. See `NOTICE.txt`.
