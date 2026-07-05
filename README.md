Dynamic Pathfinding Agent
An interactive grid-based pathfinding visualizer built with Pygame. Watch A* and
Greedy Best-First Search** explore a grid in real time, then re-plan on the fly when
obstacles randomly appear in the agent's path.
-Why this project
Most pathfinding visualizers stop at "here's a static maze, here's the solution."
This one adds a **dynamic obstacle mode**: obstacles can spawn *while the agent is
mid-walk*, forcing it to detect the blockage and re-plan a new route from its current
position — a small step toward the kind of replanning real robots and game AI need.
Features :

- **Algorithms**: A\* Search, Greedy Best-First Search (GBFS)
- **Heuristics**: Manhattan distance, Euclidean distance
- **Interactive grid**: click-and-drag wall placement before running
- **Dynamic mode**: random obstacles spawn during agent movement, triggering automatic re-planning
- **Live metrics panel**: nodes visited, path cost, execution time (ms)
- **Animated search visualization**: frontier/visited/path cells render frame-by-frame
- **Configurable setup screen**: choose grid size and obstacle density before each run
Demo Controls
| Action | Control |
|---|---|
| Add wall | Left click (while idle) |
| Remove wall | Right click (while idle) |
| Start search | `Play Search` button or `Enter` |
| Reset | `Reset` button or `R` |
| Quit | `Esc` |
Installation
Requires Python 3.9+.
```bash
git clone https://github.com/TeemanNasir/Dynamic-Pathfinding-Agent.git
cd Dynamic-Pathfinding-Agent
pip install -r requirements.txt
```
Usage

```bash
python pathfinder.py
```

You'll be prompted with a setup screen to choose:
- Grid size (rows: 5–50, columns: 5–80)
- Obstacle density (0–70%)

Then the main window opens where you can place walls, pick an algorithm/heuristic,
toggle dynamic mode, and run the search.
Project Architecture

```
Dynamic-Pathfinding-Agent/
├── pathfinder.py          # Grid, Node, search algorithms, and Pygame UI
├── requirements.txt       # Runtime dependencies
├── tests/
│   └── test_pathfinding.py  # Unit tests for the search algorithms (no Pygame window needed)
├── .github/
│   ├── workflows/ci.yml   # Lint + test on every push/PR
│   ├── ISSUE_TEMPLATE/
│   └── PULL_REQUEST_TEMPLATE.md
├── LICENSE
├── CONTRIBUTING.md
└── CHANGELOG.md
```

> **Note on refactoring:** the algorithm logic (`astar`, `greedy_bfs`, `Grid`, `Node`)
> is intentionally pure Python with no Pygame dependency at the call level, so it can
> be unit-tested independently of the GUI. A future refactor could split this into
> `algorithms.py`, `grid.py`, and `ui.py` — see [CONTRIBUTING.md](CONTRIBUTING.md).

## How it works

1. A grid of `Node` objects tracks wall state and A\*/GBFS search costs (`g`, `h`, `f`).
2. `astar()` and `greedy_bfs()` run a standard best-first search using a binary heap,
   recording a snapshot of the open/closed sets at each step for animation.
3. In **dynamic mode**, each tick has a small probability of spawning a new wall near
   the agent. If that wall lands on the agent's remaining path, `_replan()` re-runs
   the search from the agent's current cell to the goal.

## Roadmap

- [ ] Extract algorithms into a standalone, Pygame-free module
- [ ] Add D\* Lite for true incremental replanning (vs. full re-search)
- [ ] Headless benchmark CLI (compare algorithms across N random maps)
- [ ] Diagonal movement option

## FAQ

**Q: Why does the agent sometimes take a while to find a path on large grids?**
A: Both algorithms are unweighted grid search; larger grids and low obstacle density mean more nodes to explore. This is a good area to try optimizing (see Roadmap).

**Q: Can I use a different grid size than the setup screen allows?**
A: The setup screen caps rows at 50 and columns at 80 to keep the animation smooth at 60 FPS. You can adjust `SCREEN_W`/`SCREEN_H` in `pathfinder.py` if you want a larger canvas.


Contributions are welcome! 

## License

This project is licensed under the MIT License 

Background

Originally built as Assignment 2 (Question 6) for an Artificial Intelligence course,
then extended into a standalone portfolio project.
