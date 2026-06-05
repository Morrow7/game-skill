---
name: tactical-shooter-gunplay
description: Design, implement, review, or extend tactical shooter gunplay systems for battle royale and survival shooters. Use when Codex is asked to build shooting feel, recoil, spread, ADS, hip fire, hit detection, fire modes, reloads, movement accuracy, stance modifiers, leaning, cover play, weapon classes, throwable combat, or competitive shooter responsiveness. Keep guidance at game-design and simulation level, not real-world weapon instruction.
---

# Tactical Shooter Gunplay

## Overview

Use this skill to build readable, responsive shooter mechanics for tactical games. Prioritize fair hit feedback, controllable weapon identity, movement tradeoffs, and clear state transitions.

## Core Principles

- Separate input, weapon state, projectile/hit resolution, animation, audio, and UI.
- Make every weapon class feel different through fire rate, recoil, spread, range, handling, reload, attachment support, and ammo economy.
- Use gameplay-safe abstractions. Do not provide real-world firearm training or construction details.
- Favor deterministic server-side hit validation for competitive multiplayer.
- Make missed shots understandable: recoil, spread, target movement, range, obstruction, or latency.

## Weapon States

Model state transitions explicitly:

- Idle, equip, ADS, hip fire, firing, recoil recovery, reload, tactical reload, empty reload, chamber, switch weapon, sprint lockout, vault lockout, stunned, downed.
- Allow or disallow canceling each state intentionally.
- Prevent animation-only states from changing gameplay truth.

## Accuracy And Recoil

- Hip fire: wider spread, movement penalty, stance modifier.
- ADS: narrower spread, slower movement, scope sensitivity, enter/exit timing.
- Recoil: vertical kick, horizontal drift, recovery speed, pattern randomness, camera impulse, weapon climb.
- Movement: sprinting blocks fire or heavily penalizes accuracy; crouch/prone improves stability if the game supports it.
- Sustained fire: spread or recoil should grow predictably enough for skill expression.

## Hit Resolution

- Choose hitscan, projectile, or hybrid per weapon class.
- Resolve body zones, armor, cover, penetration tags, distance falloff, and damage type.
- Emit hit events for UI, audio, effects, analytics, and kill feed.
- In multiplayer, reconcile client prediction with server hit results.

## Combat Feedback

- Use distinct feedback for hit, armor hit, headshot, downed, eliminated, blocked, immune, and teammate hit if friendly fire exists.
- Keep muzzle flash, tracers, impact effects, camera shake, and sound informative but not blinding.
- Show reload, low ammo, no ammo, fire mode, stance, and ADS state clearly.

## Throwables And Utility

- Grenades, smoke, flash, decoys, mines, and deployables should use clear equip, cook, throw arc, fuse, bounce, effect radius, and counterplay rules.
- Show trajectory preview when genre and platform allow it.
- Avoid utility effects that obscure all readability for too long.

## Testing

- Fire rate cannot exceed weapon definition.
- Reload and cancel rules preserve ammo correctly.
- ADS and hip fire use intended spread.
- Recoil recovers predictably.
- Movement state modifies accuracy as intended.
- Server/client reconciliation handles rejected hits cleanly.
- Hit feedback matches resolved damage events.

## Avoid

- Real firearm operation or tactical training details.
- Copying exact weapon stats, recoil patterns, sounds, or UI from a commercial shooter.
- Letting animation events be the only source of truth for ammo or hits.
- Hidden spread or recoil behavior with no player-readable feedback.

## Acceptance Checklist

- Gunplay has clear state transitions and weapon identity.
- Recoil, spread, ADS, movement, reload, and hit rules are data-driven.
- Multiplayer hit validation is authoritative where needed.
- Feedback explains shot results without overwhelming the screen.
- Tests cover firing, reloads, recoil, spread, hit resolution, and UI-visible states.
