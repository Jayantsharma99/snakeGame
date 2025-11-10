# Snake Game (Tkinter)

A simple Snake game implemented with Python's Tkinter library.

This repository contains a small Snake game using a grid of square "space" cells. The snake moves in discrete steps, eats food to grow, and the game ends when the snake hits a wall or itself.

---

## Table of contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [How to run](#how-to-run)
- [Controls](#controls)
- [Configuration](#configuration)
- [Code overview](#code-overview)
- [Known issues & suggested fixes](#known-issues--suggested-fixes)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- Classic Snake gameplay
- Score counter
- Configurable speed, board size and color constants

---

## Prerequisites

- Python 3.8+ (Tkinter comes bundled with the standard Python installation on most platforms)
- Tkinter available on your system:
  - On Debian/Ubuntu you may need: `sudo apt-get install python3-tk`
  - On macOS and Windows Tkinter is normally included by default with Python installers

---

## How to run

1. Place the game script (for example `snake_game.py`) in this repository root.
2. From a terminal run:

   python3 snake_game.py

   or on Windows:

   py snake_game.py

The game opens a Tkinter window — the score is shown at the top and the snake will start moving. Use the arrow keys to change direction.

---

## Controls

- Left arrow: move left
- Right arrow: move right
- Up arrow: move up
- Down arrow: move down

---

## Configuration

The following constants at the top of the script control gameplay and visuals:

- GAME_WIDTH — width of the play field in pixels (default 700)
- GAME_HEIGHT — height of the play field in pixels (default 700)
- SPEED — delay in milliseconds between moves (lower = faster)
- SPACE_SIZE — size of each grid square in pixels (default 50)
- BODY_PARTS — initial length of the snake (default 3)
- SNAKE_COLOR — hex color for the snake (default `#00FF00`)
- FOOD_COLOR — hex color for the food (default `#FF0000`)
- BACKGROUND_COLOR — hex color for the game background (default `#000000`)

To change difficulty or visuals, edit these constants at the top of the script.

---

## Code overview

Main components:

- Snake class
  - Holds snake coordinates and squares (rectangles drawn on the canvas).
  - Initializes the snake body and draws initial squares.

- Food class
  - Randomly places food within the grid and draws an oval on the canvas.

- next_turn(snake, food)
  - Moves the snake according to the `direction`.
  - Handles eating food, growing the snake, updating score, and scheduling the next turn.

- change_direction(new_direction)
  - Updates `direction` while disallowing 180° reversals.

- check_collisions(snake)
  - Checks collision with walls and snake body.

- game_over()
  - Clears the canvas and displays "GAME OVER".

Global state used:
- `direction` — current moving direction
- `score` — player score
- `canvas`, `window`, and `label` for the GUI

---

## Known issues & suggested fixes

I reviewed the script you posted and found several syntax and logic issues. The game logic is clear, but the script as posted will not run until the errors below are fixed. Here are the problems I noticed with suggested corrections:

1. Bad import line
   - Current (broken): `from tkinter \nimport * import random`
   - Fix: split into two valid imports:
     ```python
     from tkinter import *
     import random
     ```

2. Class constructors use `_init_` instead of `__init__`
   - Current: `def _init_(self):`
   - Fix: use Python constructor name:
     ```python
     def __init__(self):
         ...
     ```

3. BACKGROUND_COLOR line split incorrectly
   - Current: `BACKGROUND_COLOR = \n"#000000"`
   - Fix:
     ```python
     BACKGROUND_COLOR = "#000000"
     ```

4. Typos and spacing (e.g., `Fals e` in `window.resizable(Fals e, False)`, and `sna ke` in function signature)
   - Fix those spelling errors: `window.resizable(False, False)` and `def check_collisions(snake):`

5. Indentation & line-break issues
   - Several lines are broken or misindented in your snippet. Make sure indentation is consistent with 4 spaces and lines are not split mid-token.

6. Using `canvas` inside class constructors
   - The script uses a module-global `canvas`. Ensure `canvas` is created before you instantiate `Snake()` and `Food()` — in your snippet `canvas` is created before those calls, which is fine. Alternatively, pass `canvas` into class constructors for clarity and testability.

7. Global variable usage
   - The function `next_turn` modifies `score` and expects `direction` to be global. Those globals are OK for a small script but consider grouping game state in a `Game` class if you plan to extend this project.

8. Function/variable names and types
   - Ensure you're using lists consistently when managing coordinates (the script mixes tuples and lists in a few places — that is usually OK but be consistent).

9. Missing tags and cleanup
   - When regenerating food, the script uses `canvas.delete("food")` and repaints; just ensure tags are applied correctly (your code uses `tag="food"` when creating the oval).

If you'd like, I can produce a corrected, runnable version of the script that fixes the above issues and follows PEP8 formatting, then open a PR for you to review.

---

## Contributing

Contributions and improvements are welcome. If you want me to:
- Fix the script and open a PR — say "fix script".
- Add features like pause/resume, difficulty levels, high-score persistence — tell me which feature.

Please include a short description of the change in each commit / PR.

---

## License

This project is unlicensed by default. If you want a license, I recommend adding an MIT License unless you prefer a different one.

---

Enjoy — and let me know if you want me to:
- create a corrected runnable script,
- add unit tests,
- or open a PR with the fixes described above.
```# snakeGame
