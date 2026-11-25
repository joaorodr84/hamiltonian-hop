# Hamiltonian Hop

A solo research/benchmark project — no CI, no collaborators, no release process. These rules are
adapted from the branching, task-ID and commit discipline used across the other projects, minus
anything tied to versioning or shipping a release (no `CHANGELOG.md`, no version tags).

## Branch before you work

Create the branch before the first edit, not after. The first action is `git checkout -b <name>`
off `main`, so no work lands in the working tree while `HEAD` is on `main`.

- `<name>` is a plain `kebab-case-summary` of the change, prefixed with the task ID:
  `hhop-12-add-ida-star-pruning`.
- Already on a non-`main` branch: stay on it, don't branch off a branch.
- Skip branching for read-only work: answering questions, reading code, running an existing
  benchmark without changing it, investigating a bug without fixing it. Branch the moment an
  investigation becomes a fix.
- Don't ask permission — it's cheap and reversible, and this rule *is* the standing authorization.

There's no commit agent here: commit, merge the branch back into `main` yourself (fast-forward or
a plain merge), and delete the branch.

## Task completion workflow

When completing a task:

1. **Make code changes** and commit them (with the task ID in the subject if applicable).
2. **Do bookkeeping before the summary** — update `TASKS.md` (move the task to Done, add today's
   date) and delete the `TODO.md` entry, in the closing commit.
3. **Merge the branch into `main` and delete it.**
4. **Then provide the summary** — at this point the task is truly finished.

## Task IDs

Every task carries an ID `HHOP-<n>`, registered in [TASKS.md](TASKS.md), which holds the next free
number at the top — take it and increment it in the same commit that uses it.

**Claim the ID when the task is written down, not when it ships.** A new `TODO.md` entry gets one
immediately; the commit that closes it reuses that same ID. One ID per *task*: a feature landed
over two commits repeats the ID in both subjects, and a commit closing two tasks names both —
`(HHOP-11, HHOP-12)`.

- Commit subject: `feat: Add IDA* dead-end pruning (HHOP-12)` — ID in parentheses at the end of
  the description, inside the subject line so a recovery grep keeps working. The format around it
  is Conventional Commits (see **Commit messages**).
- Branch name: `hhop-12-add-ida-star-pruning`.
- Not every commit needs one. Bookkeeping — a typo fix, a formatting pass, a `TODO.md` tidy — goes
  in unnumbered rather than inflating the counter.
- Never renumber, never reuse, and never rewrite an ID into an existing commit message. History is
  immutable; `TASKS.md` holds the mapping precisely so no rewrite is ever needed.

**When a task ships, its closing commit does the bookkeeping too — in that same commit, not a
follow-up.** Move the task's row from the Open table to the Done table in `TASKS.md` (status
`done`, today's date, Commit column `—`) and delete its `TODO.md` entry.

If `TASKS.md` and history disagree, history wins:

```sh
git log --oneline | grep -oE 'HHOP-[0-9]+' | sort -t- -k2 -n | tail -1
```

## Commit messages

Hamiltonian Hop follows [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/):

```text
<type>[optional scope][!]: <description> (HHOP-<n>)

[body]

[footers]
```

- **Type** is required and lowercase. `feat` (a new capability) and `fix` (a bug) are the two the
  spec defines — reach for them first. Also in use: `docs`, `refactor`, `perf`, `test`, `chore`,
  for changes that genuinely ship no behaviour.
- **Scope** is optional and names the area of the code, never the task: `feat(search):`,
  `fix(grid):`. Leave it off when the change is broad.
- **Description**: plain-language imperative summary, capitalised, no trailing full stop.
- **Task ID** goes last, in parentheses.
- **Body stays substantial** for anything non-trivial: what was wrong or missing, why this
  approach, what was decided and rejected, how it was verified.
- **Breaking changes** take a `!` before the colon *and* a `BREAKING CHANGE:` footer saying what
  changes for anyone building on this code.
- **Footers** are `Token: value` with hyphenated tokens; `BREAKING CHANGE` keeps its space.
  `Co-Authored-By:` is a footer like any other.

Worked examples:

```text
feat(search): Add IDA* dead-end pruning (HHOP-12)

fix(grid): Correct teleport-cell adjacency check (HHOP-13)

docs: Break the TODO into per-task entries
```

The last carries no ID on purpose — pure bookkeeping doesn't need one.
