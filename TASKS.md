# Hamiltonian Hop task ledger

Every task carries an ID of the form `HHOP-<n>`. IDs are assigned once, never reused, and never
renumbered.

**Next ID to assign: `HHOP-2`**

If this file and history ever disagree, history wins:

```sh
git log --oneline | grep -oE 'HHOP-[0-9]+' | sort -t- -k2 -n | tail -1
```

## How IDs work

- **An ID is claimed when a task is written down, not when it ships.** A new `TODO.md` entry gets
  its ID immediately; the commit that closes it reuses that same ID.
- **One ID per task, not per commit.** A feature landed over two commits carries the same ID in
  both subjects. A commit closing two tasks names both.
- Commit subject: `feat(search): Add IDA* dead-end pruning (HHOP-12)` — Conventional Commits, with
  the ID in parentheses at the end. See **Commit messages** in `CLAUDE.md`.
- Branch name: `hhop-12-add-ida-star-pruning`.

## Open

| ID | Task | Status | Commit |
| --- | --- | --- | --- |

## Done

| ID | Task | Status | Date | Commit |
| --- | --- | --- | --- | --- |
| HHOP-1 | Imported Cangupa's full level/solution set as this project's benchmark instances: `tools/packs.json` and `tools/solutions.json`, copied as-is from Cangupa commit `844008e` into `data/cangupa/`, with a new `data/cangupa/README.md` documenting both files' formats (the `rows` character legend, the difficulty-metadata fields, and the move-letter solution encoding) and noting it's a point-in-time snapshot, not a live link. 1000 levels across 20 packs, 3×3 up to 8×7, each with exactly one stored solution in matching pack/level order across both files. Owner-requested directly, not from the backlog | done | 2026-11-25 | — |
