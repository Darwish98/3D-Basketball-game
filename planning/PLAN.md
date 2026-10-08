# Plan

- [ ] 1. **Project scaffold.** `npm create vite` TypeScript template in repo root; add `three`, `@types/three`, `postprocessing`, `vitest`. Scripts: `dev`, `build`, `test`. Add `.gitignore`, `src/main.ts` rendering a spinning cube.
      Why: DESIGN Stack.
      Done when: `npm run build` and `npm test` (one trivial test) pass.

- [ ] 2. **Isometric camera and lighting.** `src/render/renderer.ts`, `src/render/IsoCamera.ts` (yaw 45°, pitch 35°, orthographic or low-FOV perspective, damped follow, zoom/shake offsets), directional sun with shadows, hemisphere light, sky gradient.
      Why: OVERVIEW Must-haves (camera).
      Done when: a demo scene of stacked boxes shows clear isometric depth, and the camera smoothly follows a target moved by arrow keys.

- [ ] 3. **Input and game loop.** `src/core/Input.ts` (keyboard + gamepad, camera-relative movement vector), fixed-timestep loop in `src/main.ts`, `src/core/Events.ts` bus, `Game` state machine.
      Why: DESIGN How it works.
      Done when: Vitest tests for the event bus and the state transitions pass; the loop runs at a fixed 60 Hz update.

- [ ] 4. **Collision and player controller.** `src/world/collision.ts` (AABB/capsule vs boxes, ground detection) and `src/entities/Player.ts` with run acceleration, variable-height jump, coyote time, jump buffering, and a placeholder capsule mesh.
      Why: Must-haves (responsive character).
      Done when: Vitest tests cover gravity landing, coyote jump, buffered jump, and wall blocking; the player can run and jump across a test platform set.

- [ ] 5. **Level data and builder.** `src/world/level1.ts` declarative data (platforms, elevation steps, floating islands, spawn, goal position) and `src/world/buildLevel.ts` creating meshes and colliders with placeholder materials.
      Why: DESIGN How it works.
      Done when: the compact multi-elevation WORLD 1-1 layout loads and is traversable to the goal location.

- [ ] 6. **Coins, score, lives.** `Coin` entity (pickup, rotation, bob), a score/coins/lives model in `src/core/State.ts`, fall-off respawn, and game over at 0 lives.
      Why: Must-haves.
      Done when: Vitest tests for scoring and lives pass; collecting coins increments the counts in the console state log.

- [ ] 7. **Moving platforms, bounce pads, checkpoints.** Entities in `src/entities/` with the player riding movers, bounce impulse, and checkpoint respawn.
      Why: Gameplay list.
      Done when: tests cover rider carry and bounce velocity; manual play shows respawn at the last checkpoint.

- [ ] 8. **Interactive blocks and enemies.** Question blocks hit from below that release items and break into shards; patrolling enemies that are stomped (bounce, score) or hurt the player (lose life, i-frames).
      Why: Gameplay list.
      Done when: tests cover stomp vs side-hit resolution; the blocks and enemies work in level 1.

- [ ] 9. **Glass pipes and travel.** `src/entities/Pipe.ts`: paired pipes with spline travel, control lock, camera zoom, exit launch; a secret tunnel in the level. Pipes render as glass tubes with an inner flowing energy mesh.
      Why: Core feature in OVERVIEW Must-haves.
      Done when: entering a pipe moves the player along the spline to the exit pipe in under 2 s; a test checks the endpoint positions.

- [ ] 10. **Glass and crystal materials.** `src/render/materials.ts`: glass (transmission, IOR, thickness), crystal, grass, colored solids, liquid, glass coin, translucent question block with glowing item inside; environment map; Bloom and AO via `postprocessing`.
      Why: Visual style sections.
      Done when: the screenshot shows glass pipes, blocks and coins with visible interiors and reflections, and solid platforms stay readable.

- [ ] 11. **Character model and animation.** Procedural rounded-primitive hero (red cap, blue/red outfit, face) in `src/entities/PlayerModel.ts` with idle, run, jump, land, climb, and pipe-travel poses, squash and stretch.
      Why: Character section.
      Done when: each animation state is triggered by the matching player state, which is verified by a unit test of the state mapping and by manual play.

- [ ] 12. **Environment dressing.** Clouds, flowers, glass waterfall, translucent water, floating ambient particles, a blob shadow under the player.
      Why: Visual style.
      Done when: the level contains all listed decorations and the frame time stays under 16 ms on the dev machine.

- [ ] 13. **Particle and camera FX.** `src/fx/Particles.ts` (instanced): coin sparkles, glass shards, landing dust, pipe droplets and energy, speed trail; camera shake and jump/pipe zoom, all driven by events.
      Why: Animation & Effects.
      Done when: each event named above spawns its effect; a test confirms that the particle pool recycles without growth.

- [ ] 14. **Glass HUD and minimap.** `src/ui/hud.ts`, `hud.css`: frosted panels with COINS × 24 style, LIVES, WORLD 1-1, SCORE zero-padded to 6 digits, and a glass minimap canvas showing level layout and the player.
      Why: Glass UI.
      Done when: a test of the score formatter passes and the HUD updates live during play.

- [ ] 15. **Menus.** Title, pause, game over, and level complete glass cards with animated transitions; wired to the Game state machine.
      Why: OVERVIEW Done when.
      Done when: the flow title → play → pause → resume → finish → results → restart works with the mouse and keyboard.

- [ ] 16. **Audio engine and SFX.** `src/audio/AudioEngine.ts` (unlocked on first click, master volume, `PannerNode` positional sounds), synthesized SFX for coin, jump, land, glass hit, block, pipe whoosh and travel, sparkle, stomp, and ambient loop.
      Why: Sound Design.
      Done when: every gameplay event has a mapped sound, checked by a test over the event-to-sound table; positional pan is audible in play.

- [ ] 17. **Music.** `src/audio/music.ts` procedural, cheerful original loop with a light layering change near the goal; mute toggle.
      Why: Sound Design.
      Done when: music loops without clicks and the mute toggle works.

- [ ] 18. **Quality settings and performance pass.** Low/High toggle (disable SSAO and transmission → cheap transparent glass, lower shadow resolution, pixel ratio cap); profile and fix hot spots.
      Why: DESIGN Constraints.
      Done when: High runs ~60 fps on the dev machine, Low is measurably faster, and the toggle is in the pause menu.

- [ ] 19. **Final polish and README.** Tune jump, camera, and difficulty; complete the playthrough; write `README.md` with controls and run instructions.
      Why: OVERVIEW Done when.
      Done when: `npm run build` and `npm test` pass and WORLD 1-1 can be completed from title to results.

## Not part of this build loop
- Playtesting with other people and feel feedback.
- Choosing a hosting location for the build.
