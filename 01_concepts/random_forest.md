Random Forest

1. Overview

Random Forest is an ensemble machine learning algorithm based on multiple decision trees.

Instead of relying on one decision tree, Random Forest builds many trees and combines their predictions.

The central idea is:

Build many different decision trees and combine their predictions to produce a more robust model.

A Random Forest can be used for both:

* Classification
* Regression

For this week’s project, the focus is on classification.

⸻

2. Why Not Use One Decision Tree?

A single decision tree can be very sensitive to the training data.

A small change in the dataset can cause the tree to choose different splits and produce a substantially different structure.

This is a high-variance behavior.

For example:

Training Data
     ↓
Decision Tree
     ↓
Prediction

If the training data changes slightly:

Slightly Different Data
     ↓
Different Decision Tree
     ↓
Potentially Different Prediction

Random Forest addresses this instability by combining many trees.

⸻

3. Basic Idea

A Random Forest creates many decision trees.

Each tree is trained with some randomness introduced into the learning process.

Conceptually:

                    ┌── Tree 1 ──┐
                    ├── Tree 2 ──┤
Training Data ──────┼── Tree 3 ──┼──→ Combined Prediction
                    ├── Tree 4 ──┤
                    └── Tree 5 ──┘

The final prediction is determined by combining the predictions of the individual trees.

For classification, this is usually done through majority voting.

⸻

4. Two Sources of Randomness

The word Random in Random Forest is important.

Random Forest introduces randomness in two major ways:

1. Random sampling of training examples
2. Random selection of features when splitting nodes

These mechanisms encourage the trees to be different from one another.

⸻

5. Bootstrap Sampling

The first source of randomness is bootstrap sampling.

A bootstrap sample is created by sampling training examples with replacement.

Suppose the original dataset contains:

A B C D E

A bootstrap sample could be:

A C C E D

Another could be:

B B A D E

Notice that:

* Some samples can appear more than once.
* Some original samples may not appear in a particular bootstrap sample.

Each tree therefore sees a slightly different version of the training data.

⸻

6. Training Multiple Trees

Suppose we have 1,000 training examples.

Random Forest may create many bootstrap datasets from these examples.

Then:

Bootstrap Sample 1 → Tree 1
Bootstrap Sample 2 → Tree 2
Bootstrap Sample 3 → Tree 3
...
Bootstrap Sample N → Tree N

Each tree learns a somewhat different decision structure.

⸻

7. Random Feature Selection

Bootstrap sampling alone is not the only source of randomness.

At each split, Random Forest typically considers only a random subset of the available features.

Suppose the dataset contains:

Feature 1
Feature 2
Feature 3
Feature 4
Feature 5
Feature 6

A particular tree might consider:

Feature 1
Feature 3
Feature 5

at a particular split.

Another tree might consider:

Feature 2
Feature 4
Feature 6

This encourages different trees to learn different structures.

⸻

8. Why Feature Randomness Matters

Imagine one feature is extremely strong.

Without feature randomness, many trees could repeatedly choose that same feature for their important splits.

The resulting trees would become highly similar.

Highly similar trees tend to make similar errors.

Random feature selection reduces this correlation.

The goal is therefore not to make every tree individually perfect.

The goal is to create a collection of diverse trees whose errors are not perfectly correlated.

⸻

9. The Complete Training Process

A simplified Random Forest training process is:

Step 1 — Start with the training dataset

Training Data

Step 2 — Create bootstrap samples

Training Data
   ↓
Sample 1
Sample 2
Sample 3
...
Sample N

Step 3 — Train a decision tree on each sample

Sample 1 → Tree 1
Sample 2 → Tree 2
Sample 3 → Tree 3
...

During tree construction, each split considers a random subset of features.

Step 4 — Repeat

Continue until the desired number of trees has been trained.

Step 5 — Combine predictions

For classification:

Tree 1 → Class A
Tree 2 → Class B
Tree 3 → Class A
Tree 4 → Class A
Tree 5 → Class B

Final prediction:

Class A

because Class A received the majority of votes.

⸻

10. Majority Voting

For classification, each tree produces a class prediction.

The forest combines these predictions through voting.

Example:

Tree 1 → Object 1
Tree 2 → Object 1
Tree 3 → Object 3
Tree 4 → Object 1
Tree 5 → Object 3

Votes:

Object 1 → 3 votes
Object 3 → 2 votes

Final prediction:

Object 1

The individual tree predictions therefore become evidence for the final forest prediction.

⸻

11. Regression Random Forest

Random Forest can also be used for regression.

Instead of voting for a class, the predictions are usually averaged.

Example:

Tree 1 → 10
Tree 2 → 12
Tree 3 → 11
Tree 4 → 13

Final prediction:

(10 + 12 + 11 + 13) / 4 = 11.5

⸻

12. Why Random Forest Reduces Variance

Suppose individual trees have high variance.

Tree 1 may overpredict.

Tree 2 may underpredict.

Tree 3 may make a different mistake.

When these predictions are combined, the influence of individual errors is reduced.

Conceptually:

High-variance Tree
        ↓
        ↓
Many diverse trees
        ↓
      Average
        ↓
Reduced variance

This is one of the main reasons Random Forest is often more stable than a single decision tree.

⸻

13. Correlation Between Trees

A particularly important concept is correlation.

If all trees are nearly identical:

Tree 1 → same behavior
Tree 2 → same behavior
Tree 3 → same behavior

then combining them provides limited benefit.

If the trees are diverse:

Tree 1 → Error A
Tree 2 → Error B
Tree 3 → Error C
Tree 4 → Correct

their errors can partially cancel when predictions are combined.

Therefore, Random Forest tries to balance:

* Strong individual trees
* Diversity between trees

⸻

14. Important Hyperparameters

Several hyperparameters control Random Forest behavior.

n_estimators

The number of trees in the forest.

Example:

n_estimators = 100

means the forest contains 100 trees.

Increasing the number of trees generally makes the ensemble more stable, although it also increases computation.

⸻

max_depth

Controls the maximum depth of each tree.

Smaller values:

* Simpler trees
* Lower model complexity
* Potentially more bias

Larger values:

* More complex trees
* Potentially lower bias
* Greater risk of overfitting

⸻

max_features

Controls how many features are considered when searching for a split.

This parameter is particularly important because it directly affects tree diversity.

Smaller feature subsets generally increase randomness.

Larger feature subsets make individual trees more informed but potentially more correlated.

⸻

min_samples_split

The minimum number of samples required to split an internal node.

Increasing this value can prevent very small, highly specific splits.

⸻

min_samples_leaf

The minimum number of samples required in a leaf.

Increasing it can make trees smoother and less sensitive to individual observations.

⸻

15. Out-of-Bag Samples

Because bootstrap sampling uses sampling with replacement, some training examples are not selected for a particular tree.

These samples are called out-of-bag (OOB) samples for that tree.

Conceptually:

Original Training Set
       ↓
Bootstrap Sample
       ↓
Selected samples → Train tree
Unselected samples → OOB

OOB samples can be used to estimate model performance without creating a separate validation set for this purpose.

This is known as OOB evaluation.

⸻

16. Feature Importance

Random Forest can provide estimates of feature importance.

Feature importance attempts to answer:

Which features contributed most to the model’s decisions?

For example:

Feature A → high importance
Feature B → medium importance
Feature C → low importance

This can be useful for understanding the model and analyzing which characteristics of the YCB-Video samples are most informative.

However, feature importance should not automatically be interpreted as causal importance.

A feature being important to the model does not mean that it causes the target.

⸻

17. Advantages

Random Forest has several useful properties:

* Usually more stable than a single decision tree
* Can model nonlinear relationships
* Captures feature interactions
* Does not require feature scaling
* Works well as a strong classical baseline
* Can estimate feature importance
* Can reduce the variance of individual trees
* Often performs well with relatively little preprocessing

⸻

18. Limitations

Random Forest also has limitations:

* Less interpretable than a single tree
* Requires more computation than one tree
* Can use substantial memory when many trees are created
* Individual predictions are harder to explain
* Feature importance measures can be misleading in some situations
* More trees do not automatically solve poor feature representation

A Random Forest cannot create useful information that is absent from the input features.

⸻

19. Random Forest vs Decision Tree

Property	Decision Tree	Random Forest
Number of trees	One	Many
Training data	One dataset	Bootstrap samples
Feature selection	All/available features	Random feature subsets
Variance	Often high	Generally reduced
Interpretability	High	Lower
Stability	Lower	Higher
Computational cost	Lower	Higher

The Random Forest can therefore be viewed as a way of turning many unstable decision trees into a more robust ensemble.

⸻

20. Application to the YCB-Video Project

For this week’s YCB-Video classification task, Random Forest will use the same feature set used by the other comparison models.

The important experimental principle is:

Change the model, not the data pipeline.

The same:

* Features
* Labels
* Train/validation/test split
* Evaluation metrics

should be used when comparing Random Forest with Logistic Regression, Decision Tree, and Gradient Boosting.

This makes the comparison more meaningful.

⸻

21. Key Takeaway

Random Forest combines many decision trees using two major sources of randomness:

Bootstrap Samples
       +
Random Feature Subsets
       ↓
Diverse Decision Trees
       ↓
Majority Voting
       ↓
Final Prediction

Its main conceptual purpose is to reduce the instability of individual decision trees while preserving their ability to model nonlinear relationships.