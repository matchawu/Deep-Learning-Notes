# 語法相關問題

---

### Groupby + 對groupby的項目計算各種統計值

link: https://stackoverflow.com/questions/26599347/groupby-pandas-dataframe-and-calculate-mean-and-stdev-of-one-column-and-add-the

```py
result = df.groupby(['a'], as_index=False).agg(
                      {'c':['mean','std'],'b':'first', 'd':'first'})
```

c,b,d 皆是欄位名稱，：後面接的是group以後要那個欄位所做的處理的名稱

*通常在做groupby的時候會用簡單的加總，只需要groupby(欄位名稱).sum()即可。

因為如此做完以後的columns名稱會較複雜，因此可以reset column names

```result.columns = ['a','c','e','b','d']```

---

### 兩個list中有否common elements

 link: https://www.kite.com/python/answers/how-to-find-common-elements-between-two-lists-in-python

```python
list1 = [1, 2]
list2 = [1, 3]


list1_as_set = set(list1)
intersection = list1_as_set.intersection(list2)
```

Find common elements of set and list

```python
intersection_as_list = list(intersection)

print(intersection_as_list) # output: [1]
```

---

### merge, concat, join大全

link:http://violin-tao.blogspot.com/2017/06/pandas-2-concat-merge.html

merge by index

```python
import pandas as pd  
import numpy as np
left = pd.DataFrame({
    'A':['A0','A1','A2'],
    'B':['B0','B1','B2']},
    index=['K0','K1','K2'])
right = pd.DataFrame({
    'C':['C0','C2','C3'],
    'D':['D0','D2','D3']},
    index=['K0','K2','K3'])
res = pd.merge(left,right, left_index=True, right_index=True, how='outer')
print(res)
```

---

