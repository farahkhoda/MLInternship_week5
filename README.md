ML Internship — Week 5

Overview

This week focuses on Advanced Learning Algorithms and their application to the YCB-Video dataset.

The main topics covered are:

* Decision Trees
* Tree splitting and decision boundaries
* Entropy, Gini impurity, and information gain
* Overfitting, tree depth, and pruning
* Ensemble learning
* Bagging and Random Forest
* Feature randomness
* Boosting and Gradient Boosting
* Model comparison and evaluation
* Cross-scene generalization

Neural networks are excluded from this week’s work.

Project

The practical project compares four classical machine learning models using the same handcrafted feature set extracted from YCB-Video:

* Logistic Regression
* Decision Tree
* Random Forest
* Gradient Boosting

The models are evaluated using both:

1. Random frame-level splitting
2. Scene-level splitting with a held-out test scene

The second evaluation is used to investigate whether models generalize to an unseen scene.

Repository Structure

MLInternship_week5/
│
├── 01_concepts/
│   ├── decision_trees.md
│   ├── ensemble_methods.md
│   ├── random_forest.md
│   ├── gradient_boosting.md
│   └── README.md
│
├── 02_implementations/
│   └── ycbvideo_model_comparison.ipynb
│
├── 03_model_comparison/
│   ├── results/
│   │   ├── comparison_table.csv
│   │   └── performance_metrics.csv
│   └── comparison_report.md
│
├── data/
│   └── ycbv/
│
├── README.md
└── weekly_summary.md

Dataset

The project uses the YCB-Video BOP19 test dataset.

The extracted features include:

* RGB mean and standard deviation
* Bounding-box width and height
* Aspect ratio
* Bounding-box area ratio

The target variable is obj_id.

Key Focus

A major focus of this week’s project is understanding the difference between high performance on randomly split frames and generalization to an unseen scene.

The results show that random frame-level evaluation can produce overly optimistic performance, while scene-level evaluation reveals substantial generalization challenges.

For detailed methodology, results, failure analysis, and limitations, see:

03_model_comparison/comparison_report.md
