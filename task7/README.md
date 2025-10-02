1 — Project objective & quick plan

State the goal (example: binary classification with SVM; compare linear vs RBF).

Decide deliverables: notebook, README, saved model + scaler, short report (plots & metrics), and an Interviews.md with highlighted Q&A.

2 — Environment setup (high level)

Create a fresh Colab notebook.

Make a small “environment” section in the notebook listing required libraries. (In Colab most are preinstalled.)

Add a brief description cell explaining dataset, task, and evaluation metrics.

3 — Data loading & initial checks

Load dataset (sklearn example or upload CSV / mount Drive).

Immediately inspect: number of rows, number of features, datatype of each feature, and class distribution.

Check for missing values and obvious anomalies (NaNs, infinities, string entries in numeric columns).

If CSV: confirm the target column and its label encoding (0/1 for binary).

4 — Exploratory Data Analysis (EDA) — what to do (no code specifics)

Summary statistics: mean, std, min/max for numeric features.

Visual checks: histograms for feature distributions, boxplots for outliers, and a correlation heatmap to spot multicollinearity.

Quick pairwise scatter (on a small subset of features) to understand separability.

Note any class imbalance and potential need for balancing techniques.

5 — Data cleaning & preprocessing (process)

Handle missing values: choose drop or impute (mean/median/KNN) depending on missingness.

Encode categorical variables (if any): one-hot or ordinal encoding as appropriate.

Detect and treat outliers if they’re clearly erroneous or harmful (cap/impute/remove).

(Optional) Feature engineering: create ratios, aggregates, or domain-specific transforms if useful.

Decide whether to apply dimensionality reduction (e.g., PCA) for visualization or feature reduction — treat PCA as a separate step used for plotting or if multicollinearity is a problem.

6 — Train / validation / test split — best practice

Split dataset into train and test (common: 80/20 or 70/30).

Use stratified splitting for classification so class proportions are preserved.

Within the training portion, use cross-validation (e.g., 5-fold) for hyperparameter tuning.

NEVER scale using information from the test set — scaler must be fitted only on training data.

7 — Scaling & pipelines (important)

Standardize numeric features (zero mean, unit variance) — SVMs are sensitive to scale.

Prefer placing scaler and classifier in a pipeline so scaling is applied correctly at CV time and there’s no leakage.

Save the pipeline (scaler + model) for inference.

8 — Model selection strategy (linear vs RBF)

Start with baseline models: linear SVM and RBF SVM with default-ish parameters.

Compare basic metrics on validation to see which kernel family is promising.

Consider linear SVM for very high-dimensional / sparse data (e.g., text). Use RBF if you believe there are nonlinear patterns.

9 — Hyperparameter tuning (process, not code)

Identify hyperparameters to tune:

Linear: C (regularization).

RBF: C and gamma (kernel width).

Use cross-validated grid search or randomized search on training data only.

Start coarse (wide ranges) then refine around best values. Typical ranges: C from 1e-2 to 1e3; gamma values spanning very small to moderate (e.g., 1e-3 to 1).

Use appropriate scoring for tuning: accuracy for balanced data, F1 or ROC-AUC for imbalanced data.

Use n_jobs=-1 (parallel) in Colab to accelerate grid search.

10 — Model evaluation — metrics & interpretation

On test set compute: accuracy, precision, recall, F1-score, confusion matrix.

Compute ROC curve and AUC (or PR curve if classes are highly imbalanced).

Inspect confusion matrix to understand types of errors (false positives vs false negatives).

For linear SVMs examine coefficients to interpret feature importance; for RBF, inspect support vectors and decision boundaries in 2D visualizations.

If cross-validation used, report mean and standard deviation across folds to show stability.

11 — Visualization & intuition (what to produce)

Decision boundary plots on 2-D data: either choose two meaningful features or reduce to 2 components with PCA for visualization only.

Plot support vectors on the scatterplot so you can point to the critical training samples.

Show ROC / PR curves and a small table of final metrics.

Include a short text interpretation of each plot (what it shows and what you infer about model behavior).

12 — Model persistence and inference

Save the fitted scaler/pipeline and trained model (joblib / pickle).

Provide a short example (in README) showing how to load scaler + model, scale new observations, and produce predictions/probabilities.

If deploying, wrap inference into a simple function or REST endpoint (Flask/FastAPI) — note what needs shipping (model file, scaler, feature order).

13 — Robustness checks & production considerations

Test model on a held-out test set and, if possible, on a different dataset or time slice (temporal holdout) to check generalization.

Test sensitivity to feature scaling, to small perturbations, and to class distribution changes.

If model decisions matter operationally, log predictions, model confidence, and inputs used for decisions.

For imbalanced and high-risk tasks, calibrate probabilities (e.g., isotonic or Platt scaling) if decision thresholds matter.

14 — Common pitfalls & how to avoid them

Data leakage: scaling or feature selection fitted on full dataset — always fit transforms only on training data.

Overfitting in grid search: evaluating performance on test set during tuning — keep test only for final evaluation.

Ignoring class imbalance: leads to high accuracy but poor minority class performance — use appropriate metrics and sampling strategies.

Using complex kernel on huge data: RBF can be extremely slow and memory heavy — consider linear SVM or approximations.

Interpreting PCA visualizations as model performance: PCA reduces variance to 2 dims — boundaries may look different in full space.



Interview questions

Q1 — What is a support vector?
A support vector is a data point that lies closest to the decision boundary (hyperplane). These points are critical because they define the position and orientation of the hyperplane. If you remove non-support vectors, the decision boundary does not change, but removing support vectors can shift it.

Q2 — What does the C parameter do in SVM?
The parameter C controls the tradeoff between maximizing the margin and minimizing classification error:

Large C → tries to classify all training points correctly (narrower margin, risk of overfitting).

Small C → allows more misclassifications but creates a wider margin (stronger regularization, risk of underfitting).

Q3 — What is a kernel and why is it useful?
A kernel is a function that computes similarity between two data points in a (possibly high-dimensional) feature space. The kernel trick allows SVM to learn nonlinear decision boundaries without explicitly computing transformations.

Common kernels:

Linear

Polynomial

RBF (Gaussian)

Sigmoid

Q4 — What is the difference between linear and RBF kernel?

Linear kernel: Decision boundary is a straight hyperplane. Works well when data is linearly separable or number of features >> number of samples (e.g., text).

RBF kernel: Creates nonlinear boundaries by mapping to infinite-dimensional space. Controlled by gamma. More flexible but can overfit and is slower on large data.

Q5 — What is the role of gamma in RBF kernel?

Small gamma → broader influence of each training example → smoother decision boundary.

Large gamma → very localized influence → complex, wiggly boundaries, risk of overfitting.

In scikit-learn, default gamma="scale" is a good starting point.

Q6 — How does SVM handle non-linearly separable data?
Two mechanisms:

Soft margin (C parameter): Allows margin violations (misclassifications).

Kernel trick: Maps data into higher-dimensional space where classes may become separable.

Q7 — Explain the concept of a margin in SVM.
The margin is the distance between the decision boundary (hyperplane) and the closest training samples (support vectors). SVM tries to maximize this margin, leading to better generalization.

Q8 — What is the soft margin formulation (mathematical intuition)?
SVM optimization problem:


Q9 — Advantages of SVM

Effective in high-dimensional spaces.

Uses only support vectors → memory efficient.

Flexible (different kernels).

Often robust to overfitting when tuned correctly.

Disadvantages of SVM

Computationally expensive for large datasets.

Requires careful feature scaling.

Hyperparameters (C, gamma) need careful tuning.

Less interpretable for nonlinear kernels.

Q10 — Can SVM handle multi-class classification?
Yes, but SVM is inherently binary. Multi-class strategies:

One-vs-Rest (OvR): Train one classifier per class.

One-vs-One (OvO): Train classifiers for each pair of classes, then use voting.
Scikit-learn’s SVC handles multiclass automatically (OvR by default).

Q11 — How do you prevent overfitting in SVM?

Use cross-validation to tune C and gamma.

Prefer smaller C or smaller gamma to simplify decision boundaries.

Use fewer features or apply dimensionality reduction (e.g., PCA).

For noisy data, consider robust feature engineering or alternative models.

Q12 — When would you NOT use SVM?

Very large datasets (millions of samples): SVMs with kernels scale poorly. Alternatives: Logistic Regression, Random Forests, Gradient Boosted Trees, or LinearSVC.

When interpretability is crucial: Tree-based models give clearer explanations.

For streaming or online learning: Consider SGDClassifier with hinge loss (approximate linear SVM).




