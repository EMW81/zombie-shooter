# 🏗️ ARCHITECTURE — Kai's Zombie Shooter

Senior engineer override decisions for long-term project health.

---

## 🎯 TL;DR

**We are moving the game out of Claude's chat widget into a standalone browser project hosted on GitHub Pages. Three.js stays. Vanilla JavaScript stays. We split the monolithic one-file blob into proper modules. We add a save system, a config file, and version control.**

---

## 🔒 Override Decisions (non-negotiable)

These are the calls I'm making as the senior dev. They're not up for debate unless there's a strong reason to revisit.

### 1. Move out of Claude's chat widget → standalone HTML project
**Why:** The widget is a sandbox. It can't save progress, keyboard focus breaks, window is cramped, and code resets every session. A real project solves all of these in one move.

**Trade-off:** Kai needs to open a link or file instead of just chatting. Worth it 100x over.

### 2. Keep Three.js r128 (for now)
**Why:** Industry-standard, huge community, perfect for blocky Roblox-style rendering, works everywhere. Upgrading to the latest version is a Phase 4+ concern — not worth the refactor risk now.

**Rejected alternatives:**
- ❌ **Babylon.js** — also great, but no reason to switch
- ❌ **PlayCanvas** — requires their cloud editor, lock-in
- ❌ **Unity / Unreal / Godot** — not browser-first, slow iteration, huge download for players
- ❌ **Roblox Studio** — fun but locks you into Roblox's ecosystem and rules

### 3. Vanilla JavaScript (no React/Vue)
**Why:** Games run on `requestAnimationFrame` loops mutating state 60 times per second. React's "re-render when state changes" model is actively bad for this. Every React game I've seen fights the framework.

**What we DO use frameworks for:** Nothing right now. If we add a main menu that's very UI-heavy later, we might add Preact for menus only. Not worrying about it yet.

### 4. Plain script tags, no build tool (for now)
**Why:** Kai is 10 and new to code. "Open index.html in a browser" should work. No npm install, no webpack, no vite until we actually need it.

**When we add Vite:** When we start needing `import` statements, shared modules across dozens of files, or TypeScript. Estimated: Phase 3–4.

### 5. Modular file structure (split the monolith)
**Why:** The current code is 2000+ lines in one `<script>` tag with 1-character variable names. Nobody can read it, not even Claude two weeks from now. This is the #1 thing holding the project back.

**See "File Structure" section below.**

### 6. localStorage for save games
**Why:** Free, instant, no backend needed, supported everywhere. Perfect for a single-player game.

**What we save:**
- Money
- Unlocked guns
- Highest wave reached
- Settings (volume, controls)

### 7. GitHub + GitHub Pages for hosting
**Why:**
- Free
- Version control built in (we never lose work)
- Auto-deploys when we push code
- Gives Kai a real URL to share
- Industry standard — teaches real dev habits

### 8. Config file for all game numbers
**Why:** Every zombie speed, gun damage, shop price, wave size should live in `config.js`, not be buried in game logic. This lets us balance the game in 10 seconds instead of hunting through code.

### 9. Defer physics engine until we need one
**Why:** Right now we use simple AABB (box vs. box) collisions. That's perfect for a top-down shooter. Adding cannon-es or rapier would mean more complexity for zero gain.

**When to add:** If we ever add proper 3D physics (ragdolls, falling barrels, etc.). Not before.

### 10. No multiplayer until Phase 6
**Why:** Multiplayer is ~10x the engineering effort of single-player. Needs a backend, lobby system, networking code, anti-cheat, lag compensation. It's a separate game. Get solo amazing first.

---

## 📁 Target File Structure

```
zombie-shooter/
├── index.html              # Entry point, loads everything
├── style.css               # All UI styling (HUD, menus, shop)
├── README.md
├── .gitignore
│
├── src/
│   ├── main.js             # Boot the game, wire modules together
│   ├── config.js           # ALL tunable numbers live here
│   ├── state.js            # Global game state (single source of truth)
│   │
│   ├── core/
│   │   ├── loop.js         # requestAnimationFrame update/render loop
│   │   ├── input.js        # Keyboard + mouse + gamepad → unified input
│   │   └── save.js         # localStorage wrapper
│   │
│   ├── world/
│   │   ├── scene.js        # Three.js scene, camera, lights setup
│   │   ├── map-nuketown.js # Nuketown map geometry
│   │   └── lighting.js     # Moon, red flicker, etc.
│   │
│   ├── entities/
│   │   ├── player.js       # Player movement, HP, aiming
│   │   ├── zombie.js       # Zombie AI, variants, spawning
│   │   └── bullet.js       # Projectile logic
│   │
│   ├── systems/
│   │   ├── waves.js        # Wave scheduler, difficulty curve
│   │   ├── combat.js       # Damage, death, hit detection
│   │   ├── economy.js      # Money drops, shop purchases
│   │   └── collisions.js   # AABB collision checks
│   │
│   ├── weapons/
│   │   ├── guns.js         # Gun definitions
│   │   └── shoot.js        # Firing logic (spread, piercing, fire rate)
│   │
│   ├── ui/
│   │   ├── hud.js          # Health bar, money, wave counter
│   │   ├── shop.js         # Shop menu
│   │   ├── main-menu.js    # Start screen
│   │   └── game-over.js    # Death screen
│   │
│   └── audio/
│       ├── music.js        # Horror drone + heartbeat + stings
│       └── sfx.js          # Gun sounds, zombie moans, hits
│
└── assets/                 # (Phase 2+) images, models, real sound files
    ├── models/
    ├── textures/
    └── sounds/
```

**Why this structure:**
- **Small files** — each under 300 lines, easy for a 10-year-old to find things in
- **Clear job per folder** — world, entities, systems, ui, audio
- **Config isolated** — change damage without touching game code
- **Grows without getting messy** — add files, don't grow files

---

## 🔁 The Game Loop (How it all fits)

```
┌─────────────────────────────────────┐
│              main.js boots             │
│                    ↓                   │
│           load save, init scene        │
│                    ↓                   │
│          requestAnimationFrame ←─┐     │
│                    ↓              │     │
│   INPUT → update entities →       │     │
│   systems (waves, combat, econ)   │     │
│                    ↓              │     │
│   render scene (Three.js)         │     │
│                    ↓              │     │
│   update HUD ─────────────────────┘     │
└─────────────────────────────────────┘
```

Each module has ONE job. `input.js` only reads input. `combat.js` only decides who takes damage. `hud.js` only updates the UI. When something breaks, we know exactly where to look.

---

## 💾 Save Data Schema

```js
{
  version: 1,              // bump when we change the shape
  money: 450,
  gunsOwned: ["pistol", "shotgun"],
  currentGun: "shotgun",
  highestWave: 7,
  totalKills: 203,
  settings: {
    musicVolume: 0.6,
    sfxVolume: 0.8,
    controllerDeadzone: 0.15
  }
}
```

Saved to `localStorage.setItem("zs_save", JSON.stringify(data))`. Versioned so we can migrate if the shape ever changes.

---

## 🧪 Testing Philosophy

For now: **manual playtesting is the test suite.** Kai plays, Claude watches, bugs get fixed. Automated tests are overkill at this scale.

**When to add real tests:** If the project grows past ~10,000 lines of code or has 3+ people touching it. Not before.

---

## 🚀 Deployment

1. Push code to GitHub repo (`zombie-shooter`)
2. GitHub Pages auto-serves from `main` branch
3. Game lives at `https://<username>.github.io/zombie-shooter/`
4. Kai can share that URL with anyone

**No backend, no server costs, no deploy command — just git push.**

---

## ⚠️ Known Architectural Risks

1. **Three.js r128 is old.** Works fine now, but upgrading later could be painful. Pin the version, deal with it when we have to.
2. **No TypeScript.** Vanilla JS is fine at current scale. If the project balloons past 5000 lines, typos will start causing silent bugs. Revisit then.
3. **Single global state object.** Easy to read, easy to debug, but easy to mess up if modules mutate it carelessly. Convention: only `systems/` can mutate state, everything else reads.
4. **No hot reload.** Every change = refresh browser. Annoying but livable. Vite fixes this when we're ready.

---

## 📌 When to revisit this doc

- When we hit a wall the current architecture can't handle
- Before starting any new Phase
- If the team grows past 2 people
- Every 6 months even if nothing's wrong
