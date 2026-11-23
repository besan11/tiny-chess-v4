# Tiny Chess v4 — book-first 4KB chess engine

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/competitions/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/besan11/tiny-chess-v4/rank.svg)](https://make.fun/competitions/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/besan11/tiny-chess-v4/reward.svg)](https://make.fun/competitions/tiny-chess-01)

An entry for make.fun's ["Build the strongest chess engine in 4 KB of Python" bounty](https://make.fun/competitions/tiny-chess-01) ($500 in USDC).

Referral code: `jpgk45b3` — https://make.fun/r/jpgk45b3

## What it is

`main.py` (at most 4,096 bytes) is the whole engine: a Python chess engine that
talks to the house env over HTTP and plays the 8-game gauntlet.

Design (v4): an opponent-agnostic opening book — precomputed Stockfish winning
lines for every opening in the kit's 40-line book, in both colours — packed as
one-character move indices, plus the strongest search that still fits in the
byte budget: 0x88 board, tapered piece-square tables, PVS + null-move pruning,
quiescence with delta pruning, transposition table, killer moves, fixed node
budget (fully deterministic, no clock in the search).

## How it works

- The book covers the opening phase: from each of the 40 kit openings, the
  engine replays a Stockfish line (generated against the strongest house rung)
  for as long as the opponent's replies match, then falls back to search.
- The search is iterative-deepening PVS to a fixed node budget, so every move
  is reproducible and well inside the 10-second move limit.

## Limits

- `main.py` <= 4,096 bytes; whole repo snapshot <= 8,192 bytes.
- Deterministic: no wall clock in the search, no unseeded randomness.
- Python 3.13, standard library only.
