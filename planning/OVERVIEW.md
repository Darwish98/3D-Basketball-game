# Overview

## Goal
A polished browser-based 3D isometric platformer set in a magical glass world: floating islands, clear glass pipes, crystal platforms, glass coins. The hero is an original cheerful plumber-style character. The aim is a premium, tactile, highly responsive game feel with a glassmorphism HUD.

## Users
Casual players on desktop browsers (keyboard, optionally gamepad) who want a short, satisfying, colorful platformer level they can pick up instantly.

## Must-haves
- Fixed-angle isometric camera (45° yaw, ~35° pitch) with smooth follow, readable gameplay.
- Responsive character: run, jump, land, climb, pipe-travel, with smooth animation.
- One complete level, "WORLD 1-1": platforms, moving platforms, bounce pads, coins, interactive blocks, small enemies, checkpoints, hidden areas, glass pipes that transport the player, finish goal.
- Glass/crystal materials (transmission, reflections) mixed with solid colored materials for readability.
- Glassmorphism HUD: COINS, LIVES, WORLD, SCORE, plus minimap; glass menu cards.
- Juice: particles (sparkles, glass shards, dust, droplets), camera shake, zoom, trails.
- Synthesized sound effects, ambient layer, original music, positional audio.

## Non-goals
- No copyrighted characters, names, or music; character and tunes are original.
- No multiplayer, level editor, save backend, or mobile touch controls in v1.
- Only one level in v1.
- No asset pipeline dependence on external paid assets; geometry and audio are procedural where possible.

## Done when
- `npm run dev` starts the game; a player can start from a menu, play WORLD 1-1 to the finish flag, and see a results card.
- All listed mechanics are present in the level and work.
- HUD shows live coins, lives, world, score, and minimap.
- Every interaction (coin, jump, land, block, pipe, enemy, checkpoint) has both a visual and sound response.
- Runs at ~60 fps on a mid-range laptop at default quality; a low-quality toggle exists.
- `npm run build` and `npm test` pass.

## Roadmap
1. Foundation: project, renderer, isometric camera, lighting.
2. Core movement and collision on a test level.
3. Level content and mechanics (coins, blocks, enemies, bounce pads, moving platforms, checkpoints, goal).
4. Glass pipes and travel.
5. Glass materials and art polish.
6. HUD, minimap, menus.
7. Particles, camera effects.
8. Audio.
9. Performance, quality settings, final tuning.

## Assumptions
- The project folder is named "3D Basketball game", but the idea describes an isometric platformer; the platformer is what is built.
- Web delivery with Three.js, TypeScript, and Vite.
- Keyboard (WASD/arrows + Space) and gamepad input; camera angle is fixed, not player-rotatable.
- "Lives" are lost on falling or enemy contact; 0 lives shows game over with restart.
- Music and SFX are synthesized with Web Audio rather than shipped as files.
