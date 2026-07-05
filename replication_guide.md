# Trial by Fire protocol

V6 freezes the candidate set from V5 and avoids adding new strategy variants. It then applies a stricter battery of tests:

1. multi-cost robustness;
2. fixed-cost breakeven curve;
3. yield-curve PC exposure diagnostics;
4. circular-shift placebo tests;
5. moving-block bootstrap checks;
6. stress-window and subperiod performance;
7. leg stability and turnover diagnostics;
8. final classification as reject, dynamic-cost candidate, repo candidate, or robust repo candidate.

The final result is repo candidate, not robust repo candidate:

- passes CS, AR, and Fixed5;
- fails Fixed10;
- fails stressed AR multipliers;
- remains close to duration-neutral and 10Y-beta-neutral.
