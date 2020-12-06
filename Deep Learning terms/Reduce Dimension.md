# 降維工具

# *PCA*

[sklearn.decomposition.PCA - scikit-learn 0.23.1 documentation](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html)

[scikit-learn中PCA的使用方法_wepon的专栏-CSDN博客_pca.fit_transform](https://blog.csdn.net/u012162613/article/details/42192293)

```python
from sklearn.decomposition import PCA
pca=PCA(n_components=1)
newData=pca.fit_transform(data)
```

`fit(X,y=None)`

- fit()可以說是scikit-learn中通用的方法，每個需要訓練的算法都會有fit()方法，它其實就是算法中的“訓練”這一步驟。因為PCA是無監督學習算法，此處y自然等於None。
- fit(X)，表示用數據X來訓練PCA模型。
- 函數返回值：調用fit方法的對象本身。比如pca.fit(X)，表示用X對pca這個對象進行訓練。

`fit_transform(X)`

- 用X來訓練PCA模型，同時返回降維後的數據。
- newX=pca.fit_transform(X)，newX就是降維後的數據。

`inverse_transform()`

- 將降維後的數據轉換成原始數據，X=pca.inverse_transform(newX)

`transform(X)`

- 將數據X轉換成降維後的數據。當模型訓練好後，對於新輸入的數據，都可以用transform方法來降維。

此外，還有get_covariance()、get_precision()、get_params(deep=True)、score(X, y=None)等方法，以後用到再補充吧。
————————————————
版权声明：本文为CSDN博主「wepon_」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：[https://blog.csdn.net/u012162613/java/article/details/42192293](https://blog.csdn.net/u012162613/java/article/details/42192293)