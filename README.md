# MacroAnchor Curve Relative Value

Duration-neutral curve relative-value candidates from macro-anchored term-premium residuals.

This repository is an advanced spin-off of the parent `macro-anchored-bond-risk-premia` project. The parent project studies macro-anchored bond-risk-premium predictability. The sparse allocation spin-off studies non-neutral tenor allocation. This repository asks the stricter relative-value question:

> After neutralizing duration and curve-level exposure, do macro-anchored term-premium residuals contain a small but persistent curve-RV component?

The current answer is **yes as a cautious repository candidate**, not as a high-return trading system. The strongest candidate is a quarterly-smoothed, DV01-neutral projection strategy based on quadratic maturity residuals. It survives Corwin-Schultz, Abdi-Ranaldo, and fixed 5bp one-way transaction-cost assumptions, but fails conservative fixed 10bp and stressed-cost assumptions.

## Core result

| Strategy family | Cost model | Ann. return | Sharpe | NW t-stat | Turnover | 10Y beta/R² | Verdict |
|---|---:|---:|---:|---:|---:|---:|---|
| Quadratic residual projection, DV01-neutral, quarterly smooth | CS lagged | 0.07% | 0.65 | 2.83 | 0.74x | near zero / <0.01 | pass |
| Quadratic residual projection, DV01-neutral, quarterly smooth | AR lagged | 0.03% | 0.31 | 1.64 | 0.74x | near zero / <0.01 | pass |
| Quadratic residual projection, DV01-neutral, quarterly smooth | Fixed 5bp | 0.03% | 0.31 | 1.63 | 0.74x | near zero / <0.01 | pass |
| Quadratic residual projection, DV01-neutral, quarterly smooth | Fixed 10bp | -0.01% | -0.06 | fail | 0.74x | near zero / <0.01 | fail |
| Quadratic residual butterfly, quarterly smooth | CS lagged | 0.10% | 0.71 | 3.19 | about 1.3x | near zero / <0.01 | dynamic-cost candidate |

This is a **low-risk, low-return residual RV sleeve**. The value of the result is not high unlevered return; it is the isolation of a duration-neutral, low-beta curve residual that survives several realistic cost assumptions.

## Trial by fire summary

The V6 notebook is intentionally restrictive:

- no new strategy fishing;
- candidate set frozen from V5;
- multiple transaction-cost models;
- fixed-cost breakeven curve;
- exposure to yield-curve PCs;
- circular-shift placebo tests;
- moving-block bootstrap;
- stress-window and subperiod diagnostics;
- leg stability and turnover diagnostics.

Final V6 classification:

| Strategy | CS | AR | Fixed5 | Fixed10 | AR 2x | Stress AR 3x | Classification |
|---|---:|---:|---:|---:|---:|---:|---|
| Quadratic residual projection, DV01-neutral, quarterly smooth | pass | pass | pass | fail | fail | fail | repo candidate |
| Quadratic residual projection, net + DV01-neutral, quarterly smooth | pass | pass | pass | fail | fail | fail | repo candidate |
| Quadratic residual butterfly, quarterly smooth | pass | pass | fail | fail | fail | fail | dynamic-cost candidate |

## What this is, and what it is not

This repository is:

- a strict test of pure curve relative value;
- a residualized term-premium strategy with duration and 10Y beta controls;
- a low-volatility RV sleeve candidate;
- a proof that at least one residualized macro-anchor signal survives CS, AR and fixed 5bp cost assumptions.

It is not:

- a high-return standalone trading strategy;
- a claim of robustness to conservative fixed 10bp costs;
- a production implementation;
- a substitute for futures/bond-level executable bid-ask data.

## Repository structure

```text
macroanchor-curve-relative-value/
├── README.md
├── requirements.txt
├── environment.yml
├── LICENSE
├── CITATION.cff
├── notebooks/
│   ├── 01_pure_curve_rv_trial_by_fire_v6_executed.ipynb
│   └── archive/
│       ├── 00_v4_pure_rv_search_executed.ipynb
│       └── 00_v5_pure_rv_robustness_and_scaling_executed.ipynb
├── docs/
│   ├── methodology.md
│   ├── transaction_costs.md
│   ├── trial_by_fire_protocol.md
│   ├── interpretation_and_claims.md
│   ├── replication_guide.md
│   └── roadmap.md
├── outputs/
│   ├── tables/
│   └── figures/
├── data/
│   └── README.md
└── src/
    └── README.md
```

## Headline figure

![Curve RV cost robustness](outputs/figures/curve_rv_cost_robustness.png)

## Naming note

`Trial by Fire` is the intended idiom: a severe test or baptism by fire. Earlier internal wording such as `proof of fire` was not idiomatic and should not be used.

## License

MIT License. See `LICENSE`.

## Disclaimer

This repository is for research and educational purposes only. It is not investment advice, not a production trading system, and not a recommendation to trade any instrument.
