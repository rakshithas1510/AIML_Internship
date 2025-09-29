

1. **Load dataset**

   * Tries to read `data/heart.csv` (like the Heart Disease dataset).
   * If not found, falls back to sklearn’s **Breast Cancer dataset**.

2. **Preprocess data**

   * Removes duplicates, handles missing values.
   * Encodes categorical (string) columns into numbers if needed.

3. **Split dataset**

   * Splits into **80% training** and **20% testing**.

4. **Train a Decision Tree**

   * Builds a decision tree classifier.
   * Tests accuracy on the test set.
   * Saves a visualization (`dt_tree_top3.png`) of the first few levels of the tree.

5. **Overfitting analysis**

   * Trains multiple decision trees with different `max_depth` values (1 → 15).
   * Plots training vs test accuracy (`dt_overfitting_depths.png`).
   * Shows how deeper trees might **overfit** (train accuracy ↑ but test accuracy ↓).

6. **Cross-validation**

   * Estimates accuracy more reliably using 5-fold cross-validation.

7. **Train a Random Forest**

   * Builds an ensemble of 200 decision trees.
   * Tests accuracy on the test set.
   * Compares with single decision tree performance.

8. **Feature importance**

   * Shows which features are most important in classification.
   * Saves plots (`*_feature_importances.png`).

9. **Save results**

   * Models are saved as `.joblib` files for reuse.
   * Summary of accuracies written in `outputs/summary.txt`.


---

## 🔹 2. Interview Questions (with short answers)

Here are some **interview-style Q&A** linked to the code:

### 🌳 Decision Tree

1. **What is a Decision Tree and how does it work?**

   * A model that splits data by asking feature-based questions until reaching leaf nodes with class predictions. Each split reduces impurity (uncertainty).

2. **What is Entropy & Gini Index?**

   * Entropy: measures impurity using information theory.
   * Gini Index: probability of incorrect classification when randomly chosen.
   * Both are used as split criteria.

3. **What is Information Gain?**

   * Reduction in impurity (e.g., entropy) after a split. Trees choose the split with the highest information gain.

4. **Why do Decision Trees overfit?**

   * Deep trees fit noise in the training set. Accuracy is high on train data but poor on test data.

5. **How can you prevent overfitting in Decision Trees?**

   * Limit tree depth (`max_depth`).
   * Set minimum samples per leaf.
   * Use pruning techniques.
   * Use ensembles like Random Forest.

---

### 🌲 Random Forest

6. **What is a Random Forest?**

   * An ensemble of multiple decision trees trained on random subsets of data and features. Predictions are made by majority voting.

7. **How is Random Forest better than a single Decision Tree?**

   * Reduces variance, more stable, less prone to overfitting.
   * Generally gives higher accuracy.

8. **What is Bagging (Bootstrap Aggregation)?**

   * Randomly sample data with replacement (bootstrap).
   * Train models on each sample.
   * Aggregate predictions (majority vote or averaging).

9. **What are Feature Importances in Random Forest?**

   * Measure how much each feature contributes to reducing impurity across all trees.
   * Helps identify important predictors.

10. **Pros and Cons of Random Forests?**

* ✅ Pros: High accuracy, less overfitting, works well with both numerical & categorical data.
* ❌ Cons: Slower, larger model size, less interpretable than a single tree.

