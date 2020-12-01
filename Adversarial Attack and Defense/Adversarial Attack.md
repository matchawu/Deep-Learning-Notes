---
tags: adversarial attack
---

# Adversarial Attack

### 起因
> 但是網絡的複雜結構也導致了模型的不可解釋性，使得深度神經網絡有一些違反人類視覺的特性。比如通過在樣本中添加一些人類無法察覺的非隨機擾動就會導致模型以高置信度給出一個錯誤的輸出，這種加入了微小擾動就會使模型錯誤分類的樣本被稱為對抗樣本。
* DNN對於對抗樣本的robustness不強
* 對抗樣本：添加了人眼無法察覺的噪聲，可以愚弄DNN
* 對於安全有危害
 

## 攻擊模式分類
### 白盒攻擊
- 攻擊者能夠獲知機器學習所使用的算法，以及算法所使用的參數。
- 攻擊者在產生對抗性攻擊數據的過程中能夠與機器學習的系統有所交互。

### 黑盒攻擊
- 攻擊者並不知道機器學習所使用的算法和參數，但攻擊者仍能與機器學習的系統有所交互，比如可以通過傳入任意輸入觀察輸出，判斷輸出。
    - 遷移式 transfer based
    - 訪問式 query based
        - score based
        - decision based

在實際應用中，這兩者的區別體現為：通過模型A來生成對抗樣本，進而攻擊模型B。當模型A與模型B是一個模型時，為白盒攻擊；當模型A與模型B不為一個模型時，則為黑盒攻擊。

---

### 無目標攻擊 untargeted
對於一張圖片，生成一個對抗樣本，使得標註系統在其上的標註與原標註無關，即只要攻擊成功就好，對抗樣本的最終屬於哪一類不做限制。

### 有目標攻擊 targeted
對於一張圖片和一個目標標註句子，生成一個對抗樣本，使得標註系統在其上的標註與目標標註完全一致，即不僅要求攻擊成功，還要求生成的對抗樣本屬於特定的類。

## 對抗樣本的生成方式

### FGSD (Fast gradient sign method)
![](https://i.imgur.com/5M44rrk.png)
基於**梯度**，
最大化J(x*,y)函數：以獲取對抗樣本x*
J(x*,y)函數：分類誤差的loss function(cross entropy)
添加噪聲以後的樣本**不再屬於y類別**
也要同時符合原始樣本與對抗樣本的**誤差要在一定範圍之內**
![](https://i.imgur.com/3c1nOLd.png)
![](https://pic4.zhimg.com/80/v2-ae1d8f63e17c24f12606fbea441f47ff_hd.jpg)

### FGM (fast gradient method)
推廣後的FGSD
滿足L2![](https://i.imgur.com/YTRFzgY.png)
![](https://pic1.zhimg.com/80/v2-5bc4542e20c1e9cdebc9817bf087d430_hd.jpg)

### IFGSD (Iterative gradient sign Method)
推廣後的FGSD
多次(遞迴?)應用
步伐進值：alpha
![](https://i.imgur.com/qwVZC0Q.png)
![](https://i.imgur.com/XoszqUG.png)
通常將迭代步長設置為
![](https://i.imgur.com/QZ95C8G.png)
T為迭代次數
> 在白盒攻擊時，IFGSD比FGSD效果更好


### Deepfool
基於超平面分類(實現分類的基礎)思想
那麼要改變某個樣本x的分類，最小的擾動就是將x挪到超平面上，這個距離的代價最小。多分類的問題也是類似。

### C&W (Carlini & Wagner)
與IFGSD同屬於一種迭代攻擊算法
變量w輔助尋找最小擾動r
![](https://pic1.zhimg.com/80/v2-7fc080650c65803e97b55a4b9612f8e0_hd.jpg)
![](https://i.imgur.com/hLETZ9J.png)

### Optimization based method
在達到攻擊目的(使分類器在對抗樣本上分類錯誤)的前提下，最小化對抗樣本和原始樣本之間的距離
![](https://pic1.zhimg.com/80/v2-fbea3bfe5ffc66d3127f4c19b7bed798_hd.jpg)
![](https://i.imgur.com/zyh0OrP.png)
(中間為對抗樣本和原始樣本之間的誤差)

> FGSD尤為重要，應用最廣

## 常見防禦方法分類

### 對抗訓練
對抗訓練旨在從隨機初始化的權重中訓練一個魯棒的模型，其訓練集由真實數據集和加入了對抗擾動的數據集組成，因此叫做對抗訓練。

### 梯度掩碼
由於當前的許多對抗樣本生成方法都是基於梯度去生成的，所以如果將模型的原始梯度隱藏起來，就可以達到抵禦對抗樣本攻擊的效果。

### 隨機化
向原始模型引入隨機層或者隨機變量。使模型具有一定隨機性，全面提高模型的魯棒性，使其對噪聲的容忍度變高。

### 去噪
在輸入模型進行判定之前，先對當前對抗樣本進行去噪，剔除其中造成擾動的信息，使其不能對模型造成攻擊。

---

第二篇主要介紹 defense 
[via](https://zhuanlan.zhihu.com/p/37922148)

---

第三篇介紹兩種 attack

## Deepfool
a simple and accurate method to fool deep neural networks

欲找**最小的噪聲**r並生成對抗樣本x* 可以使得對抗樣本被分類為y*，和原本x被分成y的類別不同。
![](https://i.imgur.com/sPcbBWk.png)
> 圖1.1 FGSD與Deepfool所生成對抗樣本對比
> 圖1.1中，第一行是原始樣本，分類器將其分類為鯨。第二行和第三行分別為Deepfool算法和FGSD[3]算法所生成的對抗樣本及它們添加的噪聲。雖然這兩種算法所添加的噪聲都讓分類器將樣本誤判為烏龜，但是可以明顯看出Deepfool所添加的噪聲是比較小的。
> FGSD算法所添加的擾動大小全靠作者自己設計，並不可控，而這也是基於梯度的一系列算法的共同問題。

## Universal adversarial perturbations
上面所提及的對抗樣本生成方法幾乎都是對不同的對抗樣本添加不同的噪聲，噪聲依賴於某一特定樣本的特徵

試圖**尋找一種通用的對抗擾動，使添加完該擾動後的所有原始圖片都會被誤分類為其他類別**

![](https://i.imgur.com/Tw47On9.png)

在保證不影響原始樣本的真實分佈的前提下，具有很好的泛化能力，不僅是所有輸入圖片通用，還在不同的網絡結構間通用。


---

第四篇主要介紹 defense 
[via](https://zhuanlan.zhihu.com/p/38795225)

---

第五篇：三篇 attack
[via](https://zhuanlan.zhihu.com/p/39285664)
## 1. Towards Evaluating the Robustness of Neural Networks
*2016*
本文中，作者將求取對抗樣本的過程，構建為了一個**最優化問題**
通過這樣的數學建模，原問題變成了基於一個等式約束和一個不等式約束的最小化問題。
![](https://i.imgur.com/csZPFcY.png)
(待研究)

## 2. Adversarial Patch
*2017*
通常來說，我們總是希望所添加的噪聲是人眼所無法識別的，在這一限制下，干擾分類器的識別(Imperceptible attack（無法察覺的攻擊）)
![](https://i.imgur.com/UoE25EL.png)

本文所提出的干擾並**沒有對噪聲進行不可察覺的限制**
![](https://i.imgur.com/uyIJj6S.png)

作者訓練得到一個patch，將這個patch加到任何圖片上，**都可以讓原圖被識別為patch所期望的輸出，即這是一個無差別的攻擊**，我們無需提前知道所攻擊的樣本
## 3. Robust Physical Adversarial Attack on Faster R-CNN Object Detector
*2018*
本文將不再針對簡單的圖片分類器進行攻擊，作者提出了對**目標檢測器**進行攻擊的方法
> 目標檢測,就是在一張圖片中找到並用box標註出所有的目標
> 目標檢測和目標識別不同之處在於,目標檢測只有兩類,目標和非目標
![](https://i.imgur.com/TlEAUnA.png)

目標檢測器[4]的運行過程如下圖所示：
![](https://i.imgur.com/3G1DIre.png)
![](https://i.imgur.com/fo0BMNX.png)
有目標攻擊(targetted attack)
無目標攻擊(untargetted attack)


---

第六篇主要介紹 defense 
[via](https://zhuanlan.zhihu.com/p/39329394)

---

第七篇主要介紹 defense
[via](https://zhuanlan.zhihu.com/p/41961524)

---

第八篇主要介紹 attack
[via](https://zhuanlan.zhihu.com/p/42604796)

## Adversarial Reprogramming of Neural Networks
*2018*
谷歌團隊於今年六月，基於之前對抗樣本的理念提出了對神經網絡任務進行攻擊的新思路，其中心思想是**通過對抗樣本使系統放棄原始任務，轉而執行其他任務**
[PAPER] ![](https://i.imgur.com/MpOvKSK.png)

### 算法思想

當這些圖片輸入系統後，攻擊模型將進行再編程( reprogramming)，進而拋棄本職任務而去進行其他任務（對抗任務）
![](https://i.imgur.com/4Qn9RZa.png)
上圖展示了一個簡單的對抗任務攻擊過程，其目標是讓ImageNet分類任務被攻擊後變成數方塊任務，這個聽起來有點不可思議的工作由以下幾步完成：

1）如圖1中(a)圖所示，在原始標籤和目標對抗標籤中間建立映射，即將ImageNet中的標籤[y]映射到[y-adv].

2）如圖1中(b)圖所示，將表示對抗任務的圖片嵌入到對抗程序圖片的中間（與[1]中位置隨機不同），生成用於對抗攻擊的測試圖片。

3）如圖1中(c)圖所示，將步驟2中生成的測試圖輸入原始ImageNet分類器中，達成攻擊。

### 算法實現
![](https://i.imgur.com/ZUAMIdz.png)

![](https://i.imgur.com/RQpDjZF.png)
![](https://i.imgur.com/zgHyOVW.png)
![](https://i.imgur.com/wZZ0rwA.png)
(待詳細看完)

### 實驗結果
![](https://i.imgur.com/QvW0tB0.png)

---

第九篇主要介紹 defense
[via](https://zhuanlan.zhihu.com/p/43544937)

---

第十篇
[via](https://zhuanlan.zhihu.com/p/40875129)

## On the Robustness of Semantic Segmentation Models to Adversarial Attacks
*2017*
[PAPER] **針對語義分割網絡進行攻擊** semantic segmentation
> 給定一張圖片,對圖片中的**每一個像素點進行分類**
> 始圖片是一張街景圖片,經過語義分割之後的圖片就是一個包含若干種顏色的圖片,**其中每一種顏色都代表一類**
> ![](https://i.imgur.com/3guB9TN.png)

之前介紹的對抗攻擊的文章大部分是針對分類器進行攻擊，分類任務是一種相對簡單的機器學習任務。文中作者對更為複雜的[語義分割模型](https://blog.csdn.net/u012931582/article/details/70314859)進行攻擊，測試了它們的魯棒性，分析了不同的網絡結構、模型容量和多尺度縮放對模型魯棒性的影響。
- Fast Gradient Sign Method (FGSM)
- FGSM ll
    - ![](https://i.imgur.com/DUamEmJ.png)
    - 作有目標攻擊，其攻擊目標是使模型輸出變為最初預測的最不可能的類別

- Iterative FGSM
    - 相對於FGSM的單步攻擊來說，I-FGSM分多步添加噪聲，更能擬合模型參數，因此通常表現出比FGSM更強的白盒攻擊能力
- Iterative FGSM II
    - ![](https://i.imgur.com/O8Sbhf4.png)


![](https://i.imgur.com/rpao0ZT.png)

本文中作者將之前提出的FGSM、I-FGSM算法用於攻擊現有的較為熱門的語義分割網絡，評估了它們面臨對抗攻擊時的魯棒性。並得出結論，殘差網絡、多尺度過程、條件隨機場等結構有利於增強卷積神經網絡的魯棒性。在所有的模型中，同時兼具這三個結構的額Deeplab v2網絡表現出了最強的抗攻擊能力。




---