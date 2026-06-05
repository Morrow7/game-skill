---
name: pixel-game-style
description: Design and refine pixel-art game visuals and interfaces with crisp low-resolution aesthetics. Use when Codex is asked to create, redesign, review, or implement pixel game UI, retro game menus, 8-bit or 16-bit inspired screens, HUDs, inventories, level select screens, pixel-art web games, canvas games, sprites, tile-based layouts, or mockups that need clean pixel styling.
---

# Pixel Game Style

## Overview

Use this skill to keep game screens visually consistent with pixel-art rules. Prioritize crisp edges, readable UI, limited palettes, grid discipline, and intentional low-resolution charm.

## Core Rules

- Render pixel art sharply. Disable smoothing for canvas and image assets when possible.
- Scale by whole numbers whenever feasible: 1x, 2x, 3x, or 4x. Avoid fractional scaling that blurs pixels.
- Design on a small base grid, then scale up. Good base sizes include 160x90, 240x135, 320x180, 256x144, or 320x240 depending on the project.
- Keep shapes aligned to the pixel grid. Avoid half-pixel positioning, soft blur, glass effects, and anti-aliased decorative edges.
- Use limited palettes. A strong pixel style usually needs fewer colors with deliberate ramps rather than many similar shades.
- Make UI readable before nostalgic. Pixel style should not make labels, counters, icons, or controls hard to understand.

## Visual System

### Palette

Start with a compact palette and expand only when the game needs it:

- Classic adventure: `#1B1F3B`, `#3F5E8C`, `#7FA7D8`, `#F7D794`, `#E86A58`, `#F8F5E4`
- Cozy pixel: `#2F2A3A`, `#6B5B7B`, `#F1C27D`, `#F6E3B4`, `#8BCB88`, `#F7F1E1`
- Dungeon UI: `#141820`, `#2E3440`, `#5E6C7F`, `#C49A6C`, `#D95F4A`, `#F0E6D2`
- Bright arcade: `#151515`, `#2D9CDB`, `#F2C94C`, `#EB5757`, `#27AE60`, `#F7F7F7`

Use 3-5 values per color ramp when drawing sprites or panels: shadow, mid, highlight, accent, outline. Keep text contrast high.

### Lines And Shapes

- Prefer 1px or 2px hard outlines at base resolution.
- Use square corners or tiny stepped corners. If rounded corners are needed, make them pixel-stepped rather than smooth.
- Build buttons and panels with visible borders, inner highlights, and simple shadow offsets.
- Use dither, checker patterns, or stepped highlights sparingly to add texture.
- Keep icons simple and blocky, with silhouettes recognizable at small sizes.

### Typography

- Prefer pixel fonts for headings, buttons, counters, and HUD labels.
- Use a readable fallback for long body text if the pixel font becomes tiring.
- Avoid subpixel font rendering effects when possible. Keep font sizes aligned to the scaling system.
- Keep labels short. Pixel UI works best with concise words, numbers, icons, and badges.

### Layout

- Use grid-based spacing: 4, 8, 12, 16, 24, and 32px increments after scaling.
- Keep HUD elements compact and anchored to predictable screen edges.
- Use repeated tile-like panels for inventory, shop items, level cards, save slots, and quests.
- Keep the playable area visually dominant. UI frames should support gameplay, not smother it.
- Design for both keyboard/gamepad and pointer input when relevant. Show focus and selected states clearly.

## Implementation Notes

For web and canvas work:

```css
canvas,
.pixel-art {
  image-rendering: pixelated;
  image-rendering: crisp-edges;
}
```

```js
const ctx = canvas.getContext("2d");
ctx.imageSmoothingEnabled = false;
```

When using CSS transforms or sprite sheets, prefer integer dimensions and integer-positioned background offsets. If assets look blurry, inspect rendered size, source size, device pixel ratio, and transform scale.

## Component Patterns

- Primary button: dark outline, flat fill, 1px inner highlight, 2-4px hard drop shadow, pressed state shifts down by the shadow amount.
- Dialog panel: thick border, dark outer line, light inner line, simple title strip, compact action row.
- Inventory slot: square tile, border, subtle checker or flat fill, selected state with bright outline.
- Health and energy: hearts, pips, small bars, or segmented meters instead of smooth progress bars.
- Currency and score: icon plus number in a bordered chip.
- Level select: tile cards with star badges, lock icons, and small pixel thumbnails.

## Avoid

- Blurry sprites, fractional scaling, soft shadows, frosted glass, smooth gradients, glow-heavy neon, and anti-aliased icons.
- Mixing realistic photos or polished vector icons into a pixel-art UI unless they are intentionally converted or framed.
- Overly tiny fonts. Pixel text still needs to be readable on mobile and desktop.
- Too many colors. A pixel look becomes weaker when every component uses unrelated colors.
- Random noise texture. Pixel texture should follow forms, lighting, or tile patterns.

## Workflow

1. Identify the target era and mood: 8-bit, 16-bit, cozy, arcade, fantasy, sci-fi, dungeon, farming, puzzle, or platformer.
2. Pick a base resolution and scaling strategy before designing details.
3. Choose a limited palette with readable text colors and clear accent colors.
4. Define reusable pixel components: buttons, panels, slots, chips, bars, icons, and selected states.
5. Implement crisp rendering rules and integer layout constraints.
6. Check desktop and mobile screenshots for blur, overlap, clipping, and inconsistent scaling.
7. Polish with small pixel details: stepped shadows, simple highlights, sprite-like icons, and clear state changes.

## Acceptance Checklist

- Pixel assets and UI edges are sharp, not blurred.
- Layout, spacing, borders, and sprites align to a consistent grid.
- Palette is limited, cohesive, and readable.
- Buttons, slots, chips, panels, and meters share a consistent pixel treatment.
- Hover, focus, selected, disabled, and pressed states are visually distinct.
- Mobile and desktop layouts preserve pixel clarity without clipped text or overlapping UI.
