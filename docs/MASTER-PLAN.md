# 🎯 MASTER PLAN — Kai's Zombie Shooter

The complete vision, broken into phases so we never bite off more than we can chew.

---

## 🌟 The Vision

A blocky, Roblox-style zombie survival shooter that feels genuinely scary at night, is fun enough to play for hours, and works on keyboard, mouse, and Xbox controller. The player fights endless waves of zombies in a Nuketown-inspired map, earning money to unlock bigger, louder, more chaotic guns.

**Core feelings we're going for:**
- "Oh god another one" — tense horror atmosphere
- "YES!" — that satisfying moment the Minigun unlocks
- "Just one more wave" — the loop that makes you keep playing

---

## 🧱 Guiding Principles

1. **Fun first, graphics second.** A blocky fun game beats a pretty boring one.
2. **Every new feature must make the game more fun, not just more complicated.**
3. **If it doesn't work on Xbox controller, it's not done.**
4. **Save the player's progress.** Nobody likes grinding the same wave twice.
5. **Small changes, ship fast, playtest, repeat.**

---

## 🗺️ The Phases

### ✅ Phase 0 — Prototype (DONE, inside Claude chat)
- Core gameplay loop working
- 5 guns, 3 zombie types, wave system
- Shop + money economy
- 3D Nuketown map
- Xbox controller
- Horror synth music
- 3-second lobby countdown

**Status:** Proven the concept works. Time to move out of Claude's chat box.

---

### 🔨 Phase 1 — Real Project (NEXT — THIS IS WHERE WE ARE)
**Goal:** Get the game out of the chat widget and into a real standalone HTML project Kai can open in his browser and share with friends.

- [ ] Move code into separate files (index.html, style.css, src/*.js)
- [ ] Fix keyboard focus bug once and for all
- [ ] Add **localStorage save system** (money, unlocked guns, high wave)
- [ ] Add a real main menu
- [ ] Deploy to GitHub Pages so Kai has a real URL
- [ ] Set up Git so we never lose work

**Exit criteria:** Kai can bookmark a link and play the game anywhere, progress saved.

---

### 🎨 Phase 2 — Feel & Polish
**Goal:** Make it feel GOOD to play.

- [ ] Muzzle flashes + bullet tracers
- [ ] Zombie hit reactions (stagger, blood puff)
- [ ] Screen shake on shots/hits
- [ ] Better sounds (gun sfx, zombie moans, reload clicks)
- [ ] Damage numbers pop off zombies
- [ ] Pickup animations for money
- [ ] Wave start/end dramatic camera zoom
- [ ] Red vignette when low HP

---

### 🧟 Phase 3 — More Content
**Goal:** Give the player reasons to keep playing.

- [ ] New zombie: **Spitter** (ranged acid attack)
- [ ] New zombie: **Exploder** (charges, explodes on contact)
- [ ] New zombie: **Boss zombie** every 10 waves
- [ ] New gun: **Flamethrower**
- [ ] New gun: **Rocket Launcher**
- [ ] New gun: **Crossbow** (silent, piercing)
- [ ] Gun **upgrade paths** (pay money to upgrade damage/fire rate/ammo)
- [ ] **Perks** you can buy (faster movement, extra HP, double money)

---

### 🗺️ Phase 4 — Maps & Variety
- [ ] Map 2: **Farm** (open fields, barns to hide in)
- [ ] Map 3: **Subway** (tight corridors, flickering lights)
- [ ] Map 4: **Rooftop** (vertical gameplay)
- [ ] Map selector on main menu
- [ ] Day/Night cycle (night is harder, more money)

---

### 💾 Phase 5 — Progression Systems
- [ ] **Prestige levels** (reset progress for bonuses)
- [ ] **Achievements** (kill 1000 zombies, survive 50 waves, etc.)
- [ ] **Daily challenges** (one-gun-only, no shop, double zombies)
- [ ] **Leaderboard** (local high scores first, online later)

---

### 🌐 Phase 6 — Stretch Goals (Way Later)
Only if we still love the game and have the time.

- [ ] **Co-op multiplayer** (2 players, same map, share money)
- [ ] **Character skins**
- [ ] **Mobile controls** (touch joystick — partially done already!)
- [ ] **Custom map editor**

---

## 🚫 What we are NOT doing

Decisions to prevent scope creep:

- ❌ **No microtransactions, ever.** This is Kai's game, not a cash grab.
- ❌ **No accounts/logins in Phases 1–5.** Local save is enough.
- ❌ **No porting to Unity/Unreal.** Web-first, period.
- ❌ **No online multiplayer before Phase 6.** It's a whole separate project.
- ❌ **No photorealistic graphics.** Blocky is the style. Lean into it.

---

## 📏 How we measure success

| Phase | Success looks like |
|---|---|
| 1 | Kai can send his friend a link and they can play |
| 2 | Kai says "oh that feels cool" when testing |
| 3 | A play session naturally lasts 10+ waves |
| 4 | Kai picks a favorite map |
| 5 | Kai wants to beat his own high score |

---

## 👥 Team (for real)

- **Kai** — Lead Designer, Creative Director, Final Say on Fun
- **Claude** — Everything else (code, art, audio, design help, QA)

**Kai's job:** Tell Claude what should happen, how things should feel, what's fun and what's boring.

**Claude's job:** Make it happen, explain it simply, flag when something is a bad idea.
