# Balanced vs Imbalanced Data in Machine Learning

In real-world machine learning tasks, especially in classification problems, the distribution of classes in the dataset plays a significant role in model performance. This post explains the concept of balanced and imbalanced datasets and explores various techniques to handle rare event modeling.

---

## What is Balanced Data?

A **balanced dataset** has roughly equal numbers of samples in each class. This makes training and evaluation more straightforward and allows most algorithms to perform effectively without bias toward one class.

### Example:
- Spam classification with 50% spam and 50% non-spam emails
- Fraud detection dataset with equal fraud and non-fraud samples

### Common Sampling Strategy:
- **Simple Random Sampling**: Randomly select samples from the population while maintaining class balance.

---

## What is Imbalanced Data?

An **imbalanced dataset** contains a disproportionate ratio of classes, where one or more classes are significantly underrepresented. This is common in fraud detection, medical diagnosis, and fault detection problems.
Imbalanced datasets, where one class significantly outnumbers others, are common in real-world applications. This imbalance can lead to biased models that perform poorly on the minority class. In this post, we will explore various techniques to handle imbalanced datasets, along with Python code examples.

### Example:
- 99% non-fraud transactions and 1% fraud transactions
- 95% healthy patients and 5% disease-positive cases

### Challenge:
Most machine learning models are biased toward the majority class, resulting in high accuracy but poor recall for minority classes.


### Understanding the Problem

In classification tasks, an imbalanced dataset has a disproportionate ratio of observations in each class. For example, a dataset with 95% negative class and 5% positive class is imbalanced. Standard classifiers tend to be biased towards the majority class, leading to poor performance on the minority class.

### Evaluation Metrics

Accuracy is not a reliable metric for imbalanced datasets. Instead, consider the following metrics:

- **Precision**: True Positives / (True Positives + False Positives)
- **Recall (Sensitivity)**: True Positives / (True Positives + False Negatives)
- **F1-Score**: 2 * (Precision * Recall) / (Precision + Recall)
- **Area Under the ROC Curve (AUC-ROC)**: Measures the ability of the classifier to distinguish between classes.

## Techniques to Handle Imbalanced Data

### 1. Random Resampling Methods
Adjust the dataset by randomly changing its class distribution.

#### a. Undersampling
- Randomly remove samples from the majority class.
- Reduces data volume and may lose useful information.
- Reduces the number of instances in the majority class.

```python
from imblearn.under_sampling import RandomUnderSampler
from collections import Counter

# Assuming X and y are your features and target
rus = RandomUnderSampler(random_state=42)
X_res, y_res = rus.fit_resample(X, y)
print(f"Resampled dataset shape: {Counter(y_res)}")
```

#### b. Oversampling
- Duplicate or generate synthetic examples from the minority class.
- Risk of overfitting due to repeated instances.
- Random Oversampling increases the number of instances in the minority class by duplicating them.

```python
from imblearn.over_sampling import RandomOverSampler

ros = RandomOverSampler(random_state=42)
X_res, y_res = ros.fit_resample(X, y)
print(f"Resampled dataset shape: {Counter(y_res)}")
```

---

#### c. **SMOTE (Synthetic Minority Oversampling Technique)**
- Generates synthetic examples of the minority class by interpolating between existing ones.
- Helps balance the dataset without duplication.

```python
from imblearn.over_sampling import SMOTE

smote = SMOTE(random_state=42)
X_res, y_res = smote.fit_resample(X, y)
print(f"Resampled dataset shape: {Counter(y_res)}")
```

##### SMOTE-NC

Handles datasets with both numerical and categorical features.

```python
from imblearn.over_sampling import SMOTENC

# Assuming categorical features are at indices 0 and 1
smote_nc = SMOTENC(categorical_features=[0, 1], random_state=42)
X_res, y_res = smote_nc.fit_resample(X, y)
print(f"Resampled dataset shape: {Counter(y_res)}")
```

#### **MSMOTE (Modified SMOTE)**
- Enhances SMOTE by considering minority class boundaries and densities.
- Reduces noise and improves learning near class boundaries.


**Overview:**
MSMOTE is an enhancement of the original SMOTE technique. It categorizes minority class samples into three types:

* **Safe:** Instances well within the minority class region.
* **Borderline:** Instances near the decision boundary between classes.
* **Noise:** Outliers or mislabeled instances.

By focusing on safe and borderline instances, MSMOTE generates synthetic samples that are more informative and reduces the risk of introducing noise into the dataset.

**Implementation:**

```python
from smote_variants import msmote
from sklearn.datasets import make_classification
from collections import Counter

# Generate an imbalanced dataset
X, y = make_classification(n_classes=2, class_sep=2,
                           weights=[0.9, 0.1], n_informative=3,
                           n_redundant=1, flip_y=0, n_features=20,
                           n_clusters_per_class=1, n_samples=1000, random_state=10)

# Apply MSMOTE
X_resampled, y_resampled = msmote().sample(X, y)
print(f"Resampled dataset shape: {Counter(y_resampled)}")
```


---

### 2. **Bootstrap Resampling**
- Draw samples with replacement from the original dataset.
- Used to increase diversity and simulate more training data.

---

### 3. Cross-Validation Techniques

### **K-Fold Cross Validation**
- Split the data into K subsets.
- Train on K-1 subsets and test on the remaining one.
- Repeat K times.

#### a. Stratified K-Fold Cross-Validation
- Ensures that each fold has a representative ratio of all classes.
- Best suited for imbalanced datasets.
- Ensures each fold has the same proportion of classes as the original dataset.

```python
from sklearn.model_selection import StratifiedKFold

skf = StratifiedKFold(n_splits=5)
for train_index, test_index in skf.split(X, y):
    X_train_fold, X_test_fold = X[train_index], X[test_index]
    y_train_fold, y_test_fold = y[train_index], y[test_index]
```

#### b. Repeated Stratified K-Fold Cross-Validation

- Repeats Stratified K-Fold multiple times with different splits.
- Repeat K-fold cross validation multiple times with different random splits.
- Reduces variance in evaluation.
  
```python
from sklearn.model_selection import RepeatedStratifiedKFold

rskf = RepeatedStratifiedKFold(n_splits=5, n_repeats=10, random_state=42)
for train_index, test_index in rskf.split(X, y):
    X_train_fold, X_test_fold = X[train_index], X[test_index]
    y_train_fold, y_test_fold = y[train_index], y[test_index]
```

#### c. **Leave-One-Out Cross Validation (LOOCV)**
- Extreme case of K-fold where K = number of samples.
- Each sample is used once as the test set.
- Computationally expensive but useful for small datasets.

---

### 4. **Cluster-Based Sampling**
- Use clustering algorithms to identify patterns in the minority class.
- Sample more intelligently by choosing representative clusters.

**Overview:**
Cluster-based sampling involves grouping similar instances using clustering algorithms (like K-Means) and then performing sampling within these clusters. This approach ensures that the diversity within the minority class is preserved and can lead to more robust models.

**Implementation:**
```python
from sklearn.cluster import KMeans
from sklearn.datasets import make_classification
from imblearn.under_sampling import ClusterCentroids
from collections import Counter

# Generate an imbalanced dataset
X, y = make_classification(n_classes=2, class_sep=2,
                           weights=[0.9, 0.1], n_informative=3,
                           n_redundant=1, flip_y=0, n_features=20,
                           n_clusters_per_class=1, n_samples=1000, random_state=10)

# Apply ClusterCentroids
cc = ClusterCentroids(random_state=42)
X_resampled, y_resampled = cc.fit_resample(X, y)
print(f"Resampled dataset shape: {Counter(y_resampled)}")

```

---

### 5. **Ensemble Techniques**
Combine multiple models to improve performance on rare classes.

Examples:
- **Bagging**: Train models on bootstrapped subsets.
- **Boosting**: Focus on misclassified minority class instances.
- **Balanced Random Forest**: Combines random undersampling with ensemble methods.

#### a. Balanced Random Forest

Combines bootstrapping and random feature selection with undersampling.

```python
from imblearn.ensemble import BalancedRandomForestClassifier

brf = BalancedRandomForestClassifier(n_estimators=100, random_state=42)
brf.fit(X_train, y_train)
```

#### b. EasyEnsemble

Trains multiple classifiers on different balanced subsets of the data.

```python
from imblearn.ensemble import EasyEnsembleClassifier

eec = EasyEnsembleClassifier(n_estimators=10, random_state=42)
eec.fit(X_train, y_train)
```


---

## Summary Table

**Techniques for Handling Imbalanced Datasets**

| Technique                         | Type           | Advantages                                             | Disadvantages                                         | Best Used When                                              |
|----------------------------------|----------------|--------------------------------------------------------|------------------------------------------------------|-------------------------------------------------------------|
| Simple Random Sampling           | Sampling       | Easy to implement                                      | May not address imbalance                            | Data is already balanced or close to balanced              |
| Random Undersampling             | Sampling       | Reduces training time                                  | Risk of losing important data                        | Large majority class with redundant data                   |
| Random Oversampling              | Sampling       | Balances data easily                                   | Risk of overfitting due to duplicates                | When minority class is very small                          |
| SMOTE                            | Synthetic      | Adds diversity to minority class                       | Can create borderline noise                          | General-purpose minority class oversampling                |
| MSMOTE                           | Synthetic      | Focuses on safe/borderline samples                     | Not available in all libraries                       | Improves SMOTE for noisy or complex data                   |
| Bootstrap Resampling             | Sampling       | Useful for variance estimation                         | May not balance classes by itself                    | Model evaluation with small datasets                       |
| Stratified K-Fold CV             | Validation     | Preserves class ratio in folds                         | Slightly slower than regular K-Fold                  | Evaluation of imbalanced classification                   |
| Repeated Stratified K-Fold       | Validation     | Reduces variance of estimates                          | More computationally expensive                       | High-stakes model evaluation                               |
| Leave-One-Out (LOOCV)            | Validation     | Maximum use of data                                    | Very slow for large datasets                         | Small datasets with few examples                           |
| Cluster-Based Sampling           | Sampling       | Preserves class structure                              | Requires tuning, clustering adds complexity          | Imbalanced data with subgroups in minority class           |
| Balanced Random Forest           | Ensemble       | Handles imbalance and maintains model power            | Slower training than regular RF                      | Any imbalanced classification task                         |
| EasyEnsemble                     | Ensemble       | Strong performance with multiple classifiers           | Resource-intensive                                   | Rare events, large datasets with extreme imbalance         |
| Class Weight Adjustment          | Cost-Sensitive | No need to modify data                                 | May underperform if weights not optimal              | When minority class is small but critical                  |
| SMOTE-NC                         | Synthetic      | Works with categorical + numerical features            | More complex to use                                  | Datasets with mixed feature types                          |


### Notes

* Synthetic techniques like SMOTE should be applied *after* splitting the data into training and testing sets to avoid data leakage.
* Ensemble methods generally provide higher robustness but require more computational power.
* Always monitor precision, recall, and F1-score - not just accuracy - when using these methods.


---

## Final Thoughts

Handling imbalanced datasets is critical for real-world applications where rare events matter most. By applying the right combination of sampling, validation, and modeling techniques, you can improve performance and create fair, reliable models. Always evaluate results using metrics like precision, recall, and F1-score rather than just accuracy.
