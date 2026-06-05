---
name: game-skill-module
description: Design, implement, review, or extend reusable game skill and ability modules, including mobile MOBA hero ability systems inspired by lane-based arena games. Use when Codex is asked to build combat skills, active abilities, passive abilities, cooldown systems, mana or energy costs, target selection, buffs, debuffs, damage effects, status effects, skill trees, upgrade scaling, hotbars, ability UI, RPG/MOBA/action/card game skill systems, hero skills, joystick aiming, basic attacks, ultimates, battle spells, or data-driven gameplay ability logic.
---

# Game Skill Module

## Overview

Use this skill to build game ability systems that are data-driven, testable, extensible, and clear to players. Separate skill definition, runtime state, targeting, validation, execution, effects, and UI presentation.

When the user asks for a style like `Wangzhe Rongyao-style`, mobile MOBA, hero arena, 5v5 lane battle, or touch joystick combat, interpret the request as an original competitive mobile MOBA skill system. Do not copy specific heroes, skill names, icons, UI art, map layout, numeric balance, or protected presentation from an existing game; extract the broader requirements: responsive hero controls, clear skill slots, directional aiming, teamfight readability, cooldown discipline, and server-authoritative combat.

## Core Principles

- Treat a skill as data plus behavior. Avoid hard-coding every ability as a one-off branch unless the project is a tiny prototype.
- Separate static definition from runtime state. A fireball definition is shared; each caster's cooldown, charges, and learned level are runtime state.
- Make skill execution explicit: validate, select targets, pay cost, start cooldown, apply effects, emit events, update UI.
- Keep deterministic gameplay logic away from visual effects. VFX and animation should listen to skill events, not decide gameplay outcomes.
- Prefer composable effects for common behavior: damage, heal, shield, buff, debuff, movement, summon, resource change, status clear, projectile, area effect.
- Design for cancellation and failure: out of range, no target, insufficient resource, silenced, stunned, cooldown active, blocked line of sight, immune target.
- Keep player feedback first-class. Every blocked cast, cooldown, hit, miss, crit, buff, and expiration should have a readable feedback path.
- For mobile MOBA skills, prioritize responsiveness and clarity over simulation complexity. Players must understand whether a skill is ready, where it will land, who it will hit, and why it failed.

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
  input?: SkillInputRule;
  cancel?: CancelRule;
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
  upgradeAvailable?: boolean;
};
```

For mobile MOBA heroes, model the default kit explicitly:

```ts
type HeroKit = {
  heroId: string;
  passiveSkillId?: string;
  basicAttackSkillId: string;
  skillSlotIds: [string, string, string] | [string, string, string, string];
  battleSpellIds?: string[];
  recallSkillId?: string;
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

For mobile MOBA casts, include an input phase before execution:

1. Press skill button.
2. Show range and target indicator.
3. Update aim direction, area, or lock target while dragging.
4. Cancel if dragged to cancel zone or released outside valid state.
5. Execute on release, tap, or quick-cast rule.
6. Reconcile result with authoritative combat state if networked.

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
- Lock-on: tracks a selected target while still validating range, visibility, and target state at cast time.
- Skillshot: resolves against position, direction, projectile speed, hit shape, collision layers, and max travel distance.

Make targeting preview visible when relevant: range ring, area decal, path line, invalid red state, valid highlight, target outline.

## Mobile MOBA Direction

Use this direction when building a `Wangzhe Rongyao-style` hero skill system:

- Kit structure: passive, basic attack, 2-3 normal skills, ultimate, optional battle spell, recall, and item active if the game supports it.
- Skill slots: fixed bottom-right radial or clustered touch layout, with the basic attack as the largest frequent action and skills around it.
- Upgrade flow: show plus indicators when level gates allow upgrades; upgrading should update cooldown, damage, duration, cost, or special modifiers from data.
- Resource model: support mana, energy, rage, no-cost skills, ammo/charges, cooldown-only skills, and empowered next attack states.
- Targeting: support tap-to-cast, drag-to-aim, smart target, nearest enemy, lowest health, hero priority, minion/tower priority, and manual lock.
- Indicators: show circles, cones, lines, rectangles, dashes, target reticles, wall collision, landing zones, and invalid red states.
- Cancel behavior: drag to cancel, cancel button, release outside joystick threshold, interrupted cast, target lost, or forced movement cancellation.
- Combat rhythm: short cooldowns, responsive animation windows, clear backswing, combo-friendly state changes, and immediate UI feedback.
- Teamfight readability: make crowd control, invulnerability, shields, execute thresholds, knockups, slows, and displacement obvious but not visually noisy.
- Network: client may predict aim and animation, but authoritative hit validation, damage, cooldown, and resource changes should be resolved by the server in multiplayer.

Do not reproduce named heroes, exact skill kits, official icons, official UI layout, exact map mechanics, or balance numbers from any specific game.

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
- Empower: modifies the next basic attack or next skill, then consumes the empowered state.
- Execute: deals bonus or lethal damage under a health threshold, with explicit immunity and shield rules.
- Reveal: grants vision, detects hidden units, or marks targets for a duration.
- Terrain interaction: blocked by wall, passes through units, stops on first hit, bounces, creates zone, or pulls to terrain.

Each effect should specify source, target, magnitude, tags, duration, stacking rules, and event output.

## Status And Stacking

Define status behavior clearly:

- Duration: instant, timed, permanent, until condition, until combat ends.
- Stack mode: refresh duration, add stacks, replace stronger, replace weaker, independent instances, capped stacks.
- Tick timing: every second, turn start, turn end, on movement, on action, on damage.
- Removal: cleanseable, dispellable, death clears, persists through death, boss immune.
- Priority: control effects and immunity rules must be deterministic.

For MOBA crowd control, define a control taxonomy:

- Hard control: stun, knockup, suppression, freeze, fear, charm, taunt.
- Soft control: slow, blind, silence, disarm, root, cripple, reveal.
- Displacement: knockback, pull, push, airborne, drag, forced dash.
- Protection: immunity, unstoppable, cleanse, shield, damage reduction, untargetable.

Document which statuses interrupt channels, prevent movement, prevent casting, prevent basic attacks, block displacement, or ignore tenacity.

## Upgrade And Scaling

Support progression without rewriting logic:

- Level scaling: magnitude, cooldown, cost, range, duration, charges, area size.
- Stat scaling: attack, magic power, defense, max health, level, rarity, equipment, elemental affinity.
- Branch upgrades: choose one modifier from multiple options.
- Skill tree prerequisites: required level, prior skill, class, weapon, quest, item.
- Rarity modifiers: common, rare, epic, legendary variants.
- Balance hooks: expose numbers in data so designers can tune them without code changes.
- For MOBA balance, expose tuning fields for base damage, scaling ratios, cooldown per level, mana cost per level, projectile speed, cast range, area radius, control duration, shield amount, healing reduction, and target priority.

## UI Requirements

- Hotbar slot: icon, keybind, cooldown overlay, disabled state, cost indicator, charge count, active toggle state.
- Tooltip: name, type, cost, cooldown, range, target type, effect summary, scaling, current level, next level preview.
- Skill tree node: locked, unlockable, learned, upgraded, maxed, prerequisite lines, resource cost.
- Cast feedback: invalid reason, range preview, target highlight, cooldown sweep, resource flash, cast bar.
- Status icon: source, stack count, remaining duration, positive/negative classification, tooltip.
- Combat log or floating text: damage, heal, miss, immune, blocked, critical, status applied, status expired.

For mobile MOBA UI:

- Skill button: icon, cooldown radial, numeric remaining time, disabled overlay, mana warning, upgrade plus, aim preview while pressed.
- Basic attack button: larger hit target, target priority toggle if supported, attack range feedback.
- Ultimate: stronger visual treatment, level gate, ready pulse, cooldown emphasis.
- Battle spell/item active: smaller adjacent slot with independent cooldown.
- Cancel zone: visible only while dragging a targeted skill.
- Target lock panel: optional hero/minion/tower lock buttons with clear selected state.
- Buff/status strip: compact icons for shields, control immunity, stealth, slow, poison, burn, mark, and empowered attack.
- Kill/teamfight feedback: concise, high-contrast, and non-blocking; do not cover aiming or hero position.

## Architecture Guidance

- Keep skill definitions in JSON, YAML, ScriptableObject-like assets, database rows, or typed config depending on the engine.
- Keep core resolution logic pure where possible so it can be unit tested.
- Use event dispatch for UI, VFX, audio, quest triggers, achievements, and analytics.
- Avoid direct dependencies from core skill logic to rendering, DOM, animation, sound, or network transport.
- In multiplayer or authoritative simulations, validate casts on the server and treat the client preview as advisory.
- Use stable IDs for skills, effects, statuses, tags, and resources.
- For real-time competitive games, keep server and client skill definitions versioned. Reject casts when client skill data does not match the server's expected version.
- Keep input buffering and latency compensation explicit. Avoid hiding network corrections that change cooldowns, hit results, or resource costs without feedback.

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
- Drag aiming updates indicator without casting until release.
- Cancel zone prevents cast and does not start cooldown.
- Smart targeting selects the expected target by priority rules.
- Server rejection restores or reconciles cooldown/resource/UI state correctly.

## Avoid

- One-off skill branches scattered through player, enemy, UI, and animation code.
- Starting cooldown before knowing whether a cast is valid unless that is an explicit design rule.
- Letting visual animation decide whether gameplay damage happens.
- Hidden failure reasons that leave the player guessing.
- Tooltips that drift from actual data.
- Status effects with undocumented stacking or removal behavior.
- Skills with hard-coded numbers duplicated across UI and gameplay logic.
- Copying specific hero kits, official skill icons, exact UI composition, named mechanics, or balance numbers from a live commercial MOBA.
- Letting the client authoritatively decide hits or damage in competitive multiplayer.
- Target indicators that are visually impressive but inaccurate to real hit shapes.

## Workflow

1. Identify game genre and skill type: RPG, action, turn-based, card, MOBA, roguelike, idle, tactics, shooter, or puzzle.
2. Define the data model for skills, runtime state, resources, targets, effects, and statuses.
3. Implement validation and execution as separate steps.
4. Implement reusable effect handlers before adding special-case skills.
5. Wire events to UI, VFX, audio, logs, quests, and analytics.
6. Add tooltips, hotbar states, targeting preview, cooldown feedback, and failure messages.
7. Write focused tests for validation, effect application, cooldowns, costs, statuses, and upgrades.

For mobile MOBA skills:

1. Define hero kit slots and input rules before implementing individual abilities.
2. Build targeting previews for tap, drag, lock-on, direction, area, dash, and skillshot skills.
3. Implement cancel, interruption, and invalid-target behavior.
4. Add upgrade data and per-level tuning.
5. Wire skill button UI to the same data used by combat logic.
6. Validate server-authoritative outcomes if multiplayer is in scope.

## Acceptance Checklist

- Skill definitions are data-driven and separate from runtime state.
- Cast validation returns clear success or failure results.
- Cooldown, cost, target, range, status, and immunity rules are deterministic.
- Effects are composable and reusable across multiple skills.
- UI reflects actual gameplay data and updates after every relevant event.
- Upgrades and scaling can be tuned without duplicating logic.
- Tests cover blocked casts, successful casts, stacking, expiration, and UI-visible state.
- For MOBA use cases, touch aiming, cancel behavior, target priority, cooldown reconciliation, control effects, and teamfight feedback are all defined and tested.
