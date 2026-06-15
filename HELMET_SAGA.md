# The Helmet Saga

Everything we tried to get elven pawns to wear combat helmets.

## Problem

Ranged units (scouts, rangers, sharpshooters) were spawning with steel circlets, tuques, top hats, berets, stellic crowns, bestower hoods -- anything but actual ballistic helmets.

## Attempts

### 1. PatchOperationReplace on apparelRequired/li

Tried replacing `<li>Apparel_SimpleHelmet</li>` with `<li>Apparel_AdvancedHelmet</li>`.

**Result:** Failed silently. XPath couldn't find the `<li>` element -- or the replace didn't work in the XML DOM. Pawns kept getting simple helmets.

### 2. PatchOperationRemove on entire apparelRequired + PatchOperationAdd

Removed the whole `<apparelRequired>` element, then re-added it with `Apparel_AdvancedHelmet`.

**Result:** Pawns spawned with no headgear at all, then fell back to random hats from `apparelTags`. The forced removal worked, but the re-add either failed or the helmet conflicted with something.

### 3. PatchOperationAdd to existing apparelRequired (don't remove, just add)

Added `Apparel_AdvancedHelmet` alongside `Apparel_SimpleHelmet` without removing anything.

**Result:** Pawns still got simple helmets. The game apparently picks one required item per body slot and prefers the existing one.

### 4. Discovered CE strips stuffCategories from Apparel_AdvancedHelmet

CE's `Apparel_Hats.xml` removes `stuffCategories` from the composite helmet, making it **non-stuffable**. The elven `specificApparelRequirements` forces `Steel` for UpperHead/FullHead body slots. When the game tries to generate a non-stuffable helmet but the constraint demands a specific stuff, the helmet gets rejected and it falls back to steel circlets (which ARE stuffable).

**Lesson:** CE's composite helmet cannot be forced via `apparelRequired` if `specificApparelRequirements` demands a stuff category.

### 5. Remove specificApparelRequirements head constraints

Removed the `<li><bodyPartGroup>UpperHead</bodyPartGroup><stuff>Steel</stuff></li>` entries from `specificApparelRequirements`, so no stuff constraint conflicts with the helmet.

**Result:** Pawns still got tuques and circlets. The `apparelTags` still had `IndustrialBasic`, `Circlet`, `Royal`, `BestowerHood`, `Robe` -- all pulling in civilian hats.

### 6. Add IndustrialMilitaryAdvanced to apparelTags

Added `IndustrialMilitaryAdvanced` tag to combat pawn kinds, so the composite helmet would be a valid pick via tag-based generation.

**Result:** Composited helmets showed up, but only ~1 in 20 spawns. Too many competing tags.

### 7. Broaden composite helmet's tags

Added `IndustrialMilitary` and `IndustrialMilitaryBasic` to the composite helmet's own tags so it matches more of the pawns' existing tags.

**Result:** Marginal improvement. Still competing with too many civilian tags.

### 8. Add civilian tags to apparelDisallowTags

Tried adding `Circlet`, `IndustrialBasic`, `BestowerHood`, `Robe`, `Royal` to `apparelDisallowTags`.

**Result:** `PatchOperationAdd` on `apparelDisallowTags` failed silently. The `apparelDisallowTags` element is inherited from the abstract base and doesn't exist as a direct child at patch time -- same issue as `techLevel` earlier.

### 9. Wrap disallowTags in PatchOperationConditional

Used `PatchOperationConditional` to check if `apparelDisallowTags` exists as a direct child. If yes, add to it. If no, create it on the def.

**Result:** Patches now apply without errors. But we also discovered `DarkElvish_Archer` (scout) was NEVER patched -- still had forced `Apparel_HatHood` and no `IndustrialMilitaryAdvanced` tag.

### 10. Fixed missing DarkElvish_Archer + Royal for high elves

Added full apparel treatment for `DarkElvish_Archer`: remove hood, remove head constraints, add tag, disallow civilian tags. Also added `Royal` to all high elf disallow lists.

**Current state:** Both high and dark elf archers (scouts) now have all civilian/fancy hats disallowed, `IndustrialMilitaryAdvanced` tag added, forced headwear removed, head material constraints removed, and apparel budgets bumped. Remaining allowed tags are `MedievalMilitaryLight`, `IndustrialMilitaryBasic`, `IndustrialMilitaryAdvanced` -- and the composite helmet now matches all three.

## Key Lessons

- **Inherited elements aren't direct children at patch time.** `techLevel`, `apparelDisallowTags`, and any other element from an abstract base must be patched via `PatchOperationConditional`.
- **CE strips stuffCategories from the composite helmet.** This makes `specificApparelRequirements` stuff constraints incompatible with it.
- **apparelRequired forces an item, but conflicts with stuff constraints cause fallback to tag-based generation.**
- **Tag-based generation picks randomly from all matching tags.** To guarantee a specific item, eliminate competing tags via `apparelDisallowTags`.
- **`PatchOperationRemove` succeeds even with 0 matches** (no error logged). `PatchOperationReplace` fails if 0 matches.
- **XML comments cannot contain `--`.** This broke the entire patch file parse at one point.
