---
name: game-engine-architecture
description: Design, implement, review, or extend game engine architecture and runtime systems. Use when Codex is asked to build or improve a game engine, game framework, runtime loop, scene system, entity-component system, rendering pipeline, input layer, physics integration, asset loading, audio, UI integration, save system, debugging tools, performance profiling, or cross-platform game infrastructure.
---

# Game Engine Architecture

## Overview

Use this skill to design game engine systems that are modular, deterministic where needed, performant, debuggable, and friendly to gameplay code. Keep runtime systems separated by responsibility while making data flow and lifecycle order explicit.

## Core Principles

- Keep the engine layer separate from game-specific content. The engine owns loops, scenes, input, rendering, resources, audio, timing, and platform adapters; game code owns rules, content, levels, characters, and progression.
- Make frame order explicit. Hidden update order causes hard-to-debug behavior.
- Prefer data-driven configuration for scenes, entities, assets, animations, physics bodies, and UI layouts when the project will grow.
- Keep systems loosely coupled through events, commands, handles, or service interfaces.
- Avoid letting rendering, audio, or UI decide gameplay truth.
- Design for debugging from the start: inspector data, logs, frame stats, collision views, asset errors, and deterministic replay hooks where useful.
- Keep the smallest viable engine for the game. Do not build a general-purpose engine when the project needs a focused runtime.

## Runtime Loop

Use a stable loop structure:

1. Poll platform events.
2. Update input state.
3. Accumulate fixed timestep if physics or deterministic simulation is needed.
4. Run fixed updates zero or more times.
5. Run variable gameplay update for non-deterministic or presentation logic.
6. Update animations, particles, camera, UI, and audio parameters.
7. Render the current frame.
8. Present and collect frame metrics.

Keep fixed update and render interpolation separate when physics matters. Clamp large delta times after tab switches, pauses, or device sleep.

## Scene And State Management

- Define clear scene lifecycle hooks: load, enter, update, pause, resume, exit, unload.
- Use scene transitions for main menu, loading, gameplay, pause, results, settings, and credits.
- Keep loading screens explicit when assets may block.
- Avoid global mutable scene state that survives accidentally between scenes.
- Use a stack only when the game truly needs modal states such as pause overlay, dialogue, inventory, or popup.
- Persist only intended game state, not transient runtime objects.

## Entity And Component Model

Choose the simplest model that fits the game:

- GameObject style: good for small games, UI-heavy games, prototypes, and hand-authored scenes.
- ECS style: good for many entities, simulation-heavy games, data-oriented performance, and reusable systems.
- Hybrid style: common for practical engines; use components for gameplay entities and services for global systems.

Recommended separation:

- Entity: stable ID and lifecycle.
- Component: data attached to an entity.
- System: logic that processes matching components.
- Resource/service: global engine facility such as assets, input, audio, physics, save, or networking.
- Event: record of something that happened, used to decouple systems.

Avoid placing all gameplay logic inside entity classes if many objects need shared behavior.

## Resources And Assets

- Use stable asset IDs or paths with a manifest.
- Centralize loading, caching, reference counting or lifetime ownership, and fallback behavior.
- Support async loading for large textures, audio, maps, models, shaders, and bundles.
- Report missing assets clearly with source ID and requester.
- Keep decoded runtime assets separate from authoring files.
- Normalize asset scale, pivot, origin, collision shape, and metadata.
- Add hot reload only if it improves iteration enough to justify complexity.

## Rendering

- Keep render state and gameplay state separate.
- Define render order explicitly: background, world, entities, effects, UI, overlays, debug.
- Use cameras/viewports for world projection and UI projection.
- Batch draw calls where possible for sprites, tiles, particles, and text.
- Make resolution strategy explicit: fixed internal resolution, responsive scaling, pixel-perfect, or dynamic resolution.
- Support debug rendering for bounds, collision, nav paths, triggers, cameras, lights, and UI boxes.
- Ensure UI and text remain readable across target resolutions.

## Input

- Normalize keyboard, mouse, touch, and gamepad into actions.
- Support action mapping instead of hard-coding device keys throughout gameplay code.
- Track pressed, held, released, pointer position, drag, focus, and text input separately.
- Make rebinding possible if the game needs accessibility or controller support.
- Keep UI input routing explicit so gameplay does not consume clicks intended for menus.
- Handle pause, focus loss, and controller disconnect gracefully.

## Physics And Collision

- Decide whether physics is authoritative gameplay, presentation-only, or a mix.
- Run physics in fixed timestep.
- Use layers/masks for collision filtering.
- Separate collision detection from response when gameplay rules need custom behavior.
- Emit collision events with stable entity IDs and contact data.
- Keep sensors/triggers distinct from solid collision.
- Add debug views for bodies, shapes, contacts, raycasts, and broadphase bounds.

## Audio

- Separate sound events from audio playback.
- Use mixer groups for music, SFX, UI, ambience, voice, and master volume.
- Support mute, volume settings, pause behavior, and focus-loss behavior.
- Avoid starting the same sound every frame by accident; use cooldowns or event deduping.
- Keep music transitions explicit: fade, crossfade, stinger, loop, and combat layer.

## UI Integration

- Keep UI state derived from game state where possible.
- Route UI commands back into gameplay systems instead of mutating gameplay state directly from widgets.
- Support layout constraints and scaling for all target aspect ratios.
- Include hover, focus, disabled, loading, selected, and pressed states.
- Ensure debug overlays can be toggled without interfering with normal UI input.

## Save And Persistence

- Save stable gameplay state, not engine internals.
- Version save data and provide migration paths.
- Use stable IDs for scenes, entities, quests, inventory items, skills, unlocks, and settings.
- Separate player progress, settings, keybinds, and runtime cache.
- Make saves atomic where possible to avoid corruption.
- Validate loaded data and provide fallback behavior for missing content.

## Events And Messaging

- Use events for cross-system notifications: entity spawned, asset loaded, scene changed, collision, input action, quest progressed, sound requested, save completed.
- Keep event payloads small and typed.
- Avoid event chains that obscure ownership of state changes.
- Prefer commands for requests that must succeed/fail and events for facts that already happened.
- Document whether events are immediate, queued, frame-delayed, or replayable.

## Performance

- Profile before heavy optimization.
- Track frame time, update time, render time, draw calls, entity count, allocations, asset memory, and physics cost.
- Avoid per-frame allocations in hot loops when using GC-heavy runtimes.
- Use pooling for short-lived particles, projectiles, hit markers, and UI popups when profiling shows churn.
- Cull offscreen or inactive entities.
- Keep debug tools available in development builds and removable from release builds.

## Tooling And Debugging

- Add an in-game debug overlay with FPS, frame time, scene name, entity count, memory, draw calls, and input state.
- Add inspectors for selected entities, components, transforms, colliders, and active effects.
- Add log categories for engine, assets, input, render, physics, audio, UI, save, and gameplay.
- Add reproducible seeds for procedural systems.
- Add screenshots, frame capture hooks, or replay logs for visual regression when useful.

## Testing

Cover these cases:

- Game loop clamps or handles large delta time.
- Scene transitions call lifecycle hooks in the expected order.
- Assets report clear errors when missing.
- Input actions produce correct pressed/held/released states.
- Physics runs at fixed timestep and emits expected collision events.
- Save/load round trips stable data.
- UI commands do not bypass gameplay validation.
- Systems update in deterministic order where required.
- Debug overlays can be enabled without breaking gameplay.

## Avoid

- Mixing engine services, gameplay rules, UI widgets, and asset loading in one object.
- Hidden update order dependencies.
- Letting rendering code mutate gameplay truth.
- Hard-coded asset paths scattered through gameplay code.
- Direct device input checks in every gameplay class.
- Saving transient runtime pointers or object references.
- Adding broad abstractions before the game has repeated needs.
- Building editor tooling that costs more than the production feature it supports.

## Workflow

1. Identify the game type, target platforms, rendering needs, entity count, input devices, physics needs, and persistence needs.
2. Choose the smallest architecture that supports those needs.
3. Define runtime loop and system update order.
4. Define scene lifecycle and resource ownership.
5. Define entity/component or object model.
6. Implement input, assets, rendering, audio, physics, UI, save, and events behind clear interfaces.
7. Add debug overlays and focused tests for lifecycle, input, assets, physics, save/load, and system order.

## Acceptance Checklist

- Engine and game-specific logic are separated cleanly.
- Frame loop, fixed update, render order, and scene lifecycle are explicit.
- Assets, input, rendering, physics, audio, UI, save, and events have clear ownership.
- Runtime systems are debuggable with logs, overlays, and inspection hooks.
- Performance metrics can identify update, render, memory, and allocation issues.
- Save/load uses stable data and handles versioning or missing content.
- Tests cover lifecycle, input, assets, physics, persistence, and deterministic ordering where relevant.
