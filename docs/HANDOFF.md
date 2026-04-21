# 🤝 HANDOFF — Kai's Zombie Shooter

> **Purpose:** If Claude's chat resets, or someone else picks up this project, this one file brings them fully up to speed. Read this first.

**Project owner:** Kai (10, first real project)
**As of:** April 21, 2026
**Current phase:** 0 → 1 (moving prototype to real project)

---

## 📸 Current state, in one paragraph

We have a working browser-based 3D zombie shooter prototype built inside a Claude chat widget using Three.js r128 + vanilla JavaScript + Web Audio. Core gameplay (WASD movement, mouse aim, shooting, zombie waves, money drops, gun shop with 5 guns, 3 zombie variants, Xbox controller, horror synth music, 3-second lobby, blocky Nuketown-style map) all functions. The prototype validates the fun. It is NOT production code — it's a single 2000+ line blob with no saves, no version control, no separation of concerns. We are transitioning to a standalone HTML project on GitHub Pages.

---

## 🎯 What Kai has explicitly asked for

From conversations on record:

1. **Zombies that walk toward the player and deal damage. Death at 0 HP.** ✅ Built
2. **Multiple guns that cost more and do more damage.** ✅ Built (5 guns)
3. **Zombies drop money, money buys guns.** ✅ Built
4. **Xbox controller support.** ✅ Built (left stick, right stick, RT, Menu button)
5. **A 20-second lobby before waves start.** ✅ Built — but Kai later reduced to 3 seconds.
6. **Scary horror music, no vocals.** ✅ Built (synth drones, heartbeat, stings)
7. **Roblox-style blocky graphics.** ✅ Built
8. **Nuketown (Call of Duty) map as default.** ✅ Built
9. **(Implicit) The game should work reliably.** ⚠️ Partial — keyboard focus bugs in chat widget

---

## 🔁 What's in flight / unresolved

- Keyboard focus in Claude's widget is unreliable across browsers. Flagged to Kai, patched twice, not fully solved. **Resolution plan: move out of widget (Phase 1).**
- No save system. Every refresh = zero money. **Resolution plan: localStorage in Phase 1.**
- Three.js r128 is pinned and old. Defer to Phase 3+.

---

## 📦 What exists, where

**Location:** All prototype code lives inside Claude conversation artifacts in the chat thread titled **"Kai's Zombie survival game"** (started April 21, 2026).

**Not yet in a Git repo.** Not yet hosted. Not yet on disk.

**Key conversation milestones:**
1. Initial build — zombies, 5 guns, 2D top-down
2. Scary music + Xbox controller + 20s lobby added
3. Converted to 3D with Three.js (Roblox-style blocky characters)
4. Nuketown-style map added
5. Keyboard focus fixes attempted (multiple)
6. On-screen WASD/shoot/shop buttons added as fallback
7. Countdown reduced from 20s → 3s
8. This handoff written

---

## 🧱 The tech stack (current prototype)

| Layer | Tech | Notes |
|---|---|---|
| Renderer | **Three.js r128** | Loaded from cdnjs CDN |
| Game logic | **Vanilla JS** | No framework |
| 2D HUD | **HTML/CSS** overlay on Canvas | Inline styles (to be refactored) |
| Audio | **Web Audio API** | Synthesized, no audio files |
| Input | **DOM events + Gamepad API** | Unified input layer lives in same big function right now |
| Storage | **None** | Add localStorage in Phase 1 |
| Host | **Claude visualize widget** | Moving to GitHub Pages in Phase 1 |

---

## 🧱 The tech stack (where we're going)

Same as above, plus:

- **GitHub** repo with Git version control
- **GitHub Pages** auto-deploy
- **Split file structure** per ARCHITECTURE.md
- **localStorage** save system
- **Optional later:** Vite build tool when we graduate to ES modules

---

## 🧠 Design decisions worth knowing

1. **Blocky graphics are a style choice, not a limitation.** Keep them.
2. **Solo-only game through Phase 5.** No multiplayer until very late.
3. **Keyboard + Mouse + Xbox controller are all first-class citizens.** Every feature must work on all three.
4. **No payments, ads, or accounts.** This is Kai's game for fun.
5. **Horror atmosphere matters.** Don't bright-colorify it to look "kid friendly" — it's supposed to feel tense.
6. **Iteration speed beats perfection.** Ship changes, playtest, repeat.

---

## 🛠️ For whoever is continuing (Claude or human)

### The very next task
Start Phase 1. See **ROADMAP.md** for exact first steps.

### Do not
- ❌ Add a new gun, zombie, or map before Phase 1 is done. Tempting, but we'll regret it.
- ❌ Switch engines to Unity/Unreal/Godot. Kai wants browser.
- ❌ Add frameworks (React/Vue) for the game itself.
- ❌ Delete the old prototype code before Phase 1 is proven working. It's our reference.

### Do
- ✅ Read ARCHITECTURE.md and CODE-AUDIT.md before touching code.
- ✅ Talk to Kai like he's 10 (because he is), but respect his design decisions — he's the director.
- ✅ Explain trade-offs in plain English whenever making a technical choice.
- ✅ Commit often with clear messages once we have Git.

---

## 📞 Communication style with Kai

- **Short.** One idea per paragraph.
- **Plain English.** No jargon unless you explain it.
- **Show, don't just tell.** When possible, make the thing and let him try it.
- **Ask before major changes.** "Want me to try X?" not "I did X."
- **Celebrate wins.** He's 10 and this is his first project. Make it feel good.

---

## 🗂️ Document index

- `README.md` — Project overview
- `MASTER-PLAN.md` — Vision + all phases
- `ARCHITECTURE.md` — Tech stack + file structure + override decisions
- `CODE-AUDIT.md` — Brutal review of the prototype
- `HANDOFF.md` — You are here
- `ROADMAP.md` — Exact next steps

---

## 🪪 Credentials

Kai is the creative director. Claude is the studio. Decisions that affect *what the game is* go through Kai. Decisions about *how the game is built* go through Claude (with explanation).
