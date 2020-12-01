# Clustering

tags: ```yuanta```

[*main reference: Clustering*](https://scikit-learn.org/stable/modules/clustering.html)
![](https://i.imgur.com/FETFH4K.png)

[toc]


## KMeans


## Affinity Propagation
```memory error```
 
![](https://i.imgur.com/MapES1z.png)

[Advantage:](https://www.twblogs.net/a/5b8e557f2b71771883446def)
 1. 不需要制定最終聚類族的個數
2. 已有的數據點作爲最終的聚類中心，而不是新生成一個族中心。
3. 模型對數據的初始值不敏感。
4. 對初始相似度矩陣數據的對稱性沒有要求。
5. 相比與k-centers聚類方法，其結果的平方差誤差較小。

[ref](http://wiki.swarma.net/index.php?title=Affinity_propagation_%E8%81%9A%E7%B1%BB&variant=zh-tw)
AP的劣勢是充分識別了數據內部的結構後，對於許多真實數據，都會聚出比較多的類，因此在聚類數量在1-5時，速度沒有K-means快，效果也不一定好。 具體來說，AP演算法複雜度為O(N*N*logN)，而K-Means是O(N*K)。因此當N比較大時(N>3000)，AP聚類演算法往往需要算很久。

```python=
>>> from sklearn.cluster import AffinityPropagation
>>> import numpy as np
>>> X = np.array([[1, 2], [1, 4], [1, 0],
...               [4, 2], [4, 4], [4, 0]])
>>> clustering = AffinityPropagation().fit(X)
>>> clustering
AffinityPropagation()
>>> clustering.labels_
array([0, 0, 0, 1, 1, 1])
>>> clustering.predict([[0, 0], [4, 4]])
array([0, 1])
>>> clustering.cluster_centers_
array([[1, 2],
       [4, 2]])
```

## X-means
https://github.com/KazuhisaFujita/X-means/blob/master/simple_xmeans.py

## [LDA](https://scikit-learn.org/stable/modules/generated/sklearn.discriminant_analysis.LinearDiscriminantAnalysis.html)
```需有label```
> 对于二分类问题，LDA针对的是：数据服从高斯分布，且均值不同，方差相同。
> 
```python=
>>> import numpy as np
>>> from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
>>> X = np.array([[-1, -1], [-2, -1], [-3, -2], [1, 1], [2, 1], [3, 2]])
>>> y = np.array([1, 1, 1, 2, 2, 2])
>>> clf = LinearDiscriminantAnalysis()
>>> clf.fit(X, y)
LinearDiscriminantAnalysis()
>>> print(clf.predict([[-0.8, -1]]))
[1]
```
## [QDA](https://scikit-learn.org/stable/modules/generated/sklearn.discriminant_analysis.QuadraticDiscriminantAnalysis.html)
```需有label```
>对于二分类问题，QDA针对的是：数据服从高斯分布，且均值不同，方差不同。

数据方差相同的时候，一次判别就可以，如左图所示;但如果方差差别较大，就是一个二次问题了，像右图那样。 [reference](https://www.cnblogs.com/xingshansi/p/6892317.html)
![](https://i.imgur.com/Ws9ns6I.png)

```python=
>>> from sklearn.discriminant_analysis import QuadraticDiscriminantAnalysis
>>> import numpy as np
>>> X = np.array([[-1, -1], [-2, -1], [-3, -2], [1, 1], [2, 1], [3, 2]])
>>> y = np.array([1, 1, 1, 2, 2, 2])
>>> clf = QuadraticDiscriminantAnalysis()
>>> clf.fit(X, y)
QuadraticDiscriminantAnalysis()
>>> print(clf.predict([[-0.8, -1]]))
[1]
```