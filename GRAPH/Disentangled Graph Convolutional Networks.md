# Disentangled Graph Convolutional Networks 
```DisenGCN``` ```DisenConv```

筆記連結：[link](https://web.kamihq.com/web/viewer.html?state=%7B%22ids%22%3A%5B%221DLTp2nBVdn5H7jsE3vyrHYWcSVnxv6xn%22%5D%2C%22action%22%3A%22open%22%2C%22userId%22%3A%22110423678406540730896%22%7D&filename=null&kami_user_id=7681522)

## Problem
之前總是把一個節點的鄰居作為整個感知整體，忽略了細微的差別。然而在真實世界中一個graph的行程是複雜且異質性的，例如一個人的節點可能就會連到跟工作有關、跟學校有關的不同節點。現有的作法無法將這些區別開來，也可能不robust。

## Works

### image
在image representation learning上的disentangled representation learning
好處：
- 對於複雜的資料有彈性
- generalization and robustness
- interpretable
- debugging and auditing

### graph
在graph上依著graph的特性，可能很難直接套用disentangled learning。資料有限、可微分、be capable of conducting inductive learning in order to enable out-of-sample node processing (Ma et al., 2018; Hamilton et al., 2017) in real time for real-world deployment.

![](https://i.imgur.com/fEsBnrN.png)
:::spoiler DisenConv
The neighborhood routing mechanism iteratively segments the neighborhood according to the underlying factors.
:::


