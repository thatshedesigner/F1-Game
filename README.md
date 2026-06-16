# F1 Racing Game

A single-file browser game built with HTML5 Canvas during an internship. No frameworks, no build tools, no dependencies. Open the file and play.

---

## How to Play

Open `f1racing-PS.html` in any modern browser. Pick a track, hit **START**, and drive.

The goal is to reach the finish line without hitting the walls, obstacles, or hurdles. The road narrows as you go, so what starts out comfortable gets tight by the end.

---

## Controls

| Key | Action |
|-----|--------|
| Arrow Up / W | Accelerate |
| Arrow Down / S | Brake |
| Arrow Left / A | Steer left |
| Arrow Right / D | Steer right |
| R | Reverse |

Lateral movement scales with speed. At low speed the car moves across the road slowly. At full speed it shifts fast, so high-speed steering near the walls is risky.

---

## Tracks

Six tracks are available. Select one before starting; switching mid-race resets the current run.

| Track | Finish Distance | Notes |
|-------|----------------|-------|
| Circuit | 8000 m | Default track, good starting point |
| Monaco | 8000 m | Narrow street circuit, four obstacle zones |
| Silverstone | 9000 m | Long and fast |
| Monza | 8500 m | Fast Italian track |
| Spa | 9200 m | Longest track, most distance to cover |
| Suzuka | 8800 m | Technical layout |

---

## What Can End Your Race

**Wall collision** -- the road curves using a sine wave offset and also narrows progressively as you cover more distance. Clip either boundary and the race ends.

**Obstacle hit** -- each track has fixed obstacle zones placed at specific distances. They appear as red-striped barriers.

**Hurdle hit** -- hurdles are placed every 1200 m in the early portion of the track and tighten to every 600 m after the 3000 m mark. There are three types:

- Chicane barriers (red panels on the left and right lane edges)
- Tire stacks (3x3 grid of black tires)
- Cone rows (five orange traffic cones in a line)

Hurdles rotate across the left, center, and right lanes in order, so you can watch the pattern and plan.

---

## HUD and Timing

While racing, the canvas shows:

- Current speed in KM/H (top left)
- Distance covered in meters (top left, below speed)
- Live race timer in M:SS.ss format (top left, in yellow)
- Best time for the current track (top left, below timer)
- Track name (top right)
- "FINISH LINE AHEAD" warning at 80% completion
- Reverse indicator when moving backward

The panel below the canvas also shows speed, distance, and the current track name.

---

## Best Times

Finishing a track records your time. Best times are saved in `localStorage` per track and persist between sessions. A new best time turns the result screen gold. Subsequent runs show both your current time and the standing best.

---

## Technical Notes

- Pure HTML, CSS, and vanilla JavaScript. No libraries, no build step.
- Rendering is done on a 1000x400 HTML5 Canvas element.
- Physics are frame-based: acceleration adds 0.4 per frame, natural deceleration is a 0.96 multiplier per frame, braking applies a 0.88 multiplier.
- Road curvature is a sine wave (`sin(distance * 0.002) * 60`) applied as a vertical offset to both road boundaries each frame.
- Collision detection checks distance proximity for obstacles (within 300 m) and hurdles (within 50 m), combined with a vertical position check against the car's Y coordinate.
- The game loop runs via `requestAnimationFrame`.

---

## File Structure

Everything is in one file: `f1racing-PS.html`

- Styles (reset, layout, canvas, control panel, game status overlay)
- HTML (header, track selector, canvas, control panel, status overlay)
- JavaScript (game state, car physics, track definitions, collision logic, drawing functions, HUD, localStorage for best times)
