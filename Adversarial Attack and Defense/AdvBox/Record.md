---

tags: AdvBox

---


[TOC]



# Record
![](https://i.imgur.com/pcX7dc1.png)

* 無目標的對抗攻擊：只是讓目標模型的判斷出錯
* 有目標的對抗攻擊：引導目標模型做出我們想要錯誤判斷（比如我們想要讓分類器將貓識別為狗）
* 白盒攻擊：在已經獲取機器學習模型內部的所有信息和參數上進行攻擊
* 黑盒攻擊：在神經網絡結構為黑箱時，僅通過模型的輸入和輸出，逆推生成對抗樣本。

## 0. 版本問題
環境：
```
python 2.7 (or 3.5)
paddlepaddle 1.4.0
```
* 主要使用：
    * 百度開發的[paddlepaddle飛槳](https://www.paddlepaddle.org.cn/documentation/docs/zh/api_cn/index_cn.html)
    * [AdvBox tutorials](https://github.com/advboxes/AdvBox/tree/master/tutorials)

* 生成模型：
    * 定義模型
    * e.g. CNN on mnist
* 運行攻擊代碼：
    * 將各種攻擊方法包成module在此運行
    * ![](https://i.imgur.com/u5KphzL.png)


### 已解決問題：
- 解決v2問題
- 更改Trainer
- 更改EndStepEvent
- 增加原始圖片&對抗樣本輸出

### 待解決問題：
- 常遇到module裡的方法在新版中被移除
    - 官方AdvBox：paddle 0.14.0
    - 目前可pip安裝：1.2.0以上的版本
        - (from versions: 1.2.0, 1.2.1, 1.3.0, 1.3.1, 1.3.2, 1.4.0, 1.4.1, 1.5.0, 1.5.1, 1.5.2, 1.6.0rc0, 1.6.0)
    - 解法：
        - 使用系統管理員安裝->不行
        - python相關套件版本檢查->不行
        - docker安裝較舊版本->未嘗試(目前運行在Anaconda虛擬環境中)
## 1. 白盒攻擊基於MNIST數據集的CNN模型
### 生成模型：mnist
> CNN on mnist data using fluid api of paddlepaddle 
> 定義模型：mnist_cnn_model(img)
```
python mnist_model.py
```
### 運行攻擊代碼：FGSM
> FGSM（fast gradient sign method）(ICLR2015)：
> 通過梯度來生成攻擊噪聲，沿梯度方向使樣本更容易越過既定的分類邊界，從而形成誤判 // non-target
```
python mnist_tutorial_fgsm.py
```
![](https://i.imgur.com/RvnoD63.png) 

```
![](https://i.imgur.com/GlelTMf.png) ![](https://i.imgur.com/FBhFiqh.png) ![](https://i.imgur.com/Tl65JoN.png)
```

#### attack success, original_label=5, adversarial_label=8, count=1
#### 5->8
![](https://i.imgur.com/7IB20v4.png)  ![](https://i.imgur.com/aOG3LDj.png) 

#### attack success, original_label=6, adversarial_label=8, count=2
#### 6->8
![](https://i.imgur.com/TTVP2ba.png) ![](https://i.imgur.com/pDgJJE0.png)

#### attack success, original_label=8, adversarial_label=5, count=4
#### 8->5
![](https://i.imgur.com/pJlcLSr.png) ![](https://i.imgur.com/aviqFPz.png)

#### attack success, original_label=7, adversarial_label=8, count=5
#### 7->8
![](https://i.imgur.com/Y2EROHd.png) ![](https://i.imgur.com/lf50owG.png)


### 運行攻擊代碼：deepfool
> [deepfool](https://kknews.cc/zh-tw/code/blx8mm6.html)
```
python mnist_tutorial_deepfool.py
```
![](https://i.imgur.com/ZrRSayj.png)

![](https://i.imgur.com/jY1Oybk.png)

#### attack success, original_label=6, adversarial_label=5, count=1
![](https://i.imgur.com/idTCIVn.png) ![](https://i.imgur.com/Fm1RLrO.png)

#### attack success, original_label=7, adversarial_label=9, count=6
![](https://i.imgur.com/dijXqhK.png) ![](https://i.imgur.com/8MhBsFc.png)

### 運行攻擊代碼：MIFGSM
> Momentum Iterative Fast Gradient Sign Method (MIFGSM)
> 2018 IEEE/CVF Conference on Computer Vision and Pattern Recognition
```
python mnist_tutorial_mifgsm.py
```
![](https://i.imgur.com/Pky3Fpa.png)
![](https://i.imgur.com/OHgjx4M.png)

#### attack success, original_label=8, adversarial_label=4, count=3
#### 8->4
![](https://i.imgur.com/l303Olw.png)
![](https://i.imgur.com/OluvuGe.png)



### 運行攻擊代碼：JSMA
> Maximal Jacobian-based Saliency Map Attack (2018)基於雅可比行列式的顯著性地圖攻擊是一系列用於愚弄分類模型的對抗性攻擊方法；該方法利用雅可比矩陣，計算從輸入到輸出的顯著圖，只需要修改一小部分的輸入特徵就能達到改變輸出結構的目的。[paper note](http://jiangxj.top/2019/04/20/%E5%AF%B9%E6%8A%97%E6%94%BB%E5%87%BB_%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0/)

> 和前面l_\infty l_2不同於用l_0-norm，在物理上，這意味著目標是僅修改圖像中的幾個像素而不是擾亂整個圖像以欺騙分類器。
> 該算法一次一個地修改原始圖像的像素，並監視改變對結果分類的影響。通過使用網絡層的輸出的梯度計算saliency map來執行監視。在該map中，較大的值表示欺騙網絡以將l_target預測為圖像的標籤比原始標籤l的可能性更高。因此，該算法執行有針對性的愚弄。一旦計算出map，算法就會選擇最有效的像素來欺騙網絡並改變它。重複該過程，直到在對抗圖像中改變允許像素的最大數量或者愚弄成功為止。
```
python mnist_tutorial_jsma.py
```
#### attack success, original_label=3, adversarial_label=2, count=4
![](https://i.imgur.com/HFzXnlV.png)
![](https://i.imgur.com/zSi77iY.png)

|攻击算法|代码文件|攻擊成功率|
|-------|---------|---------|
|[lbfgs](https://arxiv.org/pdf/1312.6199.pdf)	|mnist_tutorial_lbfgs.py|-|
|[fgsm](https://arxiv.org/pdf/1412.6572.pdf)|mnist_tutorial_fgsm.py|90%以上|
|[bim](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/45471.pdf)	|mnist_tutorial_bim.py|-|
|[ilcm](https://arxiv.org/pdf/1607.02533.pdf)	|mnist_tutorial_ilcm.py|-|
|[mifgsm](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8579055)	|mnist_tutorial_mifgsm.py|99%左右|
|[jsma](https://arxiv.org/pdf/1511.07528.pdf)|mnist_tutorial_jsma.py|10%左右*|
|[deepfool](https://arxiv.org/pdf/1511.04599.pdf)	|mnist_tutorial_deepfool.py|40%左右|

* 問題
    * lbfgs.py
        程式有問題待解決
        ![](https://i.imgur.com/BBRtvp0.png)
    * bim.py & ilcm.py
        沒反應
    * jsma.py
        攻擊率很低


## 2. 白盒攻擊基於CIFAR10數據集的ResNet模型
### 生成模型：CIFAR10
```
python cifar10_model.py
```
問題：跑得很慢
![](https://i.imgur.com/mdvh2xI.png)
[cifar10_model](/6B1GfjTlSaqvQVATaHEQXA)


### 運行攻擊代碼：FGSM
```
python cifar10_tutorial_fgsm.py
```


|攻击算法|代码文件|
|-------|---------|
|bim	|cifar10_tutorial_bim.py
|fgsm	|cifar10_tutorial_fgsm.py
|deepfool	|cifar10_tutorial_deepfool.py
|jsma	|cifar10_tutorial_ jsma.py

## 3. 白盒攻擊[caffe](https://github.com/BVLC/caffe/wiki/Using-a-Trained-Network:-Deploy)下基於MNIST數據集的LeNet模型
[LeNet](https://i.imgur.com/wl4fJod.png)

### 生成模型
```

```
### 運行攻擊代碼
```
python cifar10_tutorial_fgsm.py
```

## 4. 黑盒攻擊基於MNIST數據集的CNN模型
### 生成模型：mnist
```
python mnist_model.py
```
### 運行攻擊代碼：singlepixelattack
```
python mnist_tutorial_singlepixelattack.py
```
![](https://i.imgur.com/8P0Q1GR.png)

![](https://i.imgur.com/ABQa3ii.png)


```
attack success, original_label=0, adversarial_label=7, count=1

![](https://i.imgur.com/YprbqNM.png) ![](https://i.imgur.com/UPWnH0l.png)

attack success, original_label=3, adversarial_label=7, count=2
![](https://i.imgur.com/TZXSJ5g.png) ![](https://i.imgur.com/7j1ppoQ.png)

attack success, original_label=9, adversarial_label=7, count=3
![](https://i.imgur.com/ilUN9K4.png) ![](https://i.imgur.com/SAW1bIh.png)
```


#### attack success, original_label=3, adversarial_label=0, count=1
#### 3->0
![](https://i.imgur.com/5RAYbmW.png) ![](https://i.imgur.com/XNBV3KR.png)


#### attack success, original_label=2, adversarial_label=0, count=2
#### 2->0
![](https://i.imgur.com/7UDfQaR.png) ![](https://i.imgur.com/cLh01J9.png)


#### attack success, original_label=3, adversarial_label=9, count=3
#### 3->9
![](https://i.imgur.com/KhJHeC6.png) ![](https://i.imgur.com/V5eOTOG.png)


#### attack success, original_label=6, adversarial_label=9, count=4
#### 6->9
![](https://i.imgur.com/Ery83wG.png) ![](https://i.imgur.com/w1VrUUE.png)


#### attack success, original_label=6, adversarial_label=0, count=5
#### 6->0
![](https://i.imgur.com/ZLJ1YNP.png) ![](https://i.imgur.com/3zAjfId.png)


#### attack success, original_label=7, adversarial_label=4, count=6
#### 7->4
![](https://i.imgur.com/olLiFxb.png) ![](https://i.imgur.com/uB9G4Um.png)


---

## 5. 使用FeatureFqueezing加固基于MNIST数据集的CNN模型
### 生成模型：mnist
```
python mnist_model.py
```
### 防禦
```
python mnist_tutorial_defences_feature_squeezing.py
```
https://blog.csdn.net/m0_37870649/article/details/81665836
![](https://i.imgur.com/oNR2N2n.png)


## 6. 使用GaussianAugmentation加固基于MNIST数据集的CNN模型
```
python mnist_model.py
```
```
python mnist_model_gaussian_augmentation_defence.py
python mnist_tutorial_defences_gaussian_augmentation.py
```
![](https://i.imgur.com/FLeCMz2.png)
![](https://i.imgur.com/C5q5wer.png)

## 7. 白盒攻击PyTorch下基于MNIST数据集的CNN模型
## 8. 白盒攻击PyTorch下基于IMAGENET数据集的AlexNet模型
## 9. 白盒攻击MxNet下基于IMAGENET数据集的AlexNet模型
## 10. 黑盒攻击graphpipe下的基于tensorflow的squeezenet模型
## 11. 黑盒攻击graphpipe下的基于onnx的squeezenet模型

---

## FGSM
![](https://i.imgur.com/0m9ff6T.png)

## foolbox
[link](https://foolbox.readthedocs.io/en/latest/modules/models.html#foolbox.models.KerasModel)