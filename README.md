# nba_feature_engineering_project
file covering the dataset source, prediction goal, and a comprehensive overview of the feature engineering workflow, including all steps taken (loading data, dropping non-predictive columns, correlation analysis, engineering PPM, handling multicollinearity, and null value handling).

## Summary of Feature Engineering and Selection Choices

This section documents the feature engineering and selection decisions made throughout this project, aligning with the goal of preparing a robust dataset for NBA player longevity prediction.

### 1. Target Variable Definition
- The `target_5yrs` column was clearly defined as the dependent variable. This binary variable indicates whether a player lasted at least 5 years in the league.

### 2. Dropping Non-Predictive Columns
- **Columns Removed**: `Unnamed: 0` (likely an index artifact) and `name` (player's name).
- **Rationale**: These columns were dropped because they are non-predictive and could introduce noise or lead to data leakage if used directly in a model. Player names, in particular, serve as unique identifiers rather than generalizable features.

### 3. Correlation Analysis
- A correlation matrix was calculated and visualized using a heatmap to understand the relationships between features and with the target variable.
- **Observations**: This step helped identify features highly correlated with each other (e.g., `pts`, `fgm`, `fga`, `min`), suggesting potential multicollinearity. It also provided insights into which features had stronger linear relationships with `target_5yrs`.
- **Decision**: While strong correlations were noted, no features were immediately dropped based solely on multicollinearity at this stage, as further analysis or dimensionality reduction techniques might be applied later. The primary goal here was identification.

### 4. Engineering New Composite Features
- **Feature Created**: `ppm` (Points Per Minute).
- **Calculation**: `ppm = pts / min`.
- **Rationale**: This composite feature was engineered to provide a more normalized measure of a player's scoring efficiency, independent of total playing time. It combines two important metrics (`pts` and `min`) into a single, potentially more informative predictor that captures per-minute impact.
- **Handling Edge Cases**: Division by zero for `min` was handled by assigning `ppm` a value of 0 in such cases.

### 5. Cleaning Dataset (Handling Null Values)
- **Check Performed**: An examination of `df.isnull().sum()` revealed no missing values across any of the remaining columns.
- **Rationale**: A clean dataset free from null values is crucial for model readiness, as many machine learning algorithms cannot handle missing data directly.
- **Decision**: Since no missing values were found, no imputation or deletion steps were necessary for this dataset, confirming its initial quality in this regard.

These steps have transformed the raw NBA player performance statistics into a cleaner, more refined dataset, with an engineered feature, ready for subsequent machine learning model building and evaluation.
