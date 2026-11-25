# hamiltonian-hop

A single-agent grid-clearing puzzle, studied as a search problem.

## The puzzle

A token sits on a grid and moves by **stepping** (distance 1) or **jumping** (distance 2) along
rows and columns. It must visit every tile the number of times that tile requires: most tiles need
just one visit, but some need two or three. Some tiles restrict which direction they can be
entered or left, and some teleport the token to a paired cell elsewhere on the grid.

Ignore the multi-visit tiles and this is a **Hamiltonian path problem**. With them, it becomes a
**capacitated generalization** — one that, via vertex splitting, still reduces to an ordinary
Hamiltonian path, just over a graph with directed edges (from the entry/exit restrictions) and
teleport edges (from the paired cells) layered on top.

## What's here

This repo implements and benchmarks search strategies against that problem:

- **Plain depth-first search** — the baseline.
- **Dead-end pruning via reachability analysis** — cutting branches early by checking whether the
  remaining tiles can still all be reached/visited as required.
- **Heuristic search (A*/IDA*)** — admissible heuristics guiding the search instead of exhaustive
  backtracking.

Each strategy is run against the same benchmark instances and compared on where it succeeds, where
it fails, and where it runs out of memory.

## Benchmarks

Real instances come from Cangupa's own generated levels, rather than synthetic or hand-built
grids.

## Status

Open and completed work is tracked in [TASKS.md](TASKS.md); the active backlog is in
[TODO.md](TODO.md).
