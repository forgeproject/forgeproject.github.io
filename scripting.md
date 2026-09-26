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
Total Miner's built-in, command-based scripting system — the commands used to script players, the world, NPCs, and game logic directly (for example, in map triggers), without writing a full mod.
</p>

<p align="center">
Looking for the Lua modding API instead? See the <a href="./lua-docs.html">Lua Scripting Reference</a>.
</p>

---

## Table of contents

- [Player Interaction](#player-interaction)
- [World & Environment](#world--environment)
- [Logic & Flow Control](#logic--flow-control)
- [Variables](#variables)
- [Triggers & Conditions](#triggers--conditions)
- [NPC Control](#npc-control)
- [Miscellaneous](#miscellaneous)

---

## Player Interaction

| Command | Definition |
|---|---|
| `Message("text")` | Displays a message to the player's screen. |
| `GiveItem(player, itemID, quantity)` | Gives the specified item to the player. |
| `RemoveItem(player, itemID, quantity)` | Removes an item from the player's inventory. |
| `Teleport(player, x, y, z)` | Moves the player to specific coordinates. |
| `SetHealth(player, value)` | Sets the player's health to a specific value. |
| `AddHealth(player, value)` | Adds health to the player. |
| `SetMana(player, value)` | Sets the player's mana level. |
| `AddMana(player, value)` | Adds mana to the player. |
| `SetXP(player, value)` | Sets the player's experience points. |
| `AddXP(player, value)` | Adds experience points to the player. |
| `SetLevel(player, skill, value)` | Sets the player's skill level. |
| `AddLevel(player, skill, value)` | Adds to the player's skill level. |

---

## World & Environment

| Command | Definition |
|---|---|
| `SetBlock(x, y, z, blockID)` | Places a block at coordinates. |
| `RemoveBlock(x, y, z)` | Removes a block at coordinates. |
| `SpawnNPC(npcType, x, y, z)` | Spawns an NPC at coordinates. |
| `KillNPC(npcID)` | Removes an NPC from the world. |
| `SetTime(value)` | Sets the world time (0–24000). |
| `SetWeather(type)` | Changes weather (e.g., Clear, Rain). |
| `PlaySound(soundID, x, y, z)` | Plays a sound at coordinates. |
| `SpawnParticle(particleID, x, y, z)` | Creates a particle effect. |

---

## Logic & Flow Control

| Command | Definition |
|---|---|
| `If(condition)` | Starts a conditional block. |
| `Else` | Executes if the `If` condition fails. |
| `EndIf` | Ends a conditional block. |
| `Loop(count)` | Repeats commands a set number of times. |
| `EndLoop` | Ends a loop block. |
| `Wait(ticks)` | Pauses script execution for a set time. |
| `Goto(label)` | Jumps to a labeled section of the script. |
| `Label(name)` | Marks a location for `Goto`. |

---

## Variables

| Command | Definition |
|---|---|
| `SetVar(name, value)` | Creates or updates a variable. |
| `AddVar(name, value)` | Adds to a variable's value. |
| `SubVar(name, value)` | Subtracts from a variable's value. |
| `IfVar(name, operator, value)` | Checks a variable against a value. |
| `GlobalVar(name, value)` | Creates a variable accessible across scripts. |

---

## Triggers & Conditions

| Command | Definition |
|---|---|
| `PlayerOnBlock(blockID)` | True if player is standing on a block. |
| `PlayerHasItem(itemID)` | True if player has an item. |
| `NPCNear(player, npcType, radius)` | True if NPC is near player. |
| `BlockExists(x, y, z)` | True if block exists at coordinates. |
| `TimeIs(value)` | True if world time matches value. |

---

## NPC Control

| Command | Definition |
|---|---|
| `SetNPCHealth(npcID, value)` | Sets NPC health. |
| `MoveNPC(npcID, x, y, z)` | Moves NPC to coordinates. |
| `NPCSay(npcID, "text")` | Makes NPC speak. |
| `NPCFollow(npcID, player)` | Makes NPC follow a player. |
| `NPCAttack(npcID, target)` | Makes NPC attack a target. |

---

## Miscellaneous

| Command | Definition |
|---|---|
| `SaveWorld()` | Saves the current world state. |
| `LoadWorld(name)` | Loads a saved world. |
| `KickPlayer(player)` | Removes a player from the game. |
| `BanPlayer(player)` | Bans a player from the server. |
| `UnbanPlayer(player)` | Removes ban from a player. |

---


---

[← Back to Home](./)
