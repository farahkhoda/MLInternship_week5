Ensemble Methods

1. Overview

Ensemble learning is a machine learning approach in which multiple models are combined to produce a final prediction.

Instead of relying on one model:

Dataset
   ↓
One Model
   ↓
Prediction

an ensemble uses multiple models:

                ┌── Model 1 ──┐
                ├── Model 2 ──┤
Dataset ────────┼── Model 3 ──┼──→ Combined Prediction
                ├── Model 4 ──┤
                └── Model 5 ──┘

The central idea is that multiple models can compensate for each other’s weaknesses.

⸻

2. Why Use Multiple Models?

A single model may make errors because of:

* Noise in the training data
* Limited model capacity
* High variance
* High bias
* Sensitivity to particular training samples

If multiple models make different errors, combining their predictions can produce a more robust result.

The key idea is:

Diversity among models can make the combined prediction more reliable.

However, simply adding more models does not automatically improve performance.

The models need to provide useful and sufficiently diverse information.

⸻

3. Ensemble Learning and Bias-Variance

Ensemble methods are strongly connected to the bias-variance tradeoff.

Recall:

Bias

Bias represents systematic error caused by an overly restrictive model.

A high-bias model is often too simple.

Variance

Variance represents sensitivity to the particular training dataset.

A high-variance model may fit training data extremely well but perform poorly on unseen data.

Decision trees are often high-variance models, especially when they are deep.

Ensemble methods can reduce this instability.

⸻

4. Main Ensemble Strategies

Three major ensemble ideas are particularly important:

1. Bagging
2. Random forests
3. Boosting

They combine models in different ways.

⸻

5. Bagging

Bagging stands for Bootstrap Aggregating.

The basic idea is:

Train multiple models on different bootstrap samples of the training data and combine their predictions.

A bootstrap sample is created by randomly sampling training examples with replacement.

Suppose the original dataset contains:

A B C D E

One bootstrap sample might be:

A C C D E

Another might be:

B B C D A

Each sample has the same number of observations as the original dataset, but some observations may appear multiple times while others may be absent.

⸻

6. Bagging Process

The process can be visualized as:

Original Training Data
        ↓
 ┌──────┼──────┐
 ↓      ↓      ↓
Boot.1 Boot.2 Boot.3
 ↓      ↓      ↓
Tree 1 Tree 2 Tree 3
 └──────┼──────┘
        ↓
   Combine Results
        ↓
 Final Prediction

For classification, predictions are commonly combined using majority voting.

For regression, predictions are commonly averaged.

⸻

7. Why Bagging Helps

Suppose individual models are unstable.

If one decision tree changes significantly when the training data changes slightly, its prediction can also change significantly.

Bagging trains many such trees on different bootstrap samples.

The individual trees may make different errors.

When their predictions are averaged or voted together, some of these errors can cancel out.

Therefore, bagging primarily helps reduce variance.

⸻

8. Random Forest

A Random Forest is an ensemble of decision trees that combines two sources of randomness:

1. Random samples of training examples
2. Random subsets of features

This makes random forests a specialized and highly effective form of bagging.

⸻

9. Random Feature Selection

In ordinary bagging, different trees may still repeatedly choose the same powerful features.

Random forests add another source of diversity.

When a tree considers a split, it only sees a randomly selected subset of features.

Conceptually:

All Features
     ↓
Random Feature Subset
     ↓
Choose Best Split

Different trees therefore have opportunities to build different structures.

⸻

10. Random Forest Process

A simplified random forest training process is:

Training Data
      ↓
Bootstrap Samples
      ↓
 ┌────┼────┬────┐
 ↓    ↓    ↓    ↓
Tree Tree Tree Tree
 ↓    ↓    ↓    ↓
Random feature subsets
      ↓
Combine predictions
      ↓
Final prediction

For classification:

Majority vote

For regression:

Average predictions

⸻

11. Why Random Forests Work

A random forest benefits from two ideas:

Averaging

Combining many trees reduces the influence of any individual tree.

Diversity

Random samples and random feature subsets make the trees less correlated.

This is important because averaging highly similar models provides less benefit than averaging models that make different errors.

Therefore:

Random forests aim to create many reasonably strong but diverse decision trees and combine them.

⸻

12. Boosting

Boosting takes a different approach from bagging.

Instead of training models independently, boosting trains models sequentially.

Each new model attempts to improve upon the weaknesses of the existing ensemble.

Conceptually:

Model 1
   ↓
Identify errors / residuals
   ↓
Model 2
   ↓
Focus on remaining errors
   ↓
Model 3
   ↓
Improve again
   ↓
Final Ensemble

The models are therefore dependent on one another.

⸻

13. Bagging vs Boosting

The fundamental difference is how the models are trained.

Bagging

Models are trained independently or approximately independently.

Data
 ├──→ Model 1
 ├──→ Model 2
 ├──→ Model 3
 └──→ Model 4
       ↓
    Combine

Boosting

Models are trained sequentially.

Data
 ↓
Model 1
 ↓
Model 2
 ↓
Model 3
 ↓
Model 4
 ↓
Combine

Therefore:

Bagging primarily reduces variance through averaging, while boosting builds a sequence of models that progressively improves the ensemble.

⸻

14. Gradient Boosting

Gradient Boosting is a boosting technique that builds an ensemble of weak learners, commonly shallow decision trees.

The key idea is that each new tree attempts to correct the errors made by the current ensemble.

For regression, this is often described in terms of fitting the residual errors.

For a more general formulation, gradient boosting fits the next model in the direction that reduces the chosen loss function.

⸻

15. Loss Function

A loss function measures how far the model’s predictions are from the desired targets.

Examples include:

* Mean Squared Error for regression
* Log loss for classification

Gradient boosting uses the loss function to determine how the ensemble should improve.

Conceptually:

Current Prediction
       ↓
Calculate Loss
       ↓
Determine Direction of Improvement
       ↓
Train Next Weak Learner
       ↓
Update Ensemble

⸻

16. Learning Rate

One of the important hyperparameters in gradient boosting is the learning rate.

The learning rate controls how strongly each new tree contributes to the final model.

A smaller learning rate means:

Small contribution per tree
        ↓
Usually requires more trees

A larger learning rate means:

Larger contribution per tree
        ↓
Fewer trees may be needed

The learning rate therefore interacts strongly with the number of estimators.

⸻

17. Number of Estimators

The number of estimators determines how many weak learners are added to the ensemble.

For example:

n_estimators = 100

means the ensemble contains 100 boosting stages/trees, depending on the implementation.

Increasing the number of estimators can improve performance when combined with an appropriately chosen learning rate, but excessive complexity can increase overfitting.

⸻

18. Tree Depth in Boosting

Boosted trees are often intentionally shallow.

A shallow tree acts as a weak learner.

Instead of trying to solve the entire problem with one complex tree, boosting gradually builds a strong model from many simpler trees.

Conceptually:

Weak Tree 1
    +
Weak Tree 2
    +
Weak Tree 3
    +
...
    =
Strong Ensemble

⸻

19. Gradient Boosting vs Random Forest

Although both use decision trees, their learning strategies are fundamentally different.

Property	Random Forest	Gradient Boosting
Main strategy	Bagging	Boosting
Trees	Trained independently	Trained sequentially
Main source of diversity	Data + feature randomness	Sequential error correction
Main strength	Variance reduction	Progressive error reduction
Tree depth	Often moderate/deeper	Often shallow
Training	Highly parallelizable	Sequential
Main risk	Overfitting with excessive complexity	Overfitting through excessive boosting

Neither approach is universally superior. Their behavior depends on the dataset, features, hyperparameters, and evaluation setup.

⸻

20. Weak Learners

A weak learner is a model that performs only modestly better than a simple baseline.

In boosting, weak learners are combined to construct a stronger predictor.

Decision stumps are an extreme example:

Tree depth = 1

A stump may make a very simple decision.

Boosting repeatedly adds such simple corrections.

⸻

21. Ensemble Diversity

One of the most important ideas in ensemble learning is diversity.

Suppose five models all make exactly the same mistakes.

Combining them does not provide much additional information.

But if they make different errors:

Model 1 → Error A
Model 2 → Error B
Model 3 → Error C
Model 4 → Error A
Model 5 → Error D

their predictions can complement one another.

This is why random forests introduce randomness into both:

* training samples
* feature selection

⸻

22. Voting

For classification, multiple models can be combined through voting.

Suppose three models predict:

Model 1 → Class A
Model 2 → Class B
Model 3 → Class A

The ensemble prediction can be:

Class A

because it received the majority of votes.

This is called majority voting.

⸻

23. Averaging

For regression, predictions can be combined through averaging.

Suppose:

Model 1 → 10
Model 2 → 12
Model 3 → 11

The ensemble prediction is:

(10 + 12 + 11) / 3 = 11

Averaging reduces the influence of individual model errors.

⸻

24. Important Hyperparameters

Ensemble methods contain several important hyperparameters.

Random Forest

Common examples:

* n_estimators
* max_depth
* max_features
* min_samples_split
* min_samples_leaf

Gradient Boosting

Common examples:

* n_estimators
* learning_rate
* max_depth
* min_samples_split
* min_samples_leaf
* subsample

The exact available parameters depend on the implementation.

⸻

25. Overfitting in Ensembles

Ensembles are generally more robust than individual decision trees, but they can still overfit.

For example, a random forest can become unnecessarily complex with too many unrestricted trees and overly flexible individual trees.

Gradient boosting can be particularly sensitive to:

* Too many estimators
* Excessive tree depth
* High learning rate
* Insufficient regularization

Therefore, hyperparameter tuning and validation are important.

⸻

26. Classical Ensemble Workflow

A typical workflow for comparing ensemble models is:

Dataset
   ↓
Train / Validation / Test Split
   ↓
Baseline Model
   ↓
Random Forest
   ↓
Gradient Boosting
   ↓
Evaluate on Validation Set
   ↓
Tune Hyperparameters
   ↓
Final Evaluation on Test Set

The test set should remain separate from model-selection decisions whenever possible.

⸻

27. Why Ensembles Matter for This Project

In this week’s YCB-Video classification task, ensemble methods provide an opportunity to compare models with different learning strategies.

The comparison includes:

* Logistic Regression
* Decision Tree
* Random Forest
* Boosted Tree

These models represent different ideas:

Logistic Regression
→ Linear decision boundary
Decision Tree
→ Hierarchical rule-based partitioning
Random Forest
→ Many randomized decision trees + averaging
Boosted Tree
→ Sequentially improved decision trees

This comparison helps demonstrate how increasing model complexity and combining models can affect:

* Accuracy
* Precision
* Recall
* F1-score
* Confusion matrix
* Generalization to unseen data
* Computational cost
* Interpretability

⸻

28. Key Takeaways

The central ideas of ensemble learning are:

Bagging

Train multiple models independently on different bootstrap samples and combine their predictions.

Random Forest

Combine bagging with random feature selection to create diverse decision trees.

Boosting

Train models sequentially so that later models improve the weaknesses of earlier models.

Gradient Boosting

Use gradient-based optimization of a loss function to progressively build a strong ensemble from weak learners.

The overall idea can be summarized as:

Single Model
     ↓
Potentially unstable / limited prediction
     ↓
Multiple Models
     ↓
Combine their information
     ↓
More robust ensemble

The most important conceptual distinction is:

Bagging tries to make predictions more stable by averaging diverse models, while boosting builds models sequentially to progressively improve the overall prediction.