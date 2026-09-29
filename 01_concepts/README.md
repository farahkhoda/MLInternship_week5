Week 5 — Concepts

This folder contains the conceptual foundations required for the Week 5 machine learning tasks.

The main focus of this week is Advanced Learning Algorithms, specifically tree-based models and ensemble learning.

Neural-network topics are outside the scope of this week’s work.

⸻

Concept Map

The concepts in this folder are connected as follows:

Decision Trees
      │
      ├── Tree Splitting
      ├── Gini Impurity
      ├── Entropy
      ├── Information Gain
      ├── Decision Boundaries
      └── Overfitting / Pruning
             │
             ↓
      Ensemble Methods
             │
       ┌─────┴─────┐
       ↓           ↓
    Bagging      Boosting
       │           │
       ↓           ↓
Random Forest  Gradient Boosting

⸻

1. Decision Trees

A Decision Tree makes predictions through a sequence of feature-based decisions.

The model repeatedly splits the data into smaller groups until it reaches leaf nodes containing predictions.

Important concepts:

* Root node
* Internal nodes
* Branches
* Leaf nodes
* Tree splitting
* Gini impurity
* Entropy
* Information gain
* Decision boundaries
* Tree depth
* Overfitting
* Pruning

A decision tree is powerful and interpretable, but a deep tree can have high variance and overfit the training data.

See:

decision_trees.md

⸻

2. Ensemble Methods

An ensemble combines multiple models to produce a final prediction.

The main motivation is that multiple models can compensate for individual model weaknesses.

Two major ensemble strategies studied this week are:

Bagging

Models are trained using different samples of the training data and their predictions are combined.

Main goal:

Reduce variance and improve stability.

Boosting

Models are trained sequentially, with later models improving the current ensemble.

Main goal:

Progressively reduce prediction error.

See:

ensemble_methods.md

⸻

3. Random Forest

Random Forest is an ensemble of decision trees based primarily on:

1. Bootstrap sampling
2. Random feature selection
3. Combining tree predictions

For classification, the final prediction is generally based on majority voting.

Its main advantage over a single decision tree is improved stability through aggregation and tree diversity.

Important concepts:

* Bootstrap sampling
* Random feature subsets
* Majority voting
* Tree diversity
* Variance reduction
* Out-of-bag samples
* Feature importance
* n_estimators
* max_depth
* max_features

See:

random_forest.md

⸻

4. Gradient Boosting

Gradient Boosting builds an ensemble sequentially.

Each new decision tree is trained to improve the current model according to a loss function.

Important concepts:

* Weak learners
* Sequential learning
* Loss functions
* Residuals
* Gradient-based improvement
* Learning rate
* Number of estimators
* Tree depth
* Regularization
* Early stopping

See:

gradient_boosting.md

⸻

5. Random Forest vs Gradient Boosting

The most important distinction is how the trees interact.

Random Forest

Tree 1 ─┐
Tree 2 ─┤
Tree 3 ─┼──→ Combine → Prediction
Tree 4 ─┤
Tree 5 ─┘

Trees are trained mostly independently.

The ensemble benefits from averaging diverse models.

Gradient Boosting

Tree 1
  ↓
Tree 2
  ↓
Tree 3
  ↓
Tree 4
  ↓
Final Ensemble

Each tree is influenced by the current ensemble and attempts to improve it.

⸻

6. Week 5 Learning Goals

By the end of the conceptual part of Week 5, the following questions should be understandable:

Decision Trees

* How does a decision tree split data?
* What makes one split better than another?
* What are Gini impurity and entropy?
* What is information gain?
* How do decision trees create decision boundaries?
* Why can deep trees overfit?
* How can tree complexity be controlled?

Ensemble Learning

* Why combine multiple models?
* What is the difference between bagging and boosting?
* Why does model diversity matter?
* How can ensembles reduce variance?

Random Forest

* How does bootstrap sampling work?
* Why are random feature subsets used?
* How does majority voting work?
* Why is Random Forest usually more stable than a single tree?
* What are the important Random Forest hyperparameters?

Gradient Boosting

* Why are trees trained sequentially?
* What does a weak learner mean?
* What is the role of the loss function?
* What does the gradient represent conceptually?
* What are residuals?
* How do learning rate and number of estimators interact?
* How can Gradient Boosting overfit?

⸻

7. Connection to the Week 5 Project

The conceptual material prepares for the practical model comparison.

The YCB-Video side quest compares:

Logistic Regression
       ↓
Decision Tree
       ↓
Random Forest
       ↓
Boosted Tree

The goal is to compare different modeling approaches while keeping the experimental setup consistent.

The same:

* Dataset
* Features
* Labels
* Data split
* Evaluation metrics

should be used across models.

This allows the model itself to be the main changing factor.

⸻

8. Scope

Included

* Decision Trees
* Tree Splitting
* Gini Impurity
* Entropy
* Information Gain
* Decision Boundaries
* Overfitting
* Pruning
* Ensemble Learning
* Bagging
* Random Forest
* Boosting
* Gradient Boosting
* Boosted Trees
* Relevant hyperparameters
* Model comparison concepts

Excluded

* Neural Networks
* Deep Learning architectures
* Backpropagation
* CNNs
* Other neural-network topics

These topics are outside the scope of Week 5.

⸻

Summary

The conceptual progression of this week is:

One Decision Tree
       ↓
Understand its strengths and weaknesses
       ↓
Why combine multiple models?
       ↓
Ensemble Learning
       ↓
      / \
     /   \
Bagging  Boosting
   ↓        ↓
Random   Gradient
Forest   Boosting

The main idea is to understand why these algorithms work, not simply how to call them in a machine learning library.