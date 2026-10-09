---
title: "Scripting Command Example"
layout: default
description: "A beginner-friendly Total Miner command-scripting example using conditions, blocks, NPCs, effects, and events"
url: /scripting-example.html
robots: noindex,follow
sitemap_exclude: true
---

<h1 align="center">Total Miner Scripting Command Example</h1>

<p align="center">
A worked command-scripting example using the commands documented in the <a href="./scripting.html">Scripting Command Reference</a>.
</p>

<p align="center">
This example uses an event-triggered reward shrine. Replace the placeholders with the values and syntax offered by the in-game script editor.
</p>

---

## Table of contents

- [What This Example Does](#what-this-example-does)
- [Basic Event Script](#basic-event-script)
- [Check a Requirement](#check-a-requirement)
- [Build the Reward Sequence](#build-the-reward-sequence)
- [Add an NPC Encounter](#add-an-npc-encounter)
- [Attach the Script](#attach-the-script)
- [Learning Notes](#learning-notes)
- [Sources](#sources)

---

## What This Example Does

This example demonstrates a small shrine encounter:

1. The event checks whether the required block is present.
2. The player receives a notification when the shrine is activated.
3. A reward block is placed after a delay.
4. A particle effect and sound provide feedback.
5. An NPC can be spawned as a guardian.
6. The event is assigned to a block with `SetBlockScript`.

The command names are used by the command-scripting system. Argument order and event-specific values must be confirmed in the in-game editor.

## Basic Event Script

Start with a short action so you can verify that the event is connected correctly.

```text
Notify("The shrine is active")
```

If the notification appears when the event runs, add the rest of the sequence one section at a time.

## Check a Requirement

Use a condition before changing the world. The point and block arguments below are placeholders.

```text
IsBlock(<shrine_point>, <required_block>)
	Notify("The shrine accepts the offering")
Else
	Notify("The shrine is missing its required block")
Endif
```

Keep the condition and its result together. This makes it easier to see what happens when the requirement is not met.

## Build the Reward Sequence

Add a delay, place the reward block, and show visual and audio feedback.

```text
IsBlock(<shrine_point>, <required_block>)
	Notify("The reward is charging")
	Wait(<delay>)
	SetBlock(<reward_point>, <reward_block>)
	Particle(<particle_effect>, <reward_point>)
	Sound(<sound_id>, <reward_point>)
Else
	Notify("The shrine is missing its required block")
Endif
```

The editor may require additional arguments for block auxiliary data, particle settings, or sound position. Use the editor's command form rather than guessing those values.

## Add an NPC Encounter

Once the basic reward works, add an NPC guardian.

```text
NpcSpawn(<npc_type>, <guardian_point>)
NpcState(<npc>, <state>)
```

Test the NPC separately before adding it to the full event. This makes it easier to identify whether a problem comes from the event, the spawn position, or the NPC values.

## Attach the Script

Attach the finished script to the event source. For a block-based shrine, use `SetBlockScript`.

```text
SetBlockScript(<shrine_point>, "RewardShrineEvent")
```

For another event type, use the matching event command offered by the editor, such as `SetEventScript` where supported by that event.

## Learning Notes

- Begin with one command and test after every change.
- Keep map points, IDs, and delays as named values in your notes.
- Use `Notify` while debugging, then remove temporary messages when the script is finished.
- Confirm the loop terminator and command argument order in the editor.
- Keep a backup of the map before testing commands that change blocks, regions, NPCs, or zones.
- For Lua instead of command scripts, see the [Lua Mod Example](./lua-example.html).

## Sources

- [Original Total Miner Reference](https://totalminer.github.io/index)

---

[← Back to Scripting Documentation](./scripting.html)

[← Back to Home](./)
