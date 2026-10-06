# RSR Classic Panel

A companion Dalamud plugin that restores the Rotation Solver Reborn **7.5.6.13 control panel** while using the installed RSR's current combat logic. Keep RSR installed and updated normally.

Requires **Dalamud API 15**, .NET 10, and Rotation Solver Reborn. The adapter's contracts were checked against **RSR 7.5.6.18**. Future changes to RSR or Dalamud internals may require updating this companion plugin.

## Install

Add this custom plugin repository under `/xlsettings` → Experimental → Custom Plugin Repositories:

```text
https://raw.githubusercontent.com/xxXKraysXxx/ffxiv_pluginsrepo/refs/heads/main/plug_repos.json
```

Open `/xlplugins`, find **RSR Classic Panel**, and install it. In RSR's own settings, disable **Show Control Window** to avoid two panels.

## Use

- `/rsrclassic`: show/hide the panel.
- `/rsrclassic config`: configure icon sizes, background, position locking and visibility.
- `/rsrclassic show` / `/rsrclassic hide`: explicitly show or hide it.
- `/rsrclassic retry`: reconnect after an RSR update or a connection error.
- Click **Targeting:** to cycle through the targeting modes configured in RSR, preserving Auto/Manual/Off. Modes controlled by another plugin, such as AutoDuty, still follow RSR's overrides.
- Click **AoE:** to cycle Off/Cleave/Full; click **Burst** to toggle automatic burst.

The original control layout, game icons, cooldown frames, charge indicators, special-state highlights/countdowns and action-click behavior are carried over from the pre-Material panel. The full RSR settings interface and the removed cooldown window are outside this addon's scope.

## Build

Install the .NET 10 SDK and have Dalamud API 15 libraries available locally. From this folder:

```powershell
.\build.ps1
# Or specify the folder containing Dalamud.dll:
.\build.ps1 -DalamudLibPath 'C:\path\to\Dalamud'
```

This project does not bundle or reference RSR or ECommons DLLs. The adapter locates the live RSR plugin and reads its current state; controls use RSR's existing commands and action methods. A broken connection disables the panel until it reconnects.

## Validation

Release compilation completed without warnings. The source bundle includes a test project with 29 checks for action execution/queuing, targeting cycling, settings, visibility and reload/failure handling. RSR 7.5.6.18 member signatures were verified against the installed binaries. These checks do not replace in-game visual and interaction testing.

## License and attribution

LGPL-3.0-or-later. Legacy renderer code is adapted from [RotationSolverReborn](https://github.com/FFXIV-CombatReborn/RotationSolverReborn/tree/7.5.6.13), copyright its contributors. `COPYING` and `COPYING.LESSER` contain the license texts. Source modifications include the standalone adapter, plugin lifecycle, panel settings and clickable targeting cycling. See `NOTICE.txt`.
