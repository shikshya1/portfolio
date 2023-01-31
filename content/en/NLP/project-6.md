---
date: 2022-10-07T10:58:08-04:00
tags: ["BERT", "Cosine similarity", "Eucledian distance"]
title: "Measuring Distance"
omit_header_text: true

---

<!-- # Measuring Distance -->

### Eucledian Distance
Eucledian distance measures the distance between two points.

{{< figure src="../eucledian_distance.png" >}}

```
def eucledian_dist(a,b):
  return np.sqrt(np.sum(np.square(a - b)))
```

### Cosine similarity

Cosine similarity measures how similar the documents are irrespective of their size. Mathematically, it measures the cosine of the angle between two vectors projected in a multi-dimensional space.  It is a judgment of orientation and not magnitude. The cosine similarity is advantageous because even if the two similar documents are far apart by the Euclidean distance (due to the size of the document), chances are they may still be oriented closer together.

The similarity is:

1) 1 when θ=0∘
2) 0 when θ=90∘
3) −1 when θ=180∘

{{< figure src="../cosine_similarity.png" >}}

```
def cosine_sim(a, b): 
	return np.dot(a, b.T) / (np.linalg.norm(a) * np.linalg.norm(b))
```

### Transformers

Transformers architecture is considered as one of the major breakthrough in the field of natural language processing (NLP). The embeddings created by transformers model are rich in information. Several pre-trained models are available in huggingface to perform semantic search and clustering.

Calculate the embeddings using sentence transformers and calculate similarity between sentences using cosine similarity or other distance metrics.


### Link to github page: [Code](https://github.com/shikshya1/NLP/tree/main/Measuring%20Distance)

