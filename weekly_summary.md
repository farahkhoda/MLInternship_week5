Week 5 — Weekly Summary

Main Quest: Advanced Learning Algorithms

This week focused on understanding and implementing classical machine learning algorithms beyond basic linear models.

Topics Studied

* Decision Trees
* Tree splitting
* Decision boundaries
* Entropy
* Gini impurity
* Information gain
* Tree depth and overfitting
* Pruning and regularization
* Ensemble learning
* Bagging
* Random Forest
* Feature randomness
* Boosting
* Gradient Boosting
* Model and hyperparameter comparison

Neural-network topics were intentionally excluded from this week’s scope.

⸻

Practical Project: YCB-Video Model Comparison

The practical part of the week used the YCB-Video BOP19 dataset to compare classical classification models.

Four models were implemented using the same handcrafted feature set:

1. Logistic Regression
2. Decision Tree
3. Random Forest
4. Gradient Boosting

This allowed the models to be compared under the same data and feature conditions.

Feature Set

The models used ten handcrafted features:

* mean_r
* mean_g
* mean_b
* std_r
* std_g
* std_b
* bbox_width
* bbox_height
* aspect_ratio
* area_ratio

The target variable was obj_id.

⸻

Evaluation Strategy

Two different evaluation strategies were used.

1. Random Frame-Level Split

Frames were randomly divided into training and test sets.

All four models achieved approximately 100% test accuracy under this setup.

This result demonstrated that the classification task was very easy when frames from the same scenes could appear in both training and test sets.

2. Scene-Level Split

A stricter evaluation was then performed by keeping an entire scene completely unseen during training.

* Validation scene: 000059
* Held-out test scene: 000048

The training data came from other scenes.

This setup was used to measure cross-scene generalization.

⸻

Main Results

Scene-level test accuracy on the held-out scene was substantially lower:

Model	Random-Split Test	Scene-Level Test
Logistic Regression	100.00%	24.27%
Decision Tree	100.00%	28.80%
Random Forest	100.00%	19.73%
Gradient Boosting	100.00%	21.33%

The large performance drop shows that random frame-level evaluation did not accurately represent the difficulty of generalizing to an unseen scene.

⸻

Failure Analysis

The held-out test scene contained five object classes:

1, 6, 14, 19, 20

The models did not generalize equally across these classes.

A particularly important observation was that class 19 was completely misclassified by all four models in the held-out scene.

Class 1 was also poorly recognized by most models, while class 20 was relatively easier for some models.

These results indicate that the main challenge was not simply choosing a more sophisticated classical algorithm.

⸻

Important Findings

Random Splits Can Be Misleading

The 100% random-split accuracy initially suggested that the features were highly effective.

However, scene-level evaluation revealed a large generalization gap.

This demonstrates why the choice of train/test split is especially important for video datasets, where consecutive frames are highly correlated.

Model Complexity Does Not Guarantee Better Generalization

Decision Trees, Random Forests, and Gradient Boosting were able to fit the training data extremely well, but their performance on the unseen scene remained low.

The results suggest that increasing model complexity cannot compensate for weak or scene-dependent feature representations.

Feature Representation Is a Major Limitation

The current features are simple handcrafted RGB and bounding-box statistics.

They capture basic appearance and geometry but do not provide a sufficiently robust representation of object identity across different scenes.

Another limitation is that RGB statistics are calculated from bounding-box crops and may therefore include background pixels.

⸻

Overall Outcome

This week’s work provided practical experience with:

* Decision Tree classification
* Ensemble methods
* Random Forests
* Gradient Boosting
* Hyperparameter analysis
* Feature importance
* Confusion matrices
* Failure analysis
* Model comparison
* Cross-scene evaluation
* Generalization analysis

The most important lesson from the project was that evaluation methodology matters as much as model performance.

A model can achieve excellent accuracy on a random frame split while performing poorly when evaluated on a genuinely unseen scene.

The complete experimental methodology, detailed metrics, confusion matrices, failure analysis, and limitations are documented in:

03_model_comparison/comparison_report.md