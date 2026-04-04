# pokeemerald-expansion-frlg (QOL Fork)

A QOL-focused FireRed ROM hack built on top of [RHH pokeemerald-expansion](https://github.com/rh-hideout/pokeemerald-expansion) v1.15.1, compiled with the FireRed flag (`-DFIRERED`).

This fork adds gameplay quality-of-life features on top of the expansion's infrastructure.

---

## Features

### Auto-Run Toggle
- Press **B** at any time in the overworld to toggle between run and walk mode — no need to hold B
- Available **from the very start** of the game with no item or flag requirement
- Works **indoors** (Gen 4+ behavior)
- Toggle plays a sound cue (`SE_PC_ON` / `SE_PC_OFF`) for feedback
- The Pewter City aide that previously gave Running Shoes now gives a **White Herb** instead

### Team-Wide Exp. Share (Always On)
- All party members always share EXP after every battle — no item required
- Gen 9-style: the battling Pokémon gets full EXP; benched Pokémon get a share
- Completely hardcoded — no key item or flag to manage
- The Route 15 Oak's Aide (50 Pokémon caught) now gives a **Choice Band** instead

### Reusable TMs
- All TMs can be used multiple times — they are never consumed
- Shops prevent you from buying a TM you already own ("You already have that TM.")
- TM10 (Hidden Power) replaces TM28 (Dig) in Celadon Dept Store 2F

### Evolution Item QOL
- Trade evolution held items (Metal Coat, Electirizer, Razor Claw, etc.) can be used directly from the bag, Legends Arceus style — no trade required

### BW-Style Map Popups
- Gen 5 (Black 2/White 2) style location name popups on map transitions
- Displays current time in 12-hour format

### EV-IV Display in Summary Screen
- Switch around the EV/IV Display in summary screen

### Blocking Scripts Fix
- Pallet Town Signpost lady
- Viridian City Teacy TV Guy

---

## Config Highlights

```c
// include/config/overworld.h
OW_RUNNING_INDOORS      GEN_LATEST   // Running allowed indoors

// include/config/item.h
I_REUSABLE_TMS          TRUE         // TMs reusable, never consumed
I_USE_EVO_HELD_ITEMS_FROM_BAG TRUE   // Evo held items usable from bag
// Note: Exp. Share is always-on (IsGen6ExpShareEnabled returns TRUE)
```

---

## Gameplay Overhaul

On top of the QOL features, this fork also rewrites core FireRed gameplay to make it more fun and competitive — fixing the flat, boring vanilla difficulty curve with better encounter variety, stronger trainers, and a proper rival progression. The Kanto anime (OS EP001–EP082) is used as a loose thematic reference for what Pokémon feel right in each area, not a hard constraint.

### Gen 4 Starters
- Turtwig (grass), Chimchar (fire), Piplup (water) replace the Gen 1 starters in Oak's lab
- Gen 1 starters become rare wild encounters (1% chance):
  - Bulbasaur — Routes 5 & 6 (Hidden Village, EP010)
  - Charmander — Routes 24 & 25 (near Cerulean, EP011)
  - Squirtle — Seafoam Islands 1F (EP060)

### Rival (TERRY) — Full Team Overhaul
- Rival takes the Gen 4 starter that beats the player's pick
- 8 encounter points × 3 starter branches redesigned with anime-accurate support mons
- Levels scaled to badge caps at each point (lv14 pre-Brock → lv63 Champion)
- Raticate replaced by Eevee (Gary had Eevee — EP033); evolves to Jolteon from Silph Co onward
- Growlithe → Arcanine from Silph; Rhyhorn → Rhydon from Route 22 Late

### Trainer Teams
- **Viridian Forest Bug Catchers** (Rick/Doug/Sammy/Anthony/Charlie): levels bumped, later trainers use Beedrill/Butterfree instead of Kakuna/Metapod
- **Pewter Gym trainer Liam**: expanded to 3 mons (+Nidoran M sweep counter)
- **Brock**: expanded to 4 mons (Geodude/Sandshrew/NidoranM/Onix lv13–15, +Super Potion)

### Wild Encounters
- Route 1, Viridian Forest: anime-accurate species added (Spearow, Sandshrew, Mankey, Pidgeotto)
- All 114 FR tables: LG-exclusive species merged in at 1% slots so they're catchable in FR-only build

---

## Building

See [INSTALL.md](INSTALL.md) for toolchain setup.

```bash
make -j$(nproc)
```

---

## Credits

- [pret/pokeemerald](https://github.com/pret/pokeemerald) — base decompilation
- [rh-hideout/pokeemerald-expansion](https://github.com/rh-hideout/pokeemerald-expansion) v1.15.1 — RHH Gen 9 expansion ([credits](https://github.com/rh-hideout/pokeemerald-expansion/blob/upcoming/CREDITS.md))
