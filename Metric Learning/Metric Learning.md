---
tags: metric learning
---

# Metric Learning

## Introduction

度量相似度的距离函数:相似的目标离得近,不相似的离得远
用网络提取embedding,然后在embedding space用L2-distance来度量距离
![](https://i.imgur.com/LNmUv2r.png)

> hard negative 距離anchor最近的負樣本
## General Pipeline

1. 特征提取网络来map embedding,
2. 一个采样策略来将一个mini-batch里的样本组合成很多个sub-set,
3. 最后loss function在每个sub-set上计算loss

![](https://i.imgur.com/gj7YGPF.png)

Sample mini-batch一般是C类每类挑K个,共N个.然后通过网络得到embedding.通用的做法是会用L2-normalization来归一化网络的输出,这样得到了单位向量,其L2距离就和cos相似度成正比.

很多face recognition的相似的就是基于cos相似度来的.同时也因为softmax会产生这种结构

![](https://i.imgur.com/bRqrO7M.png)
左：沒有L2
右：有L2

向量的內積(即相似度)：(a,b)內積(c,d)=ac+bd
![](https://i.imgur.com/Ftezd6Q.png)

為啥要這樣限制?使用L2?

1. 壓縮值域
2. 不要讓長度影響相似度

*NORM 和 REGULARIZE 不同*

L2norm以後使得距離圓心都是同個距離
單位向量(距離圓心都是同個距離)：可以使得COSINE相似度(內積)比較"公平"
向量長度會影響計算cosine相似度
餘弦值越接近1，就表明夾角越接近0度，也就是兩個向量越相似，這就叫"餘弦相似性"

### 采样

将一个mini-batch里的样本组合成很多个sub-set
1. 计算embedding distance metric
2. 将每个样本都当做一个anchor
3. 根据距离挑一部分同类做正样本,一部分其他类做负样本组成sub-set.
4. 对每个anchor要么是一个大的sub-set里基本包含整个mini-batch(N个样本)只是权重不同,要么是N个更小的数据对.总的来说计算复杂度是(N*N)

## Loss Function
![](https://i.imgur.com/kA9cHXC.png)
[reference](https://zhuanlan.zhihu.com/p/27748177)
### [Contrastive loss](https://blog.csdn.net/autocyz/article/details/53149760)
同類看前半部分
不同類看後半部分
alpha: margin 不同類的要至少拉開margin的距離

![](https://i.imgur.com/90kTuno.png)

孿生神經網絡（siamese network）採用
让网络学到将同类样本map到同一个点,然后不同类样本之间有一个fix的距离

### Triplet Loss

距離正樣本 和距離負樣本 的距離 至少要差距alpha

sample的時候決定 
e.g.挑離anchor越遠的positive，最近的negative

![](https://i.imgur.com/mnZaAC7.png)

此时就不是L2空间中的绝对距离而是相对距离了.同时它不让所有同类样本map到同一点,因为这是没有必要的
**正負例樣本該有一段a距離**
![](https://i.imgur.com/uWFdf6Z.png)

### Margin Based Loss
對偶形式：保序回归(isotonic regression)：关注相对关系而不是绝对关系

#### 保序回歸：
1. 這種回歸，是這一種單調函數的回歸，回歸模型中後一個x一定比前一個x大，也就是有序，具體的數學公式在上面兩個網址中都有。保序回歸併不需要製定的目標函數。

2. 保序回歸的應用之一就是用來做統計推斷，比如藥量和毒性的關係，一般認為毒性隨著藥量是不減或者遞增的關係，藉此可以來估計最大藥量。

![](https://i.imgur.com/83drYtb.png)

我們稱anchor樣本與正例樣本之間的距離為正例對距離；稱anchor樣本與負例樣本之間的距離為負例對距離。**公式中的參數beta定義了正例對距離與負例對距離之間的界限，如果正例對距離Dij大於beta，則損失加大；或者負例對距離Dij小於beta，損失加大。** A控製樣本的分離間隔；當樣本為正例對時，yij為1，樣本為負例對時，yij為-1。
正正應該靠近；負負應該遠離


![](https://i.imgur.com/7mqeZZL.png)
下图是loss function的函数图,margin based 较之前两者主要是gradient 更稳定了,然后margin是相对距离
![](https://i.imgur.com/7jTGfHm.png)

## 采样策略
Hard Sampling：從所有候選樣本中選擇子集來訓練模型。(包括hard negative mining、OHEM、IoU-balanced Sampling等等)
[Soft Sampling](https://zhuanlan.zhihu.com/p/63954517)：為所有候選樣本安排不同的權重值。(包括Focal Loss、GHM、PISA等等)

### Naive Sample
隨機不加說明就是**均勻採樣**

很多文章說triplet loss不好就是說這個負樣本是隨機採樣的,然後說下面提到的semi-hard不好就是說在採樣負樣本時只考慮了一個正樣本

### Semi-hard sampling

對一個anchor,loop所有剩下正樣本就構建了N個正樣本對,然後每對正樣本對採樣一個負樣本,採樣規則如下:在相對正樣本距離比margin()裡的負樣本隨機採樣一個

**每對正樣本在margin內隨機採樣一個負樣本**
![](https://i.imgur.com/rjDk0qI.png)


### N-pairs sampling

基于anchor后每类挑N个.也可以看做**每类随机挑一(N?)个**
![](https://i.imgur.com/TjS7MoR.png)

### Smooth hard sampling(Lifted Structured)
挑最难的样本(离anchor最近的负样本,离正样本最近的负样本,然再挑最近的那个)
![](https://i.imgur.com/fXuJUtM.png)
![](https://i.imgur.com/Xgvhouo.png)

### Distance weighted sampling
**按離anchor的遠近給負樣本不同概率權重,越近越大.**

最佳的採樣狀態是對於分散均勻的負樣本，進行均勻地採樣
![](https://i.imgur.com/7TeJ6SP.png)

![](https://i.imgur.com/gDOnvAL.png)
**縱軸為數據梯度的方差。** 從圖中可以看出，hard negative mining方法採樣的樣本都處於高方差的區域，如果數據集中有噪聲的話，採樣很容易受到噪聲的影響，從而導致模型坍塌。隨機採樣的樣本容易集中在低方差的區域，從而使得loss很小，但此時模型實際上並沒有訓練好。Semi-hard negative mining採樣的範圍很小，這很可能導致模型在很早的時候就收斂，loss下降很慢

![](https://i.imgur.com/7NALwZc.png)


[深度學習新的採樣方式和損失函數--論文筆記](https://zhuanlan.zhihu.com/p/27748177)


1. margin based loss
[Sampling Matters in Deep Embedding Learning](https://arxiv.org/pdf/1706.07567.pdf)

2. loss 比較圖

3. 藍綠圖

4. lifted structured
[Sampling Matters in Deep Embedding Learning](https://arxiv.org/pdf/1511.06452.pdf)
