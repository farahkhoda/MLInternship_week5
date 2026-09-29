Decision Trees

1. Overview

A Decision Tree is a supervised machine learning algorithm that can be used for both classification and regression.

The main idea is to make a prediction by repeatedly asking a sequence of questions about the input features.

For example, a classification tree might ask:

Is feature A < 10?
├── Yes → Is feature B < 5?
│         ├── Yes → Class 0
│         └── No  → Class 1
└── No  → Class 1

Each question divides the data into smaller groups until the tree reaches a prediction.

A decision tree therefore represents a model as a hierarchy of if-then decisions.

⸻

2. Basic Structure

A decision tree consists of several important components.

Root Node

The root is the first node of the tree.

It contains the entire training dataset and represents the first decision made by the model.

Internal Node

An internal node represents a decision based on one feature.

For example:

feature_1 < 10

The decision divides the samples into different branches.

Branch

A branch represents the outcome of a decision.

For a binary split, there are usually two branches:

feature_1 < 10
       /      \
     Yes       No

Leaf Node

A leaf is the final node of a tree.

It contains the model’s prediction.

For classification:

Leaf → Class A

For regression:

Leaf → predicted numerical value

⸻

3. How a Decision Tree Learns

The training process is based on repeatedly splitting the training data.

At each node, the algorithm considers possible splits and tries to find one that creates more homogeneous groups.

For example, suppose we want to classify objects based on two features:

Feature 1: size
Feature 2: weight

The tree may discover that:

size < 10

creates a useful separation between classes.

It then evaluates further splits inside each resulting group.

This process continues recursively.

All Data
   ↓
Best Split
   ↓
Smaller Groups
   ↓
Best Split for Each Group
   ↓
Smaller Groups
   ↓
...
   ↓
Leaf Predictions

⸻

4. Tree Splitting

A split divides the samples at a node into two or more subsets.

For numerical features, a common binary split is:

feature ≤ threshold

For example:

age ≤ 30

creates:

Left branch:  age ≤ 30
Right branch: age > 30

The algorithm searches for a feature and threshold that produce a useful separation.

The quality of a split is measured using an impurity criterion.

Common criteria include:

* Gini impurity
* Entropy
* Information gain

⸻

5. Impurity

Impurity measures how mixed the classes are inside a node.

Consider a node containing:

Class A: 50 samples
Class B: 50 samples

The node is highly mixed.

Now consider:

Class A: 100 samples
Class B: 0 samples

This node is pure because it contains only one class.

A good classification split generally produces child nodes that are more pure than the original node.

⸻

6. Gini Impurity

Gini impurity measures the probability that a randomly selected sample would be incorrectly classified if it were labeled according to the class distribution of the node.

The formula is:

[
Gini = 1 - \sum_{k=1}^{K} p_k^2
]

where:

* (K) = number of classes
* (p_k) = proportion of samples belonging to class (k)

For a completely pure node:

p = 1

and:

Gini = 0

Therefore:

Lower Gini impurity means a purer node.

⸻

7. Entropy

Entropy is another measure of impurity.

It measures the uncertainty or disorder in a node.

The formula is:

[
H = -\sum_{k=1}^{K} p_k \log_2(p_k)
]

A pure node has:

Entropy = 0

because there is no uncertainty about its class.

A highly mixed node has higher entropy.

Therefore:

Lower entropy means less uncertainty and greater purity.

⸻

8. Information Gain

Information gain measures how much a split reduces entropy.

Conceptually:

Information Gain
=
Impurity before split
-
Weighted impurity after split

A good split produces a large reduction in impurity.

The tree-building algorithm compares possible splits and chooses the one that provides the greatest improvement according to the selected criterion.

⸻

9. Gini vs Entropy

Both Gini impurity and entropy measure node impurity.

Criterion	Main idea
Gini	Measures class mixing
Entropy	Measures uncertainty
Lower value	Better / purer node
Typical use	Classification trees

In practice, both often produce similar trees.

The important concept is not memorizing which one is “better”, but understanding that the tree needs a mathematical way to determine whether a split improves class separation.

⸻

10. Decision Boundaries

A decision tree creates decision boundaries in feature space.

For numerical features, a tree typically creates axis-aligned boundaries.

For example:

Feature 1 < 5

creates a boundary perpendicular to the Feature 1 axis.

Another split:

Feature 2 < 10

creates another boundary.

Together, these splits divide the feature space into regions.

Each region corresponds to a prediction.

Conceptually:

Feature 2
   ↑
   │   Class A | Class B
   │           |
   │           |
   │-----------|
   │           |
   │ Class A   | Class B
   └──────────────────→ Feature 1

This allows decision trees to model nonlinear relationships without explicitly creating nonlinear mathematical transformations.

⸻

11. Recursive Partitioning

Decision trees can be understood as performing recursive partitioning.

The algorithm:

1. Starts with all training samples.
2. Finds a useful split.
3. Divides the data.
4. Finds another split inside each resulting region.
5. Continues recursively.
6. Stops according to predefined stopping conditions.

The result is a hierarchy of increasingly smaller regions.

⸻

12. When Does the Tree Stop?

A tree does not necessarily continue splitting until every sample has its own leaf.

Common stopping conditions include:

* Maximum tree depth
* Minimum number of samples required to split a node
* Minimum number of samples required in a leaf
* No useful improvement from further splitting
* Maximum number of leaf nodes

These parameters help control the complexity of the model.

⸻

13. Overfitting

Decision trees are particularly susceptible to overfitting.

A very deep tree can learn extremely specific patterns in the training data.

For example:

Training data
      ↓
Many splits
      ↓
Very deep tree
      ↓
Very specific rules
      ↓
Excellent training performance
      ↓
Poor generalization

The model may effectively memorize parts of the training dataset instead of learning patterns that generalize to unseen data.

This often produces:

High training accuracy
Low validation/test accuracy

⸻

14. Controlling Tree Complexity

Several techniques can reduce overfitting.

Maximum Depth

max_depth limits how many levels the tree can have.

Smaller depth:

* simpler model
* lower variance
* potentially higher bias

Larger depth:

* more complex model
* potentially lower bias
* higher risk of overfitting

Minimum Samples per Split

min_samples_split controls the minimum number of samples required before a node can be split.

Increasing it can prevent very small, highly specific splits.

Minimum Samples per Leaf

min_samples_leaf specifies the minimum number of samples that must remain in a leaf.

Larger values generally create smoother, less complex trees.

⸻

15. Pruning

Pruning means reducing unnecessary parts of a decision tree.

The goal is to remove branches that add complexity without improving generalization.

There are two broad approaches:

Pre-pruning

Stop the tree from becoming too complex during training.

Examples:

* max_depth
* min_samples_split
* min_samples_leaf

Post-pruning

First allow the tree to grow, then remove branches that are not useful.

Pruning is essentially a form of regularization for decision trees.

⸻

16. Classification vs Regression Trees

Decision trees can solve both classification and regression problems.

Classification

The leaf predicts a class.

Example:

Leaf:
Class A → 80%
Class B → 20%
Prediction → Class A

Regression

The leaf predicts a numerical value.

For example:

Leaf samples:
10, 12, 14, 16
Prediction:
mean = 13

The splitting criterion is adapted to the task.

⸻

17. Advantages

Decision trees have several useful properties:

* Easy to understand conceptually
* Can model nonlinear relationships
* Do not require feature scaling
* Can work with numerical and categorical features depending on implementation
* Can capture feature interactions
* Predictions can be interpreted as a sequence of decisions

⸻

18. Limitations

Decision trees also have important limitations:

* Can overfit easily
* Small changes in training data can produce a different tree
* Deep trees can become difficult to interpret
* Individual trees often have high variance
* Greedy splitting does not guarantee a globally optimal tree

The instability of individual trees is one of the main motivations for ensemble methods.

⸻

19. Key Takeaway

A decision tree learns a hierarchy of feature-based decisions.

The central process is:

Data
 ↓
Choose a split
 ↓
Reduce impurity
 ↓
Partition the data
 ↓
Repeat recursively
 ↓
Create leaf predictions

The most important concepts are:

* Nodes
* Splits
* Gini impurity
* Entropy
* Information gain
* Decision boundaries
* Recursive partitioning
* Overfitting
* Tree depth
* Pruning

A single decision tree is powerful and interpretable, but it can have high variance. This motivates combining multiple models, which leads to ensemble learning.