# Patagonia: Attribution Models vs. Experiment

**Author:** Duy Nguyen | **Published:** April 2026

**Dataset:** Controlled Experiment Campaign

---

## Overview

This project analyzes Patagonia's digital marketing data to evaluate whether naive attribution models (last-touch, first-touch, linear) produce reliable signals for marketing budget allocation — or whether experimentally-derived incremental impact is necessary for sound decision-making.

Patagonia ran a 3-week holdout experiment across five marketing channels with 2 million customers randomly selected from its CRM. This project uses that experimental data to measure true incremental lift and compare it against what naive attribution would have suggested.

---

## Research Questions

1. **Attribution Without Incrementality** — What do last-touch, first-touch, and linear models say about each channel's contribution?
2. **Estimating Incremental Sales** — What is the true Intent-to-Treat (ITT) effect per channel? How does it compare to naive attribution?
3. **Regression-Based Estimation** — Does regression with control variables improve on simple ITT comparisons?
4. **ROI of Marketing Channels** — How does ROI change when calculated using incremental vs. naive attribution?
5. **Was Simple Good Enough?** — Do naive models align with incremental findings? What are the risks of relying on them?

---

## Dataset

- **Source:** Patagonia CRM experiment, Fall 2024 – Early 2025
- **Full dataset:** 2,000,000 customers, 22 variables
- **Local dataset (`data/patagonia.csv`):** Full 2,000,000 rows — gitignored, must be added locally

**Channels studied:**
- Email
- YouTube (30-second video ads)
- Instagram (in-stream video ads)
- Google Search
- Contextual Display (Backpacker.com, GearJunkie.com, National Geographic, Treehugger.com)

**Experimental design:** 20% holdout rate per channel, independent random assignment at the customer level (except Google Search, which used geo-targeting due to platform constraints).

---

## Key Findings

Naive attribution models — last-touch, first-touch, and linear — significantly overstate the effectiveness of marketing channels by attributing all observed sales to advertising, including purchases that would have occurred organically. The experimental holdout design reveals that only $385K of the $1.48M claimed by last-touch attribution was truly incremental — a **3.8× overstatement**. The remaining $1.09M represents organic sales that would have occurred without any of the five channels.

The experiment provides a more accurate basis for evaluating channel performance because it isolates **incremental impact**: the additional sales generated specifically because a customer was exposed to a channel. By comparing treatment and holdout groups, we can estimate what would have happened in the absence of marketing — a counterfactual that no attribution model can construct.

Key contrasts between the two approaches:

- **Contextual Display — most misleading:** Ranked #1 under last-touch attribution (1,197% ROI) but ranks #4 under incremental measurement with a **negative ROI of -34%**. Its ITT effect is not statistically significant. Its high naive ranking is driven entirely by impression volume, not causal impact.
- **Email — most understated:** Ranked #4 under last-touch (51% ROI) but is the **best-performing channel incrementally (63% ROI)**. Attribution undervalues it because it rarely appears as the last touchpoint before conversion.
- **Instagram — overstated:** Ranked #2 naive (541% ROI) but #3 incremental (45% ROI). Positive returns, but attribution greatly inflates its perceived value.
- **Google Search — negative under both:** The only channel where both methods agree on direction, but incremental measurement reveals a worse picture (-94% ROI) than last-touch suggests (-60% ROI), driven by its high cost-per-click.

These findings demonstrate that experiment-based incremental measurement is essential for sound marketing budget allocation. The naive ranking is largely inverted relative to the true incremental picture — the channel that appears best destroys value, while the channel that appears worst generates the highest returns.

---

## Repository Structure

```
├── data/
│   └── patagonia.csv       # Full dataset — gitignored, must be added locally
├── patagonia_attribution.ipynb  # Main analysis notebook (executed)
├── requirements.txt
├── .gitignore
└── README.md
```

---

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/duydnguyenn/Patagonia_Attribution-Models-vs-Experiment.git
   cd Patagonia_Attribution-Models-vs-Experiment
   ```

2. Add the dataset: place `patagonia.csv` in the `data/` folder (not tracked by git).

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Launch the notebook:
   ```bash
   jupyter notebook patagonia_attribution.ipynb
   ```
