---
name: game-quest-module
description: Design, implement, review, or extend reusable game quest and mission systems. Use when Codex is asked to build quests, missions, objectives, daily tasks, achievements, NPC quest lines, story chapters, task tracking, quest logs, reward claiming, progress counters, event-driven quest updates, branching quests, repeatable quests, tutorials, onboarding goals, or RPG/casual/idle/action game task modules.
---

# Game Quest Module

## Overview

Use this skill to build quest systems that are data-driven, event-aware, player-readable, and easy to extend. Separate quest definition, player quest state, objective progress, event matching, reward delivery, and UI presentation.

## Core Principles

- Treat quests as data plus state. A quest definition is shared; each player's accepted, completed, failed, and claimed progress is runtime state.
- Separate objective tracking from UI display. UI should read progress state, not decide whether a quest is complete.
- Make quest progress event-driven when possible. Combat, inventory, location, dialogue, crafting, purchase, and story events should update objectives through a clear matcher.
- Support explicit lifecycle states: locked, available, accepted, active, ready to turn in, completed, failed, abandoned, expired, claimed.
- Keep rewards deterministic and idempotent. A reward should not be claimable twice unless the quest is repeatable by design.
- Prefer composable objective types over one-off quest logic.
- Always provide player feedback for progress, completion, blockers, and rewards.

## Data Model

Define static quests with fields like:

```ts
type QuestDefinition = {
  id: string;
  title: string;
  summary: string;
  description?: string;
  category: "main" | "side" | "daily" | "weekly" | "event" | "tutorial" | "achievement";
  giverId?: string;
  prerequisites?: QuestRequirement[];
  objectives: QuestObjectiveDefinition[];
  rewards: QuestReward[];
  timeLimitMs?: number;
  repeat?: RepeatRule;
  nextQuestIds?: string[];
  tags?: string[];
};
```

Track player-specific state separately:

```ts
type QuestState = {
  questId: string;
  status: "locked" | "available" | "accepted" | "active" | "ready" | "completed" | "failed" | "claimed";
  startedAt?: number;
  completedAt?: number;
  claimedAt?: number;
  objectiveStates: QuestObjectiveState[];
};
```

## Objective Types

Use reusable objective definitions:

- Kill: defeat enemies by id, type, faction, level, area, weapon, or skill tag.
- Collect: own, obtain, craft, harvest, loot, buy, or deliver items.
- Talk: speak to a specific NPC or any NPC matching a role/faction.
- Visit: enter region, reach coordinate, discover landmark, unlock map node.
- Interact: use object, open chest, activate switch, inspect clue, build structure.
- Craft: craft item, upgrade equipment, cook recipe, refine material.
- Equip: wear item, unlock character, assign skill, change outfit.
- Win: clear level, win battle, finish dungeon, complete minigame, score threshold.
- Spend or earn: currency, energy, points, reputation, experience.
- Time: survive duration, log in daily, complete before deadline.
- Choice/story: select dialogue option, make faction decision, trigger cutscene.
- Compound: complete all, complete any, complete N of M, ordered sequence.

Each objective should define `target`, `requiredCount`, `currentCount`, `eventMatcher`, `visibility`, and optional `order`.

## Lifecycle Flow

Use this sequence for normal quests:

1. Evaluate prerequisites and unlock conditions.
2. Mark quest available and notify relevant NPC, map, or quest log.
3. Accept quest manually or auto-accept if the design requires it.
4. Initialize objective states.
5. Listen to gameplay events and update matching objectives.
6. Recompute quest readiness after objective progress changes.
7. Show completion feedback and route the player to turn-in if needed.
8. Complete the quest and grant or stage rewards.
9. Mark rewards as claimed.
10. Unlock follow-up quests, achievements, dialogue, locations, or systems.

Keep lifecycle transitions explicit and testable. Do not infer completion only from UI text.

## Event Matching

Define gameplay events with stable shape:

```ts
type GameEvent = {
  type: string;
  actorId?: string;
  targetId?: string;
  itemId?: string;
  locationId?: string;
  amount?: number;
  tags?: string[];
  timestamp: number;
};
```

Match events against objective rules. Example event types include `enemy.defeated`, `item.obtained`, `npc.talked`, `area.entered`, `item.crafted`, `level.cleared`, `currency.earned`, `dialogue.choice_selected`, and `object.interacted`.

Make event processing idempotent when events can be replayed or synced from a server. Store event IDs or derive progress from authoritative state when duplication is possible.

## Rewards

Support reward types such as:

- Currency, experience, items, equipment, cosmetics, characters, skill points, reputation, unlocks, map access, story flags, recipes, buildings, and premium/event tokens.
- Immediate rewards on completion or explicit claim rewards after turn-in.
- Random reward tables only when the game design calls for it; log the resolved result.
- Choice rewards when players choose one item or faction outcome.

Validate inventory capacity, duplicate unique items, account limits, and claim state before granting rewards.

## Quest Chains And Branching

- Use `nextQuestIds` for linear chains.
- Use prerequisites and story flags for branching.
- Record irreversible choices explicitly.
- Keep abandoned or failed quest behavior clear: can retry, cannot retry, resets daily, or branches to another quest.
- For repeatable quests, define reset schedule, per-period claim limits, and whether progress carries over.
- For daily/weekly quests, store period keys so claims do not leak across reset boundaries.

## UI Requirements

- Quest log: categories, status filters, pinned quests, objective list, rewards, giver, location, and abandon/track actions.
- Quest tracker: compact pinned objectives with current/required progress and completion state.
- NPC marker: available quest, active quest, ready turn-in, locked quest, shop/task variants.
- Map marker: quest target, area highlight, route hint, distance if useful.
- Quest detail: title, description, objectives, rewards, requirements, time limit, follow-up hint.
- Completion popup: quest title, rewards, next step, claim button if needed.
- Failure/expiry feedback: clear reason, retry path, and whether progress is lost.

Use clear status labels and icons. Players should not need to inspect raw state to know what to do next.

## Architecture Guidance

- Keep quest definitions in JSON, YAML, database rows, ScriptableObject-like assets, or typed config depending on the engine.
- Keep quest progression logic independent from rendering and animation.
- Use a quest service/system to own state transitions and event handling.
- Emit quest events for UI, NPC markers, map markers, analytics, achievements, and narrative systems.
- Persist quest state regularly and migrate it carefully when quest definitions change.
- Use stable IDs for quests, objectives, NPCs, items, regions, rewards, and flags.
- In multiplayer or server-authoritative games, resolve quest progress and rewards on the server.

## Testing

Cover these cases:

- Quest unlocks only when prerequisites are met.
- Quest cannot be accepted twice unless repeatable.
- Objective progress updates only from matching events.
- Ordered objectives do not progress out of sequence.
- Quest becomes ready only when all required objectives are complete.
- Rewards cannot be claimed twice.
- Abandon, failure, expiry, and retry behavior match the design.
- Daily/weekly reset logic uses the correct period key.
- Follow-up quests unlock after completion or claim as intended.
- UI displays correct progress, status, rewards, markers, and time remaining.

## Avoid

- Hard-coding quest progress in unrelated gameplay modules.
- Using display strings as quest IDs or objective IDs.
- Granting rewards from UI click handlers without backend/state validation.
- Letting completed quests grant rewards more than once by refreshing or replaying events.
- Making quest status ambiguous to players.
- Mixing story flags, objective state, reward claim state, and UI state in one loose object.
- Designing every quest as a custom script when reusable objective types would work.

## Workflow

1. Identify the quest type: main story, side quest, daily, weekly, event, tutorial, achievement, NPC chain, or system unlock.
2. Define quest lifecycle states and the player-specific state model.
3. Define reusable objective types and event matchers.
4. Implement event-driven progress updates and explicit lifecycle transitions.
5. Implement reward validation and idempotent claiming.
6. Wire quest updates to NPC markers, map markers, quest log, tracker, popups, and analytics.
7. Add focused tests for unlocks, progress, completion, claiming, repeat rules, and UI-visible state.

## Acceptance Checklist

- Quest definitions are data-driven and separate from player quest state.
- Objective progress is updated through clear event matching or authoritative state checks.
- Lifecycle states are explicit and deterministic.
- Rewards are validated and cannot be claimed twice accidentally.
- Quest chains, repeatable quests, and time-limited quests have clear rules.
- UI clearly shows available, active, ready, completed, failed, and claimed states.
- Tests cover unlocks, progress, completion, rewards, resets, and markers.
