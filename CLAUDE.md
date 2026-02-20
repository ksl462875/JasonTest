# CLAUDE.md

This file provides guidance to AI assistants working in this repository.

## Repository Overview

This is a minimal C++ repository containing a single source file used for testing and educational purposes. It demonstrates a bubble sort algorithm implementation with intentional bugs for debugging exercises.

## Repository Structure

```
JasonTest/
├── CLAUDE.md   # This file
└── testA       # C++ source file with bubble sort implementation
```

## Source File: `testA`

A C++ program (~28 lines) that implements a deliberately buggy bubble sort. The function is named `bubbleSort_BUGGY` to signal that it contains known defects.

### Known Bugs

1. **Out-of-bounds access (line 11):** The inner loop condition `j <= n - i` should be `j < n - i`. The current condition allows `j+1` to reach index `n`, which is one past the last valid element, causing undefined behavior (out-of-bounds array access).

2. **Infinite loop risk (line 10):** The outer loop `for (size_t i = n - 1; i >= 0; --i)` iterates over a `size_t` (unsigned integer). When `i` reaches `0` and is decremented, it wraps around to a very large number (unsigned underflow) rather than going negative, causing an infinite loop. The loop condition `i >= 0` is always true for unsigned types.

3. **`swapped` flag reset (line 8):** The `swapped` flag is initialized before the outer loop but never reset to `false` at the start of each outer iteration. Once a swap occurs, `swapped` stays `true` forever, so the early-exit optimization (`if (!swapped) break`) never fires.

### Code Conventions

- Uses `#include <iostream>`, `<vector>`, `<algorithm>` from the C++ standard library
- Uses `using namespace std;` (namespace pollution — avoid in production code)
- Uses `size_t` for index variables
- Uses STL `swap()` for element swapping
- C++11 or later: uniform initialization syntax (`vector<int> v{5, 4, 3, 2, 1}`)
- `main()` returns `0` explicitly

## Build Instructions

There is no build system configured. Compile manually with a C++ compiler:

```bash
# GCC
g++ -std=c++11 -Wall -Wextra -o testA testA

# Clang
clang++ -std=c++11 -Wall -Wextra -o testA testA
```

Run the compiled binary:

```bash
./testA
```

## Testing

There is no test framework configured. All testing is currently manual — compile and run the binary to observe output.

## Development Workflow

1. Edit `testA` directly (no build system required).
2. Compile with `g++` or `clang++` as shown above.
3. Run the binary and verify output.
4. Commit changes with descriptive messages.
5. Push to the active feature branch.

## Git Branches

| Branch | Purpose |
|---|---|
| `master` | Main branch |
| `claude/add-claude-documentation-YZHrj` | Active development branch |
| `origin/test` | Remote test branch |

Always develop on the designated feature branch and push there — never directly to `master` without explicit instruction.

## Notes for AI Assistants

- The repository is intentionally minimal — do not assume missing files are an oversight unless the user asks for them.
- When asked to fix `testA`, address all three bugs listed above unless told otherwise.
- There is no linter, formatter, or CI pipeline — do not reference or invoke tools that are not present.
- Prefer editing the existing `testA` file over creating new files unless explicitly requested.
