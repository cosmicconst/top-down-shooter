# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository

Private GitHub repo: `https://github.com/cosmicconst/top-down-shooter`
- Use git commits with descriptive messages for every meaningful change
- Push to GitHub after each commit to save versions remotely
- To restore a previous version, use `git checkout <hash>` or `git revert`

## Running the Games

All games are single HTML files — open directly in any browser, no build step or dependencies.

```powershell
Start-Process "shooter.html"
Start-Process "tictactoe.html"
```

## Games

### shooter.html — Top-Down Shooter

Retro pixel-art top-down shooter built with HTML5 Canvas and vanilla JavaScript.

**Controls:** Arrow keys to move · Mouse to aim · Hold left click to shoot · R to restart

**Architecture (all inline in one file):**

- `TYPES` / `LEVELS` — enemy stat blocks and per-level wave configs (keys: `walker`, `runner`, `tank`, `shooter`)
- `Vec2` — 2D vector math (add, sub, scale, norm, dist, angle)
- `Particle` / `ScorePopup` — visual effects; fade out over time
- `Bullet` / `EnemyBullet` — projectiles with off-screen culling
- `Enemy` — moves toward player each frame; `shooter` type fires back on a timer
- `Player` — arrow-key movement, mouse aim angle, invincibility frames after hit (`iFrames`), damage flash
- `Game` — state machine (`menu → playing → waveClear → levelClear → gameOver`), wave spawning queue, collision detection, HUD rendering
- All input on `document` listeners (not canvas) to avoid overlay-blocking issues
- `game` and `canvas` declared before event listeners to avoid temporal dead zone

**Levels:** 4 levels × 3–4 waves each; enemy speed scales by `1 + (level-1) × 0.18` per level.  
**Scoring:** Walker 100 · Runner 150 · Tank 300 · Shooter 250 · Wave bonus +500 · Level bonus +1000×level  
**Persistence:** High score saved in `localStorage` key `tds_hi`

---

### tictactoe.html — Tic-Tac-Toe

**Architecture (all inline):**
- `WINS`: 8 winning combinations
- `board[9]`: cell states (`''`, `'X'`, `'O'`)
- `scores`: cumulative X/O/draw counts
- `init()` resets board · `checkWin()` scans `WINS` · `updateScores()` syncs DOM
