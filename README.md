# blackjack-basic-strategy-simulation
# Blackjack Basic Strategy Simulation

Monte Carlo simulation of blackjack under real table conditions (8-deck shoe, 4-deck penetration), with a full basic-strategy decision engine including pair splitting, calculating house edge against the known theoretical benchmark.

## Problem Statement

Unlike roulette (single random draw) or baccarat (fixed drawing rules), blackjack's house edge depends on the player's strategy. A player using optimal "basic strategy" faces a house edge of roughly 0.5–0.6% — one of the fairest games on a casino floor. This project implements a full basic-strategy engine (hit/stand/double/split), simulates 100,000 hands under real table conditions, and confirms the simulated edge matches the theoretical benchmark.

## How to Run

1. Open [Google Colab](https://colab.research.google.com)
2. Upload `blackjack_simulation.ipynb` (or copy the cells from this repo)
3. Run all cells top to bottom (Runtime → Run all)

## Rules Modeled

8-deck shoe, cut card placed after 4 decks are dealt (real table conditions), dealer stands on soft 17, blackjack pays 3:2, double down on any first two cards, one split per pair (no resplitting), split Aces get exactly one card each with no further hits, no doubling after split.

## Results (100,000 hands)

| Metric | Count | % of bets |
|---|---|---|
| Hands dealt | 100,000 | — |
| Total bets resolved (incl. splits) | 102,512 | — |
| Wins | 44,564 | 43.4720% |
| Losses | 49,061 | 47.8588% |
| Pushes | 8,887 | 8.6692% |

| Metric | Value |
|---|---|
| Actual house edge (simulated) | 0.5575% |
| Theoretical basic-strategy edge (8-deck, stand-soft-17) | ~0.5% – 0.6% |

The simulated house edge lands directly inside the theoretical range on the first fully-validated run. The 102,512 resolved bets vs. 100,000 hands dealt (~2,512 extra bets) confirms pair-splitting is actively triggering, not silently skipped — an important sanity check, since a disabled split could still produce a plausible-looking but incorrect edge.

## Why the Theoretical Value Is a Cited Benchmark, Not a Hand Calculation

Roulette's edge comes from a simple formula. Baccarat's comes from exhaustive combinatorial analysis of a fixed rule table. Blackjack's basic-strategy edge is too combinatorially complex for either approach — it comes from computer analysis of the exact rule set, published by gaming-mathematics sources (e.g., Wizard of Odds). The ~0.5–0.6% figure used here is cited from those sources, not derived independently.

## Tools

Python, NumPy, Pandas — built and run in Google Colab (no local install required).
