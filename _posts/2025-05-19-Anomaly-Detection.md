# Anomaly Detection in Fraud Analytics using K-Means and PCA

## Introduction

Fraud detection is one of the most critical applications of data science in the financial industry. Whether it's credit card fraud, insurance fraud, or fraudulent transactions in e-commerce, detecting unusual behavior in massive datasets is essential. One of the core ideas behind fraud detection is identifying **anomalies** or data points that deviate significantly from the expected behavior. In this blog, we delve into the root concept of anomaly detection, explain why it's challenging, and explore how **K-Means Clustering** and **Principal Component Analysis (PCA)** play a key role in this domain.

---

## What is an Anomaly?

An anomaly is any data point or pattern that deviates from the rest of the dataset. In fraud analytics, anomalies could represent:

* Sudden spikes in transaction amount
* Unusual transaction time or frequency
* Rare behavior by the customer that diverges from their historical activity

However, **not all anomalies are frauds**. A high-value transaction may be legitimate (e.g., a special occasion), and a flagged event could result in false positives. Therefore, anomaly detection must be handled with nuance.

### Characteristics of Anomalies

* They are rare in occurrence.
* They differ significantly from normal behavior.
* They can be contextual (e.g., large transactions may be normal on weekends but unusual mid-week).

---

## The Challenge in Fraud Detection

Fraud detection suffers from multiple challenges:

* **Imbalanced datasets**: In most real-world datasets, fraudulent transactions are a tiny fraction.
* **No clear labels**: Often, it's not known whether a transaction is fraud unless confirmed later.
* **Dynamic patterns**: Fraudsters continuously change their behavior to avoid detection.

To overcome these challenges, unsupervised learning techniques such as **K-Means Clustering** and dimensionality reduction using **PCA** have proven effective.

---

## Why Use Unsupervised Learning?

Unsupervised learning does not require labeled data. In fraud analytics:

* Labels (fraud or non-fraud) are not always available.
* Anomalies might be context-specific and not fit standard definitions.
* Clustering allows grouping similar behaviors and identifying outliers.

---

## K-Means Clustering: The Foundation

K-Means is a popular unsupervised algorithm that partitions data into `k` clusters based on feature similarity.

### How it Works:

1. Choose the number of clusters (k).
2. Initialize k centroids randomly.
3. Assign each data point to the nearest centroid.
4. Recompute centroids based on assigned points.
5. Repeat until centroids stabilize.

### In Fraud Analytics:

* Most transactions fall into a few major clusters ("normal behavior").
* Transactions far from any cluster center are flagged as **anomalies**.

### Example: Credit Card Transactions

If a user typically transacts \$1000 to \$2000 per month, and suddenly a \$100,000 transaction appears, K-Means would likely assign this point far from the cluster center, marking it as suspicious.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

# Simulated transaction data
normal_data = np.random.normal(loc=1500, scale=200, size=(100, 1))
anomaly = np.array([[100000]])
data = np.vstack((normal_data, anomaly))

# Standardize
scaler = StandardScaler()
data_scaled = scaler.fit_transform(data)

# Fit KMeans
kmeans = KMeans(n_clusters=2, random_state=42)
kmeans.fit(data_scaled)
labels = kmeans.labels_
centers = kmeans.cluster_centers_

# Compute distances to cluster centers
from numpy.linalg import norm
distances = norm(data_scaled - centers[labels], axis=1)

# Flag top anomaly
anomaly_index = np.argmax(distances)

# Visualize
plt.scatter(data_scaled[:, 0], np.zeros_like(data_scaled), c=labels, cmap='viridis')
plt.scatter(data_scaled[anomaly_index], 0, color='red', label='Anomaly')
plt.title('K-Means Clustering: Anomaly Highlighted')
plt.legend()
plt.show()
```

---

## Elbow Method: Choosing the Right `k`

To decide on the optimal number of clusters, the **Elbow Method** is used:

* Plot the sum of squared errors (SSE) for different values of `k`.
* The "elbow" point (where the SSE starts to level off) is a good choice.

```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

sse = []
for k in range(1, 10):
    model = KMeans(n_clusters=k)
    model.fit(data)
    sse.append(model.inertia_)

plt.plot(range(1, 10), sse)
plt.xlabel('Number of Clusters')
plt.ylabel('SSE')
plt.title('Elbow Method')
plt.show()
```

---

## Principal Component Analysis (PCA)

**PCA** is used to reduce the number of features in the dataset while retaining most of the variance.

### Why Use PCA?

* High-dimensional data can make clustering ineffective.
* PCA compresses the data while preserving structure.
* Makes data visualizable in 2D or 3D.

### Applying PCA Before Clustering

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)
```

---

## Detecting Anomalies with Distance Metrics

After clustering, calculate the **distance** from each point to its assigned cluster center:

* Points with large distances are likely anomalies.

```python
import numpy as np
from numpy.linalg import norm

centers = model.cluster_centers_
distances = norm(X_scaled - centers[model.labels_], axis=1)
anomalies = np.argsort(distances)[-5:]  # Top 5 anomalies
```

---

## Visualization

Visualize clusters and anomalies using 2D PCA representation:

```python
plt.scatter(X_pca[:, 0], X_pca[:, 1], c=model.labels_, cmap='viridis')
plt.scatter(X_pca[anomalies, 0], X_pca[anomalies, 1], color='red', label='Anomalies')
plt.title('K-Means Clustering with PCA')
plt.legend()
plt.show()
```

---

## Evaluation: Confusion Matrix

In supervised setups (where labels are available), evaluate using:

* **Accuracy**
* **Precision**
* **Recall**
* **F1-score**

```python
from sklearn.metrics import classification_report
print(classification_report(y_test, y_pred))
```

---

## Conclusion

Anomaly detection is a cornerstone of modern fraud analytics. By using unsupervised models like K-Means and enhancing them with PCA, we can uncover hidden patterns and detect outliers without needing explicit labels. These methods are especially useful in domains where fraud evolves quickly and labels are delayed or missing.

While these models don't prove fraud, they significantly narrow down the search space for human auditors or downstream classifiers. With the right preprocessing and thoughtful evaluation, K-Means and PCA can become essential tools in any fraud analyst's toolkit.

---

Stay tuned for our follow-up blog on how **supervised learning** techniques like decision trees and random forests can further refine fraud detection systems.
