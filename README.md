# 🦢 Neon Boids

*Flocking simulation with Craig Reynolds' boids algorithm. Watch glowing boids swarm, weave, and turn as one. Separation keeps them apart, alignment steers them together, cohesion makes them stay close. Click to scatter. Adjust all the knobs. The emergent murmuration effect, neon-styled.*

---

## What is this?

Boids is a classic artificial life simulation of flocking behavior. Each "boid" (bird-oid) follows three simple rules:
- **Separation:** steer to avoid crowding local flockmates
- **Alignment:** steer towards the average heading of local flockmates
- **Cohesion:** steer to move toward the average position of local flockmates

From these local interactions, complex global flocking behavior emerges — swirling, merging, turning in unison, just like schools of fish or murmurations of starlings. This version adds neon trails, adjustable rule weights, and a glowing aesthetic.

---

## Features

- **Real-time boids simulation** with O(N²) neighbor checks (optimized for N ≤ 500)
- **Neon glow** on each boid (triangle body) with colored trails based on heading
- **Trail rendering** — adjustable length (0–30 segments) showing recent motion path
- **Per-boid color variation** — each boid gets a unique hue that shifts slightly over time
- **Interactive disruption** — click anywhere to apply a strong repulsion force, scattering the flock
- **Adjustable parameters:**
  - Boid Count (20–500)
  - Perception Radius (20–150) — distance at which boids sense neighbors
  - Separation Weight (0–3) — strength of "don't crowd" steering
  - Alignment Weight (0–3) — strength of "fly same direction" steering
  - Cohesion Weight (0–3) — strength of "stay together" steering
  - Max Speed (2–10) — velocity limit
  - Trail Length (0–30) — how many past positions to draw
- **Pause/Resume** and **Randomize** all sliders
- **Stats overlay** — boid count, FPS
- **Single HTML file** — no dependencies

---

## How to Use

1. Open `index.html`
2. Watch the boids flock together. They automatically separate when too close, align their headings, and gently cohere toward the flock center.
3. **Click** anywhere to scatter the flock (repulsion force from click point).
4. Use sliders to morph the behavior:
   - Increase **Separation** to make boids avoid each other more aggressively (creates spaced-out formations)
   - Increase **Alignment** to make them match velocities tightly (smoother, more unified turning)
   - Increase **Cohesion** to pull them closer together (tighter groups)
   - Adjust **Perception Radius** to change how far they "see" — smaller = many small subgroups; larger = more unified whole
   - **Max Speed** controls overall velocity
   - **Trail Length** adds motion blur and visual history
5. Press **Randomize** to pick new random parameters and see wildly different flocking styles
6. Press **Pause** to freeze; **Resume** to continue

---

## Technical Details

- **Boid update order:** For each boid, scan all other boids within perception radius → accumulate separation, alignment, cohesion vectors → apply weighted limits → update velocity, position.
- **Boundary:** Toroidal wrap-around (boids leaving one edge enter opposite edge; neighbor searches wrap too, for consistency at perception radius).
- **Forces:** Each rule outputs a desired steering vector (bounded to `maxForce`, though we apply directly here). Weights are multipliers.
- **Trail storage:** Each boid keeps a circular buffer of its last N positions.
- **Rendering:** Canvas 2D. Boids drawn as triangles oriented along velocity. Trails as polylines with alpha gradient (uniform alpha for performance). `shadowBlur` for neon glow.
- **Performance:** O(N²) neighbor checks; N=500 yields 250k checks/frame, still okay on modern JS engines. If optimizing further, spatial partitioning would help.

---

## The Real Story

Boids is one of those elegant emergent systems: simple rules yield lifelike group behavior. Tweak the weights and you can get schooling fish, flocking birds, or even chaotic swarms. The neon trails give it a retro-futuristic vibe — like watching glowing data packets dance across a cyberpunk mainframe. It's hypnotic, relaxing, and surprisingly fun to just watch. The click-to-scatter mechanic adds interactivity, letting you disrupt the flock and watch it re-cohere.

---

*Made with 🦢 and Reynolds' rules.*

**Repo:** https://github.com/Kiloooai/neon-boids
