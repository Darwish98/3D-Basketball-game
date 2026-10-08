# Design

## Stack
- **TypeScript + Vite**: fast dev loop, simple static build.
- **Three.js**: `MeshPhysicalMaterial` with transmission/IOR/thickness for glass, PBR lighting, shadow maps, environment map (`RoomEnvironment`/generated PMREM) for reflections.
- **postprocessing** (pmndrs): bloom for glowing collectibles, SSAO/N8AO for ambient occlusion, vignette.
- **Custom lightweight physics**: AABB/capsule vs. box-and-ramp collision. A full physics engine is overkill and hurts platformer feel (coyote time, jump buffering, variable jump height).
- **Web Audio API**: synthesized SFX, procedural music, `PannerNode` for spatial sound.
- **DOM/CSS HUD** over the canvas (`backdrop-filter: blur`) for glassmorphism; minimap on a 2D canvas.
- **Vitest** for logic tests (physics, state, scoring).

## How it works
- `src/main.ts`: bootstrap, game loop (fixed 60 Hz update, interpolated render).
- `src/core/`: `Game` state machine (menu, playing, paused, gameover, complete), `Input`, `Events` bus.
- `src/render/`: renderer and post-processing, `IsoCamera` (yaw 45°, pitch ~35°, damped follow, zoom/shake offsets), `materials.ts` (glass, crystal, grass, block, liquid).
- `src/world/`: level data (`level1.ts`, declarative list of platforms, pipes, coins, enemies, etc.), builders that turn data into meshes + colliders.
- `src/entities/`: `Player` (kinematic controller + procedural rigged animation), `Enemy`, `Coin`, `Block`, `Pipe`, `BouncePad`, `MovingPlatform`, `Checkpoint`, `Goal`.
- `src/fx/`: particle system (instanced), trails, camera shake.
- `src/audio/`: `AudioEngine`, `sfx.ts`, `music.ts`.
- `src/ui/`: HUD, minimap, menu cards, CSS.
- Gameplay events (coin collected, block hit, etc.) go over the event bus; audio, FX and HUD subscribe, so entities stay decoupled.
- Pipes: entering snaps the player to the pipe mouth, then moves along a spline inside the glass tube with energy particles and a camera zoom, and exits at the paired pipe.
- Character is built from rounded primitives (capsules, spheres) with a procedural skeleton animated in code. No external model needed.

## Constraints
- Browser WebGL2; target 60 fps on integrated GPUs, so transmission passes are limited (few large glass meshes, cheap fake-refraction for small ones) and a quality toggle disables SSAO/transmission.
- Audio requires a user gesture to start; the menu click unlocks it.

## Risks and open questions
- Transmission materials are costly and sort poorly when glass overlaps; mitigate with a limited glass count and a fallback transparent material.
- Isometric depth ambiguity when jumping: add a blob shadow under the player and height-colored cues.
- Procedural music may sound thin; accept a simple but cheerful loop in v1.
- Hand-built character animation takes tuning time.
