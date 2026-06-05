---
name: battle-royale-zone-map
description: Design, implement, review, or extend battle royale zone, safe area, storm circle, map, drop, rotation, and match pacing systems. Use when Codex is asked to build shrinking zones, blue-zone damage, safe circles, flight path, drop selection, map markers, pings, minimaps, vehicle rotations, late-game pacing, or survival shooter match flow.
---

# Battle Royale Zone Map

## Overview

Use this skill to design battle royale map and zone systems that create movement pressure, readable risk, and fair late-game pacing. Keep match flow data-driven so designers can tune timings, radius, damage, and placement rules.

## Core Principles

- The zone should create decisions, not random punishment.
- Communicate current safe area, next safe area, countdown, damage threat, and route options clearly.
- Separate match phase data from runtime zone state.
- Use weighted random placement with constraints to avoid impossible or unfair end zones.
- Keep map markers, pings, and team information readable under pressure.

## Zone Data

Define phase data with:

```ts
type ZonePhase = {
  index: number;
  waitMs: number;
  shrinkMs: number;
  radius: number;
  damagePerSecond: number;
  placementRule: ZonePlacementRule;
  revealNextAt?: "phase_start" | "after_delay" | "shrink_start";
};
```

Track runtime state: current center/radius, next center/radius, phase index, timers, damage tick accumulator, and whether next zone is revealed.

## Placement Rules

- Keep next zone inside current zone unless the design supports hard shifts.
- Avoid placing final zones entirely in water, cliffs, unreachable roofs, or inaccessible terrain unless those are valid combat spaces.
- Weight toward playable nav areas and away from spawn-only or vehicle-only regions.
- Respect special zones: cities, fields, hills, compounds, bridges, islands, and final-circle exclusions.
- Add deterministic seeding for replay, debug, and server validation.

## Map And Pings

- Main map: flight path, player/team position, current zone, next zone, danger zone, markers, waypoints, vehicle hints, and teammate pings.
- Minimap: nearby orientation, zone edge, shots or footsteps if supported, teammate markers, and heading.
- Ping system: location, enemy, loot, danger, regroup, vehicle, route, and defend/attack.
- Keep marker colors distinct and readable for colorblind users where possible.

## Match Flow

- Early game: broad safe area, loot and landing decisions.
- Mid game: rotation pressure, vehicle value, scouting, and compound choices.
- Late game: small safe areas, fewer UI distractions, high clarity for zone edge and enemy information.
- Overtime/final: damage and circle movement should be predictable enough for fair decisions.

## Testing

- Phase timers advance correctly.
- Zone damage applies only when outside safe area and respects downed/spectator rules.
- Next zone placement obeys constraints.
- Map and minimap display current and next zones correctly.
- Pings create, update, expire, and sync for teammates.
- Reconnect or replay reconstructs zone state from seed and phase state.

## Avoid

- Unreachable final circles unless explicitly designed.
- Hidden zone damage or unclear countdowns.
- Map clutter that hides safe area or teammate pings.
- Random placement that cannot be reproduced for debugging.
- Copying exact map, flight path UI, or zone timings from a specific commercial game.

## Acceptance Checklist

- Zone phases, damage, reveal, and shrink behavior are data-driven.
- Current and next safe areas are readable on HUD, minimap, and main map.
- Placement rules avoid invalid terrain and unfair endings.
- Pings and team markers remain readable during rotations.
- Tests cover timers, damage, placement, pings, map display, and reconnect state.
