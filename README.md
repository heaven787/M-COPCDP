# HEA for COPCDP

C++ implementation of the hybrid evolutionary algorithm (HEA) for the **Categorized Orienteering Problem with Count-Dependent Profits (COPCDP)**.

Corresponding paper: *A Hybrid Evolutionary Algorithm for the Categorized Orienteering Problem with Count-Dependent Profits*.

## Requirements

- C++17 compiler (`g++` recommended)
- GNU Make (`make` / `mingw32-make`)

## Build

**Linux / macOS**

```bash
make
```

**Windows (MinGW)**

```powershell
mingw32-make
```

The executable is `cop_hea` (or `cop_hea.exe` on Windows).

Clean build artifacts:

```bash
make clean
```

## Run

```bash
./cop_hea <instance.COPCDP> [seed] [--key=value ...]
```

Examples:

```bash
./cop_hea path/to/21_2_32.COPCDP 123
./cop_hea path/to/80_10_230.COPCDP 1 --pop=10 --L=80
```

- `seed` — random seed (default: `123`)
- Instance files use the `.COPCDP` format from Jandaghi et al. (2021)

### Output

One line on success:

```text
RESULT objective=... distance=... cpu=... seed=... route=1,3,5,...,2
```

- `objective` — route profit \(f(S)\)
- `distance` — total travel time
- `cpu` — wall-clock seconds
- `route` — visit sequence (origin `1`, destination `2`)

## Default parameters

| Parameter | Flag | Default | Paper (Table 2) |
|-----------|------|---------|-----------------|
| Population size | `--pop` | 10 | POP_SIZE |
| Elite count | `--elite` | 3 | ELITE_COUNT |
| Max generations | `--gen` | 10 | MAX_GEN |
| Stagnation limit | `--stagnation` | 5 | STAGNATION_LIM |
| Jaccard similarity trigger | `--sim` | 0.8 | SIM_THRESHOLD |
| Shaking ratio | `--shake` | 0.6 | SHAKING_PERCENT |
| Tabu depth | `--L` | 80 | L |
| 3-OPT frequency | `--uc` | 5 | uc |
| Penalty update frequency | `--up` | 5 | up |
| Tabu tenure factor | `--beta` | 0.1 | β |

## Source files

| File | Role |
|------|------|
| `main.cpp` | Entry point, CLI parsing, timing |
| `HeaConfig.cpp/h` | Algorithm parameters |
| `Popmanage.cpp/h` | Genetic loop, population update, shaking |
| `crossover.cpp/h` | LCS backbone crossover |
| `LocalSearch.cpp/h` | Tabu search (ADD/DROP/SWAP, 3-OPT, penalty) |
| `initial.cpp/h` | Randomized greedy initialization |
| `individual.cpp/h` | Route encoding and evaluation |
| `readdata.cpp/h` | Instance reader |
| `mo.cpp/h` | Move / neighborhood helpers |

## Instance data

Benchmark instances are **not** included in this folder. They can be obtained from Jandaghi et al. (2021) or the project data repository cited in the manuscript.

## Contact

Linghui Meng — menglinghui77@outlook.com
