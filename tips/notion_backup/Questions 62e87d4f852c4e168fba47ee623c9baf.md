# Questions

## Lp space

![Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled.png](Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled.png)

# model訓練相關

### Gradient-based、decision-based、score-based [x](https://zhuanlan.zhihu.com/p/139326532)

- Gradient-based
- decision-based
- score-based

### SCCE vs CCE 除了Y維度以外的差別？

在CNN簡單訓練的時候沒有問題，但是在跑fgsm tutorial的時候改成自己的CNN model SCCE loss非常高，acc非常低

![Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled%201.png](Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled%201.png)

### dense直接output vs with softmax activation

前者會變成multi-class regression 的問題

![Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled%202.png](Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled%202.png)

- **前者loss比較小**
    - dense直接output可能會有正負，log(負數)是不能計算的，若model loss沒報錯，那應該是忽略了nan的部分，致使loss比較少
- **前者acc比較高**
    - ？
    - 但epoch很少，也還沒有overfitting

### [L系列norm](https://medium.com/@montjoile/l0-norm-l1-norm-l2-norm-l-infinity-norm-7a7d18a4f40c)

思考：L1, L2的使用時機？

### 攻擊使離y true越來越遠 攻擊成功率怎麼計算？

本來就分類錯誤的也會算進去嗎？

### tensorflow中的model summary [參考](https://stackoverflow.com/questions/46560313/is-there-an-easy-way-to-get-something-like-keras-model-summary-in-tensorflow)

找到tf.trainable_variables並寫下：

```
def model_summary():
    model_vars = tf.trainable_variables()
    slim.model_analyzer.analyze_vars(model_vars, print_info=True)

model_summary()
```

---

# 語法問題

### np.reshape跟直接reshape

前者出現type的問題

### resize跟reshape的差別

resize會插值，reshape不會

### UnicodeDecodeError

### python function裡面的self.__cool = 0

兩個底線代表private的意思

### 計算[每個row有幾個為0的值](https://stackoverflow.com/questions/34968223/counting-the-number-of-non-zero-numbers-in-a-column-of-a-df-in-pandas-python?lq=1)

![Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled%203.png](Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled%203.png)

### 最大N個 Indices of N largest elements in list

[https://www.geeksforgeeks.org/python-indices-of-n-largest-elements-in-list/](https://www.geeksforgeeks.org/python-indices-of-n-largest-elements-in-list/)

---

# 安裝、硬體問題

### pip vs conda install

pip裝最新 conda確認可以跑

### cublas 64_10.dll not found

去官網下載放到資料夾上即可

### 匯出環境`conda export env —no-builds -f env.yml`

~~沒有成功？why？~~

成功解決，中間加上 `-n 自定義name`即可

### conda指令

[用conda建立及管理python虛擬環境](https://medium.com/python4u/%E7%94%A8conda%E5%BB%BA%E7%AB%8B%E5%8F%8A%E7%AE%A1%E7%90%86python%E8%99%9B%E6%93%AC%E7%92%B0%E5%A2%83-b61fd2a76566)

### Windows上的Git Bash不能跑conda activate

解法：先`source activate`，顯示目前環境，再用`conda activate (環境名稱)` 即可。離開時也是要用 `source deactivate`去做。

[Git Bash使用conda命令activate env（Windows）_一半西瓜的博客-CSDN博客_git切换conda环境](https://blog.csdn.net/qq_37672864/article/details/104890583)

---

# 其他問題

### 圖上會有部分沒有perturbations

perturbations確認是32*32但是印出來看起來只有28*28

### 是否會變回原本的label?

原本分錯的 

A model 5000張 分類成功的照片 攻擊 (裡面應該有本來就分類失敗的 會使攻擊比較容易成功)

成功率 比500張 還高

攻擊成功率：如何計算？

### ValueError: I/O operation on closed file

### 雷達圖(matplotlib方法)

[#391 Radar chart with several individuals](https://python-graph-gallery.com/391-radar-chart-with-several-individuals/)

---

### numpy dtype

[解决python调用TensorFlow时出现FutureWarning: Passing (type, 1) or 1type as a synonym of type is deprecate_BigDream123的博客-CSDN博客](https://blog.csdn.net/BigDream123/article/details/99467316)

### anaconda虛擬env安裝spyder會有的問題: `ModuleNotFoundError: No module named 'IPython.core.inputtransformer2'`

[用本地Spyder连接Linux远程服务器,spyder,linux](https://www.pythonf.cn/read/57363)

### ssh in cmd

C:\Users\wwj>ssh [wwj@140.113.31.206](mailto:wwj@140.113.31.206)
Bad owner or permissions on C:\\Users\\wwj/.ssh/config

![Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled%204.png](Questions%2062e87d4f852c4e168fba47ee623c9baf/Untitled%204.png)

---

### [vscode insider] ssh server

1. windows ssh client裝好(應用程式和功能)
2. 設定ssh key: [https://www.footmark.info/linux/centos/windows-ssh-nopassword-linux/](https://www.footmark.info/linux/centos/windows-ssh-nopassword-linux/)
3. 取得pub key以後和server端authorize，可以不用密碼就登入(cmd)
4. wwj/.ssh/裡面有config檔案，移除繼承，新增自己使用者，開啟vscode連remote ssh即可
5. 參考：[https://xenby.com/b/220-教學-產生ssh-key並且透過key進行免密碼登入](https://xenby.com/b/220-%e6%95%99%e5%ad%b8-%e7%94%a2%e7%94%9fssh-key%e4%b8%a6%e4%b8%94%e9%80%8f%e9%81%8ekey%e9%80%b2%e8%a1%8c%e5%85%8d%e5%af%86%e7%a2%bc%e7%99%bb%e5%85%a5)
6. 搜尋關鍵字：[https://www.google.com/search?q=vscode+ssh+remote&oq=vsc&aqs=chrome.0.69i59l3j69i57j69i59j69i60l3.1937j0j1&sourceid=chrome&ie=UTF-8](https://www.google.com/search?q=vscode+ssh+remote&oq=vsc&aqs=chrome.0.69i59l3j69i57j69i59j69i60l3.1937j0j1&sourceid=chrome&ie=UTF-8)