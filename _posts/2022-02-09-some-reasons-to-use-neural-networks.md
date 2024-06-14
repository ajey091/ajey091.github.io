---
layout: post
image: /assets/images/Test_image.jpeg
---
While the promise and popularity of neural networks is far more prevalent in popular media than in actual technical practice, it's useful to occasionally revisit some good reasons to use neural networks. In short, neural networks are versatile non-linear models that work well for many different types of problems. Reasons for using a deep neural network model (with more than 1 hidden layer) are primarily when our problem requires some non-obvious feature engineering - in image classification, it is unclear how to define the various steps in feature engineering to identify different components of an object. Deep neural networks are a great candidate in such context, as we are outsourcing the task of feature engineering to the neural net. 

More specifically, deep learning really becomes useful when we're dealing with unstructured data. With structured data, we often find that we can achieve comparable performance with a fraction of compute time and resources using an ensemble model such as Random Forest or XGBoost. The central challenge with unstructured data being - there not being an obvious way to encode the data as an input to ensemble models. 

Further, the sequential nature of deep learning also renders it a conducive framework when dealing with tasks involving sequential decision-making - such as reinforcement learning tasks. 

In conclusion, while deep neural networks may not always be the best choice for every problem, they excel in situations where feature engineering is challenging, particularly when dealing with unstructured data. Additionally, their sequential nature makes them well-suited for tasks involving sequential decision-making. As the field of deep learning continues to evolve, we can expect to see even more innovative applications of these powerful models in the future.