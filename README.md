# Vision Zero: Evaluating NYC Traffic Calming Interventions

A causal evaluation of whether NYC's Vision Zero traffic-calming treatments actually reduce injuries and deaths from traffic collisions — built as a capstone project for a Data-Driven Policy course (EMSE 6577).

## Research Question

Do Vision Zero traffic-calming treatments reduce the monthly number of persons killed or injured due to traffic collisions in NYC?

## Why This Matters

NYC has committed $3.2B to Vision Zero infrastructure investment from 2020–2029, with the largest spending surge still ahead (2025–2029). Despite this investment, the city lacks a rigorous causal evaluation of which interventions actually work — most existing evidence is correlational (e.g., citywide fatality trends before/after Vision Zero's 2014 launch), which cannot separate the effect of specific treatments from broader downward trends already in motion.

## Approach

1. **Data integration** — merged 1,508 traffic-calming intervention records (NYC DOT) with 487,000+ motor vehicle collision records (NYPD), filtering to collisions with injuries/fatalities and matching them to nearby intersections (within 25m)
2. **Matched control design** — matched 431 treated intersections to 431 untreated control intersections based on pre-treatment collision history and geographic similarity, yielding 83,614 observations across an 8-year window (4 years pre/post treatment)
3. **Difference-in-Differences (DiD)** — used Zero-Inflated Negative Binomial regression (appropriate given many zero-collision months) to estimate the treatment effect
4. **Parallel trends testing** — checked the core DiD assumption and found it violated: treatment locations were already on a steep downward injury trend *before* interventions began, while control locations stayed flat
5. **Trend-adjusted re-analysis (CITS)** — applied a Comparative Interrupted Time Series model to account for each site's pre-existing trajectory rather than assuming parallel trends

## Findings

| Stage | Result |
|---|---|
| Naive DiD estimate | Statistically significant 14% reduction in injuries/fatalities (p = 0.0014) |
| Parallel trends check | **Violated** — treatment sites already declining (~0.35 → ~0.25 injuries/month) pre-intervention |
| Trend-adjusted (CITS) estimate | No detectable beneficial effect once pre-existing trends are accounted for |

**This does not prove the treatments are ineffective.** It demonstrates that standard before/after or naive DiD methods cannot reliably isolate the causal effect of these interventions when treatment sites are already improving for other reasons — and that NYC currently lacks the causal evaluation infrastructure needed to know which of its $3.2B in investments are actually working.

## Proposed Deliverables (Policy Pitch)

The project concluded with a pitch for what a proper causal evaluation platform would provide: per-treatment causal effect estimates, an ROI ranking across intervention types (speed humps vs. raised crosswalks vs. curb extensions), a public-facing dashboard, and a policy report for funders and city agencies.

## Data Sources

- **NYC DOT** — Turn Traffic Calming intervention dataset (1,508 records, 2016–2025)
- **NYPD** — Motor Vehicle Collision records (487,000+ records, 2012–2025)

## Tech Stack

Python · Pandas · GeoPandas · Statsmodels (ZINB regression) · Folium (interactive mapping) · Matplotlib

## Repository Structure

```
├── notebooks/
│   └── traffic_calming_causal_analysis.ipynb   # Full DiD + CITS analysis pipeline
├── presentation.pdf                             # Final course presentation
└── README.md
```

*Data sourced from NYC Open Data (DOT traffic calming records, NYPD collision records). Not included in this repo due to size — available directly from NYC Open Data.*

## Team

Built as a team capstone project for a graduate Data-Driven Policy course at GWU.
