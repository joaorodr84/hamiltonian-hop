# Hamiltonian Hop task ledger

Every task carries an ID of the form `HHOP-<n>`. IDs are assigned once, never reused, and never
renumbered.

**Next ID to assign: `HHOP-1`**

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
