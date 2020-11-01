# 語法相關問題

---

### Groupby + 對groupby的項目計算各種統計值

link: https://stackoverflow.com/questions/26599347/groupby-pandas-dataframe-and-calculate-mean-and-stdev-of-one-column-and-add-the

```py
result = df.groupby(['a'], as_index=False).agg(
                      {'c':['mean','std'],'b':'first', 'd':'first'})
```

c,b,d 皆是欄位名稱，：後面接的是group以後要那個欄位所做的處理的名稱

因為如此做完以後的columns名稱會較複雜，因此可以reset column names

```result.columns = ['a','c','e','b','d']```

---



