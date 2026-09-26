---
title: "Lua Documentation"
layout: default
description: "Total Miner Lua scripting function reference — blocks, entities, inventory, zones, and more"
url: /lua-docs.html
robots: noindex,follow
sitemap_exclude: true
---

<h1 align="center">Total Miner Lua API Reference</h1>

<p align="center">
Complete function reference for Total Miner's Lua scripting API, organized by category.
</p>

---

## Table of contents

- [Blocks](#blocks)
- [Blueprints](#blueprints)
- [CCTV](#cctv)
- [Effects](#effects)
- [Entities](#entities)
- [GUI](#gui)
- [History](#history)
- [HUD](#hud)
- [Inventory](#inventory)
- [Intersect](#intersect)
- [Items](#items)
- [Miscellaneous](#miscellaneous)
- [NPCs](#npcs)
- [Particles](#particles)
- [Permissions](#permissions)
- [Pickups](#pickups)
- [Power](#power)
- [Scripts](#scripts)
- [Skills](#skills)
- [Sound](#sound)
- [Timer](#timer)
- [Tints](#tints)
- [Topdown Map](#topdown-map)
- [Weather](#weather)
- [Zones](#zones)
- [Getters](#getters)

---

## Blocks

Functions to manipulate blocks.

- **`add_flying_block`** — Add a falling block at the map point.
- **`copy_block`** — Copy block data (block id, aux, light) from one map point to another.
- **`copy_region`** — Copy block data (block id, aux, light) from one cubic region to another.
- **`get_aux`** — Get the aux data at a map point.
- **`get_block`** — Get the block id at a map point.
- **`move_block`** — Move block data (block id, aux, light) from one map point to another.
- **`move_region`** — Move block data (block id, aux, light) from one cubic region to another.
- **`paste`** — Paste a component.
- **`replace_region`** — Replace a block id with another block id in a cubic region.
- **`clear_block`** — Clears block id at the map point.
- **`set_block`** — Set block id and aux data at a map point.
- **`set_block_script`** — Assign a script to a block at a map point.
- **`set_falling_block`** — Set the block at the map point to be a falling block.
- **`set_region`** — Set block id in a cubic region.
- **`set_region_aux`** — Set aux data in a cubic region.
- **`set_sphere`** — Set block id in a spherical region.
- **`set_text`** — Set the text of a block (Sign, Book etc).
- **`set_texture`** — Set a block's visible texture.
- **`get_block_info`** — Get various world data of a block.
- **`get_block_light`** — Get the amount of block emitted light at a map point.

---

## Blueprints

Functions to manipulate blueprints.

- **`blueprint`** — Define a blueprint (crafting recipe) for an item.
- **`blueprint_material`** — Define the material for a blueprint (crafting recipe) slot.

---

## CCTV

- **`cctv`** — Open a CCTV (directional) for the context player.
- **`cctv_at`** — Open a CCTV (targeted) for the context player.
- **`cctv_exit`** — Close the CCTV for the context player.

---

## Effects

Functions to manipulate effects.

- **`add_health_effect`** — Add an effect which increases or decreases the context actor's health over time.
- **`add_health_effect_history`** — Add an effect which increases or decreases the context actor's health over time.
- **`remove_effect`** — Remove a character effect.
- **`set_health_modifier`** — Set the health regeneration rate for the context actor.

---

## Entities

Functions to manipulate entities.

- **`add_entity`** — Add (spawn) a single entity.

---

## GUI

Functions to manipulate GUI.

- **`input`** — Display an input field and wait for user input.
- **`input_num`** — Display an input number dialog and wait for user input.
- **`menu`** — Display a menu (list of items) and wait for user input (item selection).
- **`msgbox`** — Display a message box and wait for user input.
- **`notify`** — Post a notification to the screen.
- **`open_block`** — Open a block's interface screen.
- **`print`** — Post a notification to the screen.

---

## History

Functions to manipulate history.

- **`get_history`** — Get a value from the context player's history.
- **`get_clan_history`** — Get a value from the context player's clan history.
- **`get_sys_history`** — Get a value from system history.
- **`add_history`** — Add or subtract a value to/from the context player's history.
- **`add_clan_history`** — Add or subtract a value to/from the context player's clan's history.
- **`add_sys_history`** — Add or subtract a value to/from system history.
- **`clear_history`** — Clear (remove) a key from the context player's history.
- **`clear_clan_history`** — Clear (remove) a key from the context player's clan's history.
- **`clear_sys_history`** — Clear (remove) a key from system history.
- **`set_history`** — Set a value in the context player's history.
- **`set_clan_history`** — Set a value in the context player's clan's history.
- **`set_sys_history`** — Set a value in system history.

---

## HUD

Functions to manipulate HUD.

- **`hud_bar`** — Add a hud bar. Hud bars are a form of progress bar.
- **`hud_counter`** — Add a hud counter. A hud counter is a form of text progress counter.
- **`hud_shape`** — Add a hud shape.
- **`hud_text`** — Add hud text.
- **`remove_hud`** — Remove a hud element.
- **`set_nameplate`** — Set nameplate options.
- **`show_player_hud`** — Show / Hide the player's HUD — HotBar, Compass, Reticle, other HUD info panels. Same as HUD: ON/OFF on the Pause → Options Menu.

---

## Inventory

Functions to manipulate inventory.

- **`add_inventory`** — Add or subtract a quantity of an item to/from the context actor's inventory.
- **`add_block_inventory`** — Add or subtract a quantity of an item to/from a block's inventory.
- **`add_region_inventory`** — Add or subtract a quantity of an item to/from all block inventories in a cubic region.
- **`can_equip`** — Query whether or not the context actor can equip an item.
- **`clear_inventory`** — Clear (remove) an item from the context actor's inventory.
- **`clear_block_inventory`** — Clear (remove) an item from a block's inventory.
- **`clear_region_inventory`** — Clear (remove) an item from all block inventories in a cubic region.
- **`copy_inventory`** — Copy a block's inventory to another block.
- **`copy_inventory_region`** — Copy all block inventories in a cubic region to another region.
- **`equip`** — Cause the context actor to equip an item.
- **`get_block_inventory`** — Get the total count of an item in a block's inventory.
- **`get_inventory`** — Get the total count of an item in the context actor's inventory.
- **`move_inventory`** — Move (transfer) a block inventory to another block.
- **`move_inventory_from`** — Move (transfer) a block's inventory to the context actor's inventory.
- **`move_inventory_to`** — Move (transfer) the context actor's inventory to a block's inventory.
- **`move_inventory_region`** — Move (transfer) all block inventories in a cubic region to another region.
- **`unequip`** — Unequip an item.

---

## Intersect

Functions to manipulate intersect.

- **`intersect_box`** — Box (cubic region) intersection query.
- **`intersect_frustum`** — Frustum intersection query.
- **`intersect_ray`** — Ray intersection query.
- **`intersect_sphere`** — Sphere intersection query.

---

## Items

Functions to manipulate items.

- **`enable_item`** — Enable or disable an item.
- **`set_item`** — Set the name and description for an item.

---

## Miscellaneous

- **`is_item_type`** — Gets the specified item type.
- **`is_item_subtype`** — Gets the specified item subtype.
- **`is_item_class`** — Gets the specified item class.
- **`cave_in`** — Start a cave in.
- **`commit`** — Force a chunk mesh update.
- **`explosion`** — Create an explosion.
- **`is_chance`** — A dice query (same as `is_random`).
- **`is_cursor_valid`** — Queries if the context actor cursor is currently targeting a block.
- **`is_random`** — A dice query (same as `is_chance`).
- **`mod_callback`** — A Mod callback. Call this function to pass string data to a mod.
- **`set_random_seed`** — Change the seed for the random number generator.
- **`set_clan`** — Assign the context player's clan.
- **`set_context`** — Set the script context.
- **`set_reach`** — Set the reach of the context actor.
- **`teleport`** — Teleport the player.
- **`teleport_all`** — Teleport all actors in a cubic region.

---

## NPCs

Functions to manipulate NPCs.

- **`add_npc_health_region`** — Add or subtract to/from the health of all NPCs in a cubic region.
- **`add_npc_health_target`** — Add or subtract to/from the target NPC's health.
- **`add_npc_health_zone`** — Add or subtract to/from the health of all NPCs in a zone.
- **`set_behaviour`** — Set a behaviour tree for the context actor.
- **`set_dialog`** — Set a dialog tree for the context actor.
- **`set_npc_state_region`** — Set the state of all NPCs in a cubic region.
- **`set_npc_state_target`** — Set the state of the target NPC.
- **`set_npc_state_zone`** — Set the state of all NPCs in a zone.
- **`spawn_npc`** — Spawn an NPC (Non Player Character).

---

## Particles

Functions to manipulate particles.

- **`add_particle`** — Add (emit) a single particle.
- **`add_particle_emitter`** — Add a Particle Emitter.

---

## Permissions

Functions to manipulate permissions.

- **`set_permission`** — Set a single permission for the context player.
- **`set_permissions_all`** — Set permissions for the context player.
- **`has_permission`** — Query if the context player has a particular permission.

---

## Pickups

Functions to manipulate pickups.

- **`add_pickup`** — Spawn a pickup item.
- **`remove_pickups`** — Remove all pickups from the world.

---

## Power

Functions to manipulate power.

- **`set_power`** — Set a block's power state (on or off).
- **`set_switch`** — Set a switch's on/off position.
- **`toggle_switch`** — Toggle a switch's on/off position.

---

## Scripts

Functions to manipulate scripts.

- **`cancel_script`** — Cancel a running script.
- **`remove_event_script`** — Function undefined.
- **`require`** — Load a library.
- **`set_event_script`** — Set a script to execute on an event.
- **`set_event_button_script`** — Set a script to execute on a button press event.
- **`script`** — Call a script.

---

## Skills

Functions to manipulate skills.

- **`add_skill_level`** — Raise or lower a skill level of the context actor.
- **`add_skill_xp`** — Increase or decrease skill xp of the context actor.
- **`set_skill_level`** — Set a skill level for the context actor.
- **`set_skill_xp`** — Set xp for a skill for the context actor.

---

## Sound

Functions to manipulate sound.

- **`play_sound`** — Play a sound at a map point.
- **`play_sound_loop`** — Play a looped sound at a map point.
- **`play_sound_in_region`** — Play a sound in a cubic region.
- **`play_sound_loop_in_region`** — Play a looped sound in a cubic region.
- **`play_sound_in_zone`** — Play a sound in a zone.
- **`play_sound_loop_in_zone`** — Play a looped sound in a zone.
- **`remove_sound`** — Remove a sound from a map point.
- **`remove_sound_in_region`** — Remove a sound from a cubic region.
- **`remove_sound_in_zone`** — Remove a sound from a zone.

---

## Timer

Functions to manipulate timer.

- **`timer_reset`** — Reset the internal script timer to zero.
- **`timer_start`** — Start the internal script timer.
- **`timer_stop`** — Stop (pause) the internal script timer.
- **`get_timer`** — Read the current elapsed time in milliseconds from the internal script timer.

---

## Tints

Functions to manipulate tints.

- **`sky_color`** — Set the global sky color.
- **`sky_color_player`** — Set the context sky color.
- **`sky_color_remove`** — Remove the current global sky color.
- **`sky_color_remove_player`** — Remove the current context sky color.
- **`tint_color`** — Set the global tint color.
- **`tint_color_player`** — Set the context tint color.
- **`tint_color_remove`** — Remove the current global tint color.
- **`tint_color_remove_player`** — Remove the current context tint color.

---

## Topdown Map

Functions to manipulate the topdown map.

- **`add_marker`** — Add a marker to the top down map.
- **`remove_marker`** — Remove a marker from the top down map.
- **`remove_waypoint`** — Remove the current waypoint.
- **`set_waypoint`** — Set a waypoint for the context player.
- **`has_marker`** — Query if a marker exists.

---

## Weather

Functions to manipulate weather.

- **`fog`** — Add fog.
- **`fog_delete`** — Delete fog.
- **`hail`** — Add hail.
- **`hail_delete`** — Delete hail.
- **`rain`** — Add rain.
- **`rain_delete`** — Delete rain.

---

## Zones

Functions to manipulate zones. Use zones to control the properties of cubic regions of the world.

- **`add_zone`** — Add a new zone.
- **`set_zone_region`** — Change the region of an existing zone.
- **`set_zone_builder`** — Adds or clears zone builders.
- **`set_zone_types`** — Set a zone's types.
- **`set_zone_props`** — Set a zone's properties.
- **`set_zone_scripts`** — Set a zone's scripts.
- **`set_temp_zone_region`** — Change the region of an existing temp zone.
- **`set_temp_zone_types`** — Set a temp zone's types.
- **`set_temp_zone_props`** — Set a temp zone's properties.
- **`remove_zone`** — Remove a zone.
- **`remove_temp_zone`** — Remove a temp zone.

---

## Getters

General getter functions.

- **`get_zone_region`** — Get the region of a specified existing zone.
- **`get_item_type`** — Get the type of the specified item.
- **`get_item_subtype`** — Get the subtype of the specified item.
- **`get_item_class`** — Get the class of the specified item.
- **`get_action_count`** — Get the number of actions the context actor has performed.
- **`get_actor_name`** — Get the name of the context actor.
- **`get_clan_name`** — Get the clan name of the context actor.
- **`get_cursor_point`** — Get the world point of the context actor block cursor.
- **`get_cursor_face`** — Get the face of the block targeted by the context actor block cursor.
- **`get_cursor_distance`** — Get the distance to the block targeted by the context actor block cursor.
- **`get_eye_pos`** — Get the current world eye position of the context actor (camera position).
- **`get_gamer_count`** — Get the total number of valid gamers in the session.
- **`get_gamer_count_in_radius`** — Get the total number of enabled gamers currently positioned inside a spherical region.
- **`get_gamer_count_in_region`** — Get the total number of enabled gamers currently positioned inside a cubic region.
- **`get_gamer_count_in_zone`** — Get the total number of enabled gamers currently positioned inside a zone.
- **`get_hash_code`** — Get the hash code of a string.
- **`get_health`** — Get the current health of the context actor.
- **`get_health_as_percent`** — Get the current health of the context actor as a percentage (0–100%) of its maximum health.
- **`get_utc`** — Returns the current UTC time.
- **`get_hour`** — Get the current game hour from the 24 hour day clock.
- **`get_item`** — Get an equipped or event raising item.
- **`get_item_name`** — Get the name of an item.
- **`get_item_desc`** — Get the description of an item.
- **`get_light`** — Get full light data of a map point.
- **`get_max_health`** — Get the maximum health of the context actor.
- **`get_max_oxygen`** — Get the maximum oxygen of the context actor.
- **`get_max_stamina`** — Get the maximum stamina of the context actor.
- **`get_npc_count`** — Get the total number of NPCs in the world.
- **`get_npc_count_in_radius`** — Get the total number of NPCs currently positioned inside a spherical region.
- **`get_npc_count_in_region`** — Get the total number of NPCs currently positioned inside a cubic region.
- **`get_npc_count_in_zone`** — Get the total number of NPCs currently positioned inside a zone.
- **`get_oxygen`** — Get the current oxygen of the context actor.
- **`get_oxygen_as_percent`** — Get the current oxygen of the context actor as a percentage (0–100%) of its maximum oxygen.
- **`get_permission`** — Query if the context player has a particular permission.
- **`get_placement_point`** — Get the world point where a block would be placed by the context actor.
- **`get_point`** — Get the current world point of the context actor.
- **`get_pos`** — Get the current world position of the context actor.
- **`get_random_pos`** — Get a random position within a circle.
- **`get_random`** — Get a random number.
- **`get_reach`** — Get the reach of the context actor.
- **`get_script_offset`** — Get the map point offset of the script block that executed the current script.
- **`get_script_point`** — Get the map point of the script block that executed the current script.
- **`get_skill_level`** — Get the current level of a specified skill of the context actor.
- **`get_skill_xp`** — Get the current xp of a specified skill of the context actor.
- **`get_stamina`** — Get the current stamina of the context actor.
- **`get_stamina_as_percent`** — Get the current stamina of the context actor as a percentage (0–100%) of its maximum stamina.
- **`get_stat_bonus`** — Get the stat bonus for a skill.
- **`get_sun_light`** — Get the amount of sunlight at a world point.
- **`get_texture`** — Get the currently assigned texture id for a block.
- **`get_velocity`** — Get the current world velocity of the context actor.
- **`get_view_dir`** — Get the current view direction of the context actor.
- **`get_viewport_width`** — Get the viewport width (in pixels).
- **`get_viewport_height`** — Get the viewport height (in pixels).
- **`get_actor_avatar`** — Get the avatar of the context actor.
- **`get_text`** — Get the text of a block (Sign, Book, etc).
