---
title: "Lua Documentation"
layout: default
description: "Lua scripting reference for Total Miner"
url: /lua-docs.html
robots: noindex,follow
sitemap_exclude: true
---


# Total Miner Lua API - Complete Guide

## Overview

The Total Miner Lua API provides access to game internals through a collection of interfaces and classes. This guide documents all available components.

## Core Interfaces

### ITMGame

The main interface for accessing game state.

**Key Properties:**
- `Players` — Array of all players in the game
- `World` — Current world data
- `Map` — Current map instance

**Key Methods:**
- `GetActor(id)` — Get an actor by ID
- `SpawnActor(type, position)` — Create a new actor
- `GetBlockAt(position)` — Get block data at a position
- `SetBlockAt(position, block)` — Set a block in the world

### ITMPlayer

Represents a player character.

**Key Properties:**
- `Position` — Vector3 of player location
- `Health` — Current health (0-20)
- `Velocity` — Vector3 of movement speed
- `Inventory` — Player's inventory

**Key Methods:**
- `Damage(amount)` — Deal damage to player
- `Heal(amount)` — Restore health
- `SetPosition(vec3)` — Teleport player
- `GetEquippedItem()` — Get held item

### ITMActor

Represents a non-player character or creature.

**Key Properties:**
- `Position` — Vector3 of actor location
- `Health` — Current actor health
- `Type` — Actor type (Zombie, Skeleton, etc.)
- `IsAlive` — Whether actor is alive

**Key Methods:**
- `Damage(amount)` — Deal damage to actor
- `Kill()` — Destroy the actor
- `MoveTo(position)` — Command actor to move
- `PlayAnimation(name)` — Play an animation

### ITMMap

Interact with the map and terrain.

**Key Properties:**
- `Width` — Map width in blocks
- `Height` — Map height in blocks
- `Gravity` — Current gravity value

**Key Methods:**
- `GetBlock(x, y)` — Get block at coordinates
- `SetBlock(x, y, block)` — Set block at coordinates
- `GetEntitiesInRegion(bounds)` — Find entities in area
- `ExplodeAt(position, power)` — Create an explosion

## Hooks

Hooks allow your Lua code to respond to game events. Define a function with the hook name and it will be called automatically.

### Game Loop Hooks

**GameLoopHook()**
- Called every frame
- Use for continuous logic or updates

```lua
function GameLoopHook()
	-- Runs every frame
	-- Good for polling input, animations, etc.
end
```

### Damage Hooks

**ModifyDamageDealtHook(info)**
- Called when damage is dealt
- Allows modification of damage amount
- Return modified info

```lua
function ModifyDamageDealtHook(info)
	-- info contains: Attacker, Target, DamageDealt, etc.
	info.DamageDealt = info.DamageDealt * 2  -- Double damage
	return info
end
```

**ModifyDamageTakenHook(info)**
- Called when entity takes damage
- Allows reduction or negation of damage
- Return modified info

```lua
function ModifyDamageTakenHook(info)
	if info.Target.IsPlayer then
		info.DamageDealt = 0  -- Players take no damage
	end
	return info
end
```

### Actor Hooks

**ActorSpawnedHook(actor)**
- Called when a new actor spawns
- Modify actor properties immediately after spawn

```lua
function ActorSpawnedHook(actor)
	if actor.Type == "Zombie" then
		actor.Health = 100  -- Make zombies tougher
	end
end
```

**ActorDestroyedHook(actor)**
- Called when an actor is destroyed
- Log events, drop items, etc.

```lua
function ActorDestroyedHook(actor)
	-- Actor is being destroyed
end
```

### Player Hooks

**PlayerInputHook(player, input)**
- Called when player presses input
- Can modify or block input
- Return modified input or false to cancel

```lua
function PlayerInputHook(player, input)
	if input == "Jump" then
		-- Prevent jumping
		return false
	end
	return input
end
```

**PlayerMovedHook(player)**
- Called when player moves
- Track player movement, apply effects, etc.

```lua
function PlayerMovedHook(player)
	-- Player has moved
end
```

## Data Types

### Vector3

3D coordinate/direction vector.

**Properties:**
- `X` — X coordinate
- `Y` — Y coordinate  
- `Z` — Z coordinate

**Usage:**
```lua
local pos = Vector3.new(10, 20, 30)
local distance = Vector3.Distance(pos1, pos2)
```

### StrikeInfo

Information about a damage event.

**Properties:**
- `Attacker` — Entity dealing damage (Player or Actor)
- `Target` — Entity taking damage
- `DamageDealt` — Damage amount (can modify)
- `DamageType` — Type of damage
- `IsHit` — Whether attack connected

### ItemInfo

Information about an item.

**Properties:**
- `Type` — Item type identifier
- `Quantity` — Stack quantity
- `Durability` — Item durability (tools)
- `MetaData` — Custom data

### ActorInfo

Information about an actor.

**Properties:**
- `Type` — Actor type name
- `Position` — Vector3 position
- `Health` — Current health
- `IsAlive` — Alive status

## Common Patterns

### Damage Modification

```lua
function ModifyDamageDealtHook(info)
	-- Only player-vs-actor damage
	if info.Attacker.IsPlayer and not info.Target.IsPlayer then
		info.DamageDealt = math.floor(info.DamageDealt * 1.25)
	end
	return info
end
```

### Healing on Kill

```lua
function ActorDestroyedHook(actor)
	if actor.Killer and actor.Killer.IsPlayer then
		actor.Killer.Heal(5)  -- Heal 5 HP on kill
	end
end
```

### Movement Restriction

```lua
function PlayerInputHook(player, input)
	if input == "Move" then
		-- Prevent movement
		return false
	end
	return input
end
```

### Spawn Prevention

```lua
local BANNED_MOBS = {"Zombie", "Skeleton"}

function ActorSpawnedHook(actor)
	for _, banned in ipairs(BANNED_MOBS) do
		if actor.Type == banned then
			actor.Health = 0  -- Kill immediately
			return
		end
	end
end
```

### Event Logging

```lua
function ModifyDamageDealtHook(info)
	print(string.format(
		"%s dealt %d damage to %s",
		info.Attacker.Name,
		info.DamageDealt,
		info.Target.Name
	))
	return info
end
```

## Best Practices

1. **Check entity types** — Always verify if something is a player or actor
2. **Handle edge cases** — Entities might be dead or removed
3. **Use math.floor()** — Damage should be whole numbers
4. **Avoid infinite loops** — Don't modify hooks from within hooks
5. **Return modified data** — Always return info from modifying hooks
6. **Test thoroughly** — Lua changes can break gameplay

## Troubleshooting

**Hook not firing?**
- Check function name spelling exactly
- Make sure your script is loaded before the game event
- Verify the entity type matches your check

**Syntax errors?**
- Check Lua syntax carefully
- Look for missing commas, parentheses, etc.
- Use a Lua linter to find issues

**Performance issues?**
- Minimize work in GameLoopHook
- Cache results when possible
- Avoid excessive entity lookups

---

*See the [Quick Reference Card](./quick-reference.html) for a printable lookup guide.*
