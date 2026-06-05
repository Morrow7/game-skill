---
name: character-npc-game-style
description: Design and refine character-led and NPC-focused game visuals and interfaces. Use when Codex is asked to create, redesign, review, or implement game screens involving NPC portraits, character profiles, dialogue UI, relationship meters, quest givers, shops, party screens, visual novel scenes, RPG interactions, character selection, status panels, or NPC-driven gameplay flows.
---

# Character NPC Game Style

## Overview

Use this skill to make game interfaces feel centered on characters and NPC interaction. Prioritize expressive portraits, readable dialogue, clear relationship and quest states, and UI that frames the character without hiding gameplay context.

## Core Direction

- Treat the NPC or character as the main visual anchor. Their portrait, pose, silhouette, or nameplate should be easy to find immediately.
- Give each character a recognizable identity through color, icon, motif, frame shape, typography accent, or background prop.
- Keep interaction states explicit: available quest, active quest, completed quest, shop, locked dialogue, relationship change, giftable, recruitable, hostile, neutral, friendly.
- Use UI to support character emotion and story tone. Dialogue boxes, portraits, and choices should change subtly with mood.
- Keep text readable. Character-focused games often have more dialogue, so hierarchy and spacing matter more than decoration.
- Avoid making NPC panels feel like generic dashboards. Add story, portrait, and personality cues.

## Visual System

### Character Presentation

- Use portrait hierarchy intentionally: bust portrait for dialogue, full body for selection/profile, small avatar for HUD lists.
- Keep faces unobstructed. Do not place buttons, labels, or reward effects over facial features.
- Use nameplates with enough contrast and a clear speaker indicator.
- Include personality cues: job badge, faction mark, favorite item, emotion icon, relationship icon, or small prop.
- Use consistent portrait crops across similar screens so the interface feels stable.
- For multiple NPCs, differentiate with color accents and silhouettes rather than only names.

### Dialogue UI

- Use a wide, readable dialogue box with speaker name, portrait, dialogue text, and next/skip affordance.
- Keep line length comfortable. Do not stretch dialogue across the full width on desktop without a max width.
- Support expression changes, typing state, choice prompts, history/backlog, and important keyword emphasis when relevant.
- Make choices distinct from dialogue text. Use stacked buttons or selectable rows with hover/focus/selected states.
- Use mood-based accents sparingly: warm for friendly, cool for distant, red for danger, gold for important, muted for sad.
- If the scene has background art, use a readable panel overlay rather than relying on text shadow alone.

### Relationship And Status

- Represent affinity with hearts, stars, pips, rings, badges, or segmented bars.
- Show relationship changes immediately after gifts, dialogue choices, quests, or events.
- Use compact state badges: `Quest`, `Shop`, `Gift`, `New`, `Locked`, `Ready`, `Complete`.
- Use NPC availability states clearly: online/offline, daytime/nighttime, location, cooldown, busy, recruitable.
- Make negative or locked states polite but obvious, with muted color and clear iconography.

## Component Patterns

- NPC card: avatar, name, role/faction, relationship meter, location/status, primary action.
- Dialogue panel: portrait, nameplate, text area, next control, backlog or skip button when appropriate.
- Character profile: full body art, stats, relationship, bio, likes/dislikes, gifts, quests, outfit or equipment tabs.
- Quest giver panel: NPC portrait, quest title, objective list, reward row, accept/track/complete button.
- Shopkeeper screen: NPC portrait or bust on one side, shop inventory grid, currency chip, dialogue hint, buy/sell tabs.
- Party screen: character list, selected character detail, role icon, equipment, skills, status effects.
- Choice prompt: question text, 2-4 clear choices, consequence hint only when the game design expects transparency.
- Relationship popup: character avatar, plus/minus amount, reason, small animation, current level.

## Layout

- Give the character art a stable reserved area. Avoid layout shifts when text or choices change.
- For dialogue-heavy screens, place portrait and dialogue in a predictable bottom or side panel.
- For profile/shop/quest screens, use a two-zone layout: character identity zone plus interaction/content zone.
- On mobile, keep portrait visible but not dominant enough to squeeze dialogue into tiny lines.
- Use tabs for character subviews: `Info`, `Quests`, `Gifts`, `Skills`, `Shop`, `Story`.
- Keep repeated NPC lists scannable with avatars, names, status badges, and one primary action.

## Color And Tone

- Let the overall game genre choose the base palette, then assign each important NPC an accent color.
- Use warm, approachable colors for friendly town NPCs, refined colors for nobles or mentors, muted tones for mysterious characters, and stronger contrast for rivals or enemies.
- Do not use too many character accent colors on one screen. Use neutral panels and small accents for identity.
- Keep text colors dark enough on light panels and light enough on dark panels.
- Use rarity or importance colors consistently if NPCs have ranks, factions, or story priority.

## Motion And Feedback

- Use portrait entrance, blink, idle breathing, subtle expression changes, or small gesture loops where supported.
- Animate dialogue with restrained type-in or fade-in effects, and provide skip/instant text behavior for usability.
- Add clear feedback for choices, gifts, quest completion, relationship gains, and shop purchases.
- Avoid excessive bounce or sparkle if the character tone is serious, mysterious, or dramatic.
- For important NPC moments, use a short focus transition: dim background, brighten portrait, show nameplate, then reveal text.

## Writing And Labels

- Use character names consistently across cards, dialogue, quests, and logs.
- Keep button labels action-oriented: `Talk`, `Gift`, `Trade`, `Accept`, `Track`, `Complete`, `Invite`, `Details`.
- Keep NPC role labels short: `Blacksmith`, `Healer`, `Rival`, `Mentor`, `Merchant`, `Guard`, `Companion`.
- Use flavor text in small doses. Do not bury the actionable state under long prose.

## Avoid

- Hiding the speaker identity or making the active NPC ambiguous.
- Placing UI over faces, hands, important props, or readable character expressions.
- Generic profile cards with no personality cues.
- Dialogue text that is too small, too wide, or too low contrast.
- Too many badges competing for attention.
- Relationship meters without a clear current value or change feedback.
- Character art that resizes unpredictably between states.

## Workflow

1. Identify the character interaction type: dialogue, profile, quest, shop, party, relationship, selection, or story scene.
2. Decide the primary character anchor: portrait, full-body art, avatar list, or scene sprite.
3. Define visible states: speaker, mood, relationship, quest status, availability, faction, role, and primary action.
4. Choose a neutral UI base and 1-2 character accents.
5. Build reusable components for portraits, nameplates, dialogue, choices, status badges, meters, and action buttons.
6. Check mobile and desktop layouts for readable dialogue, stable character framing, and non-overlapping UI.
7. Add feedback for player actions and NPC state changes.

## Acceptance Checklist

- The active character or NPC is immediately identifiable.
- Dialogue, choices, quest state, relationship state, and primary action are readable at a glance.
- Character art is framed cleanly and not covered by UI.
- NPC cards, profiles, dialogue panels, and status badges share a consistent visual language.
- Each important character can carry an accent or motif without making the screen visually noisy.
- Mobile and desktop layouts avoid clipped text, overlapping art, and unstable portrait sizing.
