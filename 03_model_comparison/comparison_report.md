YCB-Video Classical Model Comparison

1. Overview

This report evaluates four classical machine learning models on the YCB-Video BOP19 dataset:

* Logistic Regression
* Decision Tree
* Random Forest
* Gradient Boosting

The models were trained using the same handcrafted RGB and bounding-box features. The goal was to compare classical classification approaches and investigate their ability to generalize from known scenes to an unseen scene.

⸻

2. Dataset and Features

The experiments used the YCB-Video BOP19 test scenes available in the project.

The input representation consisted of 10 handcrafted features:

* Mean R, G, and B values
* Standard deviation of R, G, and B values
* Bounding-box width
* Bounding-box height
* Bounding-box aspect ratio
* Bounding-box area ratio

The target variable was obj_id.

scene_id and frame_id were retained for traceability but were not used as model features.

⸻

3. Models

Four classification approaches were evaluated.

Logistic Regression

Used as a linear baseline. Standardization was applied before classification.

Decision Tree

Used to study nonlinear decision boundaries, tree depth, splitting behavior, and feature importance.

Random Forest

Used as a bagging ensemble of decision trees with feature randomness.

Gradient Boosting

Used as a sequential boosting approach in which successive trees improve the errors of previous learners.

⸻

4. Evaluation Strategy

Two evaluation strategies were used.

Random Frame-Level Split

Frames were randomly divided into training and test sets using stratification.

This evaluation produced very high performance, but samples from the same scene can occur in both training and test sets.

Scene-Level Evaluation

A complete scene was held out from training.

* Validation scene: 000059
* Held-out test scene: 000048

This evaluation was used to investigate cross-scene generalization.

⸻

5. Random-Split Results

All four models achieved 100% test accuracy under the random frame-level split.

Model	Test Accuracy
Logistic Regression	100.00%
Decision Tree	100.00%
Random Forest	100.00%
Gradient Boosting	100.00%

The identical performance across all models suggests that the random split was relatively easy for this feature representation.

However, this result should not be interpreted as evidence that the models generalize well to unseen scenes.

⸻

6. Scene-Level Results

The scene-level evaluation produced substantially lower performance.

Model	Train Accuracy	Validation Accuracy	Held-out Test Accuracy	Macro F1
Logistic Regression	98.22%	51.11%	24.27%	0.0971
Decision Tree	100.00%	44.67%	28.80%	0.1221
Random Forest	100.00%	54.44%	19.73%	0.1196
Gradient Boosting	100.00%	39.56%	21.33%	0.0907

The large difference between training performance and unseen-scene performance indicates limited cross-scene generalization.

⸻

7. Generalization Analysis

The difference between random-split and scene-level performance was substantial for all models.

Model	Random Split	Scene-Level	Accuracy Drop
Logistic Regression	100.00%	24.27%	75.73%
Decision Tree	100.00%	28.80%	71.20%
Random Forest	100.00%	19.73%	80.27%
Gradient Boosting	100.00%	21.33%	78.67%

This demonstrates that random frame-level evaluation can provide an overly optimistic estimate when highly related frames from the same scene are distributed across training and testing sets.

The scene-level experiment provides a more challenging evaluation of whether the learned feature patterns transfer to a new scene.

⸻

8. Confusion Matrix Analysis

The held-out test scene 000048 contains five object classes:

[1, 6, 14, 19, 20]

The confusion matrices showed substantial class-specific errors.

One particularly consistent observation was the difficulty of recognizing class 19. All four models failed to correctly classify this class in the held-out scene.

Class 1 was also poorly recognized by most models.

Class 20 showed relatively stronger recognition, particularly for Gradient Boosting.

These results indicate that overall accuracy alone does not fully describe model behavior across individual object classes.

⸻

9. Failure Analysis

Per-class analysis showed substantial variation between object classes.

Logistic Regression

* Class 6 was classified correctly in all test samples.
* Classes 1, 14, 19, and 20 had high error rates.
* The model frequently predicted classes that were not present in the held-out scene.

Decision Tree

* Classes 19 and 1 were not correctly recognized.
* Classes 14 and 20 showed relatively better recognition.
* The tree became considerably more complex under scene-level training, reaching depth 15 and 79 leaves.

Random Forest

* Class 19 and class 1 were not correctly recognized.
* Class 20 had comparatively stronger recognition.
* The ensemble did not eliminate the cross-scene generalization problem.

Gradient Boosting

* Class 19 was not correctly recognized.
* Class 20 had the strongest recognition among the five held-out classes for this model.
* Overall scene-level performance remained low.

The repeated failure on particular classes suggests that the main limitation may not be the choice of classifier alone.

⸻

10. Feature Importance

Feature importance varied depending on the evaluation setting.

Under the random frame-level split, aspect_ratio was particularly important for the tree-based models.

Under scene-level training, importance was more distributed across geometric and RGB features, including:

* aspect_ratio
* area_ratio
* bbox_height
* mean_r
* mean_b
* mean_g

This difference suggests that the feature patterns learned from individual scenes do not necessarily remain stable across different scenes.

Feature importance should therefore be interpreted as an indication of model behavior on the training data rather than proof that a feature is universally robust.

⸻

11. Model Strengths and Weaknesses

Logistic Regression

Strengths

* Simple and fast
* Easy to interpret
* Useful as a linear baseline

Weaknesses

* Limited to linear decision boundaries
* Poor cross-scene generalization with the current features

Decision Tree

Strengths

* Highly interpretable decision rules
* Captures nonlinear relationships
* Provides direct feature importance

Weaknesses

* Can overfit
* Sensitive to scene-specific patterns
* Became substantially more complex under scene-level training

Random Forest

Strengths

* Reduces variance through ensemble learning
* Captures nonlinear relationships
* Uses both bootstrap sampling and feature randomness

Weaknesses

* More complex and less interpretable than a single tree
* Did not solve the cross-scene generalization problem in this experiment

Gradient Boosting

Strengths

* Captures nonlinear relationships
* Sequentially improves weak learners
* Provides feature importance

Weaknesses

* More sensitive to hyperparameters
* More complex than a simple linear model
* Showed weak generalization to the held-out scene with the current features

⸻

12. Limitations

Several limitations should be considered when interpreting these results.

Random Frame Splitting

Frames from the same scene can be visually similar. Randomly distributing them between training and test sets can therefore lead to overly optimistic performance.

Limited Scene-Level Evaluation

Only one validation scene and one held-out test scene were used. Therefore, the scene-level results should be treated as observations from this experiment rather than definitive performance estimates across the entire dataset.

Simple Handcrafted Features

The feature representation contains only RGB statistics and bounding-box geometry. These features may not capture enough information to reliably distinguish objects across different scenes.

Bounding-Box Based RGB Statistics

RGB statistics are calculated from the bounding-box crop and may include background pixels. Changes in background, lighting, or object placement can therefore affect the extracted features.

Different Class Composition

The held-out scene does not contain all 21 object classes used during training. The model can therefore predict object classes that are absent from the target scene, contributing to the observed errors.

⸻

13. Conclusion

The experiments demonstrated that all four classical models can achieve perfect performance under a random frame-level split using the current handcrafted feature representation.

However, performance dropped substantially when evaluated on an unseen scene.

This difference highlights the importance of scene-aware evaluation for this dataset. The results suggest that the current RGB and bounding-box features capture patterns that are effective within the sampled scenes but do not generalize reliably to a completely unseen scene.

Overall, the experiment shows that model selection alone is not sufficient to solve the generalization problem. Improving the feature representation and using more robust scene-level evaluation would be important directions for future work.

Neural networks were intentionally excluded from this experiment according to the Week 5 scope.