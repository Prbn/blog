gini index vs entropy vs information gain vs log loss vs AUC vs ROC

Gini index, entropy, information gain, log loss, AUC, and ROC are all metrics used in machine learning and classification. Here's a breakdown of each: 
 
Gini index
Measures how well a model ranks predictions, ranging from -1 to 1, with 0 being a random classifier. It's faster to calculate than entropy but favors larger partitions. 
 
Entropy
Measures the impurity in a node, using logarithms and making it more complex to calculate than the Gini index. It's preferred for imbalanced datasets. 
 
Information gain
Measures the reduction in entropy when splitting a dataset, favoring smaller partitions with distinct values. It's easy to understand and works well in many situations. 
 
Log loss
Measures the difference between predicted probabilities and actual values for binary classification models. The higher the divergence, the higher the log-loss value. 
 
AUC
The area under the ROC curve, which measures the performance of classification rules. It's a useful metric for comparing two models, with the greater AUC generally being better. 
 
Gini impurity
Another name for the Gini index, which calculates the heterogeneity of a node. A Gini impurity value of 0 indicates a homogeneous or pure partition. 
 
Both Gini index and entropy are used to decide which feature to split on in classification scenarios. The ID3 algorithm uses information gain, while the CART algorithm uses the Gini index. 
