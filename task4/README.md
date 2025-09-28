How does logistic regression differ from linear regression?

👉 Answer:

Linear regression predicts continuous values (e.g., house price).

Logistic regression predicts the probability of a binary or categorical outcome (e.g., cancer vs no cancer).

Logistic regression applies the sigmoid function to map predictions to the range 0–1, making them interpretable as probabilities.

❓ What is the sigmoid function?

👉 Answer:

The sigmoid function is:

𝜎
(
𝑧
)
=
1
1
+
𝑒
−
𝑧
σ(z)=
1+e
−z
1
	​


It maps any real number to a probability between 0 and 1.

It’s S-shaped: values of z → -∞ approach 0, and z → +∞ approach 1.

In logistic regression, the sigmoid is applied to the linear combination of features to produce probabilities.

❓ What is precision vs recall?

👉 Answer:

Precision (Positive Predictive Value):
Of all predicted positives, how many are correct?

Precision
=
𝑇
𝑃
𝑇
𝑃
+
𝐹
𝑃
Precision=
TP+FP
TP
	​


Recall (Sensitivity/True Positive Rate):
Of all actual positives, how many did we correctly identify?

Recall
=
𝑇
𝑃
𝑇
𝑃
+
𝐹
𝑁
Recall=
TP+FN
TP
	​


Example:

In cancer detection, high recall ensures most cancer cases are caught.

High precision ensures we don’t wrongly label healthy people as sick.

❓ What is the ROC-AUC curve?

👉 Answer:

ROC curve (Receiver Operating Characteristic): plots True Positive Rate (Recall) vs False Positive Rate at different thresholds.

AUC (Area Under Curve):

Measures model’s ability to separate classes.

AUC = 1.0 → perfect classifier

AUC = 0.5 → random guessing

In practice, higher AUC means better performance in distinguishing between classes.

❓ What is the confusion matrix?

👉 Answer:

A 2x2 table that summarizes classification results:

	Predicted Positive	Predicted Negative
Actual Positive	True Positive (TP)	False Negative (FN)
Actual Negative	False Positive (FP)	True Negative (TN)

Helps visualize where the model is making errors (false positives vs false negatives).

❓ What happens if classes are imbalanced?

👉 Answer:

Example: In fraud detection, 99% transactions are normal, 1% fraudulent.

A model predicting all “normal” would still show 99% accuracy, but fail in fraud detection.

Solutions:

Use precision, recall, F1, ROC-AUC, PR-AUC instead of accuracy.

Use class weights (class_weight='balanced' in sklearn).

Apply oversampling (SMOTE), undersampling, or synthetic data generation.

❓ How do you choose the threshold?

👉 Answer:

By default, logistic regression uses 0.5 as threshold.

In practice, choose based on business needs:

Healthcare: lower threshold to maximize recall (catch all patients).

Spam detection: higher threshold to maximize precision (avoid false alarms).

Threshold tuning is often done via Precision-Recall tradeoff or maximizing F1 score.

❓ Can logistic regression be used for multi-class problems?

👉 Answer:

Yes, using strategies like:

One-vs-Rest (OvR): Train one classifier per class vs all others.

Multinomial logistic regression (Softmax): Extends logistic regression to handle multiple classes directly.

In sklearn: LogisticRegression(multi_class='multinomial', solver='lbfgs').
