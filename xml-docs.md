---
title: "XML Modding Documentation"
layout: default
description: "Total Miner XML mod reference — data types, items, blocks, NPCs, and particles"
url: /xml-docs.html
robots: noindex,follow
sitemap_exclude: true
---

<h1 align="center">Total Miner XML Modding Reference</h1>

<p align="center">
Complete reference for Total Miner's XML modding files, organized by category.
</p>

<p align="center">
Looking for a worked example? See the <a href="./xml-mod-example.html">XML Mod Example</a>.
</p>

---

## Table of contents

- [Data Types](#data-types)
- [Adding And Modifying Items](#adding-and-modifying-items)
  - [ItemData.xml](#itemdataxml)
  - [ItemTypeData.xml](#itemtypedataxml)
  - [ItemTypeClassData.xml](#itemtypeclassdataxml)
  - [ItemCombatData.xml](#itemcombatdataxml)
  - [ItemSwingTimeData.xml](#itemswingtimedataxml)
  - [ItemSwingData.xml](#itemswingdataxml)
  - [ItemSoundData.xml](#itemsounddataxml)
  - [SkillData.xml](#skilldataxml)
  - [BlueprintData.xml](#blueprintdataxml)
  - [ItemTextures16.xml/ItemTextures32.xml](#itemtextures16xmlitemtextures32xml)
- [Modifying Blocks](#modifying-blocks)
  - [BlockData.xml](#blockdataxml)
  - [BlockMaterialData.xml](#blockmaterialdataxml)
  - [BlockTextures16.xml/BlockTextures64.xml](#blocktextures16xmlblocktextures64xml)
- [Adding And Modifying NPCs](#adding-and-modifying-npcs)
  - [ActorTypeData.xml](#actortypedataxml)
  - [ActorAIData.xml](#actoraidataxml)
  - [ActorAudioData.xml](#actoraudiodataxml)
  - [ActorLevelData.xml](#actorleveldataxml)
  - [ActorPhysicsData.xml](#actorphysicsdataxml)
- [Adding Particle Templates](#adding-particle-templates)
  - [ParticleData.xml](#particledataxml)

---

## Data Types

- **`string`** — A string of characters. Can be anything.
- **`bool`** — True or False.
- **`int`** — A whole number between -2,147,483,648 and 2,147,483,647.
- **`ushort`** — A whole number between 0 and 65,535.
- **`short`** — A whole number between -32,768 and 32,767.
- **`byte`** — A whole number between 0 and 255.
- **`float`** — A real number (decimal) between -3.4 x 10³⁸ and 3.4 x 10³⁸.
- **`Vector2`** — An object representing two points.
  - `float X`
  - `float Y`
- **`Vector3`** — An object representing three points.
  - `float X`
  - `float Y`
  - `float Z`
- **`Vector4`** — An object representing four points.
  - `float X`
  - `float Y`
  - `float Z`
  - `float W`
- **`Color`** — An object representing an RGBA color.
  - `byte R`
  - `byte G`
  - `byte B`
  - `byte A`
- **`Item`** — A Total Miner Item ID. No spaces are allowed. Can usually be either an existing item or a custom item. In some rare situations, custom item IDs do not work here.
- **`Block`** — A Total Miner Block ID. No spaces are allowed. Must be an existing block.
- **`InventoryItemXML`** — An object representing an item, amount, and durability.
  - `Item ItemID`
  - `ushort Durability`
  - `int Count`
- **`InventoryItemNDXML`** — An object representing an item and amount.
  - `Item ItemID`
  - `int Count`
- **`LootItem`** — An object representing an item in a loot table.
  - `Item Item` — The item of this loot drop.
  - `DamageType Damage` — The damage type required to make this item drop. Valid Values: `Unknown`, `Combat`, `Drowning`, `Burning`, `ItemUse`, `Blast`, `BlockFallingOnHead`, `BlockCollision`, `Hail`, `ShieldDeflect`, `Effect`
  - `int Percent` — The percent chance of this item dropping.
  - `int Count1` — The minimum amount of this item dropped.
  - `int Count2` — The maximum amount of this item dropped.

---

## Adding And Modifying Items

Items can be added and modified with XML mods. If an Item ID supplied already exists, that item will be modified. Below is the documentation for each file used to add and modify items. Any file or field can be omitted to use default values.

Files: `ItemData.xml`, `ItemTypeData.xml`, `ItemTypeClassData.xml`, `ItemCombatData.xml`, `ItemSwingTimeData.xml`, `ItemSwingData.xml`, `ItemSoundData.xml`, `SkillData.xml`, `BlueprintData.xml`, `ItemTextures16.xml`/`ItemTextures32.xml`

### ItemData.xml

Contains general information about this item.

- **`ItemID`** (`Item`) — The ID of this item. If this is an existing item, that item will be modified, otherwise this item will be added.
- **`Name`** (`string`) — The name of this item that appears in the inventory, item interact screen, etc. The name can include spaces.
- **`Desc`** (`string`) — The description of this item shown on this item interact screen.
- **`IsValid`** (`bool`) — If false, this item cannot be obtained through normal means, effectively removing this item.
- **`IsEnabled`** (`bool`) — If false, this item will be initially disabled. This item can be enabled or disabled manually in this item's Options menu. If you're looking to effectively remove an item, use `IsValid`.
- **`LockedDD`** (`bool`) — If true, this item will be locked in shops in Dig Deep until either the blueprint is found or this item is equipped.
- **`LockedCR`** (`bool`) — If true, this item will be locked in shops in Creative until this item is equipped.
- **`LockedSU`** (`bool`) — If true, this item will be locked in shops in Survival until this item is equipped.
- **`MinCSPrice`** (`int`) — The price this item sells for in the shop. This item can be bought for 120% of this price. 0 = Free, -1 = Unpurchasable. Note that setting the price to -1 will also remove this item from the creative inventory.
- **`StackSize`** (`int`) — The maximum stack size of this item. If this item has durability, the stack size will always be 1.
- **`Durability`** (`ushort`) — The durability of this item. If this is above 0, this item's stack size will always be 1.
- **`StrikeDamage`** (`float`) — The base damage this item deals to targets when attacking.
- **`StrikeReach`** (`float`) — The maximum distance this item can strike enemies at, in blocks.
- **`HealPower`** (`short`) — The amount of health this item heals when used.
- **`BurnTime`** (`ushort`) — The amount of time, in seconds, this item burns in a furnace.
- **`SmeltTime`** (`float`) — The amount of time, in seconds, this item takes to be smelted in a furnace. If this item cannot be created in a furnace, this is ignored.
- **`ParticleLight`** (`byte`) — How much this item glows in the player's hand and on the ground. Valid Values: Between 0 and 15.
- **`CanDropIfLocked`** (`bool`) — If false, this item cannot be dropped by mobs unless this item has been unlocked.
- **`Plural`** (`Plural`) — How the game displays this item's name in plural. Valid Values: `None`, `S`, `ES`

### ItemTypeData.xml

Contains information about this item's type data and use.

- **`ItemID`** (`Item`) — The ID of this item. If this is an existing item, that item will be modified, otherwise this item will be added.
- **`Use`** (`ItemUse`) — The use type of this item. Valid Values: `Block`, `Item`
- **`Type`** (`ItemType`) — The type of this item. Valid Values: `Block`, `Item`, `Tool`, `Weapon`, `Armor`, `Power`, `Food`, `Decor`, `Jewelry`
- **`SubType`** (`ItemSubType`) — The sub type of this item. An item can have multiple subtypes by separating value with spaces. Valid Values: `Bow`, `Arrow`, `Shield`, `Edible`, `TillTool`, `HarvestTool`, `Grenade`, `GrenadeLauncher`, `Key`, `Door`, `RangedWeapon`, `BlockCanBeOpened`, `Leaves`, `Gun`, `RapidSwing`, `Potion`
- **`ClassID`** (`ItemTypeClass`) — The class ID of this item. The class determines the power and maximum resistance of this item when mining. This can also be a custom class. Valid Values: `None`, `CantMine`, `Wood`, `Bronze`, `Iron`, `Steel`, `GreenstoneGold`, `Platinum`, `Diamond`, `Ruby`, `Titanium`, `SledgeHammer`
- **`Inv`** (`ItemInvType`) — The shop tab this item will appear in. Valid Values — Blocks: `Natural`, `Stone`, `Ore`, `Flora`, `Utility`, `Building`; Items: `Tool`, `Weapon`, `Armor`, `Food`, `Jewelry`, `Key`, `Other`
- **`CombatID`** (`CombatItem`) — The combat ID for this item. The combat class determines the stat bonuses of this item. This can also be a custom combat class. Valid Values: Any item with stat bonuses.
- **`Model`** (`ItemModelType`) — This item's model type. The model type determines how this item looks when held. Valid Values: `Block`, `IconBlock`, `BigIconBlock`, `Item`, `MediumItem`, `MediumItemFront`, `ItemTLBR`, `Tool`, `Hatchet`, `Weapon`, `WeaponTLBR`, `WeaponTRBL`, `BigWeapon`, `SteelScimitar`, `SteelClaymore`, `Bow`, `Arrow`, `Armor`, `Shield`, `Key`, `Jewelry`, `Door`, `Torch`, `GunHand`, `GunRifle`, `Clipboard`, `Staff`
- **`Swing`** (`ItemSwingType`) — This item's swing type. The swing type determines how this item looks when swung. Valid Values: `Block`, `Item`, `IconBlock`, `Ramp`, `Weapon`, `WeaponTRBL`, `Spear`, `Bow`, `Shield`, `Eating`, `Arrow`, `SwitchArrow`, `GunHand`, `GunRifle`, `Key`, `Staff`
- **`Equip`** (`EquipIndex`) — The slot this item should be equipped in. Valid Values: `Head`, `Neck`, `Body`, `Legs`, `Feet`, `LeftSide`, `RightSide`, `LeftHand`, `RightHand`

### ItemTypeClassData.xml

Contains information about the item class. The number of hits taken to destroy a block is equal to Block Resistance / Item Power × Tool Effectiveness. E.g. Rhyolite has a resistance of 7200, and a Titanium Pickaxe has a power of 1200, meaning it will take 6 hits to destroy Rhyolite with a Titanium Pickaxe.

- **`ClassID`** (`ItemTypeClass`) — The ID of this class. No spaces are allowed. If this is an existing class, that class will be modified, otherwise the class will be added.
- **`Power`** (`ushort`) — The amount of "damage" that items of this class deal to blocks when mining.
- **`MaxResistance`** (`ushort`) — The maximum block resistance that items of this class can mine. Blocks with a higher resistance will be unmineable.

### ItemCombatData.xml

Contains information about the stat bonuses of items. Every 100 points in a stat is equal to 1 skill level.

- **`CombatID`** (`CombatItem`) — The ID of this combat class. No spaces are allowed. If this is an existing combat class, that combat class will be modified, otherwise the combat class will be added.
- **`Health`** (`short`) — The amount of Health stat points this item gives when equipped.
- **`Attack`** (`short`) — The amount of Attack stat points this item gives when equipped.
- **`Strength`** (`short`) — The amount of Strength stat points this item gives when equipped.
- **`Defence`** (`short`) — The amount of Defence stat points this item gives when equipped.
- **`Ranged`** (`short`) — The amount of Ranged stat points this item gives when equipped.
- **`Looting`** (`short`) — The amount of Looting stat points this item gives when equipped.

### ItemSwingTimeData.xml

Contains information about the swing time of this item. The `Time` field is the total amount of time this item takes to swing and is not affected by any other field. Say, `Time=1`, and `Pause=0.5`: this item will take 1 second to swing, half a second of which is spent paused.

- **`ItemID`** (`Item`) — The ID of this item. If this is an existing item, that item will be modified.
- **`Time`** (`float`) — The total time, in seconds, it takes to swing this item. Other time values are not added to this time.
- **`Pause`** (`float`) — The amount of time, in seconds, this item stays in the rest position after being swung before being able to be swung again.
- **`ExtendedPause`** (`float`) — The amount of time, in seconds, this item remains in its fully extended position.
- **`RetractTime`** (`float`) — The amount of time, in seconds, this item takes to return to the rest position after reaching its fully extended position. Setting this to -1 makes this item retract in the same amount of time it takes to extend.
- **`RetractSmooth`** (`bool`) — If true, this item will retract smoothly.

### ItemSwingData.xml

Contains information about how items are swung.

- **`SwingID`** (`ItemSwingType`) — The ID of this swing type. No spaces are allowed. Must be an existing swing type. Valid Values: `None`, `Block`, `Item`, `IconBlock`, `Ramp`, `Weapon`, `WeaponTRBL`, `Spear`, `Bow`, `Shield`, `Eating`, `Arrow`, `SwitchArrow`, `GunHand`, `GunRifle`, `Key`, `Staff`
- **`IsSwingable`** (`bool`) — If false, items with this swing type cannot be swung.
- **`SwingTime`** (`float`) — The amount of time, in seconds, it takes to swing items with this swing type. Set this to 0 to use the time specified for the specific item.
- **`RestPosition`** (`Vector3`) — The local position of this item when resting.
- **`RestRotation`** (`Vector3`) — The rotation of this item when resting.
- **`ExtendedPosition`** (`Vector3`) — The local position of this item when fully extended in third person.
- **`ExtendedPositionFPV`** (`Vector3`) — The local position of this item when fully extended in first person.
- **`ExtendedRotation`** (`Vector3`) — The rotation of this item when fully extended in third person.
- **`ExtendedRotationFPV`** (`Vector3`) — The rotation of this item when fully extended in first person.
- **`CircularY`** (`float`) — The maximum height of the circular vertical movement of this item while swinging in third person.
- **`CircularZ`** (`float`) — The maximum circular forward movement of this item while swinging in both third and first person.
- **`CircularYFPV`** (`float`) — The maximum height of the circular vertical movement of this item while swinging in first person.

### ItemSoundData.xml

Contains information about the sound this item makes.

- **`ItemID`** (`Item`) — The ID of this item. If this is an existing item, that item will be modified.
- **`Group`** (`ItemSoundGroup`) — The sound group of this item. Valid Values: `None`, `Base`, `BodyHit`, `EnvNightfall`, `GenPickup`, `GuiAccept`, `GuiCancel`, `GuiInvalid`, `GuiMoveCursor`, `GuiSelect`, `GuiTransfer`, `GuiGamerJoined`, `GuiTxtMsgIn`, `ItemActivate`, `ItemArmor`, `ItemBlock`, `ItemBow`, `ItemCooked`, `ItemCrop`, `ItemDiamantiumTool`, `ItemDiamondTool`, `ItemWoodDoor`, `ItemMetalDoor`, `ItemEarth`, `ItemFire`, `ItemFlora`, `ItemGem`, `ItemGlass`, `ItemGrass`, `ItemGreenstoneTool`, `ItemIronTool`, `ItemJewelry`, `ItemKey`, `ItemLava`, `ItemLeather`, `ItemMetal`, `ItemOre`, `ItemPorous`, `ItemPortcullis`, `ItemRareTool`, `ItemRaw`, `ItemRock`, `ItemRope`, `ItemRubyTool`, `ItemSand`, `ItemShield`, `ItemSkill`, `ItemSnow`, `ItemSteelTool`, `ItemStone`, `ItemTile`, `ItemTitaniumTool`, `ItemTree`, `ItemWater`, `ItemWood`, `ItemWoodTool`, `ItemWool`, `ItemGun`, `ItemGunSMG`, `ItemGunLaser`
- **`Sounds`** (`ItemSoundXML`) — `ItemSoundXML` class specifying the sounds this item should make on certain actions.

### SkillData.xml

Contains information about the skill types and requirements for this item.

- **`ItemID`** (`Item`) — The ID of this item. If this is an existing item, that item will be modified.
- **`MineReq`** (`int`) — If this item is a block, the minimum skill level required to mine it.
- **`UseReq`** (`int`) — The minimum skill level required to use this item.
- **`UseSkill`** (`SkillType`) — The skill this item uses. Valid Values: `Health`, `Strength`, `Attack`, `Defence`, `Ranged`, `Mining`, `Digging`, `Chopping`, `Building`, `Crafting`, `Smelting`, `Smithing`, `Farming`, `Cooking`, `Looting`
- **`CraftReq`** (`int`) — The minimum skill level required to craft this item.
- **`CraftSkill`** (`SkillType`) — The skill used to craft this item. Valid Values: `Health`, `Strength`, `Attack`, `Defence`, `Ranged`, `Mining`, `Digging`, `Chopping`, `Building`, `Crafting`, `Smelting`, `Smithing`, `Farming`, `Cooking`, `Looting`

### BlueprintData.xml

Contains information about how this item is crafted and its Dig Deep Blueprint.

- **`ItemID`** (`Item`) — The ID of this item. Blueprints can only be added this way, not removed.
- **`CraftType`** (`BlueprintCraftType`) — The method by which this item is crafted. Valid Values: `Crafting`, `Furnace`
- **`IsDefault`** (`bool`) — If true, this recipe will be automatically unlocked in Dig Deep without needing to find the blueprint.
- **`Depth`** (`Vector2`) — The minimum and maximum depth percentage of this item's blueprint in Dig Deep. 0 = highest depth, 1 = lowest depth.
- **`Result`** (`InventoryItemNDXML`) — The item this recipe crafts.
- **`Material11`** (`InventoryItemXML`) — The item to be placed in the bottom-left of the 3x3 crafting grid.
- **`Material12`** (`InventoryItemXML`) — The item to be placed in the bottom-middle of the 3x3 crafting grid.
- **`Material13`** (`InventoryItemXML`) — The item to be placed in the bottom-right of the 3x3 crafting grid.
- **`Material21`** (`InventoryItemXML`) — The item to be placed in the middle-left of the 3x3 crafting grid.
- **`Material22`** (`InventoryItemXML`) — The item to be placed in the middle of the 3x3 crafting grid.
- **`Material23`** (`InventoryItemXML`) — The item to be placed in the middle-right of the 3x3 crafting grid.
- **`Material31`** (`InventoryItemXML`) — The item to be placed in the top-left of the 3x3 crafting grid.
- **`Material32`** (`InventoryItemXML`) — The item to be placed in the top-middle of the 3x3 crafting grid.
- **`Material33`** (`InventoryItemXML`) — The item to be placed in the top-right of the 3x3 crafting grid.

### ItemTextures16.xml/ItemTextures32.xml

Contains the order of items in their respective texture atlas image. HD Texture Packs use `ItemTextures32.xml` while SD Texture Packs use `ItemTextures16.xml`. Always supply both TexturesXML files and both texture atlas images when adding custom items. The texture atlas image should have every item texture laid out next to one another. Recommended up to 32 items on one line in the texture atlas. Once the 32nd item is reached, move down a line.

- **`ItemID`** (`Item`) — The ID of this item.

---

## Modifying Blocks

At the moment, blocks cannot be added with mods, but they can be modified. Below is the documentation for each file used to modify blocks. Any file or field can be omitted.

To modify the name, description, price, etc. of blocks, you must use `ItemData.xml` with the desired Block ID as the Item ID.

Files: `BlockData.xml`, `BlockMaterialData.xml`, `BlockTextures16.xml`/`BlockTextures64.xml`

### BlockData.xml

Contains general information about this block.

- **`BlockID`** (`Block`) — The ID of this block. This must be an existing block ID.
- **`Material`** (`BlockMaterial`) — The material of this block. The material affects this block's resistance and tool efficiencies. Must be an existing block material. Valid Values: `Clay`, `Sondstone`, `Limestone`, `Basalt`, `Andesite`, `Dacite`, `Diorite`, `Tuff`, `Serpentine`, `Gabbro`, `Granite`, `Komatiite`, `Marble`, `Rhyolite`, `Bedrock`, `Flint`, `Copper`, `Cassiterite`, `Coal`, `Iron`, `Gold`, `Opal`, `Carbon`, `Sulphur`, `Cyclonite`, `Fluorite`, `Platinum`, `Greenstone`, `Diamond`, `Sapphire`, `Ruby`, `Titanium`, `Obsidian`, `Uranium`, `Composite`, `SoftComposite`, `Glass`, `FramedGlass`, `Stick`, `Wood`, `Leaves`, `Earth`, `Sand`, `Porous`, `Snow`, `Crop`, `Vegetation`, `Vapor`, `Liquid`, `Fire`, `Ice`, `Paper`, `Brick`, `Stone`, `Metal`, `Explosive`, `Key`, `Fibre`, `Color`, `SpiderEgg`, `Barrier`
- **`ClassType`** (`DataBlockType`) — Additional block type data for blocks with special functions. Must be an existing class type. Most blocks use `None`. Valid Values: `None`, `ParticleEmitter`, `Door`, `Marker`, `Shop`, `Chest`, `Furnace`, `Bookcase`, `AmbientSound`, `SentryTurret`, `ProximityDetector`, `Fire`, `NPCSpawn`, `Script`, `Sign`, `MobSpawn`, `Teleport`, `WifiReceiver`, `WifiTransmitter`, `Crop`, `Blueprint`, `WisdomScroll`, `Sundial`, `Torch`, `Painting`, `Book`, `Health`
- **`Opacity`** (`byte`) — How opaque this block is. Affects how much light passes through this block. Valid Values: 1-15 for transparent blocks, 255 for opaque blocks.
- **`Luminance`** (`byte`) — How much light this block emits. Valid Values: 0-15
- **`Friction`** (`float`) — The friction of this block. The lower the friction, the more "slippery" this block is. Most blocks use 0.35. Valid Values: 0-1
- **`Dampen`** (`float`) — Unknown.
- **`Buffer`** (`byte`) — The way this block is rendered when placed in the world. Valid Values: 0 = Full Block, 1 = Special, 2 = 2D, 3 = Transparent
- **`IsIcon`** (`bool`) — If true, this block's texture is an icon. Should be used with Buffer 2 and low opacity.
- **`IsAttached`** (`bool`) — If true, this block should be attached to another block when placed. Can be used with Buffer 2.
- **`IsPassable`** (`bool`) — If true, this block will have no collision and can be walked through.
- **`IsRotated`** (`bool`) — If true, this block can be rotated.
- **`IsOrientated`** (`bool`) — If true, this block can be orientated.
- **`IsOreDeposit`** (`bool`) — If true, this block should be considered ore.
- **`IsPowerEmitter`** (`bool`) — If true, this block can emit power when active.
- **`IsPoweredMechanism`** (`bool`) — If true, this block can be activated by power.
- **`IsVertSunlightUnhindered`** (`bool`) — If true, sunlight can pass through this block vertically without being blocked.
- **`BlastResistance`** (`ushort`) — How resistant this block is to explosions.
- **`WindAffect`** (`byte`) — How much this block sways when there is wind.
- **`TextureID`** (`byte`) — The textures list this block can use.

### BlockMaterialData.xml

Contains information about this block material. The block material affects the tools that can break the block. If any efficiency is set to 0, that respective tool cannot break the block.

- **`Material`** (`BlockMaterial`) — The ID of this block material. No spaces are allowed. Must be an existing block material. Valid Values: `Clay`, `Sondstone`, `Limestone`, `Basalt`, `Andesite`, `Dacite`, `Diorite`, `Tuff`, `Serpentine`, `Gabbro`, `Granite`, `Komatiite`, `Marble`, `Rhyolite`, `Bedrock`, `Flint`, `Copper`, `Cassiterite`, `Coal`, `Iron`, `Gold`, `Opal`, `Carbon`, `Sulphur`, `Cyclonite`, `Fluorite`, `Platinum`, `Greenstone`, `Diamond`, `Sapphire`, `Ruby`, `Titanium`, `Obsidian`, `Uranium`, `Composite`, `SoftComposite`, `Glass`, `FramedGlass`, `Stick`, `Wood`, `Leaves`, `Earth`, `Sand`, `Porous`, `Snow`, `Crop`, `Vegetation`, `Vapor`, `Liquid`, `Fire`, `Ice`, `Paper`, `Brick`, `Stone`, `Metal`, `Explosive`, `Key`, `Fibre`, `Color`, `SpiderEgg`, `Barrier`
- **`Resistance`** (`ushort`) — The resistance of this material. The number of hits required to break a block of this material is equal to Block Resistance / Item Power × Tool Effectiveness. E.g. Rhyolite has a resistance of 7200, and a Titanium Pickaxe has a power of 1200, meaning it will take 6 hits to destroy Rhyolite with a Titanium Pickaxe.
- **`BaseEfficiency`** (`ushort`) — The base percent efficiency of items when breaking a block of this material. The power of all tools when breaking a block with this material is affected by this value. E.g. if `BaseEfficiency` is 50, all tools will take twice as many hits to break a block with this material.
- **`PickEfficiency`** (`ushort`) — The percent efficiency of pickaxes when breaking a block of this material.
- **`ShovelEfficiency`** (`ushort`) — The percent efficiency of shovels when breaking a block of this material.
- **`HatchetEfficiency`** (`ushort`) — The percent efficiency of hatchets when breaking a block of this material.
- **`WeaponEfficiency`** (`ushort`) — The percent efficiency of weapons when breaking a block of this material.
- **`XPAdjust`** (`float`) — The multiplier for XP earned when this block is broken. If this is 0, the XP earned is 1x.
- **`Flags`** (`BlockMaterialFlags`) — Unused.

### BlockTextures16.xml/BlockTextures64.xml

Contains the order of items in their respective texture atlas image. HD Texture Packs use `BlockTextures64.xml` while SD Texture Packs use `BlockTextures16.xml`. The texture atlas image should have every item texture laid out next to one another. Recommended up to 32 blocks on one line in the texture atlas. Once the 32nd block is reached, move down a line.

- **`BlockID`** (`Block`) — The ID of this block.

---

## Adding And Modifying NPCs

NPCs, also known as Actors, can be added and modified with XML mods. If the NPC ID supplied already exists, that NPC will be modified. Below is the documentation for each file used to add or modify NPCs. Any file or field can be omitted to use default values.

Files: `ActorTypeData.xml`, `ActorAIData.xml`, `ActorAudioData.xml`, `ActorLevelData.xml`, `ActorPhysicsData.xml`

### ActorTypeData.xml

Contains general information about this NPC.

- **`ActorType`** (`ActorType`) — The ID of this NPC. If this is an existing NPC, that NPC will be modified, otherwise this NPC will be added.
- **`LevelType`** (`ActorLevelType`) — The level type of this NPC.
- **`PhysicsType`** (`ActorPhysicsType`) — The physics type of this NPC.
- **`AIType`** (`ActorAIType`) — The AI type of this NPC.
- **`ComName`** (`string`) — The name of the component this NPC uses for its model.
- **`ComNameWalk`** (`string[]`) — (Experimental) An array of components this NPC switches between when walking.
- **`ModelHeight`** (`float`) — The height of the NPC, in blocks. The width of the NPC will stretch to accommodate this height.
- **`ModelYRotation`** (`float`) — The rotation of the NPC's model along the Y axis. 3.1416 (Pi) = 180 degrees.
- **`IsValid`** (`bool`) — If false, this NPC cannot be spawned, effectively removing the NPC.
- **`IsFemale`** (`bool`) — If true, this NPC should be considered female.
- **`IsPassive`** (`bool`) — If true, this NPC will only spawn if passive mob spawns are enabled. If false, this NPC will only spawn if hostile mob spawns are enabled.
- **`IsImmuneToFire`** (`bool`) — If true, this NPC will not take damage from fire or lava.
- **`HasNameplate`** (`bool`) — If false, this NPC will never have a visible nameplate.
- **`HandMaxHit`** (`int`) — The maximum damage this NPC can deal without a weapon.
- **`NaturalSpawnFreq`** (`float`) — The time, in seconds, between spawns of this NPC. If this is 0, this NPC cannot spawn naturally.
- **`NaturalBehavior`** (`string`) — The behavior this NPC has when naturally spawned.
- **`LootTable`** (`LootItem[]`) — An array of items that this NPC can drop when killed.

### ActorAIData.xml

Contains information about this NPC's AI.

- **`ActorAIType`** (`ActorAIType`) — The ID of this AI Type. If this is an existing AI Type, that AI Type will be modified, otherwise this AI Type will be added.
- **`StrikeDelay`** (`float`) — The time, in seconds, between attacks of an NPC with this AI Type.
- **`StrikeRange`** (`float`) — The distance, in blocks, of the attacks of an NPC with this AI Type.
- **`RegardRange`** (`int`) — The distance, in blocks, that an NPC with this AI Type will notice a target.
- **`HearingRange`** (`int`) — The distance, in blocks, that an NPC with this AI Type will hear a target.
- **`AttackRange`** (`int`) — The distance, in blocks, that an NPC with this AI Type will try attacking and moving to attack a target.
- **`InactiveRange`** (`int`) — The distance, in blocks, that all players must be from an NPC with this AI Type for it to despawn.

### ActorAudioData.xml

Contains information about the sounds this NPC makes.

- **`ActorType`** (`ActorType`) — The ID of this NPC. If this is an existing NPC, that NPC will be modified, otherwise this NPC will be added.
- **`AudioPain`** (`string`) — The sound this NPC makes when attacked.
- **`AudioStrike`** (`string`) — Currently unused.
- **`AudioWarning`** (`string`) — The sound this NPC makes when warning a target. Currently only used when milking a cow.
- **`AudioDeath`** (`string`) — The sound this NPC makes when killed.

### ActorLevelData.xml

Contains information about this NPC's skill levels.

- **`ActorLevelType`** (`ActorLevelType`) — The ID of this Level Type. If this is an existing Level Type, that Level Type will be modified, otherwise this Level Type will be added.
- **`HealthLevel`** (`int`) — The default health level of an NPC with this Level Type. NPCs have a base health of 10 at health level 1, and every health level under level 100 adds 3 health. Every health level at level 100 or above adds 1 health.
- **`AttackLevel`** (`int`) — The default attack level of an NPC with this Level Type.
- **`StrengthLevel`** (`int`) — The default strength level of an NPC with this Level Type.
- **`DefenceLevel`** (`int`) — The default defence level of an NPC with this Level Type.
- **`RangedLevel`** (`int`) — The default ranged level of an NPC with this Level Type.

### ActorPhysicsData.xml

Contains information about this NPC's movement.

- **`ActorPhysicsType`** (`ActorPhysicsType`) — The ID of this Physics Type. If this is an existing Physics Type, that Physics Type will be modified, otherwise this Physics Type will be added.
- **`Acceleration`** (`float`) — The speed an NPC of this Physics Type moves at when walking. Blocks/s = Acceleration * 60
- **`MoveSpeed`** (`float`) — The maximum speed an NPC with this Physics Type can move at.
- **`JumpSpeed`** (`float`) — The strength of an NPC with this Physics Type's jump.
- **`RotateSpeed`** (`float`) — The speed an NPC with this Physics Type rotates at when turning and looking around.

---

## Adding Particle Templates

Particle templates can be added with XML mods. These particle templates can be used with Particle Emitter blocks and scripts. Any field can be omitted to use defaults.

Files: `ParticleData.xml`

### ParticleData.xml

Contains the data for this particle template.

- **`Name`** (`string`) — The name of this particle template. Use a backslash (`\`) to add a folder.
- **`EmitFreq`** (`int`) — The time, in milliseconds, between spawns of this particle.
- **`Duration`** (`int`) — The time, in milliseconds, this particle lasts.
- **`Rotation`** (`float`) — The rotation speed of this particle.
- **`Velocity`** (`Vector3`) — The initial velocity of this particle.
- **`VelocityVariance`** (`Vector3`) — The random velocity that can be either added to or removed from this particle when spawned.
- **`EmitPosOffset`** (`Vector3`) — The initial offset of this particle from the origin.
- **`EmitPosVariance`** (`Vector3`) — The random offset that can be either added to or removed from this particle when spawned.
- **`Size`** (`Vector4`) — The size of the particle, W being the end size multiplier.
- **`StartColor`** (`Color`) — The initial color of the particle.
- **`EndColor`** (`Color`) — The color of the particle at the end of its duration. The particle fades from the `StartColor` to this color.
- **`WindFactor`** (`float`) — How much wind moves this particle.
- **`Gravity`** (`float`) — How much gravity affects this particle.

---


[← Back to Home](./)
