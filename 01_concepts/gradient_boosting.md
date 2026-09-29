Gradient Boosting

1. Overview

Gradient Boosting is an ensemble machine learning method that builds a strong predictive model by combining many relatively simple models, usually decision trees.

Unlike Random Forest, where trees are trained independently, Gradient Boosting trains models sequentially.

The central idea is:

Each new tree is trained to improve the current ensemble.

The model therefore grows step by step.

Tree 1
  ↓
Current Ensemble
  ↓
Tree 2 corrects remaining errors
  ↓
Updated Ensemble
  ↓
Tree 3 improves it further
  ↓
...
  ↓
Final Ensemble

⸻

2. Why Boosting?

A single shallow decision tree may be too simple to model a complex relationship.

Instead of creating one extremely complicated tree, boosting combines many simple trees.

For example:

Weak Tree 1
      +
Weak Tree 2
      +
Weak Tree 3
      +
Weak Tree 4
      +
...
      =
Strong Model

Each tree contributes only part of the final solution.

⸻

3. Weak Learners

Gradient Boosting commonly uses small decision trees as weak learners.

A weak learner does not need to solve the entire prediction problem.

Instead, it should capture a useful part of the remaining pattern.

For example:

Tree 1 → learns major pattern
Tree 2 → improves mistakes
Tree 3 → improves remaining mistakes
Tree 4 → improves further

The final model is strong because the learners work together.

⸻

4. Sequential Learning

The defining characteristic of Gradient Boosting is sequential training.

Random Forest:

Tree 1 ─┐
Tree 2 ─┤
Tree 3 ─┼→ Combine
Tree 4 ─┤
Tree 5 ─┘

Gradient Boosting:

Tree 1
  ↓
Tree 2
  ↓
Tree 3
  ↓
Tree 4
  ↓
Tree 5

The next tree depends on what the previous trees have already learned.

⸻

5. The Current Ensemble

Suppose the first tree creates an initial prediction.

The model evaluates how well that prediction matches the target.

There will generally be some error.

The next tree is then trained to capture information that can improve the current prediction.

Conceptually:

Initial Model
     ↓
Prediction
     ↓
Measure Error
     ↓
Train New Tree
     ↓
Add Tree to Ensemble
     ↓
Improved Prediction

This process repeats.

⸻

6. Residuals

For regression, the idea can be understood especially clearly through residuals.

A residual is the difference between the actual value and the current prediction.

Conceptually:

Residual = Actual - Prediction

Suppose:

Actual = 100
Prediction = 80

The residual is:

20

The next tree can learn patterns in these residuals.

After adding the new tree, the ensemble’s prediction should move closer to the target.

⸻

7. General Gradient-Based View

The residual explanation is intuitive for regression, but Gradient Boosting is more general.

The algorithm works by examining the loss function and determining the direction in which the current model should change to reduce that loss.

This is why the method is called:

Gradient Boosting

The gradient provides information about how the loss changes with respect to the model’s predictions.

The next learner is trained to approximate this improvement direction.

⸻

8. Loss Function

A loss function measures how bad the current predictions are.

Different tasks can use different loss functions.

Examples include:

* Squared error for regression
* Log loss for classification

Conceptually:

Predictions
     ↓
Loss Function
     ↓
Measure Error
     ↓
Gradient
     ↓
Next Tree

The objective of training is to progressively reduce the loss.

⸻

9. Additive Model

Gradient Boosting builds the final model additively.

Instead of replacing the previous model, each new tree is added to the existing ensemble.

Conceptually:

F₀(x)
  ↓
F₁(x) = F₀(x) + Tree₁(x)
  ↓
F₂(x) = F₁(x) + Tree₂(x)
  ↓
F₃(x) = F₂(x) + Tree₃(x)

In practice, the contribution of each new tree is controlled by the learning rate.

⸻

10. Learning Rate

The learning rate determines how strongly each new tree influences the ensemble.

A small learning rate means that each tree makes a relatively small correction.

Small learning rate
      ↓
Small update per tree
      ↓
Usually more trees required

A large learning rate produces larger updates.

Large learning rate
      ↓
Larger update per tree
      ↓
Fewer trees may be required

The learning rate therefore interacts with n_estimators.

⸻

11. Number of Estimators

n_estimators controls the number of boosting stages.

For example:

n_estimators = 100

means that the ensemble will perform 100 boosting stages, with the exact interpretation depending on the implementation.

A useful conceptual relationship is:

Smaller learning rate
        ↕
More estimators

and:

Larger learning rate
        ↕
Fewer estimators

These parameters should generally be considered together.

⸻

12. Tree Depth

Boosted trees are often shallow.

For example:

max_depth = 2

produces relatively simple trees.

Why use shallow trees?

Because boosting is based on many small corrections.

If every tree were extremely complex, the model could learn the training data too aggressively.

Therefore, controlling tree depth is an important form of regularization.

⸻

13. Gradient Boosting Classification

For classification, Gradient Boosting does not simply train a tree to predict the final class independently at every stage.

Instead, the ensemble progressively improves its prediction according to the chosen classification loss.

A simplified conceptual process is:

Initial prediction
      ↓
Calculate classification loss
      ↓
Find direction of improvement
      ↓
Train tree
      ↓
Update model
      ↓
Calculate new loss
      ↓
Train next tree
      ↓
Repeat

The final ensemble combines the contributions of all boosting stages.

⸻

14. Gradient Boosting vs Random Forest

Both methods use decision trees, but their philosophies are different.

Random Forest

Random Forest asks:

How can I combine many diverse trees so that their errors become less harmful?

It relies heavily on:

* Bootstrap sampling
* Random feature selection
* Averaging/voting

Gradient Boosting

Gradient Boosting asks:

How can the next tree improve the errors of the current ensemble?

It relies heavily on:

* Sequential learning
* Loss minimization
* Gradient information
* Small incremental updates

⸻

15. Comparison

Property	Random Forest	Gradient Boosting
Training strategy	Parallel/independent trees	Sequential trees
Main idea	Reduce variance	Correct errors progressively
Tree relationship	Mostly independent	Dependent on previous ensemble
Random feature selection	Core mechanism	Not the defining mechanism
Bootstrap sampling	Core mechanism	Not required
Learning rate	Not central	Very important
n_estimators	Number of trees	Number of boosting stages
Typical trees	Often larger	Often shallow
Training speed	Highly parallelizable	More sequential
Overfitting control	Tree/forest parameters	Depth, learning rate, estimators, etc.

⸻

16. Overfitting

Gradient Boosting can achieve very strong performance, but it can also overfit.

Overfitting can occur when:

* Trees are too deep
* Too many boosting stages are used
* Learning rate is too high
* Regularization is insufficient

A typical conceptual pattern is:

Training performance
        ↑
        │
        │───────────────
        │
        │
        └────────────────→ Model complexity

Training performance can continue improving while validation performance eventually stops improving or becomes worse.

Therefore, validation data is important for selecting appropriate hyperparameters.

⸻

17. Important Hyperparameters

n_estimators

Number of boosting stages.

More stages allow the model to make more incremental corrections.

⸻

learning_rate

Controls the contribution of each tree.

Smaller values generally require more estimators.

⸻

max_depth

Controls the complexity of the individual trees.

Smaller values produce weaker, simpler learners.

⸻

min_samples_split

Controls the minimum number of samples required to split a node.

It can help prevent overly specific branches.

⸻

min_samples_leaf

Controls the minimum number of samples in a leaf.

Larger values can make the individual trees less flexible.

⸻

subsample

In implementations that support it, subsample controls the fraction of training samples used for each boosting stage.

Using less than the full dataset can introduce additional randomness and may help regularization.

⸻

18. Regularization

Gradient Boosting requires careful control of model complexity.

Important regularization mechanisms include:

* Smaller tree depth
* Smaller learning rate
* Limiting the number of estimators
* Minimum samples per leaf
* Subsampling where supported

The objective is not simply to minimize training error.

The objective is to obtain good generalization to unseen data.

⸻

19. Early Stopping

Early stopping is a strategy for preventing unnecessary boosting stages.

The model’s performance is monitored on validation data.

If performance stops improving for a certain number of iterations, training can be stopped.

Conceptually:

Boosting stage
     ↓
Validation performance
     ↓
Improving?
 ┌───┴───┐
Yes      No
 ↓        ↓
Continue  Stop

This can help prevent overfitting and reduce unnecessary computation.

⸻

20. Advantages

Gradient Boosting has several important advantages:

* Can model nonlinear relationships
* Can capture complex feature interactions
* Often provides strong predictive performance
* Can combine many weak learners into a powerful model
* Supports different loss functions
* Provides useful feature-importance information in many implementations

⸻

21. Limitations

Gradient Boosting also has limitations:

* Training is sequential and therefore less easily parallelized than Random Forest
* Hyperparameters can have a large effect on performance
* Can overfit if model complexity is not controlled
* Training can be computationally expensive
* The final ensemble is harder to interpret than a single decision tree

⸻

22. Gradient Boosting and XGBoost

XGBoost is a highly optimized implementation and extension of the gradient boosting idea.

It introduces additional engineering and regularization techniques designed to improve:

* Training efficiency
* Model performance
* Scalability
* Overfitting control

The conceptual foundation remains gradient boosting:

Current Ensemble
      ↓
Calculate how to improve it
      ↓
Train another tree
      ↓
Add the tree
      ↓
Repeat

For this week’s project, the important concept is understanding gradient boosting itself before using a boosted-tree implementation.

⸻

23. Application to the YCB-Video Project

The boosted-tree model will be evaluated using the same experimental setup as the other models.

The comparison should keep constant:

* Dataset
* Feature extraction
* Target labels
* Train/validation/test split
* Evaluation metrics
* Test set

Only the model should change.

This allows the project to investigate whether the sequential error-correction strategy of boosting provides an advantage over:

* Logistic Regression
* Decision Tree
* Random Forest

⸻

24. Key Takeaway

Gradient Boosting builds a strong model step by step.

The central loop is:

Start with an initial model
        ↓
Measure the current error/loss
        ↓
Train a small decision tree
        ↓
Add a controlled correction
        ↓
Update the ensemble
        ↓
Repeat

The most important concepts are:

* Sequential learning
* Weak learners
* Loss function
* Gradient
* Residuals
* Learning rate
* Number of estimators
* Tree depth
* Regularization
* Early stopping

The fundamental distinction from Random Forest is:

Random Forest reduces instability by averaging many diverse trees, while Gradient Boosting builds an ensemble sequentially, with each new tree improving the current model.