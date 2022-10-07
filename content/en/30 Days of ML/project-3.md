---
date: 2020-09-03T10:58:08-04:00
tags: ["t-sne", "PCA"]
title: "Day 3- t-SNE"
---

# t-Distributed Stochastic Neighbor Embedding (t-SNE)

t-SNE is a unsupervised, non-parametric (non-linear) method  used for dimensionality reduction primarily  for visualization and exploration of high-dimensional datasets. It gives an idea of how data is arranged in higher dimension. It's hard for us to visualize data beyond 3 dimension. Standard visualization methods can usually capture one or two variable at a time. In such cases, dimension reduction algorithm can help to analyze the pattern in the data. T-SNE preserves much of significant structure of high dimensional data as possible during projection. It is an iterative algorithm which minimizes non-convex objective using gradient descent. T-SNE is used to visualize genomic data, word embeddings, images etc. 

While PCA is a popular algorithm used for dimension reduction, there are few differences that set t-SNE apart from PCA.  The objective of PCA is to project data into lower dimensional space in a way that maximizes the variance. It mostly preserves the distance between the dissimilar points but it can lead to poor visualization especially when dealing with non-linear manifold structures. While t-SNE works by preserving local similarities and produces better visualization as in complex datasets, large distances are usually less indicative of actual structure.



Reference :

1) https://www.jmlr.org/papers/volume9/vandermaaten08a/vandermaaten08a.pdf : Visualizing Data using t-SNE


### Link to github page: [Code](https://github.com/shikshya1/30_days_of_ml/tree/main/Day-3(t-sne))
