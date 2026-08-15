# What Drives a Match? - Speed Dating Analysis

Exploratory data analysis, hypothesis testing, and predictive modeling on real speed dating experiment data (2002–2004), investigating the gap between what people say they want in a partner and what actually drives their decisions.

<img src="https://full-stack-assets.s3.eu-west-3.amazonaws.com/M03-EDA/Tinder-Symbole.png" width="500">

## Business context

Fewer matches on a dating platform mean users churn. Understanding what actually makes two people interested in each other, as opposed to what they *say* they're looking for, is the first step toward improving match rates.

**Central question:** What drives a match?

This project uses data from 21 speed dating events where participants had four-minute face-to-face dates with every participant of the opposite sex, then decided whether they'd want to see that person again and rated them on six attributes (Attractiveness, Sincerity, Intelligence, Fun, Ambition, Shared Interests). Participants also completed surveys about their preferences, self-perception, and beliefs about what others value, capturing both what people *say* and what they *do*.

## Key findings

- **Attractiveness is the closest thing to a universal driver of a "yes"** for both genders: the strongest predictor in the logistic regression models and consistently significant across every hypothesis test.
- **Shared interests is the biggest stated-vs-actual gap.** Both genders rank it near-last in stated importance, yet it's tied for the second-strongest predictor of an actual "yes" in the model: people underrate how much it actually shapes their decisions.
- **Men and women state and rate attributes differently:** men state attractiveness matters most and rate it higher after the date (Mann-Whitney U, `d = 0.76` stated / `d = 0.50` observed); women state ambition matters more and rate partners higher on ambition and intelligence.
- **Match rates are low overall (~16.5% of dates)** and decline as the night goes on for both genders, suggesting decision fatigue.
- **Age similarity has a small but measurable effect** on matching (`d = 0.19`); rows with all six ratings missing have a near-zero "yes" rate and were excluded as likely unrecorded/no-show dates rather than genuine rejections.

## Repository structure

```
.
├── Speed_Dating_Data.csv       # Raw dataset (speed dating events, 2002-2004)
├── Speed_Dating_Data_Key.doc   # Data dictionary and documentation
├── tinder_speed_dating.ipynb   # Main analysis notebook
└── README.md
```

## Notebook contents

1. **Setup** - imports, color palette, and helper functions (safe multi-encoding CSV loader, column normalization, per-wave rating normalization, Cohen's d, ML metrics reporting)
2. **Data loading and cleaning** - encoding detection, missing-data audit, column classification (kept for analysis / dropped / normalized across waves), since waves 1–5 and 10–21 use a 100-point allocation scale while waves 6–9 use a 1–10 scale
3. **Exploratory data analysis** - gender and age distributions, race breakdown, match rates, "yes" rate over the course of the evening, stated preferences by gender (radar chart), correlation matrix, and rating distributions by decision outcome
4. **Hypothesis testing** - five tests (with normality checks and the appropriate parametric/non-parametric test, plus effect sizes):
   - Do men and women state different preferences?
   - Do men and women say "yes" at different rates?
   - Do men and women rate partners differently?
   - Does age gap affect the likelihood of a match?
   - Is missingness in the rating columns associated with the decision (used to justify dropping fully-missing rows before modeling)?
5. **Machine learning** - separate logistic regression models per gender predicting the decision (`dec`) from the six attribute ratings, benchmarked against a majority-class dummy classifier, compared via accuracy/precision/recall/F1 and standardized coefficients

## Data source

- [Dataset (CSV)](https://full-stack-assets.s3.eu-west-3.amazonaws.com/M03-EDA/Speed+Dating+Data.csv)
- [Documentation (DOC)](https://full-stack-assets.s3.eu-west-3.amazonaws.com/M03-EDA/Speed+Dating+Data+Key.doc)
