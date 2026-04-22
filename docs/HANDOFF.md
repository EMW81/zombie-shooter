# 🤝 HANDOFF — Kai's Zombie Shooter

> **Read this FIRST if picking up fresh.** Complete project state.

**Owner:** Kai (10, creative director) — GitHub: `EMW81` — email: `ericwilsonart@gmail.com`
**Last updated:** April 22, 2026 (session 2, huge batch)
**Live GitHub commit:** `044bf0653e577675a3220ec2ac4f404ccf32a70e` (PRE-huge-batch — see "⚠️ CRITICAL" below)
**Live URL:** https://emw81.github.io/zombie-shooter/
**Repo:** https://github.com/EMW81/zombie-shooter

---

## ⚠️ CRITICAL STATE NOTE (read before anything else)

The session that wrote this handoff shipped a HUGE feature batch (13 features) to the ephemeral build disk, but **the final GitHub push did not complete** (tool call was cut off mid-stream by a 104KB content payload). That means:

- **What's on GitHub (live site):** the PREVIOUS feature set ending at commit `044bf065` — Roblox heads, gun zombies, chaos mode, darker nights, 10 wave cap, 5 guns, 9 zombie types.
- **What was built but never pushed:** DEVASTATOR gun, secondary weapon slot + 4 secondaries, rainbow + lightning zombies, wave cap 15, loot chests, grenades, army bomb, 4 powerups, cinematic death fade. See "What was built this session" below.
- **The playable version with the new features:** Kai has it as a local file (`zombie-shooter.html`, ~104KB, artifact presented at end of last session). **Ask Kai to upload that file to the new chat** — you can use it as the source of truth to recreate the beautified working copy and push to GitHub.

**Your FIRST action in a fresh chat should be:** ask Kai to upload his `zombie-shooter.html`, then beautify it into `/home/claude/game.html`, push it to GitHub, and present a fresh artifact. Only after that do any new features.

---

## 🎮 Full feature matrix AS IT EXISTS IN THE UNPUSHED BUILD (Kai's local file)

### Modes
- **REGULAR** — Survive **15 waves** (was 10) to WIN
- **HARDCORE** — Faster zombies, witch curses, beat wave 15 to TRULY BEAT THE GAME
- **MARATHON** — Endless with localStorage high-score
- **CHAOS** — Random theme + map + 0–3 disasters at start

### Themes: CITY, FOREST, DESERT, SNOW
### Sizes: SMALL 80, MEDIUM 130, BIG 180

### Zombies (11 types — 2 new)
| Type | HP | DMG | Speed | Wave | Notes |
|---|---|---|---|---|---|
| Walker | 40 | 10 | .093 | 1+ | Basic |
| Ghost | 35 | 12 | .115 | 3+ | Transparent |
| Runner | 22 | 20 | .104 | 4+ | Fast |
| Ice | 55 | 14 | .087 | 4+ | Cyan glow |
| Magma | 85 | 28 | .095 | 5+ | Red glow |
| Tank | 220 | 80 | .066 | 6+ | Bullet sponge |
| Gunner | 55 | 15 | .06 | 7+ | Stops at 12u, shoots red bullets |
| **Lightning (NEW)** | 120 | 25 | .12 | 8+ | Electric-blue glow + flicker, 2 white spark boxes on shoulders |
| **Rainbow (NEW)** | 300 | 35 | .105 | 10+ | Cycles through rainbow colors, yellow emissive crown, 250 reward |
| Witch | 70 | curse | .07 | HC 3+ | Curse orbs |
| Boss | 1800 | 35 | .082 | every 5th | Shockwave slam |

### Guns — PRIMARY (6 total, 1 new)
| Name | Cost | DMG | Fire | Bullets | Pierce |
|---|---|---|---|---|---|
| Pistol | $0 | 25 | 280 | 1 | 0 |
| Shotgun | $250 | 18 | 650 | 6 | 0 |
| AR | $600 | 22 | 100 | 1 | 0 |
| Sniper | $900 | 140 | 800 | 1 | 2 |
| Minigun | $2000 | 16 | 55 | 1 | 0 |
| **DEVASTATOR (NEW)** | $5000 | 200 | 120 | 3 | 5 |

### Guns — SECONDARY slot (all new, press G to swap)
| Name | Cost | DMG | Fire | Bullets | Pierce |
|---|---|---|---|---|---|
| Handgun | $0 (starter) | 18 | 320 | 1 | 0 |
| Revolver | $400 | 55 | 500 | 1 | 1 |
| Energy Pistol | $1200 | 40 | 160 | 1 | 1 |
| Dual Energy Pistols | $3500 | 45 | 90 | 2 | 1 |

### Power-ups (all 90 seconds; from chests or bomb is instant)
- **Faster** — Player moves 1.6x
- **Slow Zombies** — Zombies move 0.45x
- **Rapid Fire** — All guns fire at 0.5x fire rate
- **Ultra Damage** — All shots do 2x damage
- **Army Bomb** — One-time wipe-all, purple light flash, screen shake, explosion sound

### Loot Chests
- Spawn every ~15s during gameplay at 18% chance, max 2 at once
- Gold box with glowing lock, point light, bob + rotate
- Pickup radius 1.8u: gives $860 + 1 grenade + 1 random powerup

### Grenades
- Thrown on F key, physics arc with bounce
- 1.6s fuse, 8u AoE, 180 dmg with falloff
- Orange flash + shake on explode

### HUD additions
- Gun label prefixed `[1]` or `[2]` to show primary/secondary
- Heal inventory now shows BAND / MED / GREN / BOMB counts
- Power-up panel top-left: active powerups with countdown timers + color coding

### Cinematic death
- On HP=0: camera tips slowly to -π/2.5 pitch over 2.8s, eye height drops to .5
- Black fade div overlays at 0.05s with 2.8s ease-in transition
- Game-over overlay shows at 3s

### Keybinds (full)
- WASD / arrow keys: move
- Mouse: look
- Click: shoot
- B: shop
- G: swap primary/secondary
- F: throw grenade
- H: detonate army bomb
- E: bandage
- Q: medkit
- 1-5: select primary
- Esc (in shop): close

---

## 🔜 Still outstanding (deferred across sessions)

1. **Grass that bends when player walks through** (explicitly deferred this session — too big)
2. **Per-surface footstep sounds** (grass, concrete, wood — explicitly deferred)
3. **Bridges** walkable between map areas
4. **Two-story buildings** with interior stairs
5. **Round/organic objects** (replace boxes with cylinders/spheres)
6. **Skyscrapers** at city map corners (deferred from prior session)
7. **More texture polish** (consistent texture application)
8. **Scarier zombies** beyond Roblox heads — torn clothes, blood stains, randomized limbs

---

## 🧰 Build pipeline

Working copy is BEAUTIFIED on disk, MINIFIED before push.

```
/home/claude/zombie-shooter/          ← git clone (pristine reference)
/home/claude/game.html                 ← beautified file, THIS is what you edit (~3540 lines as of last session)
/home/claude/extract_and_minify.js     ← extracts <script> → /tmp/big.js
/home/claude/reassemble.js             ← puts /tmp/big.min.js back into HTML → /tmp/final.html
/tmp/big.js                            ← extracted pre-minified script
/tmp/big.min.js                        ← minified via terser
/tmp/final.html                        ← final output ready to push
/mnt/user-data/outputs/zombie-shooter.html  ← artifact version (localStorage stripped)
```

### Standard workflow per change
1. Edit `/home/claude/game.html` via `str_replace`
2. `cd /home/claude && node extract_and_minify.js && terser /tmp/big.js -c -m --toplevel -o /tmp/big.min.js`
3. Syntax-check: `node -e "new Function(require('fs').readFileSync('/tmp/big.min.js','utf8'));console.log('OK')"`
4. `node reassemble.js` → `/tmp/final.html`
5. Strip localStorage → `/mnt/user-data/outputs/zombie-shooter.html`
6. `cat /tmp/final.html` → feed to `github:create_or_update_file`
7. `present_files` the artifact

### ⚠️ Push size warning (learned this session)
When final HTML exceeds ~100KB, `create_or_update_file` with inline `content=` can TIMEOUT/DROP mid-stream. Before pushing, check size: `wc -c /tmp/final.html`. If over 95KB, consider:
- Splitting the CSS or script into external files (breaks single-file simplicity)
- Minifying CSS too (currently the CSS is NOT minified in final output)
- Using `github:push_files` which may handle large payloads better (untested here)
- Always `get_file_contents` right after to verify the push actually committed — SHA must change from what you passed as the `sha=` param

### Tools installed
- `js-beautify` and `terser` at `/home/claude/.npm-global/bin/`
- Node 20+

### Current file sizes (unpushed build)
- Beautified: ~132KB, 3540+ lines
- Minified script block: 73KB
- Final HTML: **103.9KB** — right at the danger threshold

---

## 🔑 Key function name mappings

The beautified code uses readable names but they mangle after terser. **Always edit the BEAUTIFIED file**, never hand-edit minified.

Current minified name map (may drift on next terser run):
- `Ne` = map reset (was `Oe`)
- `Fe` = start game (was `ze`)
- `Ue` = death fn (was `Ce`)
- `Ce` = announce (was `Le`)
- `ze` = HUD update (was `He`)
- `Oe` = shop toggle (was `Ce`)
- `ge` = zombie bullet spawn
- `Me` = tornado spawn
- `z` = renderer (was `k`)
- `k` = camera (was `z`)
- `P` = scene (was `B`)
- `B` = ambient light (was `P`)
- `We` = audio context (was `Fe`)

State slots added this session: `currentSecondary`, `ownedSecondaries`, `usingSecondary`, `powerups`, `bombs`, `grenades`, `chests`, `nextChestCheck`, `deathStart`, `deathStartPitch`, `deathStartEye`, `grenadesList`

New helper functions added: `activatePwr`, `detonateBomb`, `throwGrenade`, `upGrenades`, `spawnChest`, `upChests`, `upPwrHud`

Main loop now calls: `upGrenades(a)` and `upChests(a)` (wired after `upZB(a)`).

Map reset (`Ne`) now also clears: `chests`, `grenadesList`, `powerups`, `nextChestCheck`.

---

## 🗣️ How to talk to Kai

- He's 10. Plain English, no jargon. Explain technical terms in one line if you use them.
- He's the director. He says WHAT. You own HOW. Don't ask him implementation questions — pick and go.
- Keep responses short. Celebrate wins briefly.
- Minimal bullet lists. Only when genuinely list-like.
- Prefers in-chat artifacts (`present_files`) alongside GitHub push because GitHub Pages caches.
- When you run out of tool calls mid-batch, tell him exactly what's done on disk and what's left. He'll say "keep going" and you resume.
- For huge batches (5+ features): tell him up front which ones are this turn and which are deferred.

---

## 🚫 Never / ✅ Always

**Never:**
- Break spawn pool cumulative probability math (must stay < 1.0 in else-chain)
- Forget to clear new arrays in `Ne`/`Oe` map reset
- Push without syntax-checking via `new Function()`
- Hand Kai a markdown report about code changes (he wants the game, not docs)
- Hand-edit the minified output

**Always:**
- Update state init (new arrays/flags) at top of state object
- Add new zombie types to: CFG.ZOMBIE config, spawn pool, construction block, movement logic if non-standard, cleanup
- Wire new update functions into main render loop
- `new Function()` syntax-check before push
- Follow push with `present_files` of artifact
- **Verify push succeeded** by `get_file_contents` immediately after — if SHA hasn't changed, the push silently failed

---

## 📚 Other repo docs

- `README.md` — user-facing overview
- `MASTER-PLAN.md` — long-term vision
- `ARCHITECTURE.md` — tech decisions
- `CODE-AUDIT.md` — early prototype audit (historical)
- `ROADMAP.md` — phase plan (historical, we're past Phase 0)

---

## 🏁 One-line summary

Kai's browser zombie FPS has a huge unpushed batch (DEVASTATOR, secondaries, chests, grenades, bombs, rainbow+lightning zombies, wave 15, cinematic death). **Next session:** get the updated HTML from Kai's local file, push it to GitHub, THEN tackle grass bending + per-surface footsteps + skyscrapers.
