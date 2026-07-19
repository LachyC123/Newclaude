# WICK — design document

## One-sentence identity

WICK is a portrait-mode one-thumb arcade climber where the player, as the last living flame, leaps between candles to escape the rising dark, while their flame acts as health, light radius and score multiplier at once.

## Player fantasy

*"I am a tiny, stubborn fire refusing to go out."* The player thinks about routes and timing; feels warmth-as-safety and darkness-as-dread; mastery looks like long heat chains through ember-rich risky branches; tension comes from melting perches and the rising dark; relief comes from lanterns and full-blaze power; "one more climb" comes from sub-2-second restarts and the visible BEST line in the world.

## Design pillars

1. **The flame is everything.** One resource (fuel 0–100) is health, light radius, and wisp-eating power. No second currency exists.
2. **Speed vs. safety is the core decision.** Perching refuels (+9/s) but melts the candle (~4.5s wick) and expires heat (3.4s window). Chaining costs fuel (−5/jump) but multiplies sparks and grants landing bonuses.
3. **All light is earned.** The darkness veil is only punched by fire the player ignited. Readability *is* the reward for playing well.

## Core loop (≈2–4s per beat)

tap candle → arc flight (grab embers) → landing ignition (flash/squash/chime) → decide: refuel or chain → tap next candle.

## Systems and how they interact

| System | Interacts with |
|---|---|
| Fuel | flame size, light radius, wisp predation threshold (≥70), death |
| Wick burn | perch duration, candle death (gutter state), route pressure |
| Heat (combo) | ember value ×combo, landing fuel bonus, light radius bonus, chime pitch |
| The dark | pacing floor; accelerates with height; hurries when >300px behind |
| Cold drips | hit flame (−26) OR snuff candles behind you (world interaction); drift downwind |
| Wisps | threat below 70 fuel, prey above — flips risk assessment mid-run; drift downwind |
| Draughts (90m+) | telegraphed wind bursts: reach ×0.8, wick burn ×1.8, +2/s drain, all flames lean, drips/wisps pushed — an economic pressure, never an instant kill |

## Difficulty curve

- Rung gaps grow 30→56px with height; stub-candle (2s wick) chance 10%→45%.
- Dark speed 7px/s + 0.09/m, cap 34px/s. Drips from 30m, wisps from 60m, draughts from 90m.
- Lantern rest stops every 11–15 rungs (safe, slow regen, no melt, no heat).
- Biome shift every 100m (background palette + announcement bell): Tallow Cellars → Bone Gallery → Rust Chapel → Hollow.

## Art bible

- **Visual identity sentence:** a single warm ember of light crawling up a cold, black ruin — every visible pixel is lit by player-made fire.
- **Resolution:** 160px internal width, integer-scaled, `image-rendering: pixelated`; height adapts 240–400px.
- **Shape language:** soft rounded blobs for fire (friendly), tall thin rectangles for candles/pillars (fragile verticality), boiling irregular edge for the dark (formless threat).
- **Palette roles:** warm ramp `#fff7e6→#ffe08a→#ffa53d→#e8542e` = player/reward only; gold `#ffd75e` = pickups/best/heat; cyan ramp `#bdf3ff→#54d6ff→#1f7fae` = danger only; indigo grays = neutral world. Color meaning never crosses roles.
- **Lighting:** stepped 3-band punched light (no smooth gradients, no bloom), dithered edge sparkle on the dark.
- **Animation:** squash & stretch with spring return, anticipation via stretch at launch, ease-back overshoot; flame flicker is two summed sines; eyes track movement/target.
- **VFX hierarchy:** tiny (wax drips, motes) → standard (landing burst, ember pop) → strong (hit: hit-stop 60ms + shake + cyan flash) → rare (wisp devour, death slow-mo at 0.25× + soul ember).
- **Forbidden:** smooth gradients, neon outlines, glassmorphism panels, confetti, anti-aliased circles, more than one flash per event.

## Mobile UX

- One thumb, portrait. Tap targets: 30px internal assist radius (~60–90 CSS px).
- Auto-pause on blur/hidden; resume on tap. No mid-run purchases, timers or interrupts.
- Settings: SND on/off, FX FULL/SOFT (reduces shake, flash, haptics). Persisted.

## Scoring & retention

- Headline stat: **height (m)**; secondary: sparks (embers ×heat, wisps ×heat).
- Best height persisted and drawn *in the world* as a gold dashed line — the game's own ghost.
- Retention levers: mastery (routing, blaze play), curiosity (what's above 100m?), fast restart. No dark patterns.

## Known weaknesses / next priorities

*(Second pass, 2026-07: added draughts as the late-game third pressure, biome shifts every 100m, distinct snuff/howl/bell audio, ember magnetism, zoom-punch on devour, always-on trail at ×10 heat, PWA manifest + icon; fixed dead-candle landings extending combos.)*

1. **Balance still untested on real thumbs** — an optimal chainer holds full fuel; draughts pressure the wick/reach economy but drip density above 150m may need tuning up.
2. Parallax silhouettes are shared across biomes — per-biome props (bones, rust chains, nothing at all in the Hollow) would deepen the shift.
3. No offline service worker (manifest only); add one if the game gets a permanent host.
4. Wisps above 250m could gain a second behaviour (slow homing) to keep the predator/prey flip tense.

**Single highest-impact next step:** playtest on real phones and tune `K` (all tunables are one object at the top of `index.html`).
