---
layout: default
title: Lua API Reference
permalink: /lua-api/
---

# Total Miner Lua API Reference

Welcome to the comprehensive Lua scripting reference for **Total Miner**. This guide covers everything you need to know about scripting in Total Miner using Lua, including all available classes, methods, hooks, and examples.

## Quick Navigation

- **[Complete API Reference](./complete-reference.html)** — Full interactive documentation with all classes and methods
- **[Quick Reference Card](./quick-reference.html)** — Printable quick lookup guide
- **[API Guide](./api-guide.md)** — Structured guide to all available APIs

## Getting Started

### What is Lua in Total Miner?

Total Miner allows you to extend and customize gameplay using Lua scripting. The game provides a rich API that lets you:

- Access and modify game state (players, actors, maps)
- Respond to game events through hooks
- Create custom gameplay behaviors
- Interact with the game world

### Basic Example

```lua
-- A simple hook that runs when a player strikes an actor
function ModifyDamageDealtHook(info)
	if info.Attacker.IsPlayer then
		-- Double damage dealt by players
		info.DamageDealt = info.DamageDealt * 2
	end
	return info
end
```

## Main API Components

### **ITMGame**
Access to core game state and world information.

- Get/set world properties
- Access players and actors
- Manage items and inventory
- Control map behavior

### **ITMPlayer**  
Interact with player entities.

- Player position, velocity, health
- Inventory and equipment
- Movement and animation
- Input and interaction

### **ITMActor**
Control non-player characters and creatures.

- Movement and pathfinding
- Health and damage
- Animation states
- Behavior and triggers

### **ITMMap**
Interact with the map and terrain.

- Block manipulation
- Gravity and physics
- Map data and dimensions
- Lighting and rendering

### **Hooks**
React to game events and modify gameplay.

- Damage calculation hooks
- Actor spawning and behavior
- Player input and movement
- Rendering and timing

## Data Types

The API uses several common data types:

- **Vector3** — 3D position/direction (X, Y, Z)
- **StrikeInfo** — Damage and combat information
- **ItemInfo** — Item stack data
- **ActorInfo** — Actor state information

## Getting Help

- Browse the [Complete Reference](./complete-reference.html) for detailed documentation
- Check the [Quick Reference Card](./quick-reference.html) for common patterns
- See examples below for typical use cases

## Common Patterns

### Listen to a Hook

```lua
function GameLoopHook()
	-- This runs every frame
	-- Use for continuous logic
end
```

### Check Player Status

```lua
function ModifyDamageDealtHook(info)
	local player = info.Attacker
	if player.Health < 5 then
		print("Player is low health!")
	end
	return info
end
```

### Modify Damage

```lua
function ModifyDamageDealtHook(info)
	info.DamageDealt = math.floor(info.DamageDealt * 1.5)
	return info
end
```

## File Manifest

| File | Purpose |
|------|---------|
| `complete-reference.html` | Full interactive API documentation |
| `quick-reference.html` | Printable quick lookup card |
| `api-guide.md` | Detailed API guide |

## Next Steps

1. **Explore the [Complete Reference](./complete-reference.html)** — Get detailed information about every available class and method
2. **Try the examples** — Copy and modify examples to learn how the API works
3. **Check the [Quick Reference](./quick-reference.html)** — Use it as a handy lookup while coding

---

**Total Miner** is available on [Steam](https://store.steampowered.com/app/347600/Total_Miner/).

*This documentation is community-maintained for the Total Miner modding community.*
