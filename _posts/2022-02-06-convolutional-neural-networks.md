---
layout: post
image: /assets/images/Test_image.jpeg
---
Convolutional neural networks (CNNs) are a specialized type of neural networks for processing data with a grid-like topology. This essentially means time series data along a discretized grid or more commonly, images (which are RGB or grayscale pixels). CNNs have been practically very useful for image classification tasks. The problem with using conventional artificial neural networks for images is that the number of input dimensions are very high when we are working with high resolution colored images. Furthermore, just considering a flattened array of pixels and feeding into an ANN would make the network very sensitive to the location of the object in the image. CNNs help address these issues. CNNs are essentially neural networks that use convolution in place of general matrix multiplication in at least one of their layers. Hence, the convolution operation preserves the spatial relationships between pixels by learning image features by working on small regions of the whole grid.

Convolutional neural networks have 3 fundamental features that reduce the number of parameters in a neural network -

1. Sparse interaction between layers
2.  


## Components of CNNs

![Convolutional neural network layers](/assets/images/cnn_banner.png)

A very successful early implementation of a CNN was AlexNet:

![Alexnet](/assets/images/Alexnet.png)

A simple implementation of a CNN

```
import keras
import tensorflow as tf

from keras.models import Sequential
from keras.layers import Dense, Dropout, Flatten
from keras.layers import conv2D, MaxPooling2D

```

```
model = Sequential()
model.add(conv2D(32, kernel_size=(3,3), activation='relu', input_size=(28,28,1)))
model.add(MaxPooling2D(pool_size=(2,2)))
model.add(Dropout(0.25))
model.add(Dense(128, activation='relu'))
model.add(Dropout(0.5))
model.add(Dense(num_classes), activation='softmax')

model.compile(loss=keras.losses.categorical_crossentropy, optimizer=tf.keras.optimizers.Adadelta(), metrics=['accuracy'])


```
