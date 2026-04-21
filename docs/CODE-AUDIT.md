# 🔥 CODE AUDIT — Kai's Zombie Shooter (Prototype)

**Auditor:** Senior dev (Claude), wearing the bad-cop hat Kai asked for.
**Scope:** The entire prototype built inside Claude's chat widget.
**Verdict:** Good prototype, bad codebase. Keep the ideas, rewrite the structure.

---

## 🟢 What's Actually Good

Credit where it's due. The prototype works, and that's not nothing.

1. **The game is fun.** The core loop (shoot zombies → get money → buy bigger gun → repeat) is solid. No amount of refactoring can fix a boring game, and this isn't boring.
2. **Feature breadth is impressive.** 5 guns, 3 zombie types, waves, shop, 3D map, horror music, Xbox controller, touch controls — all in a prototype. That's a lot.
3. **The horror music is genuinely clever.** Synthesizing drones + heartbeat + random stings from scratch in Web Audio is a cool solution and sounds good.
4. **Xbox controller support early.** Most indie devs bolt this on last. Doing it early is smart.
5. **On-screen controls as fallback.** Good instinct for accessibility.

---

## 🔴 What's Broken or Fragile

The brutal part. None of these mean Kai did anything wrong — they mean it's time to graduate the code from "prototype" to "project."

### 1. It's one giant file
All 2000+ lines of HTML + CSS + JS live in a single visualize widget. There is no separation between:
- Three.js scene setup
- Game logic
- Input handling
- UI rendering
- Audio
- Zombie AI
- Save state (there is none)

**Why this matters:** To add a new zombie, you have to scroll through the entire thing. To fix a bug in shooting, you can't even `Ctrl+F "shoot"` because the word appears 40 times. The code can't be maintained past its current size.

### 2. Variable names are unreadable
Real variables in the code: `cv`, `cx`, `W`, `H`, `m`, `dly`, `dlg`, `actx`, `zs`, `rShop`, `zsGo`, `pData`, `hud`, `gstate`, `pDta`, `ovst`.

**Why this matters:** Future-you (or future-Claude) reading this code has to reverse-engineer what every letter means. `actx` is "audio context". `cx` is "canvas context". `m` is "master gain node." I know this because I wrote it — nobody else would. We shorten to save characters in the chat widget. In a real project, we write it out.

### 3. Global state everywhere
`keys`, `mouse`, `player`, `state`, `curGun`, `GUNS`, `bullets` — all globals. Any function can touch any of them at any time.

**Why this matters:** When a bug happens — "why is my health not going down?" — the answer could be in any of 30 places. We need a single source of truth that's only allowed to be mutated in specific places.

### 4. No save system at all
Every refresh wipes money, gun purchases, wave progress, EVERYTHING.

**Why this matters:** This alone disqualifies the project from being called a "game." It's a demo. Once Kai has players (friends, siblings), losing progress on a page reload will make them quit forever.

### 5. Keyboard focus bugs
The widget has to be clicked before it hears keys. We've patched this 3 times. Each patch worked for one user and broke for another.

**Why this matters:** This isn't fixable inside Claude's widget. It's a fundamental sandboxing thing the browser does. The fix is to leave the widget and run the game as a normal webpage where focus just works.

### 6. Magic numbers everywhere
Zombie speed: `0.028`. Pistol damage: `25`. Shotgun cost: `250`. Wave zombie count: `5 + wave * 2`. All hardcoded inline in game logic.

**Why this matters:** Balancing the game (is the shotgun too strong? are waves too easy?) means hunting through code instead of opening `config.js` and changing one number.

### 7. Draw + Update are tangled
The main loop function does math for moving entities AND draws them at the same time, in the same function. They should be separate steps. Right now it's hard to add things like pause, slow-motion, or replay.

### 8. Inline styles everywhere
`style="position:absolute;top:10px;left:12px;..."` repeated 50+ times. Changing the HUD color means a find-and-replace across a giant HTML string.

**Why this matters:** A stylesheet solves this in 5 minutes. We're just doing it the hard way because we were stuck in a chat box.

### 9. Music code is married to game code
The horror music logic is interleaved with gun logic. Can't mute. Can't change track. Can't turn off for a player who finds it annoying.

### 10. No version control
If Claude's chat history gets deleted, the code is gone. No backups. No history of "what changed when." No way to roll back a bad change.

### 11. No config for controls
Can't rebind keys. Can't change controller deadzone. Can't invert aim Y-axis.

### 12. No error handling
If Three.js fails to load, the game just silently doesn't start. The player sees a black box and has no idea why.

### 13. Three.js version pinned to r128 (old)
Current Three.js is r160+. We're 30+ major versions behind. Not urgent, but it's technical debt.

### 14. No asset pipeline
Everything is drawn with `THREE.BoxGeometry`. This is actually fine for the Roblox blocky style! But if we ever want to add a real zombie model, there's no system to load .glb/.gltf files.

---

## 🟡 Things That Are Fine Actually

Don't let the red list scare you. Not everything is bad.

- **Using primitives (boxes) instead of 3D models** → This IS the Roblox aesthetic. Keep it.
- **Simple AABB collisions** → Perfect for this game. No physics engine needed.
- **Synth music instead of audio files** → Still a good call. Small file size, infinite variation.
- **Canvas + Three.js together** → Standard technique for 2D HUD over 3D world.

---

## 🚨 Ranked Priority to Fix

In the exact order we should attack them in Phase 1:

| # | Issue | Severity | Effort |
|---|-------|----------|--------|
| 1 | One giant file → split into modules | 🔴 Critical | High |
| 2 | Move out of Claude widget → real HTML project | 🔴 Critical | Medium |
| 3 | No save system → add localStorage | 🔴 Critical | Low |
| 4 | No version control → set up Git | 🔴 Critical | Low |
| 5 | Magic numbers → extract to `config.js` | 🟠 High | Low |
| 6 | Global state → single `state` object w/ rules | 🟠 High | Medium |
| 7 | Inline styles → move to `style.css` | 🟡 Medium | Low |
| 8 | Rename cryptic variables | 🟡 Medium | Low |
| 9 | Separate music from game loop | 🟡 Medium | Low |
| 10 | Add error handling around Three.js boot | 🟢 Nice | Low |

**Rule of thumb:** Do all of 1–4 before adding a single new feature. Features built on a bad foundation just make the foundation worse.

---

## 🗣️ Plain English Summary for Kai

The game **plays** well. The **code** is a messy bedroom. Everything works if you step carefully, but nothing can be found, and if you build more on top it all collapses.

Phase 1 is literally just **cleaning the room** so we can build real furniture (new features) in it later. It's not glamorous, but it's the most important thing we'll do for this project.

Then the fun begins.
