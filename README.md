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

## Building

See [INSTALL.md](INSTALL.md) for toolchain setup.

```bash
make -j$(nproc)
```

---

## Credits

- [pret/pokeemerald](https://github.com/pret/pokeemerald) — base decompilation
- [rh-hideout/pokeemerald-expansion](https://github.com/rh-hideout/pokeemerald-expansion) v1.15.1 — RHH Gen 9 expansion ([credits](https://github.com/rh-hideout/pokeemerald-expansion/blob/upcoming/CREDITS.md))
