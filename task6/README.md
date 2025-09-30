

# 1. Process Explanation (for your Colab workflow)

Think of the pipeline like this:

### Step 1 — Install libraries

We install Python packages (`numpy`, `pandas`, `scikit-learn`, `matplotlib`, `joblib`) in Colab.
These are the tools you’ll use to handle data, build KNN, and plot results.

---

### Step 2 — Load data

* If **no CSV given**, the script loads **Iris dataset** (from sklearn).
* If you upload a **CSV**, the script expects:

  * All feature columns (numeric values).
  * The **last column = class label** (the target you want to predict).

---

### Step 3 — Preprocess (scaling)

KNN uses **distance (Euclidean by default)**.
If one feature has values in thousands and another in decimals, distance gets biased.
So we apply **StandardScaler** (zero mean, unit variance) to all features.

---

### Step 4 — Cross-validation (choose best K)

* You pass a list of `k_values` (like `1,3,5,7,9`).
* Script trains KNN with each K using **k-fold cross-validation** (splits data into folds and evaluates).
* Computes mean accuracy for each K.
* Selects **best K** (highest mean accuracy).

*Output:* A plot `accuracy_vs_k.png` showing accuracy for different K.

---

### Step 5 — Train-test split & final model

* Data split into **train (80%)** and **test (20%)**.
* Model trained with best K.
* Predictions made on test set.
* Evaluate with:

  * **Accuracy** (overall correct %).
  * **Confusion Matrix** (correct vs misclassified counts).
  * **Classification Report** (precision, recall, F1).

---

### Step 6 — Visualization

* **Confusion matrix heatmap** → shows how well model classified each class.
* **Decision boundary (PCA 2D)** → data projected into 2D, then KNN decision regions drawn (for visualization).

---

### Step 7 — Save outputs

Everything saved into `outputs/`:

* `accuracy_vs_k.png`
* `confusion_matrix.png`
* `decision_boundary.png`
* `predictions.csv` (true vs predicted labels)
* `knn_model.joblib` (serialized model, if `--save_model` used)

---

### Step 8 — Zip and download

Finally, outputs zipped and downloaded → ready to upload in GitHub / submit as assignment.

---

# 2. Interview Questions (with short, crisp answers)

### **Q1: How does KNN work?**

KNN is a **lazy learner** algorithm.

* It stores training data.
* For a new sample, it calculates **distance (usually Euclidean)** to all training points.
* Picks the **k nearest neighbors**.
* Predicts the **majority class** (classification) or average (regression).

---

### **Q2: Why do we normalize features in KNN?**

Because KNN uses **distance**.
If one feature has larger scale (e.g., age in years vs salary in dollars), it will dominate the distance measure.
Normalization ensures all features contribute equally.

---

### **Q3: How to choose the value of K?**

* **Small K (like 1, 3):** High variance, sensitive to noise, may overfit.
* **Large K:** Smooths boundaries, may underfit.
* Best K is usually chosen by **cross-validation**.
* Odd K avoids ties in binary classification.

---

### **Q4: What distance metrics can be used?**

* Euclidean (default)
* Manhattan (L1)
* Minkowski (generalized)
* Cosine similarity (sometimes in text problems)

---

### **Q5: What is the time complexity of KNN?**

* Training: **O(1)** (just storing data).
* Prediction: **O(n × d)** where `n = number of training samples`, `d = features`.
  That’s why KNN is **slow for large datasets**.

---

### **Q6: Advantages of KNN?**

* Simple and intuitive.
* No training phase (fast to build).
* Works for multi-class problems.
* Non-parametric (no assumption about data distribution).

---

### **Q7: Disadvantages of KNN?**

* Prediction is slow for large datasets.
* Sensitive to noise and irrelevant features.
* Needs normalization.
* Memory-heavy (stores all data).

---

### **Q8: How does KNN handle multi-class classification?**

It counts the votes of K nearest neighbors.
The class with the **highest frequency** among neighbors is assigned.

---

### **Q9: What happens if dataset has categorical features?**

KNN needs **numeric data**.
So categorical features must be **encoded** (One-hot encoding, Label encoding) before applying KNN.

---

### **Q10: What is the difference between KNN and K-means?**

* **KNN** = supervised classification algorithm (predicts labels).
* **K-means** = unsupervised clustering algorithm (groups similar data without labels).

