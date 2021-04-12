# 語法相關問題

### np array 按照某column排序

參考：https://stackoverflow.com/questions/2828059/sorting-arrays-in-numpy-by-column

```python
a[a[:, 1].argsort()] # 1: 要按照的column，1代表第二column
```



### 寫入檔案

參考：https://stackoverflow.com/questions/3263672/the-difference-between-sys-stdout-write-and-print

```python
import sys
temp = sys.stdout                 # store original stdout object for later
sys.stdout = open('log.txt', 'w') # redirect all prints to this log file
print("testing123")               # nothing appears at interactive prompt
print("another line")             # again nothing appears. it's written to log file instead
sys.stdout.close()                # ordinary file object
sys.stdout = temp                 # restore print commands to interactive prompt
print("back to normal")           # this shows up in the interactive prompt
```

用途在把for包起來的training的output存起來。這樣好像是不會印出來的樣子。

### .all() vs .any() 小實驗

參考：https://medium.com/jeasee%E9%9A%A8%E7%AD%86/python-all-any-40bfdb39f6e8

因為之前總是跳過瞭解這個差別，所以現在來用個小實驗自行領悟一下。

```python
import numpy as np

# init a boolean array: all False
k = np.array(np.zeros((2708)), dtype=bool)

# experiments
print(k.all()==True, k.any()==True) # >> False False

# change an element to True
k[0] = True 
print(k.all()==True, k.any()==True) # >> False True
print(k.all()==False, k.any()==False) # >> True False 
```

從上面的小實驗就可以推測出這兩者的差別：這兩者都得用iterative的方式去想它們，all()只要有個錯他就是False，any()只要裡面有一個是對的他就是True。

以原本就是boolean形式的array來看可能會比較容易混淆，可以先看左式，`k.all()`以及`k.any()`，直接去想它們，前者在所有為False但有一個為True的陣列裡，會得到False，因此`k.all()==False`會回傳True，而後者則是因為這個陣列裡面有一個True，所以就能回傳True，因此在`k.any()==True`是成立的。

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

---

### isinstance

[link](https://www.runoob.com/python/python-func-isinstance.html)

```python
>>>a = 2
>>> isinstance (a,int)
True
>>> isinstance (a,str)
False
>>> isinstance (a,(str,int,list))    # 是元组中的一个返回 True
True
```

---

### AssertionError

[link](https://www.geeksforgeeks.org/python-assertion-error/)

```python
# Handling it manually 
try: 
    x = 1
    y = 0
    assert y != 0, "Invalid Operation"
    print(x / y) 
  
# the errror_message provided by the user gets printed  
except AssertionError as msg:  
    print(msg) 
```

---

### list to string, string to list

[link](https://www.geeksforgeeks.org/python-program-to-convert-a-list-to-string/)

```python
# list to string
s = 'hihihi'
s_list = list(s)

# string to list
s = ['I', 'want', 4, 'apples', 'and', 18, 'bananas'] 
  
# using list comprehension 
listToStr = ' '.join([str(elem) for elem in s]) 
  
print(listToStr) 
```

