---
layout: post
image: /assets/images/Test_image.jpeg
---

The central challenge in machine learning is that our trained algorithm must perform well on new, previously unseen data — not just those on which our model was trained. This ability for the model to perform well on previously unobserved inputs is called generalization. Although machine learning models almost always perform better on the training samples than unseen data, the goal is to maintain a modest discrepancy between training error and generalization error. This essentially suggests that our model has to be sophisticated enough to model the complex relationships between our features and the target, while not overfitting to the training data and hence not generalizing to unseen data. This problem of overfitting is common during the practice of machine learning, and a lot of time and attention is focused on addressing the problem of overfitting. The **No Free Lunch Theorem** for machine learning ([Wolpert, 1996][Wolpert-1996]) states that, averaged overall possible data-generating distributions, every classification algorithm has the same error rate when classifying previously unobserved points. In other words, in some sense, no machine learning algorithm is universally any better than any other. The most sophisticated algorithm we can conceive of has the same average performance (over all possible tasks) as merely predicting that every point belongs to the same class. There are a series of techniques used to prevent overfitting called Regularization.

## L1 and L2 Regularization

L1 and L2 regularization involves adding a penalty term to the cost function

```math
a^2+b^2=c^2
```

## Dropout Regularization

Dropout regularization is a method to reduce overfitting in a neural network by randomly turning off some nodes. This reduces overfitting since the network learns to not be dependent on the weights of the neurons. The basic idea is that some of the nodes are temporarily prevented from influencing or activating the neuron downstream in a forward pass, and none of the weights updates are applied on the backward pass.

So if neurons are randomly dropped out of the network during training, the other neurons step in and make the predictions for the missing neurons. This results in independent internal representations being learned by the network, making the network less sensitive to the specific weight of the neurons. Such a network is better generalised and has fewer chances of producing overfitting.


## Early stop


## Data Augmentation


[Wolpert-1996]: https://direct.mit.edu/neco/article-abstract/8/7/1341/6016/The-Lack-of-A-Priori-Distinctions-Between-Learning
