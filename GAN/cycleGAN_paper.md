# cycleGAN
slide:https://hackmd.io/jf7iIYNSSBm-Qek8DL6ptA?both

![](https://i.imgur.com/qfBUaQ2.png)

> 做Cross Domain的轉換
> 光是有上面那row不夠
> 

但這樣的架構也不是沒有極限的，作者提到了只有在兩個domain分享類似的語義內容才能成功，斑馬跟馬之間可以成功轉換，但狗跟貓之間就無法轉換。

[ref](https://data-sci.info/2017/05/25/cyclegan/)
![](https://i.imgur.com/qtEG3LM.png)
![](https://i.imgur.com/g4xtaAJ.png)

![](https://i.imgur.com/89r3QLe.png)

```
Generator  G:X→Y : translates images from  X  to  Y  (e.g. horse to zebra)
Generator  F:Y→X : translates images from  Y  to  X  (e.g. zebra to horse)
Discriminator  DX : scores how real an image of  X  looks (e.g. does this image look like a horse?)
Discriminator  DY : scores how real an image of  Y  looks (e.g. does this image look like a zebra?)
```

詳細的架構
https://hardikbansal.github.io/CycleGANBlog/

## Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks

### Abstract
- Our goal is to learn a mapping G : X → Y such that the distribution of images from G(X) is indistinguishable from the distribution Y using an adversarial loss.
- where paired training data does not exist, including collection style transfer, object transfiguration改變形象, season transfer, photo enhancement, etc. 
- for unpaired image-to-image translation.

### 1. Introduction 
![](https://i.imgur.com/aWidgHq.png)
- unpaired training data!
    - 來自兩個領域的圖片並沒有相互對應的關係
- capturing special characteristics of one image collection and figuring out how these characteristics could be translated into the other image collection, all in the absence of any paired training examples. 
    - 嘗試著找到圖像的特色並想辦法如何轉換到另一個domain

- However, obtaining paired training data can be difficult and expensive. 
    - output很複雜可能需要藝術創作、資料集太小、object transfiguration需要改變物體的型態(output沒有well-defined)

- We assume there is some underlying relationship between the domains – for example, that they are two different renderings of the same underlying world – and seek to learn that relationship.
    - 假設有一些未明瞭的關係存在於兩個domain之間，例如他們只是兩個不同的效果圖(它們是同一潛在世界的兩種不同的渲染)

- 雖然沒有paired samples，我們可以在集合層面(at the level of sets)做supervision:
    - we are given one set of images in domain X and a different set in domain Y .
    - We may train a mapping G : X → Y such that the output ˆ y = G(x), x ∈ X, is indistinguishable from images y ∈ Y by an adversary trained to classify ˆ y apart from y.

- training both the mapping G and F simultaneously, and adding a cycle consistency loss [60] that encourages F(G(x)) ≈ x and G(F(y)) ≈ y

### 2. Related work
- Generative Adversarial Networks (GANs)
    - adversarial loss that forces the generated images to be, in principle, indistinguishable from real images.
    - We adopt an adversarial loss to learn the mapping such that the translated image cannot be distinguished from images in the target domain
- Image-to-Image Translation
    - However, unlike these prior works, we learn the mapping without paired training examples
- Unpaired Image-to-Image Translation
    - the goal is to relate two data domains, X and Y
        - Rosales et al. [37] propose a Bayesian framework that includes a prior based on a patch-based Markov random field computed from a source image, and a likelihood term obtained from multiple style images.
        - CoupledGANs [28] and cross-modal scene networks [1] use a weight-sharing strategy to learn a common representation across domains.
        - Liu et al. [27] extends this framework with a combination of variational autoencoders [23] and generative adversarial networks.
    -  the input and output to share certain “content” features even though they may differ in “style“. They also use adver-sarial networks, with additional terms to enforce the output to be close to the input in a predefined metric space
        -  such as class label space [2], image pixel space [42], and image feature space [45].
    -  our formulation does not rely on any task-specific, predefined similarity function between the input and output, nor do we assume that the input and out-put have to lie in the same low-dimensional embedding space
    -  general-purpose solution for many vision and graphics tasks. 
- Cycle Consistency
    - In this work, we are introducing a similar loss to push G and F to be consistent with each other.
- Neural Style Transfer
    - Our main focus, on the other hand, is learning the mapping between two domains, rather than between two specific images, by trying to capture correspondences between higher-level appearance structures. 
    - Therefore, our method can be applied to other tasks, such as painting→ photo, object transfiguration, etc

### 3. Formulation
- two mapping:
    - G : X → Y 
    - F : Y → X
- two adversarial discriminators
    - Dx
        - {x} 
        - {F(y)}
    - Dy
        - {y}
        - {G(x)}
- adversarial losses
    - matching the distribution of generated images to the data distribution in the target domain
- cycle consistency loss
    - prevent the learned mappings G and F from contradicting each other

#### 3.1. Adversarial Loss 
1. G : X → Y and its discriminator DY 
    ![](https://i.imgur.com/o0gh1CG.png)
2. F : Y → X and its discriminator DX
    ![](https://i.imgur.com/LuXVD4T.png)

#### 3.2. Cycle Consistency Loss 
REASON:
> However, with large enough capacity, a network can map the same set of input images to any random permutation of images in the target domain, where any of the learned mappings can induce an out-put distribution that matches the target distribution. 
> generator可以拿domain x裡隨便一張圖片騙過discriminator x 

the learned mapping functions should be cycle-consistent:

![](https://i.imgur.com/b4sQ7QN.png)
forward cycle consistency
![](https://i.imgur.com/R8pebZl.png)
backward cycle consistency
![](https://i.imgur.com/NIP5X4t.png)
![](https://i.imgur.com/dxDdZzF.png)

> we also tried replacing the L1 norm in this loss with an adversarial loss between F(G(x)) and x, and between G(F(y)) and y, but did not observe im-proved performance.
> 嘗試加入L1 norm但沒有顯著效果提升
#### identical loss
![](https://i.imgur.com/yyNrmJr.png)
The effect of the identity mapping loss on Monet's painting→ photos. From left to right: input paintings, CycleGAN without identity mapping loss, CycleGAN with identity mapping loss. **The identity mapping loss helps preserve the color of the input paintings.** 

(refer to author's code)
本來我要從X經過G生成fake_Y，
但如果我把Y輸入進G呢？它還是應該生成fake_Y,我們可以稱為fake_Y2；
也就是說，本來生成器G是用來生成Y這種風格的影象的，如果輸入本身就是Y，那麼就更應該生成Y這個影象了，
這就是要讓這個生成器G能夠做到identity mapping，所以可以計算fake_Y2和輸入Y的L1-loss，稱之為identity-loss；
同理，對於生成器F，如果輸入Y，就會生成fake_X;
但如果我把X輸入F，那麼就得到fake_X2,也要讓生成器F具備identity mapping的能力；
計算二者的L1-loss，也是作為identity-loss的一部分
![](https://i.imgur.com/w1xgJTR.png)
![](https://i.imgur.com/eh1yW3A.png)



#### 3.3. Full Objective
![](https://i.imgur.com/ixqrZaY.png)
- λ controls the relative importance of the two objectives 控制兩種loss的相對重要性
- we aim to solve:
    - ![](https://i.imgur.com/j3xqUU8.png)


### 4. Implementation
- Network Architecture
    - ++Generator++
        - 兩個stride-2的卷積
        - 和數個residual blocks
        - (Stride: kernel map在移動時的步伐長度 S)
    - ++Discriminator++
        - 我們運用70 * 70 PatchGANs
- Training details
    - we replace the negative log likelihood objective by **a least square loss** . 不使用log 而改成平方 來計算ad-loss (least-squares loss)
        - ![](https://i.imgur.com/wWd3rZF.png)
        - This loss performs more stably during training and generates higher quality results. 表現得更穩定 也會產出較好的圖像
    - to reduce model oscillation 減少模型震盪
        - update the discriminators DX and DY **using a history of generated images** rather than the ones produced by the latest generative networks. 利用過去generate出來的圖片來更新Discriminators而非用最新的(前次的)網路產出來的圖片來更新
        - We keep an image buffer that stores the 50 previously generated images.有一個image buffer儲存前50次產生的圖片
    - 令λ = 10 ，使用Adam優化，base learning rate = 0.0002. 
        - We keep the same learning  rate for the first 100 epochs and linearly decay the rate to zero over the next 100 epochs.

### 5. Results 
https://github.com/junyanz/CycleGAN

---
### identity mapping 衡等函數
![](https://i.imgur.com/OUEdo2y.png)
傳回和其輸入值相同
在resNet的論文裡面強調了他可以達成identity mapping的效果：
> 作者認為ResNet的效能很好主要是因為identity mapping的存在

---
### Instance Normalization
[read](https://www.jiqizhixin.com/articles/2018-08-29-7)
[reference](https://zhuanlan.zhihu.com/p/56542480)
![](https://i.imgur.com/1Xo5qlm.png)
適用於批量較小且單獨考慮每個像素點的場景中，因為其計算歸一化統計量時沒有混合批量和通道之間的數據，對於這種場景下的應用，我們可以考慮使用IN
適合對單個像素有更高要求的場景的歸一化算法（IST，GAN等）
單通道，單樣本上的數據進行計算

有兩個場景建議不要使用IN:
- MLP或者RNN中：因為在MLP或者RNN中，每個通道上只有一個數據，這時會自然不能使用IN；
- Feature Map比較小時：因為此時IN的採樣數據非常少，得到的歸一化統計量將不再具有代表性。

---
### PatchGAN
[reference](https://www.slideshare.net/xavigiro/imagetoimage-translation-with-conditional-adversarial-nets-upc-reading-group)
(Markovian discriminiator)
設計DISCRIMINATOR的方法
做法：設計一個PATCH(補丁)，只在上面計算loss
大小通常設為70x70 (經驗)
將最後每個得出的結果取平均值
unlike普通的GAN:整個畫面一起看，只是一言堂
![](https://i.imgur.com/hbfdfas.png)
![](https://i.imgur.com/XPmvwh5.png)
![](https://i.imgur.com/OvPye5W.png)

> L2和L1损失函数有可能在图像生成中造成模糊结果。尽管这些对高频清晰度而言效果较差，但在许多情况下仍能准确地捕获低频。对于这些问题，我们不需要一个全新的网络在低频部分进行纠正。L1已经可以完成了。

> 这使得GAN的判别器仅模拟高频结构，依靠L1来强制低频部分的正确性。对于模拟高频，只要将注意力限制在局部图像块中结构就可以了。

> 只在補丁（patch）範圍內對結構進行懲罰。這個判別器嘗試在一幅圖的每個N×N大小的補丁上進行real or fake的判斷。我們在整個圖片上運行這個判別器，並對所有的結果取均值，以避免判別器的極端輸出。
> 

> N可以比image的尺寸小很多並且仍舊可以產生高質量的結果。這是有利的，因為一個更小的PatchGAN有更少的參數，運行更快，並且可以在任意大小的圖片上運行。

other:
[ref](https://blog.csdn.net/xiaoxifei/article/details/86506955)
一般的GAN是只需要輸出一個true or fasle 的矢量，這是代表對整張圖像的評價；
但是PatchGAN輸出的是一個N x N的矩陣，這個N x N的矩陣的每一個元素，比如a(i,j) 只有True or False 這兩個選擇
（label 是N x N的矩陣，每一個元素是True 或者False），

這樣的結果往往是通過卷積層來達到的，因為逐次疊加的捲積層最終輸出的這個N x N 的矩陣，
其中的每一個元素，實際上代表著原圖中的一個比較大的感受野，也就是說對應著原圖中的一個Patch，
因此具有這樣結構以及這樣輸出的GAN被稱之為Patch GAN

other:
[ref](https://zhuanlan.zhihu.com/p/38411618)
為什麼選擇PatchGAN?

之前在介紹AE和VAE的時候有說，用L1和L2 loss重建的圖像很模糊，也就是說L1和L2並不能很好的恢復圖像的高頻部分(圖像中的邊緣等)，但能較好地恢復圖像的低頻部分(圖像中的色塊)。為了能更好得對圖像的局部做判斷，作者提出patchGAN的結構，也就是說把圖像等分成patch，分別判斷每個Patch的真假，最後再取平均！作者最後說，文章提出的這個PatchGAN可以看成所以另一種形式的紋理損失或樣式損失。在具體實驗時，不同尺寸的patch，最後發現70x70的尺寸比較合適。

other:
[ref](https://blog.csdn.net/weixin_35576881/article/details/88058040)
有什麼好處呢？直觀上理解就可以了，普通GAN輸出一個數，像是一言堂，PatchGAN輸出一個矩陣，最終結果求平均，考慮到圖像的不同部分的影響，就像考慮了多人的建議然後給出決定。
PatchGAN並不神秘，其只是一個全卷積網絡而已，只是最終輸出是一個特徵圖X，而非一個實數.它就相當於對圖像先進行若干次70x70的隨機剪裁，將剪裁後圖像輸入普通的判別器，然後對所有輸出的實數值取平均

---
### downsampling & upsampling
> also see: downsampling, upsampling/ oversampling, undersampling
> 

downsampling即下採樣，主要是對數字信號進行下採樣操作，例如數字圖像處理中對圖片進行壓縮時，N * N的矩陣變成了(N/2) * (N/2)，這個步驟就是對原圖片進行了下採樣。
upsampling與downsampling概念相反，也可以理解成插值(interpolation)。舉個例子，比如在放大某個數字圖像的時候，新放大的圖像的某些像素點的值是需要預測插值的，這個插值的過程其實就是上採樣。

---
#### 參考資料
https://blog.csdn.net/hhy_csdn/article/details/82913776
https://www.twblogs.net/a/5c9bc545bd9eee7523882703
https://www.machunjie.com/deeplearning/203.html
https://zhuanlan.zhihu.com/p/28342644
https://data-sci.info/2017/05/25/cyclegan/
https://medium.com/@yaoyaowd/%E8%AF%BB%E8%AE%BA%E6%96%87%E4%B9%9F%E8%AF%BB%E4%BB%A3%E7%A0%81-cycle-gan%E4%B8%8Epix2pix-gan-24e36fce71ed
https://junyanz.github.io/CycleGAN/

http://shikib.com/CycleGan.html
https://www.itread01.com/content/1544398959.html

#### code
"it works!":
https://github.com/eriklindernoren/Keras-GAN
pytorch(orginal paper):
https://github.com/junyanz/CycleGAN/tree/master/models
keras:
eriklindernoren/Keras-GAN
https://github.com/eriklindernoren/Keras-GAN/blob/master/cyclegan/cyclegan.py

https://blog.csdn.net/jiongnima/article/details/80113976
https://blog.csdn.net/weixin_40548136/article/details/86014596

How to Implement CycleGAN Models From Scratch With Keras
https://machinelearningmastery.com/how-to-develop-cyclegan-models-from-scratch-with-keras/


#### paper note
https://web.kamihq.com/web/viewer.html?state=%7B%22ids%22%3A%5B%221huzJJhQNxObqlfIy4ptZK8DjQ-TJ49fb%22%5D%2C%22action%22%3A%22open%22%2C%22userId%22%3A%22110423678406540730896%22%7D&filename=null