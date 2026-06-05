---
name: game-skill-module
description: Design, implement, review, or extend reusable game skill and ability modules. Use when Codex is asked to build combat skills, active abilities, passive abilities, cooldown systems, mana or energy costs, target selection, buffs, debuffs, damage effects, status effects, skill trees, upgrade scaling, hotbars, ability UI, RPG/MOBA/action/card game skill systems, or data-driven gameplay ability logic.
---

# Game Skill Module

## Overview

Use this skill to build game ability systems that are data-driven, testable, extensible, and clear to players. Separate skill definition, runtime state, targeting, validation, execution, effects, and UI presentation.

## Core Principles

- Treat a skill as data plus behavior. Avoid hard-coding every ability as a one-off branch unless the project is a tiny prototype.
- Separate static definition from runtime state. A fireball definition is shared; each caster's cooldown, charges, and learned level are runtime state.
- Make skill execution explicit: validate, select targets, pay cost, start cooldown, apply effects, emit events, update UI.
- Keep deterministic gameplay logic away from visual effects. VFX and animation should listen to skill events, not decide gameplay outcomes.
- Prefer composable effects for common behavior: damage, heal, shield, buff, debuff, movement, summon, resource change, status clear, projectile, area effect.
- Design for cancellation and failure: out of range, no target, insufficient resource, silenced, stunned, cooldown active, blocked line of sight, immune target.
- Keep player feedback first-class. Every blocked cast, cooldown, hit, miss, crit, buff, and expiration should have a readable feedback path.

## Data Model

Define skills with fields like:

```ts
type SkillDefinition = {
  id: string;
  name: string;
  description: string;
  icon: string;
  tags: SkillTag[];
  kind: "active" | "passive" | "toggle" | "ultimate";
  target: TargetRule;
  cost: ResourceCost[];
  cooldownMs: number;
  castTimeMs?: number;
  range?: number;
  charges?: number;
  effects: SkillEffect[];
  scaling?: ScalingRule[];
  requirements?: Requirement[];
};
```

Track runtime state separately:

```ts
type SkillState = {
  skillId: string;
  level: number;
  cooldownUntil: number;
  chargesRemaining?: number;
  chargeReadyAt?: number;
  isEquipped?: boolean;
  isToggledOn?: boolean;
};
```

## Execution Flow

Use this sequence for active skills:

1. Resolve caster and skill definition.
2. Read caster's skill runtime state.
3. Validate learned/equipped status.
4. Validate cooldown, charges, required weapon, silence/stun/root state, and resource cost.
5. Resolve target using target rules.
6. Validate range, line of sight, faction rules, immunities, and target liveness.
7. If valid, reserve or pay resources.
8. Start cast time or execute instantly.
9. Apply effects in a deterministic order.
10. Start cooldown or consume charge.
11. Emit events for animation, sound, combat log, floating text, quest triggers, analytics, and UI updates.

Return a structured result:

```ts
type CastResult =
  | { ok: true; events: SkillEvent[] }
  | { ok: false; reason: CastFailureReason; message: string };
```

## Targeting

Support target modes based on game genre:

- Self: affects caster only.
- Unit: one ally, enemy, neutral unit, or any valid unit.
- Area: circle, cone, line, rectangle, arc, or tile region.
- Direction: fires toward a vector or facing.
- Ground point: targets a position.
- Chain: jumps between units with constraints.
- Aura: continuously affects entities in range.
- Passive trigger: activates on event such as hit, kill, dodge, block, low health, turn start, or card draw.

Make targeting preview visible when relevant: range ring, area decal, path line, invalid red state, valid highlight, target outline.

## Effects

Model common effects as composable units:

- Damage: flat, scaled, percent health, true, physical, magical, elemental.
- Heal: instant, over time, percent, smart target.
- Shield: absorb amount, damage type filter, duration, break event.
- Buff/debuff: stat modifier, movement speed, attack speed, defense, vulnerability, haste, slow.
- Crowd control: stun, root, silence, charm, fear, knockback, pull, taunt, disarm.
- Resource change: mana, stamina, rage, energy, ammo, combo points, cards.
- Movement: dash, teleport, leap, blink, forced movement.
- Summon: minion, trap, turret, projectile, zone.
- Cleanse/dispel: remove statuses by tag or priority.
- Trigger: schedule delayed effect, periodic tick, on-hit, on-expire, on-kill.

Each effect should specify source, target, magnitude, tags, duration, stacking rules, and event output.

## Status And Stacking

Define status behavior clearly:

- Duration: instant, timed, permanent, until condition, until combat ends.
- Stack mode: refresh duration, add stacks, replace stronger, replace weaker, independent instances, capped stacks.
- Tick timing: every second, turn start, turn end, on movement, on action, on damage.
- Removal: cleanseable, dispellable, death clears, persists through death, boss immune.
- Priority: control effects and immunity rules must be deterministic.

## Upgrade And Scaling

Support progression without rewriting logic:

- Level scaling: magnitude, cooldown, cost, range, duration, charges, area size.
- Stat scaling: attack, magic power, defense, max health, level, rarity, equipment, elemental affinity.
- Branch upgrades: choose one modifier from multiple options.
- Skill tree prerequisites: required level, prior skill, class, weapon, quest, item.
- Rarity modifiers: common, rare, epic, legendary variants.
- Balance hooks: expose numbers in data so designers can tune them without code changes.

## UI Requirements

- Hotbar slot: icon, keybind, cooldown overlay, disabled state, cost indicator, charge count, active toggle state.
- Tooltip: name, type, cost, cooldown, range, target type, effect summary, scaling, current level, next level preview.
- Skill tree node: locked, unlockable, learned, upgraded, maxed, prerequisite lines, resource cost.
- Cast feedback: invalid reason, range preview, target highlight, cooldown sweep, resource flash, cast bar.
- Status icon: source, stack count, remaining duration, positive/negative classification, tooltip.
- Combat log or floating text: damage, heal, miss, immune, blocked, critical, status applied, status expired.

## Architecture Guidance

- Keep skill definitions in JSON, YAML, ScriptableObject-like assets, database rows, or typed config depending on the engine.
- Keep core resolution logic pure where possible so it can be unit tested.
- Use event dispatch for UI, VFX, audio, quest triggers, achievements, and analytics.
- Avoid direct dependencies from core skill logic to rendering, DOM, animation, sound, or network transport.
- In multiplayer or authoritative simulations, validate casts on the server and treat the client preview as advisory.
- Use stable IDs for skills, effects, statuses, tags, and resources.

## Testing

Cover these cases:

- Cannot cast while on cooldown.
- Cannot cast without enough resource.
- Cannot cast on invalid target or out-of-range target.
- Cooldown starts only after a successful cast unless design says otherwise.
- Costs, charges, and cooldowns update correctly.
- Effects apply in deterministic order.
- Buffs and debuffs stack according to rules.
- Expiration and cleanse behavior work.
- UI reflects cooldown, disabled state, tooltip numbers, charges, and active status.
- Upgrade scaling changes only the intended values.

## Avoid

- One-off skill branches scattered through player, enemy, UI, and animation code.
- Starting cooldown before knowing whether a cast is valid unless that is an explicit design rule.
- Letting visual animation decide whether gameplay damage happens.
- Hidden failure reasons that leave the player guessing.
- Tooltips that drift from actual data.
- Status effects with undocumented stacking or removal behavior.
- Skills with hard-coded numbers duplicated across UI and gameplay logic.

## Workflow

1. Identify game genre and skill type: RPG, action, turn-based, card, MOBA, roguelike, idle, tactics, shooter, or puzzle.
2. Define the data model for skills, runtime state, resources, targets, effects, and statuses.
3. Implement validation and execution as separate steps.
4. Implement reusable effect handlers before adding special-case skills.
5. Wire events to UI, VFX, audio, logs, quests, and analytics.
6. Add tooltips, hotbar states, targeting preview, cooldown feedback, and failure messages.
7. Write focused tests for validation, effect application, cooldowns, costs, statuses, and upgrades.

## Acceptance Checklist

- Skill definitions are data-driven and separate from runtime state.
- Cast validation returns clear success or failure results.
- Cooldown, cost, target, range, status, and immunity rules are deterministic.
- Effects are composable and reusable across multiple skills.
- UI reflects actual gameplay data and updates after every relevant event.
- Upgrades and scaling can be tuned without duplicating logic.
- Tests cover blocked casts, successful casts, stacking, expiration, and UI-visible state.
