# ML Data Cleaning and Correlation

Practical work (TP2) on missing-value handling, correlation analysis, and feature selection using the Hepatitis dataset.

## Dataset

`hepatitis.csv` contains patient records with 19 features and a target variable.

| Type | Columns |
|------|---------|
| Numeric | `age`, `bilirubin`, `alk_phosphate`, `sgot`, `albumin`, `protime` |
| Boolean | `steroid`, `antivirals`, `fatigue`, `malaise`, `anorexia`, `liver_big`, `liver_firm`, `spleen_palpable`, `spiders`, `ascites`, `varices`, `histology` |
| Categorical | `sex` |
| Target | `class` (`live` / `die`) |

## Part 1: Missing Values

### Objectives

1. Explain why data is missing.
2. Print all samples that contain missing values.
3. Print the features that contain missing values.
4. Print the samples together with the features that contain missing values.
5. Count the missing values in each feature.
6. Create a new dataframe and drop the samples containing missing values.
7. Create a new dataframe and drop the columns containing missing values. Is deleting missing values a solution?
8. Replace missing values using the mean (continuous features) or the mode (categorical features), then print the number of missing values after imputation.

### Why is data missing?

Typical causes in medical datasets like this one:

- A test was not performed or not recorded for the patient (e.g. `protime`, `alk_phosphate`).
- The patient refused or could not provide the information.
- Data entry or transcription errors.
- Equipment failure or lost records.
- Merging data from different sources.

Missing data is usually classified as:

- **MCAR** (Missing Completely At Random): missingness is unrelated to any variable.
- **MAR** (Missing At Random): missingness depends on other observed variables.
- **MNAR** (Missing Not At Random): missingness depends on the missing value itself (e.g. a test is skipped because the patient is healthy).

### Approach

- Missing values are detected with `isnull()`. Samples are listed with `df[df.isnull().any(axis=1)]` and features with `df.columns[df.isnull().any()]`.
- Counts per feature use `df.isnull().sum()`.
- **Row deletion:** `df.dropna()` creates a new dataframe without incomplete samples.
- **Column deletion:** `df.dropna(axis=1)` creates a new dataframe without incomplete features.
- **Imputation:** mean for continuous features, mode for boolean and categorical features. The number of remaining missing values is printed afterwards (expected: 0).

### Is deleting missing values a solution?

Generally no:

- **Dropping samples** can remove a large share of the dataset. With a small dataset like this one, many rows have at least one missing value, so little data is left for training.
- **Dropping columns** loses potentially informative features.
- Both can introduce bias, especially if the data is not MCAR.

Deletion is acceptable only when very few values are missing, or when a column is almost entirely empty. Imputation keeps all samples and features, at the cost of reducing variance and possibly adding bias (mean imputation shrinks the spread of a feature).

## Part 2: Correlation and Feature Selection

### Objectives

1. Drop the feature `sex`.
2. Plot the Pearson correlation heatmap to observe the correlation of the independent variables with the output variable.
3. Keep only features with an absolute correlation above 0.5 with the output variable.
4. Drop the features that are highly correlated with `malaise` (threshold: |r| > 0.7).
5. Discuss whether features should be correlated.

### Approach

- **Encoding:** `class` is mapped to `live = 1`, `die = 0`. Boolean columns are converted to `1.0` / `0.0`.
- **Missing values:** kept as `NaN` during encoding (not converted to category codes), so they do not create a fake category. Pandas computes Pearson correlation pairwise and ignores `NaN`.
- **Feature selection:** features are filtered by `|r| > 0.5` with `class`, then features highly correlated with `malaise` are removed from that selection.

### Should features be correlated?

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

<!-- Part 1: number of missing values per feature, shape of the dataframe after row deletion / column deletion, missing count after imputation. -->
<!-- Part 2: which features passed the 0.5 threshold, which were dropped because of malaise. -->

## Author

i-brahmi
