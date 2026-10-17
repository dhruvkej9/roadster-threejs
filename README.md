# Roadster — Three.js Tesla Roadster Flight Sim

Single-file browser game. Drive a Tesla-Roadster-inspired car through a procedural
city, and take off with cold-gas thrusters when the road is not enough.

No build step, no `npm install`. Three.js loads from a CDN via an import map.
Open `index.html` and it runs.

## Controls

| Action | Desktop | Phone / tablet |
|---|---|---|
| Throttle / reverse | `W` / `S` | left pad — drag up / down |
| Steer | `A` / `D` | left pad — drag left / right |
| Ascend | `Space` | ▲ button |
| Descend | `Shift` | ▼ button |
| Reset | `R` | — |

Phone: drag anywhere in the left 46% of the screen for the virtual stick,
▲/▼ on the right to fly. Controls only appear on coarse-pointer devices.

## Mechanics

- Nitrogen tank burns while you climb and refills automatically on the ground.
- `GROUND` / `FLIGHT` / `DRY` state shown in the HUD. Run dry mid-air and you fall.
- Chase camera, speed / altitude / nitrogen HUD.

## Performance notes

The device is detected with `matchMedia('(pointer:coarse)')`:

| | Desktop | Phone |
|---|---|---|
| Buildings | 1388 | 524 |
| Shadow map | 2048² | off |
| Pixel ratio cap | 2 | 1.5 |
| Window strips | yes | no |
| Antialiasing | on | off |

1388 individual meshes plus a 2048² shadow map will melt a mid-range phone, so
the coarse-pointer path drops all three rather than micro-optimising.

## Known gaps

- **No building collision** — free-roam sandbox. Next step is an AABB sweep.
- **No multiplayer** — single player only.

## About the thrusters

Tesla's own Roadster page says cold-gas thrusters are *"positioned around the
perimeter"* but never publishes a count, capacity, or refill time. The ten
thrusters here are a design choice, not a published Tesla spec.

## Run locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

(Opening `index.html` via `file://` works in most browsers too, but a local
server is more reliable for ES module imports.)

## Stack

Three.js r160 via `unpkg` import map. No other dependencies.