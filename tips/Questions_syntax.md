# 語法相關問題

---

### Groupby + 對groupby的項目計算各種統計值

link: https://stackoverflow.com/questions/26599347/groupby-pandas-dataframe-and-calculate-mean-and-stdev-of-one-column-and-add-the

```python
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

![image-20201208150146067](C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201208150146067.png)

而後會有NaN，再用.fillna(0.0)來處理即可。

---

### generate txt and write texts in txt

[link](https://stackoverflow.com/questions/48959098/how-to-create-a-new-text-file-using-python/48964410)

```python
file = open("copy.txt", "w") 
file.write("Your text goes here") 
file.close() 
```

---

### plt.save()

需要寫在plt.show()之前，否則會存到全白的圖

---

### file or folder exists or not

[link](https://www.guru99.com/python-check-if-file-exists.html) [link2](https://www.tutorialspoint.com/How-can-I-create-a-directory-if-it-does-not-exist-using-Python)

```python
import os.path
from os import path
path.exists("guru99.txt") # file
```

```python
import os
if not os.path.exists('my_folder'):
    os.makedirs('my_folder') # create folder if not exists
```

---

### datetime

[link](https://www.programiz.com/python-programming/datetime/strftime) [link2](https://www.programiz.com/python-programming/datetime/current-time)

```python
from datetime import datetime

now = datetime.now()

current_time = now.strftime("%H:%M:%S")
print("Current Time =", current_time)
```

[處理時區問題](https://kkc.github.io/2015/07/08/dealing-with-datetime-and-timezone-in-python/) [可用時區列表](https://gist.github.com/pamelafox/986163)

---

### sample n element from list

[link](https://www.geeksforgeeks.org/python-random-sample-function/)

```python
# import random  
import random 

# Prints list of random items of 
# length 3 from the given list. 
list1 = [1, 2, 3, 4, 5, 6]  
print("With list:", random.sample(list1, 3)) 
  
# Prints list of random items of 
# length 4 from the given string.  
string = "GeeksforGeeks"
print("With string:", random.sample(string, 4))
```

---

### ignore FutureWarning

[link](https://stackoverflow.com/questions/15777951/how-to-suppress-pandas-future-warning)

```python
import warnings
warnings.simplefilter(action='ignore', category=FutureWarning)

import pandas
```