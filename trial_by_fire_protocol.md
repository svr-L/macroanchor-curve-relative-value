# Methodology

This repository tests whether macro-anchored term-premium residuals contain a duration-neutral curve relative-value component.

## Signal construction

The parent MacroAnchor project produces model-implied term-premium signals by tenor. The RV notebooks transform these tenor signals into cross-sectional residuals across maturity.

The strongest family uses quadratic maturity residuals: remove broad maturity structure and focus on residual richness/cheapness along the curve.

## Portfolio construction

The headline candidate is a quarterly-smoothed DV01-neutral projection strategy:

1. construct residual term-premium scores across tenors;
2. project scores into a DV01-neutral portfolio;
3. smooth/rebalance quarterly to reduce turnover;
4. lag weights and transaction-cost estimates;
5. test across multiple cost assumptions.

A butterfly construction is kept as a challenger, but it is not the headline because it fails the fixed 5bp gate in V6.

## Pure-RV criteria

The strategy is evaluated as RV only if it has:

- near-zero duration exposure;
- near-zero 10Y beta;
- low R² versus 10Y returns;
- low exposure to the first yield-curve PCs;
- positive net return after realistic costs;
- reasonable turnover.
