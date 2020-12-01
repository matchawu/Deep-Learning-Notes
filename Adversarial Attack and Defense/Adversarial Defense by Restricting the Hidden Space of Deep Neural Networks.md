# Adversarial Defense by Restricting the Hidden Space of Deep Neural Networks
ICCV 2019
[note](https://kami.app/xmWn2ynAFijj)
[code](https://github.com/aamir-mustafa/pcl-adversarial-defense)

## 摘要

目前的防禦大部分對於白盒攻擊不怎麼有效，
白盒攻擊對網路有所有的瞭解且可以遞迴去找到最強的擾動。

認為會造成這樣的主要原因是
這些擾動都是來自那些不同類別卻在feature space很接近的樣本
如此
只要加一些肉眼不可察覺的擾動就能完全改變模型的分類

因此作者推出了一個將feature representations盡可能分解/開的方法
也就是我們強迫所有類別的feature應該在不同類別之間分開最大化

可以大大提升robustness，甚至在白盒攻擊也有很好的效果
這樣的方法也不會影響原本在乾淨樣本上的分類

## Introduction
![](https://i.imgur.com/mFo1e08.png)

### 防禦的分類
- 被動防禦
    - 在測試期間修改輸入，使用圖像變換來對抗對抗性擾動的影響
- 積極防禦
    - 改變底層架構或learning程序
    - 在白盒攻擊上有比較高的robustness
- 但是兩種防禦都被**遞迴式的白盒攻擊**給規避了

### Contributions
提出新的防禦方法，
也就是最大程度上，將學到的feature representations盡量分開

我們注意到，在輸入域中添加擾動
會在中間特徵和輸出分類空間的高維流形中導致相應的多態性

基於這樣的觀察，因此在任兩種類別之間我們會有最小的overlap

增強類內的近似與類間的差異
並不會遇到混淆梯度的問題，這是大部分防禦方法會遇到的

> gradient masking（[梯度隱藏](https://zhuanlan.zhihu.com/p/31875682)）
> 意思是說，大部分的“對抗樣本”構建技術都是利用模型梯度來進行攻擊的。
> 比如針對某一個分類模型觀察一張最後被分類為熊貓的圖片，但這個分類結果只是因為在“熊貓”這個類別上最後的概率最大，分類器還會有很小的置信度把這個圖片當成“長臂猿”，於是攻擊者反複測試圖片空間的哪一個方向上長臂猿的概率會增加，然後就在這個方向上“推波助瀾”一下，添加一些擾動，那麼這張經過修改的新圖片就會被錯誤識別為“長臂猿”了。
> 但是，如果沒有梯度呢？針對這個熊貓的圖片，模型只輸出熊貓，不輸出其他信息，模型不透露給攻擊者有用的信息，那麼攻擊者便無法得知應該在圖片哪個方向上“推波助瀾”。
> 但這個措施本身是有問題的，雖然看起來我們使用“最可能類別”模式，而不是“概率”模式，攻擊者不知道到哪裡去找能被歸類為“長臂猿”的輸入值。但是，如果攻擊者能夠猜測到防禦弱點，由此製作“對抗樣本”，那麼圖片仍然會被錯誤歸類。這個措施並沒有讓模型更加穩定，我們只是讓攻擊者弄清楚模型防禦的弱點的線索變更少，讓攻擊變的（看起來）困難了一些而已。

## Prototype Conformity Loss

![](https://i.imgur.com/zdIcwdt.png)

### 對抗攻擊
攻擊算法試圖在最小的擾動預算內實現這一目標

![](https://i.imgur.com/bVADll2.png)

### cross entropy loss在對抗攻擊中
只是將input指定到某個以之類別，沒有辦法對乾淨和對抗的樣本做出區別
此外，它沒有明確地在學習的分類區域之間強制執行任何邊距約束
![](https://i.imgur.com/xuP3zNi.png)

### 定義overlap
between polytopes for each data sample pair (i,j) 
![](https://i.imgur.com/5TFsr7O.png)

### proposition 1
第i個input sample之類別為yi，
欲減少其和其他類別的樣本之overlap
會使得擾動大小受限制的對抗攻擊成功率降低

![](https://i.imgur.com/v3aBpDA.png)

### proposition 2
lambda: 從多邊形中心到凸外邊界多邊形的最大距離
設定不同類別的兩個最接近樣本至少要相隔margin的距離
![](https://i.imgur.com/JBAs3XH.png)

如果兩個不同類別的樣本並沒有重疊，則在擾動限制下不具有可行的擾動。

因此，增加最大分離這樣的限制可以使得攻擊變得困難。

傳統的CE loss沒有這樣的限制，會使得生成的模型容易受攻擊。

另外也可以定義**各類別的區域**，只要出現在區域外就為攻擊樣本。

### proposed objective

每個類別都分配一個固定且不重疊的p-norm ball，
並且鼓勵將屬於第i類的訓練樣本映射到其hyper-ball中心附近

![](https://i.imgur.com/yMXGdJO.png)

在模型推斷過程中，將計算所有類原型的特徵相似度，
並且僅當樣本**位於其決策區域內**時，才會為其分配最接近的類標籤：

![](https://i.imgur.com/LC4Jabm.png)

the classification rule is similar to the Nearest Class Mean (NCM) classifier
但不同的地方在於：
(a) the centroids for each class are not fixed as the mean of training samples, rather learned automati-cally during representation learning, 
中心點是不斷learn出來的，並不是簡單地用mean來當作從頭到尾固定的中心點

(b) class samples are explicitly forced to lie within respective class norm-balls
各類樣本必須放置於各類的norm-ball範圍之內

(c) feature representations are appropriately tuned to learn discriminant mappings in an end-to-end manner
對特徵表示進行適當調整，以端到端的方式學習判別式映射

(d) to avoid inter-class confusions, disjoint classification re-gions are considered by maintaining a large distance be-tween each pair of prototypes.
為了避免類間模糊，透過在**每對原型**之間保持較大的距離，來使得每個類別都不會相交

The overall loss function used for training our model is given by: 
![](https://i.imgur.com/2OMMFDh.png)
實現類內緊湊性和類間分離

輔助損失(act as companion objective functions for the final loss)![](https://i.imgur.com/r1wDZi8.png)
adding an auxiliary branch ![](https://i.imgur.com/wXcgOuF.png)將特徵映射到較低維的輸出
![](https://i.imgur.com/llaaxeM.png)

![](https://i.imgur.com/OBMOyPm.png)

這樣的functions避免了gradient vanishing並扮演了regularizers的角色，鼓勵同類靠近、不同類遠離




## 實驗
### five datasets
MNIST
Fasion-MNIST (F-MNIST)
CIFAR-10
CIFAR-100
Street-View House Numbers (SVHN)
不同資料集有不同的layer數量、model

![](https://i.imgur.com/RlfOpLZ.png)

T'代表先用來train Lce 多少個epoch (不同資料集不同次)

![](https://i.imgur.com/faZH8iy.png)

### Adversarial Training
> A. Kurakin, I. Goodfellow, S. Bengio, Y. Dong, F. Liao, M. Liang, T. Pang, J. Zhu, X. Hu, C. Xie, et al. Adversarial attacks and defences competition. InThe NIPS’17 Competi-tion: Building Intelligent Systems, pages 195–231. Springer, 2018

為用來增強目前各種防禦方法，
作者發現將此與他們提出的方法一起同時訓練乾淨與對抗樣本，
不論在黑盒還是白盒攻擊下，防禦效果會更好

![](https://i.imgur.com/0QFtelT.png)

[reference](https://medium.com/trustableai/%E9%87%9D%E5%B0%8D%E6%A9%9F%E5%99%A8%E5%AD%B8%E7%BF%92%E7%9A%84%E6%83%A1%E6%84%8F%E8%B3%87%E6%96%99%E6%94%BB%E6%93%8A-%E4%B8%80-e94987742767)
```
![](https://i.imgur.com/wWdDANA.png)
```

![](https://i.imgur.com/fgBMG85.png)


### 結果
#### 黑盒白盒攻擊
(model accuracy)

![](https://i.imgur.com/q83Gati.png)

#### 不同資料集上的表現

> 對照論文：
C. Song, K. He, L. Wang, and J. E. Hopcroft. Improving the generalization of adversarial training with domain adap-tation. arXiv preprint arXiv:1810.00740, 2018. 7 

![](https://i.imgur.com/BOH3xkG.png)

#### 不同training方法下的classification結果
![](https://i.imgur.com/yTBmRPv.png)

#### 在白盒攻擊下和其他防禦方法的比較
![](https://i.imgur.com/cTNJP1K.png)


其他關於更多實驗待補

#### Transferability Test 
類似架構的轉移性能較高
#### Ablation Analysis 
在不同的層加loss
![](https://i.imgur.com/xj1EP4V.png)

#### Identifying Obfuscated Gradients
識別模糊梯度
[混淆梯度（Obfuscated Gradients Give a False Sense of Security Circumventing Defense）](https://blog.csdn.net/tyu1853/article/details/90714581)
[文章](https://zhuanlan.zhihu.com/p/33554466)
[文章-機器之心](https://www.jiqizhixin.com/graph/technologies/2b1b138d-13b8-4e4e-8987-2ee03bdde468)

![](https://i.imgur.com/PdUy3u4.png)
