---
title: "Exploring performance metrics of classification algorithms"
date: "2020-02-19"
categories: 
  - "classification"
  - "data-science"
  - "machine-learning"
  - "python3"
tags: 
  - "artificial-neural-network"
  - "income-class-classification"
  - "pandas"
  - "random-forest"
  - "scikit-learn"
  - "support-vector-machines"
---

In this post, we will explore the various performance metrics for classification algorithms. We will use a popular dataset to predict income class (whether a person of the population makes more than 50K or not). The dataset is available on UCI Machine Learning database: https://archive.ics.uci.edu/ml/datasets/census+income.

The prediction task involves the following standard steps:

1. loading the training data,
2. conduct exploratory data analysis,
3. conduct some preprocessing and cleaning,
4. fit classification models to training data,
5. make predictions on the test data,
6. the performance of the models using metrics.

We will start by first loading the important modules and the training dataset. Pandas and scikit-learn are the important modules we will be using here.

<script src="https://gist.github.com/ajey091/506a6825b6bce6b2f1d27babf30f854d.js"></script>

![Screen Shot 2020-02-19 at 12.33.46 PM.png](/assets/images/screen-shot-2020-02-19-at-12.33.46-pm.png)

Our input data consists of both categorical and numeric features. The last column is the dependent variable. We have to do a few things now - separate the raw data into independent features and dependent feature (label), identify if any features are double counted or are irrelevant, then encode the categorical features and the output label.

<script src="https://gist.github.com/ajey091/a66cbb5c90805a29fea3dcc7f618fe5f.js"></script>

![Screen Shot 2020-02-19 at 12.40.42 PM.png](/assets/images/screen-shot-2020-02-19-at-12.40.42-pm.png)

We see that the feature fnlwgt is not correlated at all with the output class, so we can safely drop that feature. Also, we see that there are two features describing eduction level - "education" and "education_num". So, we can drop the categorical feature "education".

<script src="https://gist.github.com/ajey091/e17f558ad983396c73e0d6683226e16b.js"></script>

![Screen Shot 2020-02-19 at 12.41.47 PM.png](/assets/images/screen-shot-2020-02-19-at-12.41.47-pm.png)

We note that we have both categorical features and numerical features. The categorical features are encoded using OneHotEncoder, which is the standard encoder used for non-cardinal features.

<script src="https://gist.github.com/ajey091/9366ce609ab947811adecc4a12b78168.js"></script>

We would ideally like to use OneHotEncoder to encode the categorical features (since none of them have any cardinality). But, in one of the features, there are more distinct values in the training data than in the test data. So, if we apply OneHotEncoder to the two datasets separately, there is one more column in the training data than in the test data. One way to overcome this is to combine the two datasets, apply the encoder on the combined dataset, and then separate the training and test datasets, as below:

<script src="https://gist.github.com/ajey091/650d427f7c76a687aeafe2bc7240e21d.js"></script>

Shown below is a snippet of the output:

![Screen Shot 2020-02-19 at 12.43.59 PM.png](/assets/images/screen-shot-2020-02-19-at-12.43.59-pm.png)

We're almost ready to train models with the dataset. One last step is to normalize/scale the features such that they are of comparable magnitudes. We will use StandardScaler for this purpose. Further, we will apply a series of standard classification algorithms.

<script src="https://gist.github.com/ajey091/12bf201a3983aab591ddcbdae81d4c08.js"></script>

<script src="https://gist.github.com/ajey091/3c84aed799cb7549a4f37e1ded03f745.js"></script>

<script src="https://gist.github.com/ajey091/56f639216a9c1f787ece1c3a9b66d3c6.js"></script>

<script src="https://gist.github.com/ajey091/bc2d564ee6327796cd77585dbef3eea2.js"></script>

<script src="https://gist.github.com/ajey091/c927d04b1fecfe64dd0c684a82bd5ada.js"></script>

Now, we have fit the training data to many classification algorithms with some standard parameters, and calculated probabilities. We will use these for evaluating the models.

<script src="https://gist.github.com/ajey091/df895f8b524f4ffe1d0aa9c9c8073f96.js"></script>

![Screen Shot 2020-02-19 at 12.52.11 PM.png](/assets/images/screen-shot-2020-02-19-at-12.52.11-pm.png)

In summary, we have used four different machine learning algorithms to make predictions about the income class. All four classification models give reasonable accuracies, with Random Forest algorithm providing the best accuracy. We also used area under the ROC curve as a metric and we saw that Random Forest performs best again. We can definitely perform much better on these models with some parameter tuning, which we will undertake in an upcoming post.
