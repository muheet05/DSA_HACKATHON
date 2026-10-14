# 🧩 Dynamic Bitmask BFS Maze Solver with Interactive Tkinter GUI

An optimized pathfinding engine and interactive desktop visualizer designed to solve $N \times N$ mazes containing multiple collectible keys (`a`–`f`) and corresponding locked doors (`A`–`F`). 

The solver utilizes a **3D Bitmask Breadth-First Search (BFS)** to guarantee the global shortest path while keeping track of collected inventory states, exporting annotated CSV solutions and providing live desktop playback.

---

## 🚀 Key Features

* **Bitmask State-Space BFS:** Models the state as `(row, col, key_mask)` to cleanly handle backtracking after collecting keys without cyclic infinite loops.
* **Dual Deliverables:**
  * **Output 1:** Exact shortest path length (or `-1` if unreachable).
  * **Output 2 (`shortest_path_output.csv`):** Annotated grid marking traversal steps with `x`, retaining key pick-ups (`x(a)`) and door unlocks (`x(A)`).
* **Live Interactive Desktop GUI (Tkinter):**
  * Step-by-step agent animation and dynamic path highlighting.
  * Real-time Key Inventory HUD showing collected keys.
  * Door unlocking and key collection animations.
  * **Hot-Reloading:** Change the target destination or modify the source CSV file and click **`🔄 Reload File & Run`** to re-solve instantly without restarting the application.
* **Evaluator-Ready Input Support:** Seamlessly load external test cases from any standard CSV matrix.

---

## 📊 Complexity Analysis

Let:
* $N$ = grid dimension (total cells = $N^2$)
* $T$ = number of unique key/door pairs ($1 \le T \le 6$)

| Metric | Complexity | Explanation |
| :--- | :--- | :--- |
| **Time Complexity** | $\mathcal{O}(N^2 \cdot 2^T)$ | Every cell can be visited at most $2^T$ times (once per distinct key collection state). Each transition takes $\mathcal{O}(1)$ via bitwise operations. |
| **Space Complexity** | $\mathcal{O}(N^2 \cdot 2^T)$ | Maximum size of the BFS queue and `visited` hash set tracking `(row, col, bitmask)` tuples. |

> **Note on Performance:** Since $T \le 6$, $2^T \le 64$. For a typical $30 \times 30$ grid, the state space is bounded by $30^2 \times 64 = 57,600$ states, completing in **under 0.1 seconds**.

---

## 🛠️ Project Structure

```text
├── maze.ipynb                  # Jupyter Notebook with solver and visualizer
├── maze.csv                    # Default input maze CSV
├── shortest_path_output.csv    # Generated solution with annotated 'x' path
├── README.md                   # Project documentation
└── .gitignore                  # Git ignore rules