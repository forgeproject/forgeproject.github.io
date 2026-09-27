---
title: "XML Mod Example"
layout: default
description: "A worked Total Miner XML mod example — a custom weapon, a modified block, a custom NPC, and a particle template"
url: /xml-mod-example.html
robots: noindex,follow
sitemap_exclude: true
---

<h1 align="center">Total Miner XML Mod Example</h1>

<p align="center">
A worked example mod using the fields documented in the XML Modding Reference.
</p>

---

## Table of contents

- [Overview](#overview)
- [Adding a custom item — Frost Blade](#adding-a-custom-item--frost-blade)
- [Modifying an existing block — Rhyolite](#modifying-an-existing-block--rhyolite)
- [Adding a custom NPC — Frost Wraith](#adding-a-custom-npc--frost-wraith)
- [Adding a particle template — FrostSpark](#adding-a-particle-template--frostspark)
- [Notes](#notes)

---

## Overview

This example mod does four things:

Adds a new weapon, Frost Blade, with its own combat stats, swing timing, sound, skill requirement, and crafting recipe.
Modifies the existing Rhyolite block to make it slightly more resistant and give it a faint glow.
Adds a new hostile NPC, Frost Wraith, with its own AI, audio, level, and physics data, and a loot table that can drop the Frost Blade.
Adds a FrostSpark particle template that the Frost Wraith (or a Particle Emitter block) could use.

Each section below shows the relevant snippet for every file it touches. Swap in your own values, item IDs, and block IDs as needed.

---

## Adding a custom item — Frost Blade

**ItemData.xml**

```xml
<Item>
  <ItemID>FrostBlade</ItemID>
  <Name>Frost Blade</Name>
  <Desc>A blade infused with lingering cold. Slows anything it strikes.</Desc>
  <IsValid>true</IsValid>
  <IsEnabled>true</IsEnabled>
  <LockedDD>true</LockedDD>
  <LockedCR>false</LockedCR>
  <LockedSU>true</LockedSU>
  <MinCSPrice>450</MinCSPrice>
  <StackSize>1</StackSize>
  <Durability>800</Durability>
  <StrikeDamage>18</StrikeDamage>
  <StrikeReach>2.5</StrikeReach>
  <ParticleLight>4</ParticleLight>
  <CanDropIfLocked>false</CanDropIfLocked>
  <Plural>S</Plural>
</Item>
```

**ItemTypeData.xml**

```xml
<Item>
  <ItemID>FrostBlade</ItemID>
  <Use>Item</Use>
  <Type>Weapon</Type>
  <SubType>RapidSwing</SubType>
  <ClassID>Titanium</ClassID>
  <Inv>Weapon</Inv>
  <CombatID>FrostBladeCombat</CombatID>
  <Model>Weapon</Model>
  <Swing>Weapon</Swing>
  <Equip>RightHand</Equip>
</Item>
```

**ItemCombatData.xml**

```xml
<Combat>
  <CombatID>FrostBladeCombat</CombatID>
  <Health>0</Health>
  <Attack>250</Attack>
  <Strength>150</Strength>
  <Defence>0</Defence>
  <Ranged>0</Ranged>
  <Looting>50</Looting>
</Combat>
```

**ItemSwingTimeData.xml**

```xml
<Item>
  <ItemID>FrostBlade</ItemID>
  <Time>0.6</Time>
  <Pause>0.2</Pause>
  <ExtendedPause>0.05</ExtendedPause>
  <RetractTime>0.15</RetractTime>
  <RetractSmooth>true</RetractSmooth>
</Item>
```

**ItemSoundData.xml**

```xml
<Item>
  <ItemID>FrostBlade</ItemID>
  <Group>ItemSteelTool</Group>
</Item>
```

**SkillData.xml**

```xml
<Item>
  <ItemID>FrostBlade</ItemID>
  <UseReq>35</UseReq>
  <UseSkill>Attack</UseSkill>
  <CraftReq>35</CraftReq>
  <CraftSkill>Smithing</CraftSkill>
</Item>
```

**BlueprintData.xml**

```xml
<Blueprint>
  <ItemID>FrostBlade</ItemID>
  <CraftType>Crafting</CraftType>
  <IsDefault>false</IsDefault>
  <Depth>
    <X>0.4</X>
    <Y>0.9</Y>
  </Depth>
  <Result>
    <ItemID>FrostBlade</ItemID>
    <Count>1</Count>
  </Result>
  <Material22>
    <ItemID>Titanium</ItemID>
    <Durability>0</Durability>
    <Count>1</Count>
  </Material22>
  <Material12>
    <ItemID>Ice</ItemID>
    <Durability>0</Durability>
    <Count>2</Count>
  </Material12>
  <Material32>
    <ItemID>Stick</ItemID>
    <Durability>0</Durability>
    <Count>1</Count>
  </Material32>
</Blueprint>
```

---

## Modifying an existing block — Rhyolite

Because Rhyolite already exists, supplying its `BlockID` modifies it in place rather than adding a new block.

**BlockData.xml**

```xml
<Block>
  <BlockID>Rhyolite</BlockID>
  <Luminance>2</Luminance>
  <BlastResistance>9000</BlastResistance>
</Block>
```

**BlockMaterialData.xml**

```xml
<Material>
  <Material>Rhyolite</Material>
  <Resistance>7800</Resistance>
  <PickEfficiency>100</PickEfficiency>
</Material>
```

To also change Rhyolite's shop name, description, or price, add an `ItemData.xml` entry using the block ID as the `ItemID`:

```xml
<Item>
  <ItemID>Rhyolite</ItemID>
  <Name>Glowing Rhyolite</Name>
  <Desc>A volcanic stone that now pulses with a faint inner light.</Desc>
</Item>
```

---

## Adding a custom NPC — Frost Wraith

**ActorTypeData.xml**

```xml
<Actor>
  <ActorType>FrostWraith</ActorType>
  <LevelType>FrostWraithLevel</LevelType>
  <PhysicsType>FrostWraithPhysics</PhysicsType>
  <AIType>FrostWraithAI</AIType>
  <ComName>FrostWraithModel</ComName>
  <ModelHeight>2.1</ModelHeight>
  <ModelYRotation>0</ModelYRotation>
  <IsValid>true</IsValid>
  <IsFemale>false</IsFemale>
  <IsPassive>false</IsPassive>
  <IsImmuneToFire>false</IsImmuneToFire>
  <HasNameplate>true</HasNameplate>
  <HandMaxHit>12</HandMaxHit>
  <NaturalSpawnFreq>90</NaturalSpawnFreq>
  <NaturalBehavior>Wander</NaturalBehavior>
  <LootTable>
    <LootItem>
      <Item>FrostBlade</Item>
      <Damage>Combat</Damage>
      <Percent>5</Percent>
      <Count1>1</Count1>
      <Count2>1</Count2>
    </LootItem>
  </LootTable>
</Actor>
```

**ActorAIData.xml**

```xml
<AI>
  <ActorAIType>FrostWraithAI</ActorAIType>
  <StrikeDelay>1.2</StrikeDelay>
  <StrikeRange>2.5</StrikeRange>
  <RegardRange>20</RegardRange>
  <HearingRange>12</HearingRange>
  <AttackRange>16</AttackRange>
  <InactiveRange>40</InactiveRange>
</AI>
```

**ActorAudioData.xml**

```xml
<Audio>
  <ActorType>FrostWraith</ActorType>
  <AudioPain>WraithHurt</AudioPain>
  <AudioWarning>WraithGrowl</AudioWarning>
  <AudioDeath>WraithDeath</AudioDeath>
</Audio>
```

**ActorLevelData.xml**

```xml
<Level>
  <ActorLevelType>FrostWraithLevel</ActorLevelType>
  <HealthLevel>60</HealthLevel>
  <AttackLevel>45</AttackLevel>
  <StrengthLevel>40</StrengthLevel>
  <DefenceLevel>25</DefenceLevel>
  <RangedLevel>0</RangedLevel>
</Level>
```

**ActorPhysicsData.xml**

```xml
<Physics>
  <ActorPhysicsType>FrostWraithPhysics</ActorPhysicsType>
  <Acceleration>0.12</Acceleration>
  <MoveSpeed>0.22</MoveSpeed>
  <JumpSpeed>7.5</JumpSpeed>
  <RotateSpeed>4</RotateSpeed>
</Physics>
```

---

## Adding a particle template — FrostSpark

**ParticleData.xml**

```xml
<Particle>
  <Name>FrostSpark</Name>
  <EmitFreq>80</EmitFreq>
  <Duration>600</Duration>
  <Rotation>0.5</Rotation>
  <Velocity>
    <X>0</X>
    <Y>0.6</Y>
    <Z>0</Z>
  </Velocity>
  <VelocityVariance>
    <X>0.2</X>
    <Y>0.1</Y>
    <Z>0.2</Z>
  </VelocityVariance>
  <EmitPosOffset>
    <X>0</X>
    <Y>0.5</Y>
    <Z>0</Z>
  </EmitPosOffset>
  <EmitPosVariance>
    <X>0.3</X>
    <Y>0</Y>
    <Z>0.3</Z>
  </EmitPosVariance>
  <Size>
    <X>0.1</X>
    <Y>0.1</Y>
    <Z>0.1</Z>
    <W>0.2</W>
  </Size>
  <StartColor>
    <R>180</R>
    <G>220</G>
    <B>255</B>
    <A>255</A>
  </StartColor>
  <EndColor>
    <R>255</R>
    <G>255</G>
    <B>255</B>
    <A>0</A>
  </EndColor>
  <WindFactor>0.4</WindFactor>
  <Gravity>0.05</Gravity>
</Particle>
```

This particle could be referenced by a Particle Emitter block, or emitted from the Frost Wraith's script/AI to sell the "cold" theme.

---

## Notes

- Element/root tag names above (`<Item>`, `<Actor>`, `<Block>`, etc.) are illustrative — match whatever wrapper structure your Total Miner mod loader expects for each file; 
- IDs like `FrostBlade`, `FrostWraith`, `FrostWraithAI`, `FrostWraithLevel`, `FrostWraithPhysics`, and `FrostSpark` are custom and must stay consistent across every file that references them.
