# 🤝 HANDOFF — Kai's Zombie Shooter

> **If you (Claude or human) are picking this up fresh, read this FIRST.** This file is the complete state of the project as of the last session.

**Project owner:** Kai (10, creative director) — GitHub: `EMW81` — email: `ericwilsonart@gmail.com`
**Last updated:** April 22, 2026
**Live commit:** `044bf0653e577675a3220ec2ac4f404ccf32a70e`
**Live URL:** https://emw81.github.io/zombie-shooter/
**Repo:** https://github.com/EMW81/zombie-shooter

---

## 🎮 What the game is RIGHT NOW (as of commit 044bf065)

A browser-based 3D zombie shooter FPS. Single HTML file, ~92KB. Three.js r128. No build step on-site — the source lives beautified on disk, gets minified back down before push.

### Modes (menu-selectable)
- **REGULAR** — Survive 10 waves to WIN
- **HARDCORE** — Faster zombies, witch curses, more chaos, beat wave 10 to TRULY BEAT THE GAME
- **MARATHON** — Endless waves with localStorage high-score tracking
- **CHAOS** (new!) — Random theme + random map size + 0–3 random disasters at game start

### Themes (menu-selectable): CITY (Nuketown), FOREST (Dark Woods), DESERT (Wasteland), SNOW (Frozen)

### Map sizes: SMALL (80×80), MEDIUM (130×130), BIG (180×180)

### Zombies (10 types)
| Type | HP | DMG | Speed | Wave | Notes |
|---|---|---|---|---|---|
| Walker | 40 | 10 | .093 | 1+ | Basic |
| Runner | 22 | 20 | .104 | 3+ | Fast, low HP |
| Tank | 220 | 80 | .066 | 5+ | Slow bullet-sponge |
| Boss | 1800 | 35 | .082 | every 5th | Shockwave slam every 9s, 40 dmg ring, screen shake |
| Witch | 70 | curse | .07 | HC wave 3+ | Casts curse orbs → 2min slow/blurry/weak |
| Ice | 55 | 14 | .087 | 2+ | Cyan blue, icy glow |
| Magma | 85 | 28 | .095 | 4+ | Red-hot, emissive glow + red point light |
| Ghost | 35 | 12 | .115 | 2+ | Transparent 45% opacity, fastest |
| **Gunner** | 55 | 15 | .06 | **6+** | Stops at 12u, shoots red bullets every 1.5s, no melee |

**All non-witch zombies now have Roblox-style heads:** taller blocky shape, pale greenish face (gunners have darker gray), white rectangular eyes with black pupils, dark open mouth. Witches keep their pointy-hat green-eyed look.

### Weather / disasters (active during gameplay)
- **Meteor shower** — confined to map, 2.5× cylinder size, 22-unit light range
- **Tornadoes** — double-cone + 8 orbiting debris blocks, pulls player, 12 dmg
- **Hurricanes** — 1.8× bigger tornado, 14 debris, 20 dmg
- **Thunder storms** — dims ambient, random lightning flashes, WebAudio thunder rumble

### Guns (persist across deaths; money resets)
Pistol ($0, 25 dmg), Shotgun ($250, 18×6 pellets), AR ($600, 22 dmg fast), Sniper ($900, 140 dmg pierce 2), Minigun ($2000, 16 dmg 55ms fire rate).

### HUD / gameplay feel
- HP 150 max, iframes 400ms on hit, bandage (28 HP, 5 max stack, .7s cast) + medkit (100 HP, 3 max stack, 2s cast)
- 14-second lobby before wave 1 for scavenging
- Pointer-lock FPS mode, WASD + mouse + Xbox controller + mobile d-pad all work
- Zombies drop coins and sometimes heal items; boss drops rainbow coin ($500)
- Muzzle flash, blood splash particles, HP bars on tough enemies, corpse ragdoll, headshots (1.3× dmg + stun)
- Nighttime is notably darker now (city ambI 0.85, moonI 0.75; forest even darker)

---

## 🔜 OUTSTANDING — Kai's open requests (deferred on purpose)

In the last session, Kai gave a HUGE wishlist. We did a chunk. These are still pending:

1. **Bridges** — walkable platforms connecting areas of the map
2. **Two-story buildings** — second floor with interior stairs the player can climb
3. **Round/organic objects** — replace boxy meshes with cylinders/spheres for realism
4. **Skyscrapers** — very tall buildings in city maps (was planned for this session, ran out of tool calls at the insertion point)
5. **More texture polish** — make sure everything has the right texture applied
6. **More realistic/scarier zombies** — beyond the Roblox head change; think torn clothes, blood stains, maybe randomized limb positions

**Pick up with skyscrapers first** — they were the specific piece we couldn't finish. Find the city theme block in `N()` (now minified to `D()`) and add four tall concrete buildings at the map corners with lit windows. Only if `t >= 130`.

---

## 🧰 Build pipeline

Working copy is BEAUTIFIED on disk, MINIFIED before push.

```
/home/claude/zombie-shooter/          ← git clone of the repo (pristine reference)
/home/claude/game.html                 ← beautified file, THIS is what you edit (~3200 lines)
/home/claude/extract_and_minify.js     ← extracts <script> → /tmp/big.js
/home/claude/reassemble.js             ← puts /tmp/big.min.js back into HTML → /tmp/final.html
/tmp/big.js                            ← extracted pre-minified script
/tmp/big.min.js                        ← minified via terser
/tmp/final.html                        ← final output ready to push
/mnt/user-data/outputs/zombie-shooter.html  ← artifact version (localStorage stripped)
```

### Standard workflow for every change
1. Edit `/home/claude/game.html` via `str_replace` (or `create_file` for net-new code)
2. Run `cd /home/claude && node extract_and_minify.js && terser /tmp/big.js -c -m --toplevel -o /tmp/big.min.js`
3. Syntax-check: `node -e "new Function(require('fs').readFileSync('/tmp/big.min.js','utf8'));console.log('OK')"`
4. `node reassemble.js` → `/tmp/final.html`
5. Strip localStorage for artifact version, write to `/mnt/user-data/outputs/zombie-shooter.html`
6. `cat /tmp/final.html` → pass content to `github:create_or_update_file`
7. `present_files` the artifact so Kai can play immediately

### Tools installed
- `js-beautify` (global at `/home/claude/.npm-global/bin/`)
- `terser` (same path)
- Node 20+

### Current file sizes (commit 044bf065)
- Beautified: ~132KB, 3200+ lines
- Minified script block: 73KB
- Final HTML: 92KB (well within GitHub's file API limits)

---

## 🔑 Key function name mappings (beautified → minified)

The beautified code uses readable names. After terser, they mangle. When editing the minified output for reference:
- `addTor` → `Me` (tornado spawn)
- `upMet` / `upTor` / `upStorm` → inline in main loop
- `spawnZB` → `ge` (zombie bullet spawn)
- `upZB` → inline function in main loop
- Announce function → `ze` (minified) / `Le` (beautified at one point) / often aliased

**Always edit the BEAUTIFIED file** (`/home/claude/game.html`). Never hand-edit the minified.

---

## 🗣️ How to talk to Kai

- **He's 10.** Plain English, no jargon. If you use a technical term, explain it in one sentence.
- **He's the director.** He says WHAT and HOW IT LOOKS/FEELS. You own HOW IT'S BUILT. Don't ask him to pick between implementation approaches — just pick one and go.
- **Keep responses short.** One idea per paragraph. Celebrate wins briefly.
- **Minimal bullet lists.** Only when genuinely list-like.
- **He prefers in-chat artifacts** for immediate play (via `present_files`) alongside the GitHub push, because GitHub Pages has browser-cache lag.
- **When you run out of tool calls mid-batch**, tell him exactly what's done on disk and what's left — he'll say "keep going" and you pick up.
- **For huge batches (5+ features),** tell him up front: "I'll do the biggest ones this turn, the rest next turn." Don't try to cram.

---

## 🚫 Never

- Never break the spawn pool math — keep cumulative probabilities < 1.0 in the else-chain
- Never forget to clear new arrays in `Oe()` (map reset) — it'll leak meshes across games
- Never push without syntax-checking minified output via `new Function()`
- Never hand the user a markdown report about code changes — they want the game, not docs

## ✅ Always

- Always update state init (add new arrays/flags) at the top of the state object
- Always add new zombie types to: CFG.ZOMBIE, spawn pool, construction block, movement logic (if non-standard), cleanup
- Always wire new update functions into the main render loop
- Always test with `new Function()` before pushing
- Always follow the push with `present_files` of the artifact

---

## 📚 Other docs in this repo

- `README.md` — user-facing project overview
- `MASTER-PLAN.md` — long-term vision
- `ARCHITECTURE.md` — tech stack decisions
- `CODE-AUDIT.md` — early prototype audit (mostly historical now)
- `ROADMAP.md` — phase plan (also mostly historical; we're past Phase 0)

---

## 🏁 One-line summary

Kai's browser zombie FPS is live, playable, and feature-rich. Next session: finish skyscrapers + bridges + 2-story buildings. Pipeline works. Ship fast, celebrate wins.
