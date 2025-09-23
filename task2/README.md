**Part 1: Summary of Overall Content & Process (EDA Task)**

Dataset: Titanic dataset (titanic.csv) — passengers info (age, fare, sex, class, etc.) + survival status.


Process Flow:

Data loading → read CSV (or seaborn sample if demo).

Basic checks → shape, column types, missing values.

Summary statistics → mean, median, std, skewness, kurtosis (saved in summary_stats.csv).


Visualization:

Histograms for numeric distributions.

Boxplots by Survived to see differences.

Correlation matrix & heatmap.

Pairplot (relationships between numeric features).

Countplots for categorical variables.

Skewness detection → log-transform applied if highly skewed (e.g., Fare).

Multicollinearity check → Variance Inflation Factor (VIF) (saved in vif.csv).

Missing values treatment → demo with median imputation (saved in numeric_imputed_sample.csv).


Simple inferences:

Women had higher survival (~74%).

1st class had higher survival (~63%).

3rd class & males had lowest survival.

Fare distribution skewed → transformation helps.


Outputs (saved/generated):

summary_stats.csv → stats of numeric columns.

vif.csv → multicollinearity table.

numeric_imputed_sample.csv → imputed numeric dataset.

inferences.txt → key findings.

plots/ → histograms, boxplots, correlation heatmap, pairplot, countplots.


Key Learnings from Process:

EDA is not just about numbers, but about discovering data quality issues, patterns, and insights.

Visualizations reveal outliers, skewness, and relationships better than tables alone.

Skewness & multicollinearity need to be treated before ML models.

Simple group-wise averages (e.g., survival by sex/class) already give strong feature importance intuition.



**🔹 Part 2: Interview Questions (with concise answers)**

What is the purpose of EDA?
To understand the dataset’s structure, detect anomalies/outliers, explore relationships, handle missing values, and generate insights before modeling.

How do boxplots help in understanding a dataset?
 Show distribution, median, quartiles, and outliers. Quick way to compare spread across groups.

What is correlation and why is it useful?
 Correlation measures how two numeric variables move together. Useful to detect relationships and multicollinearity (important for regression models).

How do you detect skewness in data?
Statistical skewness metric, histograms, or boxplots. If skew > |1|, data is strongly skewed → may need log/transform.

What is multicollinearity?
 When predictor variables are highly correlated, making model coefficients unstable. Detected via correlation matrix or VIF.

What tools do you use for EDA?
Pandas, Matplotlib, Seaborn (sometimes Plotly for interactivity), statsmodels (VIF), scikit-learn (imputation).

Can you explain a time when EDA helped you find a problem?
 Example: Found a column with many missing values (Cabin in Titanic), which was better dropped/engineered instead of directly used in models.

What is the role of visualization in ML?
 Helps communicate findings, detect data issues, understand feature-target relationships, and guide feature engineering.
