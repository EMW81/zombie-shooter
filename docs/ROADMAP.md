# 🗺️ ROADMAP — Kai's Zombie Shooter

The exact step-by-step path, starting right now.

---

## 👉 RIGHT NOW — Phase 1, Step 1: Get the code out of the chat

Before anything else, we need the game to live in actual files Kai can open, not a chat widget.

### Option A (fastest) — Local HTML file
1. Claude generates a full standalone `.html` file with the current game bundled in.
2. Kai downloads it. Opens it in his browser. Plays it.
3. Keyboard focus works instantly — it's a normal webpage now.

**Pros:** Kai can play offline. Works in 2 minutes.
**Cons:** No save yet. No sharing yet.

### Option B (better long term) — GitHub repo + Pages
1. Claude generates the full project structure.
2. Kai (or an adult helping) creates a free GitHub account.
3. Uploads the files to a repo.
4. Turns on GitHub Pages.
5. Game has a public URL Kai can share.

**Pros:** Shareable link, version control, free forever.
**Cons:** ~15 minutes of account setup, probably needs an adult's help.

**Recommendation:** Do **Option A first** (instant win), then **Option B** next session.

---

## 📅 Phase 1 — Full checklist

Do these in order. Don't skip.

### 1.1 — Standalone HTML file *(first deliverable)*
- [ ] Bundle current game into `index.html` + inline Three.js
- [ ] Test keyboard focus on Chrome, Safari, Firefox
- [ ] Confirm Xbox controller still works
- [ ] Confirm music still plays

### 1.2 — Split into modules
- [ ] Create folder structure per ARCHITECTURE.md
- [ ] Extract `config.js` with every tunable number
- [ ] Extract `state.js` as single source of truth
- [ ] Move input code → `src/core/input.js`
- [ ] Move scene setup → `src/world/scene.js`
- [ ] Move Nuketown geometry → `src/world/map-nuketown.js`
- [ ] Move player → `src/entities/player.js`
- [ ] Move zombies → `src/entities/zombie.js`
- [ ] Move waves → `src/systems/waves.js`
- [ ] Move shop → `src/ui/shop.js`
- [ ] Move music → `src/audio/music.js`

### 1.3 — Save system
- [ ] Create `src/core/save.js`
- [ ] Auto-save after every zombie kill and shop purchase
- [ ] Auto-load on game start
- [ ] Add "Reset Progress" button in main menu

### 1.4 — Main menu
- [ ] New screen before game starts
- [ ] Shows high wave, total kills, total money earned
- [ ] Buttons: PLAY, SETTINGS, RESET PROGRESS
- [ ] Works with keyboard, mouse, AND Xbox controller

### 1.5 — Settings screen
- [ ] Music volume slider
- [ ] SFX volume slider
- [ ] Controller deadzone
- [ ] Save preferences to localStorage

### 1.6 — GitHub + Pages
- [ ] Create GitHub account (adult help)
- [ ] Create repo `zombie-shooter`
- [ ] Upload project
- [ ] Enable GitHub Pages
- [ ] Test the live URL
- [ ] Bookmark it everywhere

### 1.7 — Playtest
- [ ] Kai plays for 30 minutes start-to-finish
- [ ] Kai shares URL with a friend, they play
- [ ] Write down any bugs or "ugh" moments
- [ ] Fix the top 3

**Exit Phase 1 when:** Kai and one other person can play the full game from a URL, progress saves, no critical bugs.

---

## 📅 Phase 2 — Feel & Polish (after 1 is done)

Quick wins that make the game feel 10x better without adding complexity.

1. **Muzzle flash** — small yellow flash sprite on gun tip when firing
2. **Bullet tracers** — visible line/streak following bullets
3. **Hit flash** — zombie turns white for 1 frame when hit
4. **Blood puff** — small red particle burst on hit
5. **Damage numbers** — pop up over zombie head when hit
6. **Screen shake** — small camera shake on shots, bigger on player hit
7. **Low HP vignette** — red blurry edges when HP < 30%
8. **Wave-start zoom** — camera briefly pulls back with wave number flash
9. **Better gun sounds** — real synthesized bangs, different per gun
10. **Zombie moans** — random ambient moans from offscreen zombies

---

## 📅 Phase 3 — More Content

New zombies, guns, and upgrades. ONLY start after Phase 2 feels tight.

- Spitter zombie (ranged attack)
- Exploder zombie
- Boss zombie (every 10 waves)
- Flamethrower, Rocket Launcher, Crossbow
- Gun upgrade system (damage / fire rate / mag size)
- Player perks (speed, extra HP, double money)

---

## 📅 Phase 4 — Maps

- Farm map
- Subway map
- Rooftop map
- Map selector
- Day/Night cycle

---

## 📅 Phase 5 — Progression

- Achievements
- Daily challenges
- Prestige system
- Leaderboards (local)

---

## 📅 Phase 6 — Stretch (only if we still love it)

- Co-op multiplayer
- Character skins
- Mobile polish
- Custom map editor

---

## 🎯 Definition of Done (for any task)

Before checking a box, all of this must be true:

1. ✅ Works with keyboard + mouse
2. ✅ Works with Xbox controller
3. ✅ Doesn't break on browser refresh
4. ✅ Doesn't console.error anything
5. ✅ Kai has played it and said "ok cool"
6. ✅ Code is readable (variables have real names)
7. ✅ Committed to Git (once we have it)

---

## 🚦 When to say NO

Kai might ask for stuff that breaks the plan. Senior-dev Claude should push back politely when:

- Adding a feature before Phase 1 cleanup is done → "Let's finish the cleanup first, then this'll be way easier to build."
- Adding multiplayer → "That's a Phase 6 thing — huge project on its own, let's get solo great first."
- Switching engines → "Three.js is still the right tool; let's see what the issue really is."
- Porting to iPhone app store → "Browser version works on iPhone's browser already. App store is a whole different project."

Push back with reasons, not just "no." And if Kai really wants it, hear him out — he's the director.
