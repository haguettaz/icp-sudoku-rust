# Sudoku Solver

A high-performance Sudoku solver implemented in Rust, utilizing **iterative constraint propagation** to efficiently navigate the search space.
This solver is designed to handle grids of any difficulty, including ill-posed puzzles with multiple solutions.

---

## Features

* **Constraint Propagation:** Employs message-passing algorithms to prune the search space before resorting to backtracking.
* **Exhaustive Search:** Capable of identifying and returning all possible valid solutions for a given grid.
* **Rust-Powered:** Leverages Rust's memory safety and speed for rapid execution.
* **Simple Interface:** Clean CLI for processing puzzle files.

---

## Mathematical Foundation

The solver treats Sudoku as a **Constraint Satisfaction Problem (CSP)**. 
Each cell $c_{i,j}$ is a variable with a domain $C \subseteq \{1, 2, \dots, 9\}$. 
The solver iteratively enforces the following constraints:

$$\forall \text{ unit } U, \forall s_1, s_2 \in U : s_1 \neq s_2$$

Where a "unit" $U$ represents any row, column, or $3 \times 3$ block.

---

## Getting Started

### Prerequisites

Ensure you have the Rust toolchain installed. 
If not, you can get it at [rustup.rs](https://rustup.rs/).

### Installation

Clone the repository and navigate into the directory:

```bash
git clone https://github.com/yourusername/sudoku-solver.git
cd sudoku-solver
```

### Usage

The solver reads puzzles from `.txt` files.
The grid should be represented by numbers $1-9$, using `_` for empty cells.

To solve a puzzle, run:

```bash
cargo run -- path/to/your_grid.txt
```

Several example grids are provided in the `examples/` directory to get you started.

---

## Implementation Details

The algorithm follows these primary steps:

1. **Initialization:** Load the grid and assign initial domains to all cells.
2. **Constraint Propagation:** Reduce domains by message-passing over local (row, column, and block) constraints.
3. **Search (if required):** If propagation does not result in a full solution, the solver branches on the cell with the smallest remaining domain to find all valid completions.

