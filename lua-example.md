---
title: "Lua Mod Example"
layout: default
description: "A worked Total Miner Lua example using blocks, inventory, NPCs, particles, and event scripts"
url: /lua-example.html
robots: noindex,follow
sitemap_exclude: true
---

<h1 align="center">Total Miner Lua Mod Example</h1>

<p align="center">
A beginner-friendly Lua example that combines the functions documented in the <a href="./lua-docs.html">Lua Scripting Reference</a>.
</p>

<p align="center">
This page demonstrates the structure and order of a small mod. Replace the placeholders with the values and callback data used by your mod.
</p>

---

## Table of contents

- [What This Example Does](#what-this-example-does)
- [Start a Mod Callback](#start-a-mod-callback)
- [Prepare a Reward Area](#prepare-a-reward-area)
- [Give an Item](#give-an-item)
- [Spawn an NPC and Effects](#spawn-an-npc-and-effects)
- [Attach an Event Script](#attach-an-event-script)
- [Learning Notes](#learning-notes)
- [Sources](#sources)

---

## What This Example Does

This example shows a simple reward encounter:

1. A callback displays a message.
2. A block is placed at a chosen map point.
3. The context actor receives an item.
4. An NPC and particle effect are created.
5. An event script is attached for later interaction.

The function names are taken from `lua-docs.md`. The argument placeholders are intentionally generic because the current reference documents function purposes but not every parameter signature.

## Start a Mod Callback

Use `mod_callback` when Lua needs to pass data to a mod callback.

```lua
-- Replace the callback name and data with values used by your mod.
mod_callback("RewardEncounter", "Frost encounter started")
notify("A frozen encounter has appeared")
```

## Prepare a Reward Area

The block functions can build or inspect a small area. Keep map coordinates in named values so the rest of the script is easy to change.

```lua
local reward_point = <map_point>
local reward_block = <block_id>
local reward_aux = <aux_data>

set_block(reward_point, reward_block, reward_aux)
```

To verify or inspect the result, use the corresponding getter documented on the reference page:

```lua
local placed_block = get_block(reward_point)
local light_level = get_block_light(reward_point)
```

## Give an Item

`add_inventory` changes the context actor's inventory. Use a positive quantity to add an item or a negative quantity to remove one when supported by the calling context.

```lua
local reward_item = <item_id>
local reward_count = 1

add_inventory(reward_item, reward_count)
notify("Reward received")
```

## Spawn an NPC and Effects

Use `spawn_npc` to create an NPC and `add_entity` when a general entity is needed. Particle functions can provide visual feedback.

```lua
spawn_npc(<npc_type>, reward_point)
particle(<particle_template>, reward_point)
sound(<sound_id>, reward_point)
```

Use the function names and argument order accepted by the in-game Lua environment when replacing the placeholders.

## Attach an Event Script

`set_event_script` assigns a script to an event. Keep event setup separate from the action code so it is easier to remove or replace later.

```lua
set_event_script(<event>, "RewardEncounterEvent")
```

A zone can also have scripts assigned with `set_zone_scripts`:

```lua
set_zone_scripts(<zone>, "RewardEncounterEnter", "RewardEncounterLeave")
```

## Learning Notes

- Start with one function and test it before combining systems.
- Keep coordinates, IDs, and counts in named values.
- Use the getter functions to verify changes while debugging.
- Use `notify` or `print` for temporary diagnostics.
- Confirm signatures and callback context in the game or the original Lua reference before publishing a mod.
- Command-based scripts and Lua scripts are separate systems. For command scripts, use the [Scripting Command Reference](./scripting.html).

## Sources

- [Original Total Miner Reference](https://totalminer.github.io/index)

---

[← Back to Lua Documentation](./lua-docs.html)

[← Back to Home](./)
