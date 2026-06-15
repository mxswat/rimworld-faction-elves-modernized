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
| `Archer` | archer | **scout** | SMG skirmisher |
| `Spearmen` | spearmen | **ranger** | rifle infantry |
| `Ranger` | swordmen | **blademaster** | melee + sidearm |
| `HeavyArcher` | heavy archer | **sharpshooter** | precision rifle |
| `Noble` | noble | *(unchanged)* | trader, sidearm + melee |
| `Emperor` | emperor | *(unchanged)* | leader, precision + melee |
| `Citizen` | citizen | *(unchanged)* | civilian |
| `Child` | citizen | *(unchanged)* | civilian |

Combat kinds: 3 ranged (scout, ranger, sharpshooter) + 1 melee (blademaster). Balanced lineup.

### Dark Elvish Kingdom

| defName | Old Label | New Label | CE Role |
|---------|-----------|-----------|---------|
| `Archer` | archer | **scout** | SMG skirmisher |
| `Ranger` | ranger | **marauder** | melee + sidearm |
| `Spearmen` | spearmen | *(unchanged)* | melee (polearm) |
| `Swordmaster` | swordmaster | **blademaster** | elite melee + sidearm |
| `Noble` | noble | *(unchanged)* | trader, sidearm + melee |
| `Lord` | emperor | *(unchanged)* | leader, precision + melee |
| `Citizen` | citizen | *(unchanged)* | civilian |
| `Child` | citizen | *(unchanged)* | civilian |

Combat kinds: 1 ranged (scout) + 3 melee (marauder, spearmen, blademaster). Melee-heavy to match their gene package (Remarkable Melee, Strong Melee Damage, Aggressive).

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
- Weapons: SMG, sidearm, light rifle
- Armor: Light armor, cloaks
- Ammo: FullMetalJacket (standard issue)
- Magazines: 3 to 6

### Rangers -- General infantry
- Weapons: Assault rifle, bolt-action rifle, hunting rifle
- Armor: Medium armor
- Ammo: FullMetalJacket (standard issue)
- Magazines: 3 to 5

### Sharpshooters -- Precision marksmen
- Weapons: Sniper rifle, precision rifle, DMR
- Armor: Light armor, recon gear
- Ammo: HollowPoint, ArmorPiercing, IncendiaryAP (specialist only)
- Magazines: 3 to 5

### Blademasters -- Close assault
- Weapons: Elven saber (melee) + sidearm
- Armor: Light armor, shield
- Ammo: FullMetalJacket (sidearm, standard issue)

### Nobles/Elites -- Command and precision
- Weapons: Precision rifle + melee
- Armor: High-quality ceremonial armor, shield
- Ammo: ArmorPiercing, HollowPoint, IncendiaryAP (specialist only)
- Magazines: 4 to 8

## Weapon Tags Preference Order
1. Precision rifles (`CE_AI_SR`)
2. Hunting rifles (`SimpleGun`, `CE_AI_SR`)
3. Carbines (`CE_SMG`)
4. Assault rifles (`CE_AI_AR`)
5. Sidearms (`CE_Sidearm`, `CE_Sidearm_Melee`)

Heavy machine guns (`CE_MachineGun`) and launchers are excluded from all elven combat pawn kinds.

Note: `CE_AI_AR` matches both AssaultRifle and ChargeRifle in CE (ChargeRifle has `CE_AI_AR` + `AdvancedGun` tags). Rangers with this tag may occasionally spawn with charge rifles if weapon money overlaps. This is intentional since charge rifles fit the elven precision theme.

Ranged units (scouts, rangers, sharpshooters) have their required helmet upgraded from `Apparel_SimpleHelmet` (medieval pot helmet) to `Apparel_ArmorHelmet` (flak helmet) for better ballistic protection under CE.

Note: Dark Elves have no rifleman line (ranger) or dedicated sharpshooter. Their gene package (Remarkable Melee, Strong Melee Damage, Aggressive) favors close-quarters combat. Their ranged capability comes from a single scout kind and elite nobles with precision rifles.

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
| Noble | FullMetalJacket | ArmorPiercing, HollowPoint, IncendiaryAP |
| Emperor/Lord | FullMetalJacket | ArmorPiercing, HollowPoint, IncendiaryAP |
| Councilor | FullMetalJacket | ArmorPiercing, HollowPoint, IncendiaryAP, ExplosiveAP |

Line troops use standard FullMetalJacket only. Specialty ammunition is reserved for elites and marksman specialists.

## Implementation

All changes are pure XML patches (no C#). The mod consists of a single `Patches/` file that applies `PatchOperationReplace`, `PatchOperationAdd`, `PatchOperationAddModExtension`, and `PatchOperationConditional` to the target Faction - Elves defs.

CE integration uses `LoadoutPropertiesExtension` added via `PatchOperationAddModExtension` with:
- `primaryMagazineCount`: ammo magazines carried
- `weightedAmmoCategories`: ammo type preferences (HollowPoint, FullMetalJacket, ArmorPiercing, IncendiaryAP)
- `minAmmoCount`: minimum loose ammo
- `shieldMoney`, `shieldTags`, `shieldChance`: personal shields
- `forcedSidearm`, `sidearms`: backup weapons

## Patched Pawn Kinds

### High Elvish Kingdom
- `HighElvish_Citizen`: CE loadout (minimal)
- `HighElvish_Noble`: weaponTags sidearm + melee, CE loadout with shield
- `HighElvish_Emperor`: weaponTags precision + melee, elite CE loadout
- `HighElvish_Ranger`: label becomes "blademaster", melee + sidearm
- `HighElvish_Spearmen`: label becomes "ranger", AR/rifle loadout
- `HighElvish_Swordmaster`: melee + sidearm
- `HighElvish_Archer`: label becomes "scout", SMG loadout
- `HighElvish_HeavyArcher`: label becomes "sharpshooter", precision loadout

### Dark Elvish Kingdom
- `DarkElvish_Citizen`: CE loadout (minimal)
- `DarkElvish_Noble`: weaponTags sidearm + melee, precision ammo
- `DarkElvish_Lord`: weaponTags precision + melee, elite CE loadout
- `DarkElvish_Ranger`: label becomes "marauder", melee + sidearm
- `DarkElvish_Swordmaster`: label becomes "blademaster", elite melee + sidearm
- `DarkElvish_Archer`: label becomes "scout", SMG loadout

Dark Elvish Spearmen keep their original label and melee role (unchanged).

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
- `CelestiaElvish_Citizen`: CE loadout (minimal)
- `CelestiaElvish_Trader`: CE loadout
- `CelestiaElvish_Council`: elite CE loadout with shield
- `CelestiaElvish_BladeMaster`: melee + sidearm, shield
- `CelestiaElvish_Ranger`: spacer gun loadout
- `CelestiaElvish_Mechanitor`: spacer gun loadout

No role or label changes. CE loadout plumbing only.

## Future Ideas
- Unique CE-compatible weapons (elven precision rifles, DMRs)
- Elven marksman armor with camo variants
- Recon units with cloaking
- Sniper squads
- Specialized ammunition (elven match, elven AP-I)
- Compatibility with Waymakers mod
