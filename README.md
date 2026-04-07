# Patagonia: Attribution Models vs. Experiment

**Author:** duydnguyenn

## Overview

This project analyzes Patagonia's digital marketing data to evaluate whether naive attribution models (last-touch, first-touch, linear) produce reliable signals for marketing budget allocation — or whether experimentally-derived incremental impact is necessary for sound decision-making.

Patagonia ran a 3-week holdout experiment across five marketing channels with 2 million customers randomly selected from its CRM. This project uses that experimental data to measure true incremental lift and compare it against what naive attribution would have suggested.

## Research Questions

1. **Attribution Without Incrementality** — What do last-touch, first-touch, and linear models say about each channel's contribution?
2. **Estimating Incremental Sales** — What is the true Intent-to-Treat (ITT) effect per channel? How does it compare to naive attribution?
3. **Regression-Based Estimation** — Does regression with control variables improve on simple ITT comparisons?
4. **ROI of Marketing Channels** — How does ROI change when calculated using incremental vs. naive attribution?
5. **Was Simple Good Enough?** — Do naive models align with incremental findings? What are the risks of relying on them?

## Dataset

- **Source:** Patagonia CRM experiment, Fall 2024 – Early 2025
- **Full dataset:** 2,000,000 customers, 22 variables
- **Sampled dataset (`data/sample.csv`):** 50,000 rows, stratified by conversion status

**Channels studied:**
- Email
- YouTube (30-second video ads)
- Instagram (in-stream video ads)
- Google Search
- Contextual Display (Backpacker.com, GearJunkie.com, National Geographic, Treehugger.com)

**Experimental design:** 20% holdout rate per channel, independent random assignment at the customer level (except Google Search, which used geo-targeting due to platform constraints).

## Key Findings

Naive attribution models — last-touch, first-touch, and linear — significantly overstate the effectiveness of marketing channels by attributing all observed sales to advertising, including purchases that would have occurred organically. The experimental holdout design reveals that the majority of Patagonia's sales among exposed customers were driven by organic demand, not by the channels that received credit under attribution.

The experiment provides a more accurate basis for evaluating channel performance because it isolates **incremental impact**: the additional sales generated specifically because a customer was exposed to a channel. By comparing treatment and holdout groups, we can estimate what would have happened in the absence of marketing — a counterfactual that no attribution model can construct.

Key contrasts between the two approaches:

- **Channels that attribution overstates:** Google Search and Contextual Display appear highly effective under last-touch attribution due to their position in the conversion journey. Incremental analysis shows both channels generate negative ROI after accounting for their cost relative to true lift.
- **Channels that attribution understates:** Email and YouTube are undervalued by attribution models focused on last-touch but demonstrate strong positive incremental ROI in the experiment.
- **Scale of the gap:** Naive attribution attributes roughly 4× more revenue to marketing than the experiment supports. The remainder represents organic sales that would have occurred without any of the five channels.

These findings demonstrate that experiment-based incremental measurement is essential for sound marketing budget allocation. Attribution models, while operationally convenient, systematically mislead investment decisions by conflating correlation with causation.

## Repository Structure

```
├── data/
│   └── sample.csv          # 50,000-row stratified sample
├── patagonia_attribution.ipynb  # Main analysis notebook (executed)
├── requirements.txt
├── .gitignore
└── README.md
```

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/duydnguyenn/Patagonia_Attribution-Models-vs-Experiment.git
   cd Patagonia_Attribution-Models-vs-Experiment
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Launch the notebook:
   ```bash
   jupyter notebook patagonia_attribution.ipynb
   ```
