***

# Sudoku Heuristic Solver (C++)

This project implements a **constraint satisfaction problem (CSP) solver** for Sudoku puzzles in C++.
It uses a combination of modern heuristic techniques to efficiently solve puzzles:

- **MRV (Minimum Remaining Values)** with **degree tie-breaker**
- **LCV (Least Constraining Value)** value ordering
- **Forward checking** for domain pruning
- **Singleton (naked single) propagation**
- **Undo/Redo backtracking mechanism** for fast exploration

***

### Features

- Reads Sudoku puzzles either from a **sample hardcoded grid** or from **stdin** (with the `--stdin` argument).
- Detects **invalid starting puzzles** (duplicate numbers in row/col/box).
- Applies **domain propagation** to prune early contradictions.
- Backtracking with **heuristics** ensures efficient exploration.
- If a solution exists, prints the solved Sudoku grid to `stdout`. Otherwise, outputs `"UNSAT or invalid"`.

***

### Build Instructions

Make sure you have a modern C++ compiler (supporting C++17 or later).

```bash
g++ -O2 -std=c++17 sudoku_heuristic_solver_fixed.cpp -o sudoku_solver
```


***

### Usage

1. **Run with built-in sample puzzle:**

```bash
./sudoku_solver
```

2. **Provide puzzle via stdin:**

```bash
./sudoku_solver --stdin < puzzle.txt
```

    - The input file `puzzle.txt` must contain **81 integers (0 for blanks, 1–9 for digits)**.
    - Example format:

```
0 0 0 2 6 0 7 0 1
6 8 0 0 7 0 0 9 0
1 9 0 0 0 4 5 0 0
8 2 0 1 0 0 0 4 0
0 0 4 6 0 2 9 0 0
0 5 0 0 0 3 0 2 8
0 0 9 3 0 0 0 7 4
0 4 0 0 5 0 0 3 6
7 0 3 0 1 8 0 0 0
```


***

### Example Output

Solving the included sample puzzle might produce something like:

```
4 3 5 2 6 9 7 8 1
6 8 2 5 7 1 4 9 3
1 9 7 8 3 4 5 6 2
8 2 6 1 9 5 3 4 7
3 7 4 6 8 2 9 1 5
9 5 1 7 4 3 6 2 8
5 1 9 3 2 6 8 7 4
2 4 8 9 5 7 1 3 6
7 6 3 4 1 8 2 5 9
```


***

### Code Structure

- **Bit helpers**: Compact domain representation with fast popcount.
- **Neighborhood cache**: Precomputes peers for each cell (rows, columns, boxes).
- **Ledger**: Tracks candidate domains and used digits in rows/cols/boxes.
- **Undo/Redo stack**: Allows efficient backtracking.
- **Heuristics**:
    - Cell selection via MRV + Degree tie-breaker.
    - Value selection via LCV.
- **Propagation engine**: Naked single inference and forward checking.
- **DFS solver**: Recursive search using the above heuristics and undo system.

***

### Performance Notes

- Works efficiently on standard Sudoku puzzles (easy to expert level).
- May struggle with specially constructed “hard” Sudoku instances designed to defeat human tactics.
- The heuristic combination prunes most branches early compared to naive backtracking.

***

### License

This project is released under the MIT License. You are free to use, modify, and distribute it.

***

Would you like me to also include a **benchmark section** (performance stats on easy vs hard puzzles) in this README to showcase solver efficiency?

