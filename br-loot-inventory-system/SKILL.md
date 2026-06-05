---
name: br-loot-inventory-system
description: Design, implement, review, or extend battle royale loot, inventory, equipment, backpack, ammo, attachment, armor, healing, crate, and pickup systems. Use when Codex is asked to build ground loot, item rarity, weapon attachments, quick pickup, drag inventory, armor durability, ammo stacks, healing items, supply crates, loot tables, or tactical shooter equipment UI.
---

# BR Loot Inventory System

## Overview

Use this skill to build battle royale inventory systems where fast looting, clear equipment comparison, scarcity, and risk under pressure matter.

## Core Principles

- Separate item definitions, item instances, inventory state, equipment slots, and UI.
- Make pickup decisions fast: compatible, better, full, duplicate, needed ammo, or blocked.
- Support partial stacks and capacity constraints explicitly.
- Keep attachments and ammo compatibility data-driven.
- Prevent UI actions from granting items without inventory validation.

## Item Model

Use item categories:

- Weapon, ammo, attachment, armor, helmet, backpack, healing, boost, throwable, utility, key, currency, cosmetic, crate item.
- Define rarity, stack size, weight/volume, compatible slots, tags, pickup priority, and drop behavior.
- For armor, track durability separately from definition.
- For attachments, define compatible weapon classes and stat modifiers.

## Inventory Flow

1. Detect nearby loot.
2. Sort by pickup priority, distance, rarity, compatibility, and player need.
3. Validate capacity and equipment compatibility.
4. Pick up, stack, swap, auto-equip, or reject with a reason.
5. Update weapon stats if attachments changed.
6. Emit events for UI, sound, tutorial, quests, and analytics.

## Equipment Slots

- Primary weapon, secondary weapon, sidearm if supported, melee, throwable slots, armor, helmet, backpack, healing quick slots, utility.
- Attachments: optic, muzzle, magazine, grip, stock, ammo variant, special module.
- Define whether attachments move with dropped weapons or return to inventory.

## Loot Tables

- Use tiered spawn tables by location risk, building type, crate type, match phase, and mode.
- Support rare crate-only items without relying on exact existing-game drop rates.
- Keep ammo availability aligned with weapon rarity.
- Add debug views for spawn table output and empty loot locations.

## UI Requirements

- Nearby loot list: compact, sorted, compatible indicators, pickup button, quantity.
- Inventory grid/list: weapons, ammo, attachments, armor, healing, throwable, capacity.
- Comparison: current vs pickup item, stat changes, attachment compatibility, armor durability.
- Quick pickup: one-tap or auto-pick rules for ammo, healing, better attachments, and upgrades.
- Drag/drop: swap, split stack, discard, equip, attach, detach.
- Warning states: backpack full, incompatible, lower tier, no ammo, duplicate, cannot use now.

## Testing

- Stacks merge and split correctly.
- Capacity blocks pickups without losing items.
- Auto-equip chooses intended upgrades.
- Attachments modify only compatible weapons.
- Dropping weapons preserves or detaches attachments according to rules.
- Loot tables produce valid items for each location tier.
- UI cannot duplicate or delete items through rapid interactions.

## Avoid

- Hard-coded compatibility checks scattered through UI.
- Loot lists that are too slow for combat situations.
- Duplicating item stats in tooltips.
- Copying exact item icons, rarity colors, drop rates, or weapon names from a specific commercial game.

## Acceptance Checklist

- Loot, inventory, equipment, stack, attachment, and armor rules are data-driven.
- Pickup, swap, attach, detach, drop, and use flows validate state correctly.
- UI supports fast combat looting and clear comparison.
- Loot tables are tunable and debuggable.
- Tests cover capacity, stacks, compatibility, drops, auto-equip, and UI edge cases.
