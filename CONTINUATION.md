# Continuation — Gameplay Overhaul

## What This Project Is
A **QOL-focused FireRed ROM hack** built on pokeemerald-expansion v1.15.1 (see README.md for the QOL feature list). This continuation doc tracks a *second layer*: rewriting core FireRed gameplay to make it **fun and competitive** — fixing vanilla's flat difficulty, repetitive encounters, and pushover trainers.

The Kanto anime (OS EP001–EP082) is used as a loose thematic guide for what Pokémon fit each area, not a strict accuracy constraint. Species choices prioritise encounter variety and trainer challenge over lore fidelity.

Single FireRed build — no LeafGreen. Gen 4 starters replace Gen 1. Gen 1 starters become rare wild catches.

---

## DONE

### Wild Encounters (`src/data/wild_encounters.h`)
- **Viridian Forest** (JSON): Reduced 6-slot Caterpie/Weedle monotony. Added Pidgey (10%), Spearow (4%), Pidgeotto (4% rare), Beedrill/Butterfree (1% each version); Pikachu fixed to lv4-8; Metapod+Kakuna kept at 5% each; all entries use level ranges
- **Route 3** (JSON): Fixed Jigglypuff lv3 bug (was a placeholder, now lv6-10); added Nidoran F at 10% in FR (was 1%), Nidoran M at 10% in LG; Mankey upgraded to 4% rare slot; all flat levels converted to ranges
- **2 new Viridian Forest trainers** (map.json + scripts.inc + trainers_frlg.party): KEVIN (south-mid path: Caterpie/Weedle/Metapod lv10-11) and JOSE (north-mid path: Weedle/Kakuna/Beedrill lv11-12). Map positions estimated — verify placement in porymap.
- **Route 1** (FR+LG, lines ~8466): Spearow lv3-5 (5%×2), Sandshrew lv3-5 (1%), Mankey lv3-5 (1%) added; flat single-level Pidgey/Rattata entries replaced with level ranges
- **Route 2** (FR+LG, lines ~8506): Nidoran M/F lv3-5 (10% each), Spearow lv3-5 (4%), Ekans lv3-5 (4%) added; plain Rattata/Pidgey duplicates replaced; Caterpie/Weedle kept at 5% and 1%
- **Route 22** (FR+LG, lines ~9814): Rattata/Mankey dominant (45%/45%), Spearow (10%) — Mankey and Spearow are the key additions over vanilla
- **114 FR tables**: All LeafGreen-exclusive species merged into FireRed tables at low encounter rates (slots 10-11 for land). LG exclusives added: Bellsprout/Weepinbell, Vulpix, Slowpoke/Slowbro, Pinsir, Magmar, Misdreavus, Staryu, Marill, Sneasel, Kingler, Remoraid, Mantine, Sandslash, Muk
- **Gen 1 Starters as rare wilds**: Bulbasaur lv5-8 at slot 11 (1%) in Route 5 + Route 6 FR tables; Charmander lv5-8 at slot 11 (1%) in Route 24 + Route 25 FR tables; Squirtle lv5-8 at slot 11 (1%) in SeafoamIslands1F FR table

### Starters (`src/starter_choose.c:113-115`, `data/maps/PalletTown_ProfessorOaksLab_Frlg/scripts.inc`)
- FRLG starters swapped to Gen 4: Turtwig (grass), Chimchar (fire), Piplup (water)
- Oak lab script updated: all 3 ball event PLAYER/RIVAL_STARTER_SPECIES vars use Gen 4 species; confirmation text strings updated to name Turtwig/Piplup/Chimchar with vanilla-style dialogue

### Viridian Forest Trainer Teams (`src/data/trainers_frlg.party`)
All 5 Bug Catchers updated (RICK/DOUG/SAMMY/ANTHONY/CHARLIE):
- Rick: Weedle lv10, Caterpie lv10, Kakuna lv11
- Doug: Weedle lv10, Beedrill lv11 (Poison Sting/Fury Attack), Metapod lv11
- Sammy: Butterfree lv11 (Confusion), Weedle lv11
- Anthony: Caterpie lv11, Weedle lv11, Kakuna lv12
- Charlie: Butterfree lv12 (Confusion), Beedrill lv12 (Poison Sting/Fury Attack), Caterpie lv11

### Pewter Gym Overhaul (`src/data/trainers_frlg.party`)
TRAINER_CAMPER_LIAM (gym trainer):
- Geodude lv11 (Tackle/Defense Curl/Rock Throw)
- Sandshrew lv12 (Scratch/Defense Curl/Sand Attack)
- Nidoran M lv12 — sweep counter (Leer/Tackle/Poison Sting/Double Kick; Poison resists Grass starter)

TRAINER_LEADER_BROCK (4 mons, Super Potion):
- Geodude lv13 — thematic (Tackle/Defense Curl/Rock Throw)
- Sandshrew lv14 — thematic (Scratch/Defense Curl/Sand Attack)
- Nidoran M lv14 — anti-sweep (Leer/Tackle/Poison Sting/Double Kick)
- Onix lv15 — Ace (Screech/Tackle/Bind/Rock Tomb)

### Rival Battle Overhaul (`src/data/trainers_frlg.party`)
All 8 encounter points × 3 starter branches = 24 trainer blocks updated.

**Design rules:**
- Rival's starter: SQUIRTLE branch → Piplup→Prinplup→Empoleon; BULBASAUR → Turtwig→Grotle→Torterra; CHARMANDER → Chimchar→Monferno→Infernape
- Raticate (non-anime) replaced with Eevee; evolves to Jolteon from Silph onward (anime Gary had Eevee)
- Growlithe → Arcanine from Silph onward (Fire Stone, anime-accurate)
- Rhyhorn → Rhydon from Route 22 Late (lv42 evolution)
- All mons given proper movesets (SS Anne and Tower entries were moveset-less)
- Abra given Confusion (was Teleport-only)

**Level caps per location (rival ace = badge cap):**
| Location | Context | Ace level |
|---|---|---|
| Oak's Lab | pre-game | lv5 |
| Route 22 Early | pre-Brock | lv14 |
| Cerulean | post-Brock | lv20 |
| SS Anne | post-Misty | lv24 |
| Pokémon Tower | post-Surge | lv29 |
| Silph Co | post-Erika | lv43 |
| Route 22 Late | post-all 8 | lv53 |
| Champion | final | lv63 |

---

## TODO (in order)

### 1. Anime-Accurate Route Encounters (remaining routes)
Read the FR table, cross-ref anime pool below, replace duplicate/non-anime slots.
Key locations still untouched: Route 2, Route 3, Route 4, Route 5/6, Route 7, Route 8, Route 9/10, Route 11-15, Route 22-25, Mt. Moon, Rock Tunnel, Pokémon Tower, Safari Zone, Seafoam, Victory Road.

### 2. Broader Trainer Team Overhaul
Once wild pools are expanded, trainers in each area should reflect available Pokémon for that route. Check trainers_frlg.party for each route's trainer class and expand their pools to match.

---

## Thematic Wild Pools (anime as reference, not hard rule)

| Location | Wild Pokémon (anime-confirmed) |
|---|---|
| Route 1 | Pidgey, Rattata, Spearow, Sandshrew, Mankey, Magikarp |
| Viridian Forest | Caterpie, Metapod, Weedle, Kakuna, Beedrill, Pidgey, Pidgeotto, Pikachu, Spearow |
| Route 3 | Pidgey, Jigglypuff (EP036 area) |
| Mt. Moon | Zubat, Geodude, Paras, Sandshrew, Clefairy |
| Routes 5/6 | Oddish, Rattata, Paras, Weepinbell, Caterpie + rare Bulbasaur |
| Route 7 | Mankey, Primeape, Poliwag, Poliwhirl, Bellsprout, Slowpoke, Dodrio |
| Celadon area | Oddish, Bellsprout, Gloom, Weepinbell, Tangela, Exeggcute |
| Pokémon Tower | Gastly, Haunter, Gengar ONLY |
| Fuchsia approach (R14/15) | Diglett, Dugtrio |
| Safari Zone | Tauros, Rhyhorn, Gyarados, Dratini, Dragonair, Kangaskhan |
| Water routes 19/20/21 | Tentacool, Tentacruel, Horsea, Krabby, Magikarp, Gyarados |
| Seafoam Islands | Shellder, Krabby, Gyarados, Slowpoke, Magikarp + rare Squirtle |
| Route 24/25 | Spearow + rare Charmander |
| Victory Road | Onix, Sandslash |

## Key Corrections (common misconceptions)
- Bulbasaur is NOT in Viridian Forest — Routes 5/6 Hidden Village (EP010)
- Pinsir/Scyther are NOT wild in Kanto OS — Dark City gym only (EP042)
- Charmander is near Cerulean (Route 24), NOT near Cinnabar

---

## File Map
| File | Purpose |
|---|---|
| `src/data/wild_encounters.h` | All wild tables. FRLG tables use `#ifdef FIRERED` / `#ifdef LEAFGREEN`. Kanto routes start ~line 8466 |
| `src/data/trainers_frlg.party` | All FRLG trainer parties. Human-readable format |
| `src/starter_choose.c:113-115` | Starter species macros |
| `data/maps/PalletTown_ProfessorOaksLab_Frlg/scripts.inc` | Oak lab starter dialogue and event vars |

## Table Format
```c
const struct WildPokemon sRoute1_FireRed_LandMons[] =
{
    { minLevel, maxLevel, SPECIES_XXX },  // slot 0: 20%
    ...                                    // slot 1: 20%
    ...                                    // slots 2-5: 10% each
    ...                                    // slots 6-7: 5% each
    ...                                    // slots 8-9: 4% each
    ...                                    // slots 10-11: 1% each
};
```
Always update BOTH `_FireRed_` and `_LeafGreen_` variants even though only FR compiles.

## Editing Protocol
- Read only the specific table being edited (use offset+limit in Read tool)
- Edit only changed slots
- Verify with grep after each batch, not by re-reading the full file
- Trainer format: search `=== TRAINER_NAME ===` in trainers_frlg.party, read -A 30 lines
