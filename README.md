# WICK — the last flame

**WICK is a portrait-mode, one-thumb pixel-art climber where you play the last living flame leaping candle to candle up an endless dark tower — and your flame is simultaneously your health, your light source, and your score engine.**

Everything is in one file: **[`index.html`](index.html)**. No build, no dependencies, no assets — art, FX and audio are all procedural. Open it in any browser (best on a phone) or host it anywhere (GitHub Pages works as-is).

## How to play

- **Tap a candle** to leap to it. Gold carets mark everything in reach.
- **Perch** on a burning candle to refuel — but the wick melts beneath you, and lingering kills your heat.
- **Chain fast jumps** to build **heat (×combo)** — it multiplies every spark you collect.
- **Grab gold embers** mid-flight for fuel and sparks.
- **Dodge cold drips** (watch the cyan shimmer) — they snuff flames, including you.
- **Blue wisps** steal your fire… unless you're at full blaze, in which case *you eat them*.
- **Cold draughts** (from ~90m) howl through the tower: shorter leaps, faster-melting wicks, every flame bent sideways. Hunker down or push through.
- **Outrun the rising dark.** It never stops.

The tower changes as you climb — cross into **the Bone Gallery** (100m), **the Rust Chapel** (200m) and **the Hollow** (300m).

One resource rules everything: your flame. Big flame = more health, a wider light radius, and wisp-eating power — but every jump and every second burns it down.

## Design pillars

1. **The flame is everything** — health, light, and multiplier are one resource, so every choice is a trade-off.
2. **Speed vs. safety** — perching refuels but melts your platform and fades your heat; chaining is hungry but scores.
3. **All light is earned** — the world is only visible where fire you lit still burns.

## Game feel notes

Register: playful-but-moody pixel character (flame has eyes that track its target). Feedback stack per the effect hierarchy: squash/stretch on jump & land, hit-stop + trauma-based screen shake + palette-role flashes on impacts (warm = reward, cyan = danger), afterimage trail in flight, procedural WebAudio SFX with combo-pitched chimes, haptics on supported devices. Shake/flash respect the FX SOFT toggle; particle counts are capped for stable 60fps at 160px internal resolution.

Full art bible, economy tuning and known weaknesses: [`DESIGN.md`](DESIGN.md).

## Development

```bash
# just open it
open index.html
# headless smoke test (drives a full run via window.WICK debug hooks)
# see scratchpad smoke test in the session; the game exposes window.WICK for automation
```

Saved locally: best height, sound/FX settings, seen tutorials (`localStorage`).

Installable as a PWA (manifest + icon + offline service worker) when served over HTTPS — e.g. GitHub Pages. Once installed it plays with no connection.

Feel details worth knowing: taps during flight are buffered into the next leap (chain by rhythm, not by waiting), beating your best pops **NEW BEST!** live mid-run, dying wicks flash a warning, and the dark visibly reaches for you when it's close.
