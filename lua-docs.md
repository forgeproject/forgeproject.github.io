---
title: "Lua Documentation"
layout: default
description: "Lua modding API reference for Total Miner — for mod-level hooks, not the built-in command scripting system"
url: /lua-docs.html
robots: noindex,follow
sitemap_exclude: true
---

<p align="center">
  <a href="https://forgeproject.net">
	<img src="https://i.postimg.cc/SJpSBRNH/logo.png" alt="ForgeProject Logo" />
  </a>
</p>

<h1 align="center">Total Miner Lua API Reference</h1>

<p align="center">
Complete guide to Total Miner's Lua modding API — classes, methods, hooks, and data types for building mods that go beyond what the built-in command scripting can do.
</p>

<p align="center">
Looking for the simpler, built-in command scripting used for map triggers instead? See the <a href="./scripting.html">Scripting Command Reference</a>.
</p>

---

## Table of contents

- [Overview](#overview)
- [Core Interfaces](#core-interfaces)
- [Hooks](#hooks)
- [Data Types](#data-types)
- [Examples](#examples)
- [Best Practices](#best-practices)

---

## Overview

The Total Miner Lua API provides access to game internals through interfaces and events. Your Lua scripts can:

- Access and modify game state (players, actors, maps)
- Respond to game events through hooks
- Create custom gameplay behaviors
- Control the game world

Lua is the language behind Total Miner's modding API — a level below the built-in [command scripting](./scripting.html), and what the [Mods](./mods.html) on this site are built with.

---

## Core Interfaces

### ITMGame

Main interface for accessing game state and world information.

**Key Properties:**
- `Players` - Array of all players
- `World` - Current world data
- `Map` - Current map instance

**Key Methods:**
- `SpawnActor(type, position)` - Create a new actor
- `PrintToChat(message)` - Send message to all players

---

### ITMPlayer

Represents a player character.

**Key Properties:**
- `Name` - Player's username
- `Position` - Vector3 position
- `Health` - Current health (0-20)
- `MaxHealth` - Maximum health value
- `IsAlive` - Whether player is alive
- `IsPlayer` - Always true for players

**Key Methods:**
- `Damage(amount)` - Deal damage to player
- `Heal(amount)` - Restore player health
- `SetPosition(vec3)` - Teleport player
- `PrintToChat(message)` - Send private message

---

### ITMActor

Represents a non-player character or creature.

**Key Properties:**
- `Type` - Actor type (Zombie, Skeleton, Spider, etc)
- `Position` - Vector3 position
- `Health` - Current health
- `MaxHealth` - Maximum health
- `IsAlive` - Alive status
- `IsPlayer` - Always false for actors

**Key Methods:**
- `Damage(amount)` - Deal damage
- `Kill()` - Destroy actor
- `PlayAnimation(name)` - Play animation
- `SetPosition(vec3)` - Set actor location

---

### ITMMap

Interact with the map and terrain.

**Key Properties:**
- `Width` - Map width in blocks
- `Height` - Map height in blocks
- `Depth` - Map depth in blocks
- `Gravity` - Current gravity value

**Key Methods:**
- `GetBlock(x, y, z)` - Get block data
- `SetBlock(x, y, z, block)` - Set block data
- `ExplodeAt(position, power)` - Create explosion
- `GetEntitiesInRegion(bounds)` - Find entities in area

---

## Hooks

Hooks allow your Lua code to respond to game events. Define a function with the hook name and it will be called automatically.

### GameLoopHook()

Called every frame for continuous logic. Use for animations, updates, and real-time checks.

```lua
function GameLoopHook()
	-- Runs every frame
	if Game.Players[1] then
		print("Player is in game")
	end
end
```

---

### ModifyDamageDealtHook(info)

Called when damage is dealt. Modify damage or prevent it.

**StrikeInfo Properties:**
- `Attacker` - Entity dealing damage
- `Target` - Entity taking damage
- `DamageDealt` - Damage amount (can modify)
- `DamageType` - Type of damage

Return the modified info, or `false` to cancel.

```lua
function ModifyDamageDealtHook(info)
	if info.Attacker.IsPlayer then
		info.DamageDealt = info.DamageDealt * 2
	end
	return info
end
```

---

### ModifyDamageTakenHook(info)

Called when entity receives damage. Reduce or negate damage.

```lua
function ModifyDamageTakenHook(info)
	if info.Target.IsPlayer then
		info.DamageDealt = math.floor(info.DamageDealt * 0.5)
	end
	return info
end
```

---

### ActorSpawnedHook(actor)

Called when a new actor spawns. Modify properties immediately.

```lua
function ActorSpawnedHook(actor)
	if actor.Type == "Zombie" then
		actor.MaxHealth = 100
	end
end
```

---

### ActorDestroyedHook(actor)

Called when an actor is destroyed.

```lua
function ActorDestroyedHook(actor)
	print(actor.Name .. " was destroyed")
end
```

---

### PlayerInputHook(player, input)

Called when player presses input. Can modify or block input.

**Return values:**
- Return input string to allow
- Return `false` to cancel

```lua
function PlayerInputHook(player, input)
	if input == "Sprint" then
		return false  -- Disable sprinting
	end
	return input
end
```

---

### PlayerMovedHook(player)

Called when player moves. Track movement or apply effects.

```lua
function PlayerMovedHook(player)
	if player.Position.Y < 0 then
		player.SetPosition(Vector3.new(0, 50, 0))
	end
end
```

---

## Data Types

### Vector3

3D coordinate or direction vector.

**Properties:**
- `X` - X coordinate
- `Y` - Y coordinate
- `Z` - Z coordinate

**Usage:**
```lua
local pos = Vector3.new(10, 20, 30)
local distance = Vector3.Distance(pos1, pos2)
```

### StrikeInfo

Information about a damage event.

**Properties:**
- `Attacker` - Entity dealing damage
- `Target` - Entity taking damage
- `DamageDealt` - Damage amount
- `DamageType` - Type of damage
- `IsHit` - Whether attack connected

### ItemInfo

Information about an item.

**Properties:**
- `Type` - Item type
- `Quantity` - Stack quantity
- `Durability` - Item durability

---

## Examples

### Double Player Damage

```lua
function ModifyDamageDealtHook(info)
	if info.Attacker.IsPlayer and not info.Target.IsPlayer then
		info.DamageDealt = info.DamageDealt * 2
	end
	return info
end
```

### Healing on Kill

```lua
function ActorDestroyedHook(actor)
	if Game.Players[1] then
		local player = Game.Players[1]
		player.Heal(10)
	end
end
```

### Prevent Player Damage

```lua
function ModifyDamageTakenHook(info)
	if info.Target.IsPlayer then
		return false  -- Players take no damage
	end
	return info
end
```

### Movement Boost

```lua
function PlayerInputHook(player, input)
	if input == "Sprint" then
		player.Velocity.X = player.Velocity.X * 1.5
		player.Velocity.Z = player.Velocity.Z * 1.5
	end
	return input
end
```

### Teleport on Fall

```lua
function PlayerMovedHook(player)
	if player.Position.Y < 0 then
		player.SetPosition(Vector3.new(0, 50, 0))
		player.PrintToChat("You fell too far!")
	end
end
```

---

## Best Practices

1. **Check entity types** - Always verify if something is a player or actor
2. **Handle missing entities** - Check `if entity then` before using
3. **Use math functions** - Use `math.floor()` for damage values
4. **Return modified data** - Always return from modifying hooks
5. **Avoid infinite loops** - Don't trigger hooks from within hooks
6. **Cache references** - Store commonly used objects
7. **Minimize frame logic** - Keep `GameLoopHook()` lightweight

---

## Troubleshooting

**Hook not firing?**
- Check function name spelling exactly
- Verify your script is loaded
- Ensure entity type matches your check

**NullReferenceException?**
- Entity was destroyed or removed
- Always check before using

**Syntax errors?**
- Check Lua syntax carefully
- Look for missing parentheses or brackets

**Performance issues?**
- Minimize work in `GameLoopHook()`
- Cache results when possible
- Avoid expensive operations in loops

---

**Building a mod?** Browse the [Mods](./mods.html) page for scripts that use these hooks, or the [Mod Installation Guide](./mod-installation.html) to load one in-game. For general gameplay guidance (not scripting), see the [Tutorials](./tutorials.html).
