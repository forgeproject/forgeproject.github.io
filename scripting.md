---
title: "Scripting Command Reference"
layout: default
description: "Total Miner's built-in command-based scripting reference — player, world, logic, variable, trigger, and NPC commands"
url: /scripting.html
robots: noindex,follow
sitemap_exclude: true
---

<p align="center">
  <a href="https://forgeproject.net">
    <img src="https://i.postimg.cc/SJpSBRNH/logo.png" alt="ForgeProject Logo" />
  </a>
</p>

<h1 align="center">Total Miner Scripting Command Reference</h1>

<p align="center">
Total Miner's built-in command-based scripting system for players, the world, NPCs, and game logic.
</p>

<p align="center">
<a href="./lua-docs.html">Lua</a> · <a href="./scripting.html">Command Scripting</a> · <a href="./xml-docs.html">XML Modding</a>
</p>

---

## Table of contents

- [Start Here](#start-here)
- [How Scripts Work](#how-scripts-work)
- [Common Script Patterns](#common-script-patterns)
- [Worked Example](#worked-example)
- [Command Reference](#command-reference)
  - [Flow and Execution](#flow-and-execution)
  - [Blocks and Regions](#blocks-and-regions)
  - [World Queries](#world-queries)
  - [NPCs and Actors](#npcs-and-actors)
  - [Items, Inventory, and Skills](#items-inventory-and-skills)
  - [Conditions and Variables](#conditions-and-variables)
  - [HUD, Menus, and Permissions](#hud-menus-and-permissions)
  - [Effects and World Presentation](#effects-and-world-presentation)
  - [History, Clans, and Callbacks](#history-clans-and-callbacks)
  - [Runtime and Lua Interop](#runtime-and-lua-interop)
- [Sources](#sources)

---

## Start Here

Total Miner scripts are made from commands. A command performs an action, tests a condition, changes a value, or controls what runs next. Scripts can be attached to map events, blocks, zones, and other game systems.

The easiest way to learn is:

1. Start with one action, such as `Notify`, `SetBlock`, `Sound`, or `Teleport`.
2. Add `Wait` when an action needs to happen later.
3. Add a condition such as `IsBlock`, `HasItemData`, or `IsInZone`.
4. Use `Else`, `Endif`, `Loop`, or `Exit` to control the result.
5. Test the script in a copy of the map before attaching it to a live event.

> **Important:** Use the in-game script editor to confirm each command's parameter order, required values, and context.

## How Scripts Work

### Commands

Commands are listed here by their engine names, for example `SetBlock` and `NpcSpawn`. Names are case-sensitive in this reference. A command may require a player, actor, map point, region, item, block, or other context supplied by the event that started the script.

### Values and context

Common values include coordinates, block IDs, item IDs, NPC types, numbers, text, and variable names. The same command can behave differently depending on whether it runs from a player event, block event, NPC event, zone, or system script.

### Conditions and branches

Condition commands test game state. Put the commands that should run when the condition succeeds inside the corresponding conditional block, then close it with `Endif`.

### Variables

`Var` is the variable command described in this reference. Variable names and operations must be entered using the syntax accepted by the in-game editor. Do not assume that older names such as `SetVar`, `AddVar`, or `GlobalVar` are literal engine commands.

## Common Script Patterns

The following patterns are for learning and show the intent of a script. Replace argument placeholders with the form shown by the in-game script editor.

### Action followed by a delay

```text
Notify("The door will open")
Wait(<delay>)
OpenBlock(<door>)
```

### Conditional action

```text
IsBlock(<point>, <block>)
    Notify("The required block is present")
Else
    Notify("The required block is missing")
Endif
```

### Repeated action

```text
Loop(<count>)
    Particle(<effect>, <point>)
    Wait(<delay>)
<loop terminator>
```

The loop terminator should be selected from the command offered by the editor. It is shown as a placeholder here because the exact loop-closing syntax should be confirmed in the editor.

## Worked Example

For a complete beginner-friendly command script, see the [Scripting Example](./scripting-example.html).

## Command Reference

The following commands are grouped by their primary purpose, although some commands can be used in more than one context.

### Flow and Execution

| Command | Use |
|---|---|
| `Behaviour`, `Context` | Control or inspect script execution context. |
| `Else`, `Endif` | Select an alternate branch and close a conditional block. |
| `Exit` | Stop the current script path. |
| `InlineLua` | Run Lua from a command script. |
| `Loop` | Repeat a script section. |
| `Nop` | Perform no action. |
| `Script` | Invoke or work with a script. |
| `Wait` | Delay subsequent commands. |

### Blocks and Regions

`CopyBlock`, `CopyRegion`, `MoveBlock`, `MoveRegion`, `Paste`, `ReplaceRegion`, `SetBlock`, `SetBlockScript`, `SetEventScript`, `SetRegion`, `SetRegionAux`, `SetSphere`, `SetSwitch`, `SetText`, `SetTexture`

Use these commands for individual blocks, cubic regions, block metadata, scripts attached to blocks, switches, and event scripts.

### World Queries

`CaveIn`, `Explosion`, `Fog`, `Hail`, `Intersect`, `IsBlock`, `IsBlockDeliveringPower`, `IsBlockEdited`, `IsBlockLightSource`, `IsBlockOpen`, `IsBlockOre`, `IsBlockPassable`, `IsBlockReceivingPower`, `IsBlockResistance`, `IsBlockSolid`, `IsBlockTexture`, `OpenBlock`, `SetPower`

These commands inspect or change block state, power, lighting, weather effects, explosions, and other world conditions.

### NPCs and Actors

`HasActor`, `NpcHealth`, `NpcSpawn`, `NpcState`, `SetNameplate`

Use `NpcSpawn` for spawning, `NpcHealth` for health changes, and `NpcState` for NPC state operations. `HasActor` tests whether the required actor context exists.

### Items, Inventory, and Skills

`CanEquip`, `Equip`, `Inventory`, `Item`, `Pickup`, `Unequip`, `SetItemData`, `HasInventory`, `HasItemData`, `HasSkill`, `HasStatBonus`, `Health`, `HealthMod`, `Skill`, `SkillXP`

These commands cover equipment, item data, inventory, health, skills, skill experience, and related checks.

### Conditions and Variables

`HasAction`, `HasHistory`, `HasMarker`, `HasPermission`, `IsAvatar`, `IsClan`, `IsClock`, `IsCombat`, `IsDayTime`, `IsDistance`, `IsEquipped`, `IsFiniteResources`, `IsGamerCount`, `IsInZone`, `IsLight`, `IsNameplate`, `IsNightTime`, `IsNpcCount`, `IsRandom`, `IsSkills`, `IsTime`, `IsVar`, `Random`, `Var`

Use these commands to test game state, permissions, time, distance, zones, history, and variables. `Random` can be used when a script needs nondeterministic behavior.

### HUD, Menus, and Permissions

`HUDBar`, `HUDCounter`, `HUDShape`, `HUDText`, `Input`, `Menu`, `MessageBox`, `Notify`, `Permission`, `Kick`, `SetReach`

These commands provide player-facing messages and interfaces, HUD elements, permission checks, player removal, and reach settings.

### Effects and World Presentation

`Particle`, `ParticleEmitter`, `Rain`, `SetHour`, `SkyColor`, `Sound`, `Teleport`, `TintColor`

These commands control particles, particle emitters, weather, time, sound, sky color, tints, and movement.

### History, Clans, and Callbacks

`CCTV`, `Clan`, `Commit`, `History`, `Marker`, `ModCallback`, `Waypoint`, `Zone`

These commands work with history, clans, CCTV, markers, waypoints, zones, and callbacks. `SetBlockScript` and `SetEventScript` are listed under [Blocks and Regions](#blocks-and-regions) because they attach scripts to game objects and events.

### Runtime and Lua Interop

Runtime operations include `QueueScript`, `ExecuteScript`, `CancelScript`, and `GetListOfQueuedScripts`. `InlineLua` connects command scripts to the Lua API.

For Lua functions covering blocks, inventory, NPCs, zones, history, HUD, and events, see the [Lua Scripting Reference](./lua-docs.html).

---

## Sources

- [Original Total Miner Reference](https://totalminer.github.io/index)

---

[← Back to Home](./)
