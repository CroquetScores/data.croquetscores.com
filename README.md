# Croquet Scores data

The tournaments of [Croquet Scores](https://croquetscores.com) and
[Gateball Scores](https://gateballscores.com), one JSON file for each, so that
anybody can read the results, or build something from them, without asking
the websites for them.

This repository is written by a script and not by hand. Each run writes the
tournaments that are public now, takes away the files of those that no longer
are, and commits and pushes what changed. A correction to a tournament shows
here as a change with a date on it.

## Where a file is

A tournament is a file named by its address on its website:

```
2026/ac/spring-open.json
```

is the page `/2026/ac/spring-open`. The year is the year it starts in, and the
middle part is its sport. Both websites are here together, and the sport tells
them apart.

| Code  | Sport               | Website            |
| ----- | ------------------- | ------------------ |
| `ac`  | Association Croquet | croquetscores.com  |
| `gc`  | Golf Croquet        | croquetscores.com  |
| `a6w` | American 6 Wicket   | croquetscores.com  |
| `rc`  | Ricochet            | croquetscores.com  |
| `gb`  | Gateball            | gateballscores.com |

## What a file says

Every file is JSON, laid out the same way each run with the same things in the
same order, so a file changes only when what it says has changed. It has
`layout`, which is the version of this layout and is `1` now. A reader is told
when the layout changes by that number going up.

A file says the tournament's `name`, `sport`, `firstDay` and `lastDay`,
`country` and `region` (which is `null` where it has none).

A tournament played by players has:

- `players`: each by `name`, and `representing`, or `null` where they represent
  nothing.
- `competitions`: each with its `name`, its `kind` (`block`, `knockout` or
  `swiss`) and its games. A knockout has `matches` in place of `games`, each
  being the two players who met and the games between them in the order they
  were played.

A tournament played by teams has:

- `teams`: each by `name` and `shortName`, and the `players` it has.
- `tests`: each with the two `teams` that met, the first team's first, its
  `group` (or `null`), what each match is the `bestOf`, and the `matches`
  played: the first team's player and the second team's, with their games.

A game says the two players and what each scored, as it was typed (so `26tp`
is possible), whether it was `drawn`, and whether it was `withdrawn`. A
withdrawn game was played but counts for nothing, and is kept so that it is
not lost; do not count it.

## What is not here

- Nobody's account: not who manages a tournament, not who added a player or a
  game, and no email address.
- A tournament's notes and its commentary.
- A tournament, a competition or a player that is archived, as the websites
  leave them out too.
- How the teams stand, or how the players in a block are placed. These are
  worked out from the games by whoever reads them.
- Flags.
- Anything from a try website.

## Licence

[CC0 1.0 Universal](LICENSE). To the extent possible under law, the data in
this repository is dedicated to the public domain: use it for anything, with
no need to ask or to give credit.
