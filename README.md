# Event Detection Validation

Validation study comparing the UPLIFT algorithm's automated event detection against human ground truth annotations for baseball hitting and pitching movements.

## Overview

This study evaluates the accuracy and reliability of automated event detection for biomechanical analysis of baseball movements. The UPLIFT algorithm automatically identifies key temporal events (e.g., foot contact, ball contact, swing through, ball release) from motion capture data, and these detections are compared against expert human annotations.

## Key Findings

| Metric | Value | Interpretation |
|--------|-------|----------------|
| CCC (Auto vs Human) | >0.998 | Almost Perfect Agreement |
| ICC (Inter-Rater) | >0.999 | Excellent Reliability |
| Mean Error | ±3-5 frames | ~12-21 ms at 240 fps |
| Detection Accuracy | >90% | Within ±12 frames of ground truth |

## Data

### Main Comparison Data
- **Hitting** (`data/hitting_data.csv`): 200 trials comparing UPLIFT vs human annotations
- **Pitching** (`data/pitching_data.csv`): 108 trials comparing UPLIFT vs human annotations

### Inter-Rater Reliability Data
- **Hitting Inter-Rater** (`data/hitting_inter_rater.csv`): 22 trials with both raters (Shun & Ricky)
- **Pitching Inter-Rater** (`data/pitching_inter_rater.csv`): 13 trials with both raters

### Events Analyzed

| Movement | Events |
|----------|--------|
| Hitting | Foot Contact, Ball Contact, Swing Through |
| Pitching | Foot Contact, Ball Release |

## Repository Structure

```
event-detection-validation/
├── README.md
├── data/
│   ├── hitting_data.csv           # Auto vs Human comparison (n=200)
│   ├── pitching_data.csv          # Auto vs Human comparison (n=108)
│   ├── hitting_inter_rater.csv    # Shun vs Ricky (n=22)
│   └── pitching_inter_rater.csv   # Shun vs Ricky (n=13)
├── notebooks/
│   └── Event_Detection_Analysis.ipynb
└── figures/
    ├── figure1_error_distribution.png
    ├── figure2_tolerance_intervals.png
    ├── figure3_ccc_concordance.png
    └── figure4_bland_altman.png
```

## Analysis Contents

The notebook generates the following tables and figures:

### Tables
- **Table 2**: Error Distribution Statistics (Mean, SD, Median, MAE, Range, R², CCC)
- **Table 3**: ICC Inter-Rater Reliability Overview
- **Table 4**: ICC Scores with Full Precision
- **Table 5**: CCC Values (Auto vs Human)
- **Table 6**: CCC Values (Inter-Rater: Shun vs Ricky)

### Figures
- **Figure 1**: Error Distribution Histograms
- **Figure 2**: Tolerance Interval Proportions
- **Figure 3**: CCC Concordance Plots
- **Figure 4**: Bland-Altman Plots (Inter-Rater)

## Requirements

```
numpy
pandas
matplotlib
seaborn
pingouin
scikit-learn
```

Install with:
```bash
pip install numpy pandas matplotlib seaborn pingouin scikit-learn
```

## Usage

1. Clone the repository
2. Install requirements
3. Open `notebooks/Event_Detection_Analysis.ipynb` in Jupyter
4. Run all cells to reproduce the analysis

## Methods

### Concordance Correlation Coefficient (CCC)
Lin's CCC measures agreement between two methods by evaluating both precision (how tightly clustered points are) and accuracy (how close to the 45° line of perfect concordance). CCC = ρ × Cb, where ρ is Pearson's correlation and Cb is the bias correction factor.

### Intraclass Correlation Coefficient (ICC)
ICC(3,1) two-way mixed-effects model with absolute agreement was used to assess inter-rater reliability between human annotators.

### Tolerance Thresholds
- **Very Accurate**: 0-6 frames (0-25 ms at 240 fps)
- **Accurate**: 7-12 frames (25-50 ms)
- **Moderate**: 13-24 frames (50-100 ms)
- **Inaccurate**: >24 frames (>100 ms)

## License

© UPLIFT. All rights reserved.
