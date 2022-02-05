---
layout: post
image: /assets/images/Test_image.jpeg
---


Dropout regularization is a method to reduce overfitting in a neural network by randomly turning off some nodes. This reduces overfitting since the network learns to not be dependent on the weights of the neurons. The basic idea is that some of the nodes are temporarily prevented from influencing or activating the neuron downstream in a forward pass, and none of the weights updates are applied on the backward pass.

So if neurons are randomly dropped out of the network during training, the other neurons step in and make the predictions for the missing neurons. This results in independent internal representations being learned by the network, making the network less sensitive to the specific weight of the neurons. Such a network is better generalised and has fewer chances of producing overfitting.
