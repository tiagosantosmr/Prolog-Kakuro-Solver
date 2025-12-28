# Kakuro Puzzle Solver (Prolog)

This project is a **Kakuro puzzle solver** implemented in **Prolog**.  
It automatically solves Kakuro puzzles using logical reasoning, list manipulation, and constraint satisfaction principles — without relying on brute force.

<img src="kakuro_puzzle.png" alt="Kakuro Puzzle Example" width="500"/>


## 🧩 Overview

Kakuro is a numeric logic puzzle similar to a crossword, but with numbers.  
Each "across" or "down" entry must add up to a specified sum, using digits **1–9** with no repeats in the same group.

This solver takes a Kakuro puzzle represented as a nested list (matrix) and finds a valid assignment of numbers that satisfies all constraints.

The solver works by:
1. Identifying all **spaces** (groups of cells with a sum constraint).
2. Generating **all valid combinations** of digits that satisfy each sum.
3. Eliminating impossible options through **shared variable reasoning**.
4. Iteratively **simplifying** the possibilities until the puzzle is solved.

---

## ⚙️ How It Works

The solver is divided into modular predicates, each responsible for a distinct part of the solving process.

| Predicate | Description |
|------------|--------------|
| `combinacoes_soma/4` | Generates all combinations of a given length whose sum matches a target value. |
| `permutacoes_soma/4` | Extends combinations to include all their permutations. |
| `constroi_espaco/3` | Constructs an abstract representation (`espaco`) for each Kakuro space. |
| `espacos_puzzle/2` | Extracts all spaces from the puzzle (both horizontal and vertical). |
| `permutacoes_soma_espacos/2` | Computes all valid permutations for every space based on its sum constraint. |
| `permutacoes_possiveis_espacos/2` | Associates each space with the list of its possible value permutations. |
| `atribui_comuns/1` | Assigns values that must be common among overlapping spaces. |
| `retira_impossiveis/2` | Removes permutations incompatible with already known variable values. |
| `simplifica/2` | Applies the two steps above iteratively until stable. |
| `inicializa/2` | Prepares all possible permutations for every puzzle space before solving. |
| `resolve/1` | Top-level predicate — orchestrates the entire solving process. |

---

## 🧠 Solving Algorithm

1. **Initialization**
   - Analyze the puzzle and identify all spaces (sets of variables sharing a sum constraint).

2. **Permutation Generation**
   - For each space, calculate all possible permutations of digits (1–9) that sum correctly.

3. **Constraint Propagation**
   - Simplify through local reasoning: assign shared digits and remove inconsistent permutations.

4. **Backtracking with Heuristics**
   - When stuck, pick the space with the fewest alternatives and test possible solutions recursively.

This approach combines **logical inference** with **heuristic search**, making it both educational and efficient.

---

## 🧾 Puzzle Representation

A Kakuro puzzle is represented as a **matrix of lists**, e.g.:

```prolog
Puzzle = [
    [[*,*],[*,16],[*,24]],
    [[17,*], _, _],
    [[35,*], _, _]
].
```

- `[* , Sum]` indicates a **sum constraint** (horizontal or vertical).
- Variables (`_`) represent **empty cells** to be filled.

---

## 🚀 Running the Solver

1. Make sure you have **SWI-Prolog** installed.
2. Load your solver:

   ```prolog
   ?- [kakuro_solver].
   ```

3. Define a puzzle and call:

   ```prolog
   ?- Puzzle = [...],
      resolve(Puzzle).
   ```

4. The solver will fill in the puzzle with consistent values that satisfy all constraints.

---

## 🧩 Example Usage

```prolog
?- Puzzle = [
       [[*,*],[*,16],[*,24]],
       [[17,*], A, B],
       [[35,*], C, D]
   ],
   resolve(Puzzle).

Puzzle = [
    [[*,*],[*,16],[*,24]],
    [[17,*], 9, 7],
    [[35,*], 8, 9]
].
```

---

## 🧰 Dependencies

- **SWI-Prolog** or a compatible Prolog interpreter.
- A helper file `codigo_comum.pl` must define utility predicates like `combinacao/3`, `mat_transposta/2`, etc.

---

## 📚 Concepts Used

- Constraint satisfaction problem (CSP)
- Logical reasoning and backtracking
- List processing (findall, member, etc.)
- Matching and unification-based filtering

---

## 👨‍💻 Author

**Tiago Santos**  
Student project for logic programming (Prolog-based Kakuro solver).  
Developed as part of the IST course on Programming Paradigms.
