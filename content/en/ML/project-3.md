---
date: 2023-01-01T10:58:08-04:00
tags: ["kmeans", "clustering"]
title: "Clustering Amazon books based on book title"
---


### Dataset: 

The dataset contains 946 books obtained from scraping Amazon books.

Reference: https://www.kaggle.com/datasets/die9origephit/amazon-data-science-books

Read DataFrame

```
df= pd.read_csv('CSVPATH')
```

Representing text using TF-IDF

```
from sklearn.feature_extraction.text import TfidfVectorizer
vectorizer = TfidfVectorizer(stop_words='english', ngram_range=(1,2))
X = vectorizer.fit_transform(df["title"])
```

### Clustering:

For the clustering, KMeans is used. KMeans is an unsupervised learning method that clusters dataset into 'k' different clusters. Each sample is assigned to the cluster with the nearest mean and then the means are updated during iterative optimization process.

Steps:

1) Initialize random cluster centers <br>
2) Repeat until converged:
 - Update cluster points: Assign data points to the nearest cluster centroid
 - Update cluster centers: set center to the mean of each cluster

Calculating 'K' in KMeans:

There are several methods to calculate number of clusters in KMeans. Elbow method is one of the most popular method to calculate optimal number of 'K'. The iterative approach is to calculate Within-Cluster-Sum of Squared Errors (WSS) for different values of k. The squared distance between the data point and its predicted centroid is calculated using distance metrics like Eucledian or Manhattan distance.The sum of all squared errors of all data points gives WSS. Then, we choose the value of K where the WSS starts to diminish and forms an elbow like shape as the optimal cluster number.

```
from sklearn.cluster import KMeans
sum_of_squared_distances = []
K = range(2,10)
for k in K:
   km = KMeans(n_clusters=k, max_iter=600, n_init=10)
   km.fit(X)
   sum_of_squared_distances.append(km.inertia_)
```

Plot number of clusters wrt sum of squared distance to determine the optimal number of cluster. In this dataset, We can see a elbow shape forming at cluster 6. So, we will use that as optimal number of cluster in our dataset.

Fit the model and assign cluster to book label.

```
optimal_k = 6
model = KMeans(n_clusters=optimal_k, init='k-means++', max_iter=600, n_init=10)
model.fit(X)

labels = model.labels_
book_cluster = pd.DataFrame(list(zip(df["title"],labels)),columns=['title','cluster'])
```

Naming clusters based on the top features on each clusters: <br/>
Cluster number 0 => statistics and probability <br/>
Cluster number 1 => Data Science <br/>
Cluster number 2 => Machine Learning <br/>
Cluster number 3 => Data Analysis <br/>
Cluster number 4 => Deep Learning <br/>
Cluster number 5 => Python <br/>

```
cluster number 0
('statistics', 'probability', 'practice', 'data', 'introduction', 'dummies', 'probability statistics', 'applications', 'sciences', 'business', 'ap', 'ap statistics', 'behavioral', 'statistics applications', 'practice statistics')


cluster number 1
('data', 'science', 'data science', 'analytics', 'python', 'guide', 'data analytics', 'learning', 'series', 'using', 'introduction', 'business', 'machine learning', 'machine', 'beginners')


cluster number 2
('learning', 'machine', 'machine learning', 'data', 'introduction', 'python', 'edition', 'series', 'introduction machine', 'algorithms', 'computation', 'computation machine', 'engineering', 'science', 'end')


cluster number  3
('data', 'analysis', 'data analysis', 'using', 'python', 'qualitative', 'statistics', 'introduction', 'social', 'guide', 'methods', 'analysis using', 'practical', 'qualitative data', 'sciences')


cluster number  4
('learning', 'deep', 'deep learning', 'python', 'intelligence', 'artificial', 'artificial intelligence', 'neural', 'tensorflow', 'machine', 'networks', 'machine learning', 'neural networks', 'learning python', 'pytorch')


cluster number  5
('python', 'programming', 'edition', 'data', 'guide', 'learning', 'learn', 'python programming', 'using', 'algorithms', 'introduction', '2nd edition', '2nd', 'build', 'code')

```

### Link to github page: [Code](https://github.com/shikshya1/ML_Basics/tree/main/KMeans%20clustering)



