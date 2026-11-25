# Cangupa benchmark instances

A snapshot of every level and its stored solution from
[Cangupa](https://github.com/joaorodr84/cangupa) — the mobile puzzle game
this project's problem is drawn from. Copied as-is from that repo's
`tools/packs.json` and `tools/solutions.json` at commit `844008e`
(2026-11-25).

1000 levels across 20 packs (two 10-pack collections, "Lay of the Land" and
"Down Under"), board sizes from 3×3 up to 8×7. Every level has exactly one
stored solution, in the same pack/level order in both files — index `i` of
pack `p` in `packs.json` is the same level as index `i` of pack `p` in
`solutions.json`.

This is a point-in-time copy, not a live link: Cangupa's own levels can
change (new packs, rebuilt content) independently of this repo. Re-copy
both files from Cangupa's `tools/` directory, noting the new commit above,
if a refreshed benchmark set is ever needed.

## `packs.json`

```jsonc
{
  "seed": 1000,
  "collections": [{ "name": "Lay of the Land", "packCount": 10 }, ...],
  "packs": [
    {
      "name": "Meadow",
      "blurb": "...",
      "width": 3, "height": 3,
      "levels": [
        {
          "rows": [".11", "1.1", "1S."],
          "full": true, "mix": 0, "pathBits": 1, "decisions": 1,
          "effort": 5, "bits": 0, "solutions": 2, "visits": 6
        },
        ...
      ]
    },
    ...
  ]
}
```

- **`rows`** is the level grid itself, one string per row, read top-to-bottom
  and left-to-right within each row. The character legend is in Cangupa's
  own [docs/rules.md](https://github.com/joaorodr84/cangupa/blob/main/docs/rules.md):
  `.` empty, `1`/`2`/`3` a tile needing that many visits, `S`/`s`/`T` the
  start tile on a 1-/2-/3-visit tile, `>`/`<`/`v`/`^` a Departure tile
  (one-way to leave) pointing right/left/down/up, `R`/`L`/`D`/`U` an Arrival
  tile (one-way to enter) by that direction, `#` a Pillar, `m` a Mud tile,
  and a repeated letter (`a`/`b`) a Tunnel pair's two mouths.
- The other fields are difficulty metadata from Cangupa's own level
  generator (`tools/difficulty.js`) — not needed to reproduce or verify a
  solution, but potentially useful as independent, pre-computed difficulty
  signals when comparing against this project's own search-effort
  measurements. `solutions` is the number of distinct shortest solutions
  the generator's own search found (separate from — and not necessarily
  equal to — the single stored solution path in `solutions.json` below).

## `solutions.json`

```jsonc
{
  "packs": [
    { "name": "Meadow", "solutions": ["luRul", "rdrdL", ...] },
    ...
  ]
}
```

One string per level: a letter per move, read left to right in play order.
Lowercase is a step, uppercase the equivalent jump, in `r`/`l`/`d`/`u` =
right/left/down/up. A Tunnel move is encoded as the direction actually
moved into the mouth that was entered — the warp to its twin is implicit,
not a separate letter.
