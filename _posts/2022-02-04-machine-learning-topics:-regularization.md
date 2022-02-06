---
layout: post
image: /assets/images/Test_image.jpeg
---

The central challenge in machine learning is that our trained algorithm must perform well on new, previously unseen data — not just those on which our model was trained. This ability for the model to perform well on previously unobserved inputs is called generalization. Although machine learning models almost always perform better on the training samples than unseen data, the goal is to maintain a modest discrepancy between training error and generalization error. This essentially suggests that our model has to be sophisticated enough to model the complex relationships between our features and the target, while not overfitting to the training data and hence not generalizing to unseen data.

This problem of overfitting is common during the practice of machine learning, and a lot of time and attention is focused on addressing the problem of overfitting. The **No Free Lunch Theorem** for machine learning ([Wolpert, 1996][Wolpert-1996]) states that, averaged overall possible data-generating distributions, every classification algorithm has the same error rate when classifying previously unobserved points. In other words, in some sense, no machine learning algorithm is universally any better than any other. The most sophisticated algorithm we can conceive of has the same average performance (over all possible tasks) as merely predicting that every point belongs to the same class. There are a series of techniques used to prevent overfitting called Regularization. Regularization is any modiﬁcation we make to a learning algorithm that is intended to reduce its generalization error but not its training error.

> It is best to think of feedforward networks as function approximation machines that are designed to achieve statistical generalization, occasionally drawing some insights from what we know about the brain, rather than as models of brain function.
Deep Learning by Ian Goodfellow, Yoshua Bengio, Aaron Courville


## L1 and L2 Regularization

L1 and L2 regularization involves adding a penalty term to the cost function so that the model learns to not overfit to the larger errors. The difference between L1 and L2 regularization methods is that in L1, we add the absolute value of the error term to the cost function; while in L2, we add the square of the error term to the cost function.

For L1 regularization:

```math
cost = loss + \lambda |\beta|
```

For L2 regularization:

```math
cost = loss + \lambda |\beta|^2
```


## Dropout Regularization

A primary reason to use neural networks is to capture more complex relationships between our features than our typical linear models affords us. The neurons at each layer are essentially the weighted sums of all the neurons at the previous layer, with an activation function. While this might seem like a good idea to use _all_ the neurons in the previous layer to determine the output at a given neuron, this leads to neurons learning redundant patterns. Further, important and unique patterns that are learned might not get reinforced strongly enough. All this leads to overfitting. 

Dropout regularization is a method to reduce overfitting in a neural network by randomly turning off some nodes. This reduces overfitting since the network learns to not be dependent on the weights of specific neurons. The basic idea is that some of the nodes are temporarily prevented from influencing or activating the neuron downstream in a forward pass, and none of the weights updates are applied on the backward pass.

So if neurons are randomly dropped out of the network during training, the other neurons step in and make the predictions for the missing neurons. This results in independent internal representations being learned by the network, making the network less sensitive to the specific weight of the neurons. Such a network is better generalized and has fewer chances of producing overfitting.

In practice, this involves including additional `dropout layers` between the layers of a neural network.


## Early stop

Early stopping is another regularization/cross-validation technique where the learning model is tested on a validation set and if the model performs poorly on the validation set, training is stopped. During the training process, the trained model is tested on a validation set after each iteration. If the model performance on the training model hasn't improved, the training step is stopped.


## Data Augmentation

Data Augmentation is a regularization technique that is particularly relevant when training a model with images as the input dataset. The idea is that we generate additional images subjecting the images we have to minor transformations such as rotation, flipping, cropping, or blurring a few pixels in the image. This is analogous to Synthetic Minority Oversampling TEchnique (or [SMOTE][SMOTE]) technique which is commonly used in oversampling data when working with imbalanced datasets.  


[Wolpert-1996]: https://direct.mit.edu/neco/article-abstract/8/7/1341/6016/The-Lack-of-A-Priori-Distinctions-Between-Learning
[SMOTE]: https://arxiv.org/abs/1106.1813
