# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Project

Open `tictactoe.html` directly in any browser — there is no build step, server, or dependency to install.

To launch from the terminal:
```powershell
Start-Process "tictactoe.html"
```

## Architecture

The entire application is a single file: `tictactoe.html`, with three inline sections:

- **CSS (lines 7–100):** Dark-themed styles; CSS Grid for the 3×3 board.
- **HTML (lines 102–135):** Scoreboard (X Wins / Draws / O Wins), status label, 9 board cells (`data-i` index), and Restart button.
- **JavaScript (lines 136–206):** All game logic — no external dependencies.
  - `WINS`: 8 winning combinations
  - `board[9]`: current cell states (`''`, `'X'`, `'O'`)
  - `scores`: cumulative X/O/draw counts across restarts
  - `init()`: resets board and UI
  - `checkWin()`: scans `WINS` for a winning triple
  - `updateScores()`: syncs score counters to DOM
  - Cell click listeners handle turns, win detection, and draw detection
  - Restart button calls `init()`
