---
name: light-game-ui-style
description: Design and refine game interfaces with a simple, relaxed, beautiful light-color style. Use when Codex is asked to create, redesign, review, or implement UI for games, game menus, HUDs, inventory screens, level select screens, settings panels, casual game apps, prototypes, HTML/CSS/React game screens, or visual mockups that should feel clean, approachable, bright, soft, and polished.
---

# Light Game UI Style

## Overview

Use this skill to guide game UI toward a minimal, light-toned, relaxed visual direction. Favor clarity, friendly shapes, soft contrast, and polished interaction details over heavy ornament, dark fantasy themes, or noisy effects.

## Design Principles

- Make the game usable first: players should read state, actions, progress, and rewards at a glance.
- Keep the screen airy and calm with generous spacing, restrained panels, and clear hierarchy.
- Use light palettes as the foundation: warm white, pale sky, mint, peach, lavender, butter yellow, soft coral, and light teal can work together if contrast stays readable.
- Avoid single-hue palettes. Add 2-3 supporting hues so the interface feels fresh rather than washed out.
- Keep decoration purposeful: small icons, subtle patterns, soft shadows, tiny sparkles, stickers, badges, and item illustrations are acceptable when they support the game mood.
- Prefer simple geometry with slightly rounded corners. Use 8-14px radius for panels and buttons unless the existing game style says otherwise.
- Use motion lightly: hover lift, button press, panel slide, score tick, reward pop, and small easing can make the UI feel alive without becoming distracting.

## Visual System

### Color

Start with one of these light palette patterns, then adapt to the game:

- Cozy casual: `#FFF8ED` background, `#FFE0B5` panels, `#FF8F70` primary, `#68C3A3` success, `#5E6B7A` text.
- Fresh arcade: `#F5FBFF` background, `#CFEFFF` panels, `#4BA3FF` primary, `#FFD166` rewards, `#334155` text.
- Soft puzzle: `#FAF7FF` background, `#E8DDFF` panels, `#8B7CF6` primary, `#7DD3C7` secondary, `#3F3A56` text.
- Garden idle: `#F7FFF4` background, `#DDF6D2` panels, `#6DBE73` primary, `#FFB86B` rewards, `#35433A` text.

Maintain contrast. Body text should not sit on low-contrast pastel backgrounds without a darker text color or a light overlay.

### Layout

- Build around a clear primary play area, then place HUD, navigation, and secondary controls around it.
- Keep controls thumb-friendly on mobile: use 44px minimum hit targets and avoid tiny text-only controls.
- Use compact top bars for currency, hearts, timers, and settings. Use bottom bars for mode tabs or frequent actions.
- Keep panels shallow. Do not stack cards inside cards; use bands, drawers, popovers, or simple grouped rows instead.
- Leave breathing room around major calls to action. The player should know which button advances play.

### Components

- Buttons: rounded rectangle, clear label, icon when useful, pressed state, disabled state, and one strong primary style.
- HUD chips: icon plus number, pale fill, darker text, compact but not cramped.
- Cards: use for repeated items such as levels, inventory items, quests, shop products, or characters. Keep radius consistent.
- Modals: use sparingly for confirmations, rewards, pause, and settings. Make the primary action obvious.
- Progress: use bars, rings, step dots, stars, or badges instead of dense numeric text when the game allows it.
- Icons: use simple filled or rounded-line icons. Keep stroke widths consistent and avoid overly technical symbols.

### Typography

- Use rounded, friendly sans-serif fonts when available; otherwise use the app's existing font system.
- Keep hierarchy simple: title, section heading, body, caption, button label.
- Do not make UI labels oversized. Reserve large type for screen titles, reward moments, or important game state.
- Keep letter spacing at 0 unless matching an existing brand system.

## Implementation Workflow

1. Identify the screen purpose: main menu, gameplay HUD, pause, settings, shop, inventory, results, level select, or onboarding.
2. Define the core player action and make it the strongest visual element.
3. Choose a light palette with readable text and at least one warm accent and one cool accent.
4. Sketch the layout density before styling. Reduce clutter if the first pass has too many panels, borders, or decorative pieces.
5. Implement responsive states for desktop and mobile. Check that labels, counters, and buttons do not resize or overlap.
6. Add small interaction feedback: hover, active, selected, disabled, progress, loading, and success states.
7. Verify the UI with screenshots or browser inspection when building a frontend.

## Avoid

- Dark, metallic, gritty, or high-contrast neon styles unless the user explicitly requests them.
- Dense dashboards that feel like productivity software instead of a game.
- Oversized marketing-style heroes when the task is a playable screen or tool.
- Decorative gradients as the main design idea. If gradients are used, keep them subtle and support the palette.
- Text embedded in images when it should be live UI.
- Low-contrast pastel text, tiny tap targets, or UI elements whose content can overflow.

## Acceptance Checklist

- The interface is light, simple, relaxed, and game-like.
- The primary action and game state are immediately clear.
- The palette has enough contrast and is not dominated by one hue.
- Controls have normal, hover/focus, active, selected, disabled, and loading states where relevant.
- Mobile and desktop layouts are stable, with no overlapping or clipped text.
- Visual polish comes from spacing, hierarchy, icons, subtle shadow, and small motion rather than heavy decoration.
