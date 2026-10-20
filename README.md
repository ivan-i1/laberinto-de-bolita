# Laberinto de Bolita

A tilt-maze ("ball in a labyrinth") game for Android, iOS and web: tilt the phone to roll the ball through the maze without falling into the holes.

**Status:** bootstrapped from [Base App](https://github.com/ivan-i1/BaseApp) at `81ddd19`. Every Base App module and demo is still in place. Gameplay hasn't started yet. The first deliverable is navigating the plane.

## Run it

```bash
npm install
npm run android    # dev build on an emulator or device (tilt needs a real phone)
npm run ios        # dev build on the iOS Simulator
npm run web        # browser, no tilt sensor: the ball falls with plain gravity
npm run check      # typecheck + unit tests + lint
```

## Identity

| | |
|---|---|
| Android package | `io.github.ivan_i1.laberinto_de_bolita` |
| iOS bundle id | `io.github.ivan-i1.laberinto-de-bolita` |
| URL scheme | `laberintodebolita://` |
| Version | 0.1.0 (versionCode 1) |

Release signing needs **this app's own** upload keystore in `credentials/`. Don't reuse Bounce Fidget's. See `credentials.example/`.

## Starting points for the maze

These pieces already exist:

- **Tilt input:** `src/engines/sensors/`. It smooths the signal, applies a dead zone, sets the current angle as level, and detects shakes. The axes are verified on Android only.
- **Frame loop:** `src/engines/game-loop/`. It includes `frameScale` (scales the loop to the display refresh rate) and `stepBall`, which handles screen-edge walls only.
- **Bump feedback:** `src/engines/audio/` and `src/engines/haptics/`.
- **Pause and options menus:** `src/menu/`.

The open design questions (camera, what "fall" means, the first deliverable's definition of done, ball size, platforms, visual tilt) are numbered 1–9 in `ADV-REV-laberinto-V1.md` §8. The maze-specific findings are in §3.4–§4 of that file: collision against interior walls, sub-stepping against tunnelling, holes, and the level format. It is in the repo root of the primary checkout and isn't tracked yet.

## Further docs

- `CLAUDE.md`: architecture rules that are easy to break.
- `docs/base-app.md`: what each inherited module does, plus icons, bundling, signing and debugging.
