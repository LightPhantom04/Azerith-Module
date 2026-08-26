# Astari

A Foundry VTT module providing compendium structure for the Astari setting (D&D 5e).

## Requirements

- Foundry VTT v13 or v14
- D&D 5e system v5.3.0 or later

## Structure

This module creates one Compendium folder, **Astari**, in the Compendium sidebar, containing:

```
Astari/
├── Characters/
│   ├── Backgrounds   (empty Item compendium)
│   └── Races         (empty Item compendium)
├── Items and Spells/
│   ├── Items         (empty Item compendium)
│   └── Trade Goods   (empty Item compendium)
└── NPCs/             (empty folder, no compendiums yet)
```

**Races** is now populated with 11 playable species: Human, Dwarf, Vashino, Orc, Goblin,
Tabaxi, Elf, Owlin, Loxodon, Goliath, and Naga.

### How the Races are built

Each race is a full `race`-type Item with:
- Fixed Ability Score Improvement (matches the homebrew doc, no player choice)
- Size and base walking speed (Goblin: Small/25ft, Goliath: Large/35ft, Naga: 35ft,
  Dwarf: 25ft, everyone else: Medium/30ft)
- Darkvision range
- A "Racial Traits" advancement that auto-grants each race's named traits as separate
  Feature items, filed under that race's own "<Race> Features" subfolder

Where a trait maps cleanly onto a system mechanic, it's backed by a real Active Effect
or an Attack activity (e.g. Dwarven Toughness grants automatic advantage on Constitution
saves; Wings grants a real flying speed; Vashino's bite and tail whip, Tabaxi's claws,
and Naga's venomous bite are rollable attacks). Traits with no clean automatable
mechanic (Tunnel Sense, Water Retainer, Reserves, Advanced Adrenaline's 0-HP trigger,
etc.) are feature items with a full description only — call this out to your players
and adjudicate manually.

**Worth testing first:** the three attack-granting features (Vashino's Natural Defenses,
Tabaxi's Claws, Naga's Venomous) use Foundry's newer Activities system. The damage
numbers and abilities are correct, but this is the one part of the build I couldn't
cross-check against the live system schema — open each one on an actor sheet and
confirm the Attack/Damage buttons work as expected before relying on them at the table.

**Items** is now populated too: a **Mana Crystal (100)** consumable in Consumables (100
charges, no quantity stacking — see below), and 46 armor pieces under Armor's four tier
folders, covering all 14 materials from the homebrew doc in Light/Medium/Heavy (Elf-Steel
and Mythril skip Light; Dragon Hide and Ancient Dragon Hide come in Fire and Lightning
versions). Backgrounds and Trade Goods are still empty.

### Mana Crystal & mana-costing abilities

The Mana Crystal is a single item with 100 uses/charges (not quantity — quantity stays
at 1, the "(100)" is in the name per your instruction). Moon Silver's False Life, Uru's
Misty Step, and Orichalcum's Greater Invisibility each have an Activity that consumes
charges from a Mana Crystal on the same character (matched by identifier, so it works
with any copy of the crystal in that character's inventory) — 1/2/4 charges respectively.

### Armor automation

AC, Dex cap, Strength requirement, and stealth disadvantage are all real fields (Light:
AC 13/full Dex, Medium: AC 15/+3 Dex cap, Heavy: AC 18/no Dex — Medium/Heavy normally
need Str 14/16 except Elf-Steel and Mythril, which waive it). Damage resistances and the
Ancient Dragon Hide weapon-damage bonus are live Active Effects. A few traits have no
clean system mechanism to hook into and are description-only — each one says so directly
in its item description: Adamantine's crit immunity, Stalker Hide/Dark Steel's saves
against magic specifically, Sand Drake Hide's imposed disadvantage on attackers, and
Bullet Hide's damage reflection.

**Worth testing first:** the mana-consuming Activities (heal and utility types) are the
least-verified part of this batch, similar to the attack Activities from the Races
compendium — open one on a character sheet and confirm the Mana Crystal charge actually
decrements before relying on it at the table. Price and weight on every armor piece are
placeholder values (scaled roughly by tier), not numbers from your document — adjust as
needed.

## Installation

1. Copy this `astari` folder into your Foundry `Data/modules/` directory, **or**
   install it in Foundry via Add-on Modules using the local folder / a hosted manifest URL.
2. Enable the "Astari" module in your World's Manage Modules settings.
3. Launch the World. Foundry will automatically initialize the empty compendium
   databases declared in `module.json` the first time the module is active — you
   don't need to create anything by hand in the `packs/` folder.
4. Open the Compendium sidebar tab; you'll see the "Astari" folder with the
   Characters, Items and Spells, and NPCs sub-folders as described above.

## Notes

- Backgrounds, Races, Items, and Trade Goods are all `Item`-type compendiums
  (matching how the dnd5e system stores backgrounds, races/species, and equipment).
- The NPCs folder has no compendium yet — add one later by adding an `Actor`-type
  pack entry to `module.json` and listing it under the NPCs folder's `packs` array.
- Author name in `module.json` is left blank — fill in `authors[0].name` when ready.
