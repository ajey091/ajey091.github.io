---
title: "Improving the performance of classification models"
date: "2020-02-23"
categories: 
  - "classification"
  - "data-science"
tags: 
  - "grid-search"
  - "python"
---

This post is a continuation of the [previous post](https://ajeyvenkataraman.com/2020/02/19/exploring-performance-metrics-of-classification-algorithms/), where a few classification algorithms were used to predict the income class. Here, we will take several steps to improve the prediction accuracy. Just to reiterate, we will use a popular dataset to predict income class (whether a person of the population makes more than 50K or not). The dataset is available on UCI Machine Learning database: [https://archive.ics.uci.edu/ml/datasets/census+income](https://archive.ics.uci.edu/ml/datasets/census+income).

We will pick up where we left off in the previous post. We found that Random Forest classifier gave the best performance among the four classifiers used.

<script src="https://gist.github.com/ajey091/63e64a366777d80fe72fe32b67746e76.js"></script>

`Random Forest: Baseline accuracy=0.857`

We will use three different approaches to attempt to improve the predictions:

1. [GridSearchCV](https://scikit-learn.org/stable/modules/grid_search.html) - an exhaustive search in the parameter space to find the best parameters.
2. [Ensemble methods](https://scikit-learn.org/stable/modules/ensemble.html) - an ensemble of many base estimators are used to improve the performance of prediction.
3. Additional feature engineering - we did some feature engineering already in the previous post, but we will go into more detail here.

## Additional Feature Engineering

<script src="https://gist.github.com/ajey091/9463b4bea0826173bcf51bef129e27cf.js"></script>

![feature1.png](/assets/images/feature1.png)

![feature2.png](/assets/images/feature2.png)

<script src="https://gist.github.com/ajey091/1b87f7e499f984d2dc48b3e88ddd46ba.js"></script>

![feature3.png](/assets/images/feature3.png)

We will first use GridSearch to find the best parameters to improve the performance of the Random Forest classifier.

<script src="https://gist.github.com/ajey091/7aa0b9a8164eef97dda34ce10ae005f4.js"></script>

`{'bootstrap': True, 'max_depth': 20, 'max_features': 3, 'min_samples_leaf': 3, 'min_samples_split': 8, 'n_estimators': 1000}`

`Random Forest: Grid Search accuracy=0.864`

Next, we will use ensemble methods starting with AdaBoost, where we fit a classifier with 1000 weak learners:

<script src="https://gist.github.com/ajey091/c9614a81bd2124b231783d0765e02392.js"></script>

`AdaBoost accuracy=0.862`

This is not better than the parameter-optimized Random Forest algorithm.

[Gradient Tree Boosting](https://en.wikipedia.org/wiki/Gradient_boosting) is a generalization of boosting to arbitrary differentiable loss functions.

<script src="https://gist.github.com/ajey091/1be0f3c74d326a6e45e0b95427460625.js"></script>

`Gradient Boosting classifier accuracy=0.862`

There's so much more we can do with the dataset but this has already been a long post. More to come next time.
