---
name: light-game-ui-style
description: Design and refine game interfaces with a simple, relaxed, beautiful light-color style, including ethereal exploration and cozy town life-sim styles inspired by cloud, candlelight, wind, flight, gentle social adventure, home decoration, farming, crafting, fishing, town NPCs, and relaxed daily-life play. Use when Codex is asked to create, redesign, review, or implement UI for games, game menus, HUDs, inventory screens, level select screens, settings panels, casual game apps, life simulation games, prototypes, HTML/CSS/React game screens, or visual mockups that should feel clean, approachable, bright, soft, healing, atmospheric, cozy, social, and polished.
---

# Light Game UI Style

## Overview

Use this skill to guide game UI toward a minimal, light-toned, relaxed visual direction. Favor clarity, friendly shapes, soft contrast, atmospheric space, and polished interaction details over heavy ornament, dark fantasy themes, or noisy effects.

When the user asks for a style like `Sky-like`, cloud exploration, healing adventure, candlelight social play, or flying through luminous ruins, interpret the request as an original soft atmospheric adventure style. Do not copy logos, named characters, exact costumes, icons, maps, or proprietary UI layouts from a specific game; extract the broader qualities: warm light, vast sky, quiet companionship, soft silhouettes, minimal HUD, and gentle discovery.

When the user asks for a style like `Heartopia-style`, cozy town, cute town life sim, social town simulation, home decoration, fishing and farming life, or relaxed community play, interpret the request as an original warm town life-sim style. Do not copy logos, named characters, exact outfits, furniture sets, town maps, icons, or proprietary UI layouts from a specific game; extract the broader qualities: sunny small-town warmth, soft 3D charm, daily routines, social visits, home customization, collection, and low-pressure progression.

## Design Principles

- Make the game usable first: players should read state, actions, progress, and rewards at a glance.
- Keep the screen airy and calm with generous spacing, restrained panels, and clear hierarchy.
- Use light palettes as the foundation: warm white, pale sky, mint, peach, lavender, butter yellow, soft coral, and light teal can work together if contrast stays readable.
- Avoid single-hue palettes. Add 2-3 supporting hues so the interface feels fresh rather than washed out.
- Keep decoration purposeful: small icons, subtle patterns, soft shadows, tiny sparkles, stickers, badges, and item illustrations are acceptable when they support the game mood.
- Prefer simple geometry with slightly rounded corners. Use 8-14px radius for panels and buttons unless the existing game style says otherwise.
- Use motion lightly: hover lift, button press, panel slide, score tick, reward pop, and small easing can make the UI feel alive without becoming distracting.
- For ethereal exploration, let the world carry the emotion. Keep interface chrome sparse, translucent, and quiet so sky, light, character silhouettes, and movement remain dominant.
- Prefer symbolic interaction over dense menus when possible: gesture, call, light, constellation, path marker, candle, wing, echo, or simple glyphs can replace long instructions.
- For cozy town life sims, keep the UI friendly, practical, and warm. Players should quickly understand daily tasks, inventory, crafting, outfits, home decoration, NPC relationships, events, and map errands without feeling rushed.
- Use playful affordances only where they help the routine feel pleasant: small badges, rounded tabs, soft item cards, readable icons, and cheerful progress states.

## Visual System

### Color

Start with one of these light palette patterns, then adapt to the game:

- Cozy casual: `#FFF8ED` background, `#FFE0B5` panels, `#FF8F70` primary, `#68C3A3` success, `#5E6B7A` text.
- Fresh arcade: `#F5FBFF` background, `#CFEFFF` panels, `#4BA3FF` primary, `#FFD166` rewards, `#334155` text.
- Soft puzzle: `#FAF7FF` background, `#E8DDFF` panels, `#8B7CF6` primary, `#7DD3C7` secondary, `#3F3A56` text.
- Garden idle: `#F7FFF4` background, `#DDF6D2` panels, `#6DBE73` primary, `#FFB86B` rewards, `#35433A` text.
- Ethereal sky: `#F8FBFF` mist, `#DDEEFF` cloud blue, `#FFE7B8` candle glow, `#F8B66D` warm accent, `#5B6472` slate text.
- Dawn ruins: `#FFF6EA` warm haze, `#E8D8C7` stone, `#F6C579` sunlight, `#9BB7C9` distant blue, `#4B4650` text.
- Starlit cloud: `#F4F1FF` pale lavender, `#C9D8FF` sky shadow, `#FFF0B7` light, `#FFFFFF` cloud, `#46415B` text.
- Cozy town morning: `#FFF7EA` cream, `#F8D8A8` warm wood, `#9FD3B4` garden green, `#7FB7D8` sky blue, `#5A4A42` text.
- Home decor pastel: `#FFFDF8` canvas, `#F7C9D5` blush, `#FFE39A` soft yellow, `#A8D8C6` mint, `#66565D` text.
- Market day: `#FFF4DE` sunlight, `#E7B97A` wicker, `#EE8E7F` coral, `#84BFA4` leaf, `#4F5148` text.

Maintain contrast. Body text should not sit on low-contrast pastel backgrounds without a darker text color or a light overlay.

### Ethereal Adventure Direction

Use this direction when the user wants a `Sky-like` feeling:

- Mood: healing, quiet, poetic, open, warm, mysterious, communal, and non-aggressive.
- Environment cues: cloud sea, sunrise, sunset, mist, soft ruins, wind paths, floating islands, candles, stars, bells, cloth, birds, sand, water, and gentle light beams.
- Character cues: small silhouettes against vast space, capes or flowing cloth, simple masks or faces, soft glow, readable body language, and friendly distance.
- UI cues: minimal HUD, rounded translucent panels, soft glyph icons, low-opacity edge prompts, floating interaction rings, candle/wing/light counters, and unobtrusive social prompts.
- Interaction cues: call-and-response, handholding, shared charging, lighting objects, unlocking constellations, guiding lost spirits, collecting light, and cooperative doors.

Keep this as inspiration for original work, not a direct remake. Change icon shapes, costume details, map structure, names, and progression metaphors when creating final assets or screens.

### Cozy Town Life-Sim Direction

Use this direction when the user wants a `Heartopia-style` feeling:

- Mood: sunny, relaxed, friendly, cute, wholesome, social, low-pressure, and homey.
- Environment cues: town square, cozy houses, gardens, beaches, rivers, cafes, craft benches, markets, festivals, flower beds, mailboxes, signposts, and soft outdoor lighting.
- Gameplay cues: home decoration, outfit changes, fishing, farming, gathering, cooking, crafting, shopping, errands, NPC friendship, photo moments, seasonal events, and casual multiplayer visits.
- UI cues: rounded cream panels, pastel item cards, soft iconography, small sticker-like category labels, friendly map pins, daily task cards, relationship hearts, calendar chips, and clear inventory filters.
- Progression cues: daily checklist, home level, collection book, recipe book, town reputation, friendship levels, event pass, furniture sets, outfit wardrobe, and crafting mastery.

Keep this as inspiration for original work, not a direct remake. Change town layout, character designs, furniture shapes, icon language, progression names, and event presentation when creating final assets or screens.

### Layout

- Build around a clear primary play area, then place HUD, navigation, and secondary controls around it.
- Keep controls thumb-friendly on mobile: use 44px minimum hit targets and avoid tiny text-only controls.
- Use compact top bars for currency, hearts, timers, and settings. Use bottom bars for mode tabs or frequent actions.
- Keep panels shallow. Do not stack cards inside cards; use bands, drawers, popovers, or simple grouped rows instead.
- Leave breathing room around major calls to action. The player should know which button advances play.
- For exploration screens, use as little permanent UI as possible. Prefer temporary prompts near interaction targets and a compact corner HUD for essential state.
- Let camera framing show scale: small character, large sky, visible horizon, and a hint of the next destination.
- For social play, reserve clean space around players so connection lines, handholding prompts, emotes, names, or call markers do not overlap.
- For town life-sim screens, use a practical hub layout: compact top status, bottom or side tool shortcuts, map/task entry, inventory access, and a clear main play area.
- Use tabs and filters for large collections such as wardrobe, furniture, recipes, fish, crops, materials, and decorations.
- For home decoration, keep placement controls stable and icon-led: rotate, move, store, confirm, cancel, grid toggle, and camera.

### Components

- Buttons: rounded rectangle, clear label, icon when useful, pressed state, disabled state, and one strong primary style.
- HUD chips: icon plus number, pale fill, darker text, compact but not cramped.
- Cards: use for repeated items such as levels, inventory items, quests, shop products, or characters. Keep radius consistent.
- Modals: use sparingly for confirmations, rewards, pause, and settings. Make the primary action obvious.
- Progress: use bars, rings, step dots, stars, or badges instead of dense numeric text when the game allows it.
- Icons: use simple filled or rounded-line icons. Keep stroke widths consistent and avoid overly technical symbols.
- Floating prompt: small glyph plus short label, soft white fill, warm glow, fades in near interactable objects.
- Light meter: wing, flame, orb, or segmented glow indicator instead of a mechanical progress bar.
- Social action: circular icon cluster for wave, call, sit, gift, guide, hold, or emote; keep it sparse and thumb-friendly.
- Constellation/progression: node map with soft points, connecting lines, locked dim nodes, and warm glow for unlocked states.
- Discovery card: translucent panel with location, spirit, memory, collectible, or reward, shown briefly and then dismissed.
- Daily task card: cream panel, small category icon, short objective, progress chip, reward preview, and claim state.
- Inventory item card: item art, rarity or category ribbon, count, favorite/lock state, and quick action.
- Crafting recipe: output item, required materials, owned/missing counts, time or station requirement, craft button.
- Wardrobe/decor grid: large preview, compact filters, favorite marker, set tag, and clear selected state.
- Town map pin: NPC, shop, home, quest, event, resource, friend, and custom marker types with distinct soft colors.

### Typography

- Use rounded, friendly sans-serif fonts when available; otherwise use the app's existing font system.
- Keep hierarchy simple: title, section heading, body, caption, button label.
- Do not make UI labels oversized. Reserve large type for screen titles, reward moments, or important game state.
- Keep letter spacing at 0 unless matching an existing brand system.
- For ethereal adventure, prefer short poetic labels only for titles or discoveries. Keep control text plain and direct.
- For cozy town life sims, use concise, friendly labels for repeated actions: craft, place, store, sell, visit, gift, track, claim, filter, preview.

## Motion And Atmosphere

- Use slow ease-in-out fades, soft scale, gentle float, light bloom, and small particle drift.
- Use wind, cloth, candle flame, cloud, dust, and star particles as environmental feedback, not constant UI decoration.
- Reward discovery with quiet light expansion, warm chime-like feedback, and a short glow trail.
- Avoid aggressive screen shake, sharp flashes, heavy popups, or fast competitive UI animation unless the game mode requires it.
- If a prompt appears near an object, let it breathe: fade in, hold, then fade out without snapping.
- For cozy town life sims, use gentle bounce, soft checkmark, item sparkle, stamp-like completion, and smooth panel slides.
- Keep routine feedback satisfying but calm: pickup, craft complete, fish caught, recipe learned, relationship up, decor placed, and task claimed.

## Implementation Workflow

1. Identify the screen purpose: main menu, gameplay HUD, pause, settings, shop, inventory, results, level select, onboarding, map, crafting, wardrobe, home decoration, or social profile.
2. Define the core player action and make it the strongest visual element.
3. Choose a light palette with readable text and at least one warm accent and one cool accent.
4. Sketch the layout density before styling. Reduce clutter if the first pass has too many panels, borders, or decorative pieces.
5. Implement responsive states for desktop and mobile. Check that labels, counters, and buttons do not resize or overlap.
6. Add small interaction feedback: hover, active, selected, disabled, progress, loading, and success states.
7. Verify the UI with screenshots or browser inspection when building a frontend.

For ethereal exploration screens:

1. Establish the emotional anchor first: dawn flight, cloud sea, candlelit ruin, quiet temple, shared journey, or starlit memory.
2. Place the character and destination before adding UI.
3. Add only essential HUD state: energy/light, nearby interaction, social connection, navigation hint, or pause.
4. Use warm glow for important actions and cool mist for background depth.
5. Test that UI remains readable over bright clouds, sunset gradients, and pale ruins.
6. Check that prompts do not cover characters, faces, path markers, or interaction objects.

For cozy town life-sim screens:

1. Identify the daily loop first: gather, craft, decorate, shop, visit NPCs, complete tasks, socialize, and collect rewards.
2. Define the primary surface: open-world HUD, inventory, wardrobe, home decoration, crafting, town map, relationship, event, or shop.
3. Keep collection-heavy screens filterable and scannable.
4. Use warm neutral panels and pastel accents; reserve stronger color for primary actions and event rewards.
5. Test that long item names, material counts, prices, timers, and task text fit on mobile.
6. Verify that decoration and placement controls do not cover the object being edited.

## Avoid

- Dark, metallic, gritty, or high-contrast neon styles unless the user explicitly requests them.
- Dense dashboards that feel like productivity software instead of a game.
- Oversized marketing-style heroes when the task is a playable screen or tool.
- Decorative gradients as the main design idea. If gradients are used, keep them subtle and support the palette.
- Text embedded in images when it should be live UI.
- Low-contrast pastel text, tiny tap targets, or UI elements whose content can overflow.
- Directly copying recognizable UI, icons, characters, map layouts, names, costumes, or progression screens from a specific existing game.
- Turning a quiet exploration mood into a dense mobile RPG interface with many currencies, red dots, banners, and competitive prompts.
- Turning a cozy life sim into a cluttered management dashboard with too many currencies, red-dot notifications, sale banners, or urgent timers.
- Overusing bloom until text, silhouettes, path markers, or item labels become unreadable.
- Copying recognizable characters, furniture sets, town maps, event screens, icons, or brand-specific UI from a specific existing life-sim game.
- Making collection grids too tiny to inspect item art or too sparse to browse efficiently.

## Acceptance Checklist

- The interface is light, simple, relaxed, and game-like.
- The primary action and game state are immediately clear.
- The palette has enough contrast and is not dominated by one hue.
- Controls have normal, hover/focus, active, selected, disabled, and loading states where relevant.
- Mobile and desktop layouts are stable, with no overlapping or clipped text.
- Visual polish comes from spacing, hierarchy, icons, subtle shadow, and small motion rather than heavy decoration.
- If using the ethereal adventure direction, the screen feels vast, warm, quiet, social, and exploratory without copying a specific game's protected assets or layouts.
- HUD and prompts are minimal enough that environment, character movement, and emotional atmosphere remain the focus.
- If using the cozy town life-sim direction, the screen feels warm, social, collectible, decorative, and low-pressure without copying a specific game's protected assets or layouts.
- Inventory, crafting, wardrobe, decoration, map, daily tasks, and NPC relationship surfaces are easy to scan and pleasant to repeat.
