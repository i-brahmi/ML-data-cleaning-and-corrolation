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
