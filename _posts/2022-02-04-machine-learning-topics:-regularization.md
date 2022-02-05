---
layout: post
image: /assets/images/Test_image.jpeg
---

The central challenge in machine learning is that our trained algorithm must perform well on new, previously unseen data — not just those on which our model was trained. This ability for the model to perform well on previously unobserved inputs is called generalization. Although machine learning models almost always perform better on the training samples than unseen data, the goal is to maintain a modest discrepancy between training error and generalization error. This essentially suggests that our model has to be sophisticated enough to model the complex relationships between our features and the target, while not overfitting to the training data and hence not generalizing to unseen data. This problem of overfitting is common in regular practice of machine learning. There are a series of techniques used to prevent overfitting called Regularization.

## L1 and L2 Regularization

L1 and L2 regularization involves adding a penalty term to the cost function

![\Large cost = loss + \frac{\lambda}{2m}||y-\bar{y}||](https://latex.codecogs.com/svg.latex?x%3D%5Cfrac%7B-b%5Cpm%5Csqrt%7Bb%5E2-4ac%7D%7D%7B2a%7D)


## Dropout Regularization

Dropout regularization is a method to reduce overfitting in a neural network by randomly turning off some nodes. This reduces overfitting since the network learns to not be dependent on the weights of the neurons. The basic idea is that some of the nodes are temporarily prevented from influencing or activating the neuron downstream in a forward pass, and none of the weights updates are applied on the backward pass.

So if neurons are randomly dropped out of the network during training, the other neurons step in and make the predictions for the missing neurons. This results in independent internal representations being learned by the network, making the network less sensitive to the specific weight of the neurons. Such a network is better generalised and has fewer chances of producing overfitting.


## Early stop


## Data Augmentation
