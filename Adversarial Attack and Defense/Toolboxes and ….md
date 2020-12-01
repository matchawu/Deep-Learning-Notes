# Toolboxes and ...
*updated at:* ```0309```

[toc]

## Adversarial Robustness 360 Toolbox (ART)
> 說真的我沒看過也沒用過QQ昨天突然被老師cue這個XD 
> 不過如果有問題的話也可以一起討論~~
### 官方說明
- [官方GitHub](https://github.com/IBM/adversarial-robustness-toolbox?fbclid=IwAR2zKimw-IsJF-R9YUzXwFevnEshC6JxJFJY02Iye3zVtLyfIp4jW2sIAaE)
    - [examples](https://github.com/IBM/adversarial-robustness-toolbox/blob/master/examples/README.md)
    - [tutorials](https://github.com/IBM/adversarial-robustness-toolbox/blob/master/notebooks/README.md)
    - [文檔](https://adversarial-robustness-toolbox.readthedocs.io/en/latest/index.html)

> 簡略地看了一下，他的[程式碼](https://github.com/IBM/adversarial-robustness-toolbox/blob/master/examples/README.md)應該比Advbox來得簡潔許多XD 或許能比較快拿來應用。應該是來自[這篇論文](https://arxiv.org/pdf/1807.01069.pdf)。
> 

## Advbox
> 當初跑的時候大概是修正程式問題以後就開始下指令跑，程式的細節你可以再多研究。如果要參考[我之前的code](https://drive.google.com/drive/folders/1cJ65TXHrdoycqOxBv4il3f6uQ4hr9ABQ?usp=sharing)也可以看看，應該沒改多少，只是修正一些我在[紀錄hackmd](https://hackmd.io/MDoZFdkVRKmiy7J53L-0HA?view)上面提到的**已解決問題**。裡面的待解決問題，感覺好像解決ㄌ~(如下圖所示，今年一月的留言)。在跑之前，需要安裝一些套件，可以跑一次看錯誤看需要裝什麼，例如[安裝paddlepaddle](https://www.paddlepaddle.org.cn/install/quick)。跑的方式每次會下兩個指令，一個用來生成測試模型，一個用來運行攻擊，詳細可以參考別人寫的使用說明或是我的紀錄hackmd。
> ![](https://i.imgur.com/s0CYodN.png)
> 
### 官方說明
- [官方GitHub](https://github.com/advboxes/AdvBox?fbclid=IwAR3A--kHwujC0VkFx4tYIZXaEL3xrgkL9qcdueK3FVmcVx6gnle8k8aioDk)

### 使用說明
> 當初大多是按照這個上面跑的。注意一下套件的版本需求即可。

[开源AI安全工具箱AdvBox](https://www.freebuf.com/column/180324.html)


## Adversarial Attack or Defense
> 關於Adversarial Attack or Defense可以參考的資料
### Survey Paper
> 我之前主要是看第一篇(覺得整理的比較有脈絡XD)，可以從中間大致看attack或defense每一種方法主要的做法以及key idea。後面幾篇我沒有詳細看過，有空的話你也可以參考。
- [Threat of Adversarial Attacks on Deep Learning in Computer Vision: A Survey](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8294186)

> 以下的部分是我當時有找過但還沒詳細看過的，你也可以直接從Google學術搜尋上面搜尋```attack```,```adversarial```,```survey```等等關鍵字去找survey paper。
- [Adversarial Attacks and Defenses in Images, Graphs and Text: A Review](https://arxiv.org/pdf/1909.08072.pdf)
- [Adversarial Attacks and Defences: A Survey](https://arxiv.org/pdf/1810.00069.pdf)
- [Adversarial Examples: Attacks and Defenses for
Deep Learning](https://arxiv.org/pdf/1712.07107.pdf)



### EYD 與機器學習
![](https://i.imgur.com/VreBdpO.png)
> [EYD 與機器學習](https://zhuanlan.zhihu.com/c_170476465)知乎專欄。裡面有很多Deep Learning的相關主題，其中一個是**對抗攻擊基礎知識**，大約有三十幾篇文章，有空的話也可以看看，或是在找某篇adversarial paper的說明的話也可以參考他們寫的，我記得重點幾篇大作他們幾乎都有涵蓋到。

