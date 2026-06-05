---
name: br-sniper-weapon-system
description: Design, implement, review, or extend battle royale sniper weapon systems inspired by high-powered bolt-action rifles and long-range combat. Use when Codex is asked to build sniper rifles, scope aiming, bullet drop, travel time, headshot damage, attachments, zeroing, sway, breath hold, reload cycles, rare crate weapons, anti-armor shots, long-range UI, or tactical shooter weapon balance. Do not use real-world weapon instructions; keep guidance at game-system level.
---

# BR Sniper Weapon System

## Overview

Use this skill to design sniper weapons for battle royale games where long-range precision, rarity, risk, and readable counterplay matter. Treat the AWM-like fantasy as an original high-powered crate sniper archetype, not a copy of any specific game's weapon values, icons, sounds, or assets.

## Core Principles

- Make the sniper role distinct: high precision, high damage, low fire rate, limited ammo, loud report, and exposure while aiming.
- Balance power with scarcity, reload time, scope handling, bullet travel, target movement, and positional risk.
- Keep hit rules explicit: body zones, armor interaction, headshot multiplier, falloff, penetration, and shield or helmet behavior.
- Separate weapon definition from runtime weapon state and player attachments.
- Avoid real ballistic or weapon-building guidance. Model game feel, not real-world operation.

## Weapon Data

Define weapon data with fields like:

```ts
type SniperWeaponDefinition = {
  id: string;
  displayName: string;
  archetype: "bolt_sniper" | "marksman" | "anti_material" | "energy_sniper";
  rarity: "common" | "rare" | "epic" | "legendary" | "crate";
  ammoType: string;
  magazineSize: number;
  fireIntervalMs: number;
  reloadMs: number;
  chamberMs: number;
  baseDamage: number;
  headMultiplier: number;
  armorRules: ArmorInteractionRule[];
  projectile: ProjectileRule;
  handling: HandlingRule;
  attachments: AttachmentSlot[];
};
```

Track runtime state separately: ammo in mag, reserve ammo, chambered state, reload state, scope state, last shot time, current attachments, and durability if the game uses it.

## Long-Range Mechanics

- Projectile travel: use speed, gravity/drop, max lifetime, drag only if the engine already supports it.
- Bullet drop: communicate through scope marks, zeroing, or training cues.
- Sway: increases while standing, moving, exhausted, damaged, or holding breath too long.
- Breath hold: temporarily stabilizes aim, drains stamina, then adds recovery sway.
- Scope zoom: support multiple optics, field of view changes, sensitivity scaling, and scope-in time.
- Sound: long-range shots should reveal direction or approximate location through audio cues.
- Tracers and impacts: use subtle visual feedback so targets can infer incoming fire without clutter.

## Damage And Armor

- Define body zones: head, torso, limb, vehicle, deployable, and destructible cover if relevant.
- Define armor interaction: helmet reduction, armor durability, penetration tag, damage cap, or shield break.
- Make rare sniper shots feel decisive but not unfair. If one-shot headshots exist, counter them with rarity, sound, aim time, helmet rules, and cover.
- Keep downed-state and revive-state damage rules explicit.
- For vehicles, decide whether the sniper can damage occupants, tires, engine, or only vehicle health.

## Attachments

Support game-level attachments:

- Optic: 4x, 6x, 8x, thermal-like, variable zoom, or fictional long-range scope.
- Muzzle: suppressor, flash hider, compensator. Suppressors reduce detectability, not raw lethality by default.
- Magazine: extended, quickdraw, extended quickdraw.
- Stock/grip: sway reduction, ADS speed, recoil recovery.
- Ammo variant: rare high-caliber rounds only if the game has ammo scarcity rules.

Attachments should change clear stats and update UI/tooltips from the same data used by gameplay.

## UI Requirements

- Scope overlay: clean reticle, range marks, zeroing indicator if supported, ammo count, hold breath indicator, and low obstruction.
- Weapon HUD: ammo in mag, reserve ammo, reload state, fire mode, attachment icons, and rarity.
- Hit feedback: headshot, armor break, downed, eliminated, limb hit, vehicle hit, and blocked by cover.
- Loot tooltip: damage class, ammo type, supported attachments, rarity, and role description.
- Training prompt: explain bullet travel/drop in game terms, not real-world instruction.

## Testing

- Cannot fire while reloading or chambering unless design allows canceling.
- Scope sensitivity and zoom state update correctly.
- Projectile hit detection matches reticle and travel rules.
- Armor and body-zone damage are deterministic.
- Attachments affect only intended stats.
- Ammo, reload, chamber, and reserve counts cannot desync.
- Rare weapon spawn and ammo scarcity rules match loot tables.

## Avoid

- Real-world weapon operation guidance or exact real weapon performance claims.
- Copying official game weapon icons, names, sounds, UI, or numeric stats.
- Perfect hitscan behavior if the game promises long-range projectile skill.
- Scope overlays that hide targets or make mobile aiming unreadable.
- Damage values duplicated between weapon logic and UI tooltip.

## Acceptance Checklist

- Sniper identity is high-impact, long-range, scarce, and counterplay-aware.
- Projectile, scope, sway, reload, chamber, ammo, and armor rules are explicit.
- UI communicates readiness, range, ammo, hit feedback, and attachment changes.
- Weapon data is tunable without rewriting gameplay code.
- Tests cover firing, reload, hit detection, armor, attachments, and rare loot behavior.
