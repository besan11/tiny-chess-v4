# Tiny Chess v4 — engine-only 4KB chess engine

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/competitions/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/besan11/tiny-chess-v4/rank.svg)](https://make.fun/competitions/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/besan11/tiny-chess-v4/reward.svg)](https://make.fun/competitions/tiny-chess-01)

An entry for make.fun's ["Build the strongest chess engine in 4 KB of Python" bounty](https://make.fun/competitions/tiny-chess-01) ($500 in USDC).

Referral code: `jpgk45b3` — https://make.fun/r/jpgk45b3

## What it is

`main.py` (at most 4,096 bytes) is the whole engine: a Python chess engine that
talks to the house env over HTTP and plays the 8-game gauntlet.

Design (v4): ENGINE-ONLY — no opening book. The search is the whole engine:
a 0x88 board, tapered piece-square tables computed from formulas, PVS +
null-move pruning + LMR, quiescence with delta pruning, transposition table,
killer moves, and a fixed node budget of 50,000 nodes per move (fully
deterministic, no clock in the search). Book experiments showed a book hurts
this engine, so the bytes go to search strength instead.

## Run it

    python3 -P -s main.py

It reads `MAKEFUN_ENV_URL` from the environment, plays the trial's games
through the env, and exits when every game is over.

## Limits

- `main.py` <= 4,096 bytes; whole repo snapshot <= 8,192 bytes.
- Deterministic: no wall clock in the search, no unseeded randomness
  (only a seeded RNG for Zobrist keys).
- Python 3.13, standard library only.
