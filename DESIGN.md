# Elves Expanded - Combat Extended Design

## Overview

Elves Expanded is a lightweight compatibility and flavor mod for Faction - Elves (`ICC.FOV.ELVES`) and Combat Extended (`CETeam.CombatExtended`).

The goal is not to replace the elven identity, but to adapt it to a world where firearms and modern warfare exist. Elves are envisioned as disciplined marksmen and skirmishers who have embraced gunpowder without abandoning their traditions.

## Design Goals

- Preserve the fantasy aesthetic.
- Improve faction survivability under Combat Extended.
- Avoid turning elves into generic industrial factions.
- Encourage accurate, mobile combat.
- Favor quality over quantity.

## Combat Doctrine

Elves prefer:
- Precision.
- Range.
- Mobility.
- Ambush tactics.
- High-quality equipment.

Elves avoid:
- Heavy machine guns.
- Disposable troops.
- Mass assaults.
- Crude weapons.

## Faction Role Mapping

### High Elvish Kingdom

| defName | Old Label | New Label | CE Role |
|---------|-----------|-----------|---------|
| `Archer` | archer | **scout** | assault rifle |
| `Spearmen` | spearmen | **ranger** | rifle infantry |
| `Ranger` | swordmen | **blademaster** | melee + sidearm |
| `HeavyArcher` | heavy archer | **sharpshooter** | precision rifle |
| `Emperor` | emperor | *(unchanged)* | leader, precision + melee |

Combat kinds: 3 ranged (scout, ranger, sharpshooter) + 1 melee (blademaster). Balanced lineup. Nobles and citizens are non-combat roles left as-is.

### Dark Elvish Kingdom

| defName | Old Label | New Label | CE Role |
|---------|-----------|-----------|---------|
| `Archer` | archer | **scout** | SMG |
| `Ranger` | ranger | **marauder** | melee + sidearm |
| `Spearmen` | spearmen | *(unchanged)* | melee (polearm) |
| `Swordmaster` | swordmaster | **blademaster** | elite melee + sidearm |
| `Lord` | emperor | *(unchanged)* | leader, precision + melee |
| `Reaver` | *(new)* | **reaver** | SMG + shotgun rusher |

Combat kinds: 2 ranged (scout, reaver) + 3 melee (marauder, spearmen, blademaster). Melee-heavy to match their gene package, with a new CQB option. Nobles and citizens are non-combat roles left as-is.

### Wild Elvish Tribe

| defName | Old Label | New Label | CE Role |
|---------|-----------|-----------|---------|
| `Hunter` | hunter | *(unchanged)* | neolithic bow |
| `warrior` | warrior | *(unchanged)* | melee |
| `Archer` | archer | *(unchanged)* | neolithic bow |
| `HeavyArcher` | heavy archer | *(unchanged)* | heavy neolithic bow |
| `Swordkins` | swordkins | *(unchanged)* | melee |
| `SwornBlade` | swornblade | *(unchanged)* | elite melee |
| `Chief` | chief | *(unchanged)* | leader, melee |
| `Tribesmen` | tribesmen | *(unchanged)* | civilian |
| `Trader` | trader | *(unchanged)* | trader |
| `Child` | kins | *(unchanged)* | civilian |

All combat kinds remain pure tribal. No firearms. CE changes are loadout plumbing only (arrow magazines, shields).

### Celestia Elvish Empire

| defName | Old Label | New Label | CE Role |
|---------|-----------|-----------|---------|
| `Ranger` | celestia ranger | *(unchanged)* | spacer guns |
| `BladeMaster` | celestia blademaster | *(unchanged)* | melee + sidearm |
| `Mechanitor` | celestia mechanitor | *(unchanged)* | spacer guns + mechs |
| `Council` | celestian councilor | *(unchanged)* | leader, elite spacer |
| `Trader` | celestian trader | *(unchanged)* | trader |
| `Citizen` | celestian citizen | *(unchanged)* | civilian |
| `Child` | celestian citizen | *(unchanged)* | civilian |

Already spacer-tier. CE changes are loadout plumbing only (magazine counts, shields, sidearms).

## Loadout Philosophy

### Scouts -- Reconnaissance and skirmishing
- Weapons: SMG (Dark Elf) or assault rifle (High Elf)
- Armor: Light armor, cloaks
- Ammo: FullMetalJacket (standard issue)
- Magazines: 3 to 6
- Sidearm: Forced melee knife

### Rangers -- General infantry
- Weapons: Assault rifle
- Armor: Medium armor
- Ammo: FullMetalJacket (standard issue)
- Magazines: 3 to 5
- Budget: 300-650 (prices out most charge rifles)

### Sharpshooters -- Precision marksmen
- Weapons: Sniper rifle, precision rifle, DMR
- Armor: Light armor, recon gear
- Ammo: HollowPoint, ArmorPiercing, IncendiaryAP (specialist only)
- Magazines: 3 to 5
- Budget: 800-1600 (ensures proper snipers are reachable)

### Reavers -- Close quarters
- Weapons: SMG + shotgun (via `ElvesExpanded_Shotgun` tag)
- Armor: Flak vest, devilstrand hood, no helmet
- Ammo: FullMetalJacket, buckshot
- Magazines: 3 to 5
- Sidearm: Melee knife (50% chance)
- Smoke grenades: 50% chance, 1-3 shots

### Marauders -- Shield tank
- Weapons: One-handed melee (knife, club, mace, gladius, ikwa) + forced pistol
- Armor: Flak vest, ballistic shield (80% chance)
- Ammo: FullMetalJacket (pistol)
- Smoke grenades: 50% chance, 1-3 shots

### Blademasters -- Elite melee
- Weapons: Medieval melee + forced pistol
- Armor: Light armor, ballistic or energy shield (60% chance)
- Ammo: FullMetalJacket (pistol)
- Smoke grenades: 50% chance, 1-3 shots

### Spearmen -- Polearm melee
- Weapons: Polearm, spear
- Armor: Light armor, energy or ballistic shield (30% chance)
- Smoke grenades: 50% chance, 1-3 shots

### Elites/Leaders -- Command and precision
- Weapons: Precision rifle + melee
- Armor: High-quality ceremonial armor, ballistic shield (60%)
- Ammo: ArmorPiercing, HollowPoint, IncendiaryAP (specialist only)
- Magazines: 4 to 8

## Weapon Tags Preference Order
1. Precision rifles (`CE_AI_SR`)
2. Assault rifles (`CE_AI_AR`)
3. Shotguns (`ElvesExpanded_Shotgun`)
4. Carbines (`CE_SMG`)
5. Sidearms (`CE_Sidearm`, `CE_Sidearm_Melee`)

Heavy machine guns (`CE_MachineGun`) and launchers are excluded from all elven combat pawn kinds.

Note: `CE_AI_AR` matches both AssaultRifle and ChargeRifle in CE (ChargeRifle has `CE_AI_AR` + `AdvancedGun` tags). Rangers with this tag may occasionally spawn with charge rifles if weapon money overlaps. The ranger budget was lowered to 300-650 to reduce charge rifle frequency while keeping assault rifles affordable. The scout budget is 400-700 with `CE_AI_AR` only, meaning they share the assault rifle pool with rangers at a lower tier.

Ranged units use weighted alternate tag choices for headgear (60% basic / 40% advanced military pool), giving budget-driven variety from steel pots to composite helmets.

Note: Dark Elves have no rifleman line (ranger) or dedicated sharpshooter. Their gene package (Remarkable Melee, Strong Melee Damage, Aggressive) favors close-quarters combat. Their ranged capability comes from the scout and reaver kinds, with the Lord providing precision support.

## Faction Identity Changes

| Faction | Tech Level | Trader Kinds | Raid Loot |
|---------|-----------|-------------|-----------|
| High Elvish Kingdom | Medieval to Industrial | Neolithic to Outlander | Tribe to Outlander |
| Dark Elvish Kingdom | Medieval to Industrial | Neolithic to Outlander | Tribe to Outlander |
| Wild Elvish Tribe | Medieval (unchanged) | Neolithic (unchanged) | Tribe (unchanged) |
| Celestia Elvish Empire | Ultra (unchanged) | Outlander (unchanged) | Outlander (unchanged) |

## Ammo Usage by Role

| Role | Standard Ammo | Specialty Ammo |
|------|--------------|----------------|
| Scout | FullMetalJacket | none |
| Ranger | FullMetalJacket | none |
| Marauder | FullMetalJacket (sidearm) | none |
| Blademaster | FullMetalJacket (sidearm) | none |
| Sharpshooter | none | HollowPoint, ArmorPiercing, IncendiaryAP |
| Reaver | FullMetalJacket (SMG), Buckshot (shotgun) | none |
| Emperor/Lord | FullMetalJacket | ArmorPiercing, HollowPoint, IncendiaryAP |
| Councilor | FullMetalJacket | ArmorPiercing, HollowPoint, IncendiaryAP, ExplosiveAP |

Line troops use standard FullMetalJacket only. Specialty ammunition is reserved for elites and marksman specialists.

## Implementation

All changes are pure XML patches (no C#). The mod consists of four faction-specific files under `Patches/` that apply `PatchOperationReplace`, `PatchOperationAdd`, `PatchOperationAddModExtension`, and `PatchOperationConditional` to the target Faction - Elves defs.

CE integration uses `LoadoutPropertiesExtension` added via `PatchOperationAddModExtension` with:
- `primaryMagazineCount`: ammo magazines carried
- `weightedAmmoCategories`: ammo type preferences (HollowPoint, FullMetalJacket, ArmorPiercing, IncendiaryAP)
- `minAmmoCount`: minimum loose ammo
- `shieldMoney`, `shieldTags`, `shieldChance`: personal shields
- `forcedSidearm`, `sidearms`: backup weapons (pistols, melee, smoke grenades)

Custom tags created for this mod:
- `ElvesExpanded_Shotgun`: added to all shotguns via defName-based xpath; used by reavers to pull only shotguns without CE_AI_BROOM's pistol contamination

## Patched Pawn Kinds

### High Elvish Kingdom
- `HighElvish_Emperor`: weaponTags precision + melee, elite CE loadout
- `HighElvish_Ranger`: label becomes "blademaster", melee + sidearm
- `HighElvish_Spearmen`: label becomes "ranger", AR/rifle loadout
- `HighElvish_Swordmaster`: melee + sidearm
- `HighElvish_Archer`: label becomes "scout", assault rifle loadout
- `HighElvish_HeavyArcher`: label becomes "sharpshooter", precision loadout

### Dark Elvish Kingdom
- `DarkElvish_Lord`: weaponTags precision + melee, elite CE loadout
- `DarkElvish_Ranger`: label becomes "marauder", melee + sidearm
- `DarkElvish_Swordmaster`: label becomes "blademaster", elite melee + sidearm
- `DarkElvish_Reaver`: **new** rusher, SMG + shotgun loadout, devilstrand hood
- `DarkElvish_Archer`: label becomes "scout", SMG loadout

Dark Elvish Spearmen keep their original label and melee role (unchanged).

### Shotgun Tag Solution (5 WHYs)

The reaver uses a custom tag `ElvesExpanded_Shotgun` instead of CE's `CE_AI_BROOM` for shotguns. Here is why:

1. **Why were reavers spawning with handguns?**
   Because `CE_AI_BROOM` is CE's catch-all close-quarters tag -- it matches shotguns, handguns, revolvers, and SMGs together.

2. **Why does CE_AI_BROOM include handguns?**
   CE designed it as a single pool for every short-range weapon. There is no shotgun-only tag in CE.

3. **Why couldn't budget fix it?**
   RimWorld's weapon generator picks by weighted random from all weapons within budget. Once budget covers shotguns (~200 silver), all handguns (~70 silver) fit too. The odds are fixed at about 23% handgun regardless of budget size.

4. **Why not patch CE items?**
   Modifying third-party tags creates hidden dependencies -- patches can break on CE updates, affect other mods, and are fragile. Our rule: never patch CE or workshop mod items without explicit authorization.

5. **Why does a custom tag work?**
   `ElvesExpanded_Shotgun` is added to every shotgun across all installed mods via a single xpath that matches defNames containing `Shotgun`, `TrenchGun`, `USAS`, or `Saiga`. Zero handguns match. The reaver uses this tag instead of `CE_AI_BROOM`, pulling only shotguns. No CE tags are removed or modified -- only added to, which is safe.

### Wild Elvish Tribe
- `WildElvish_warrior`: CE loadout with shield (unchanged role)
- `WildElvish_Swordkins`: TribalShield
- `WildElvish_SwornBlade`: TribalShield
- `WildElvish_Archer`: arrow magazines, TribalShield
- `WildElvish_Hunter`: arrow magazines, TribalShield
- `WildElvish_HeavyArcher`: arrow magazines, TribalShield
- `HighElvish_Chief`: TribalShield

All wild elf combat kinds remain pure tribal with no firearm access.

### Celestia Elvish Empire
- `CelestiaElvish_Council`: elite CE loadout with shield
- `CelestiaElvish_BladeMaster`: melee + sidearm, shield
- `CelestiaElvish_Ranger`: spacer gun loadout
- `CelestiaElvish_Mechanitor`: spacer gun loadout

CE loadout plumbing for existing spacer-tier gear.

## Future Ideas
- Unique CE-compatible weapons (elven precision rifles, DMRs)
- Elven marksman armor with camo variants
- Recon units with cloaking
- Sniper squads
- Specialized ammunition (elven match, elven AP-I)
- Compatibility with Waymakers mod
