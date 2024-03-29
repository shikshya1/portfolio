---
date: 2022-10-01T10:58:08-04:00
tags: ["Normalization", "ML"]
title: "Feature Scaling"
omit_header_text: true

---

Feature scaling is one of the most important transformation in most of the ML projects. When one feature is on small range; say 0 to 10 while the other one is on a large range (suppose 0 to 10000); ML algorithms donot perform well. We have to scale the features so that both of them takes a comparable ranges of values to each other. In simpler terms, it means transforming data into a common range of values.

#### When should we use feature selection?

1. While using distance-based metrics:
    While using distance based methods like SVM, k-nearest neighbors; choosing not to scale data may drastically impact predictions leading to wrong interpretations.

2. While using regularization:
    Penalty on weights depends heavily on the scale associated with the features. Applying regularization on two features with huge difference on scale will result in unfair punishment of feature with small range.

Feature scaling can be done through:

- Normalization
- Standardization

#### Normalization: 

Normalization also referred as Min-Max scaling is the simplest where values are shifted and rescaled such that data is scaled between 0 & 1. 

X<sup>1</sup> = (X-X<sub>min</sub>)/(X<sub>max</sub> - X<sub>min</sub>)

```
from sklearn.preprocessing import MinMaxScaler
min_max_scaler = MinMaxScaler()
```



#### Standardization:

Standardization is done by subtracting each value from mean of column and dividing it by standard deviation. It centers the values around mean with a unit standard deviation. When the standardized data is plotted, it follows guassian distribution.

X<sup>1</sup> = (X-μ)/σ

```
from sklearn.preprocessing import StandardScaler
std_scaler = StandardScaler()
```

Standardization doesnot bound values to a specific range while normalization does which might be a problem for algorithms expecting values between 0 & 1. It is also robust to outliers.

### Batch Normalization in Deep Learning

- Batch Normalization:

There are several ways in which we can initialize weights during training. But even that cannot ensure unstable gradient problem while training neural networks. Batch normalization addresses this issue; it zero centers and normalizes each input followed by scaling and shifting of result with two new parameters per layer (one for shifting and one for scaling). It helps to find good transformation to overcome the unstable gradient problem and helps in faster model training. Although the training epoch will take longer due to the added computation but it will converge faster. Also, there's no need to standardize the data before feeding into the neural network and reduces the need of using regularization techniques too.

```
model = keras.models.Sequential([
    keras.layers.Flatten(input_shape=[28,28]),
    keras.layers.BatchNormalization(),
    keras.layers.Dense(300, activation='relu'),
    keras.layers.BatchNormalization(),
    keras.layers.Dense(100, activation='relu'),
    keras.layers.BatchNormalization(),
    keras.layers.Dense(10, activation='softmax'),
])
```

### Link to github page: [Code](https://github.com/shikshya1/ML_Basics/tree/main/Feature%20Scaling)
