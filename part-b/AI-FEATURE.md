# AI Feature Specification: Ticket Confirmation Predictor

## Problem It Solves
Addresses Problem 2 & 5 — uncertainty in booking success.

## Proposed Feature
Shows probability of ticket confirmation before booking.

Example:
"Chance of confirmation: 82% (High)"

## Model Choice
XGBoost classifier (better for structured tabular data)

## Training Data
- Historical booking data
- WL movement trends
- Train occupancy

## Output UI
Displayed on train search results:
"✔ High chance of confirmation"

## Confidence Threshold
- >70% → show prediction
- <70% → show "uncertain"

Fallback:
Hide prediction if unavailable

## Success Metrics
- Increase booking confidence
- Reduce abandoned sessions

## Risks
- Wrong predictions may mislead users
