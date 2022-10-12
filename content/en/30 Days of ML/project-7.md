---
date: 2022-10-07T10:58:08-04:00
tags: ["BERT", "Cosine similarity", "Eucledian distance"]
title: "Day 7- Measuring Distance"
---

# Measuring Distance

### Eucledian Distance
Eucledian distance measures the distance between two points.

{{< figure src="./eucledian_distance.png" >}}


### Cosine similarity

Cosine similarity measures how similar the documents are irrespective of their size. Mathematically, it measures the cosine of the angle between two vectors projected in a multi-dimensional space.  It is a judgment of orientation and not magnitude. The cosine similarity is advantageous because even if the two similar documents are far apart by the Euclidean distance (due to the size of the document), chances are they may still be oriented closer together.

The similarity is:

1) 1 when θ=0∘
2) 0 when θ=90∘
3) −1 when θ=180∘

{{< figure src="./cosine_similarity.png" >}}


### Transformers

Transformers architecture is considered as one of the major breakthrough in the field of natural language processing (NLP). The embeddings created by transformers model are rich in information. Several pre-trained models are available in huggingface to perform semantic search and clustering.



### Link to github page: [Code](https://github.com/shikshya1/30_days_of_ml/tree/main/Day-7%20(Measuring%20Distance))

