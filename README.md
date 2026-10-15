# ML Data Cleaning and Correlation

Practical work (TP2) on data cleaning, correlation analysis, and feature selection using the Hepatitis dataset.

## Dataset

`hepatitis.csv` contains patient records with 19 features and a target variable.

| Type | Columns |
|------|---------|
| Numeric | `age`, `bilirubin`, `alk_phosphate`, `sgot`, `albumin`, `protime` |
| Boolean | `steroid`, `antivirals`, `fatigue`, `malaise`, `anorexia`, `liver_big`, `liver_firm`, `spleen_palpable`, `spiders`, `ascites`, `varices`, `histology` |
| Categorical | `sex` |
| Target | `class` (`live` / `die`) |

The dataset contains missing values (e.g. `steroid`, `alk_phosphate`, `protime`).

## Objectives

1. Drop the feature `sex`.
2. Plot the Pearson correlation heatmap to observe the correlation of the independent variables with the output variable.
3. Keep only features with an absolute correlation above 0.5 with the output variable.
4. Drop the features that are highly correlated with `malaise` (threshold: |r| > 0.7).
5. Discuss whether features should be correlated.

## Approach

- **Encoding:** `class` is mapped to `live = 1`, `die = 0`. Boolean columns are converted to `1.0` / `0.0`.
- **Missing values:** kept as `NaN` during encoding (not converted to category codes), so they do not create a fake category. Pandas computes Pearson correlation pairwise and ignores `NaN`.
- **Feature selection:** features are filtered by `|r| > 0.5` with `class`, then features highly correlated with `malaise` are removed from that selection.

## Discussion: should features be correlated?

- **Feature vs target:** yes. A strong correlation means the feature carries predictive information.
- **Feature vs feature:** no. Highly correlated features are redundant and cause multicollinearity, unstable coefficients, and unnecessary dimensionality.

## Repository Structure

```
├── hepatitis.csv   # Dataset
├── TP2.ipynb       # First version of the notebook
├── TP2V2.ipynb     # Revised notebook
└── README.md
```

## Requirements

- Python 3.9+
- pandas
- seaborn
- matplotlib
- Jupyter

```bash
pip install pandas seaborn matplotlib jupyter
```

## Usage

```bash
git clone https://github.com/i-brahmi/ML-data-cleaning-and-corrolation.git
cd ML-data-cleaning-and-corrolation
jupyter notebook TP2V2.ipynb
```

## Results

<!-- Fill in after running: which features passed the 0.5 threshold, which were dropped because of malaise. -->

## Author

i-brahmi
