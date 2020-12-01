#  Manifold Learning

tags: ```yuanta```

[*main reference: Manifold Learning*](https://scikit-learn.org/stable/modules/manifold.html)

[toc]

## [Locally Linear Embedding (LLE)](https://scikit-learn.org/stable/modules/generated/sklearn.manifold.LocallyLinearEmbedding.html#sklearn.manifold.LocallyLinearEmbedding)
```跑很久```

```python=
from sklearn.manifold import LocallyLinearEmbedding

embedding = LocallyLinearEmbedding(n_components=2)
X_transformed = embedding.fit_transform(X[:100])

X_transformed.shape
(100, 2)
```



## Modified Locally Linear Embedding


## Hessian Eigenmapping
> also known as Hessian-based LLE: HLLE. 

> HLLE can be performed with function locally_linear_embedding or its object-oriented counterpart LocallyLinearEmbedding, with the keyword method = 'hessian'
> 

## [Spectral Embedding](https://scikit-learn.org/stable/modules/generated/sklearn.manifold.SpectralEmbedding.html#sklearn.manifold.SpectralEmbedding)
 ```memory error```

```python=
from sklearn.manifold import SpectralEmbedding

embedding = SpectralEmbedding(n_components=2)
X_transformed = embedding.fit_transform(X[:100])

X_transformed.shape
(100, 2)
```

## [t-distributed Stochastic Neighbor Embedding (t-SNE)](https://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html#sklearn.manifold.TSNE)
```跑很久```

```python=
from sklearn.manifold import TSNE

X_embedded = TSNE(n_components=2).fit_transform(X)

X_embedded.shape
(4, 2)
```