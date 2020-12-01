---
tags: paper
---

# Defenses against Adversarial Attacks
[Paper:Threat of Adversarial Attacks on Deep Learning
in Computer Vision: A Survey](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8294186)

[TOC]

##  三個方向
1. modified training during training or modified input during testing
2. modifying networks
3. external models as network add-on when classifying unseen examples

1.和nn model較無關
2.3.和nn model有關
![](https://i.imgur.com/mm3PoKA.png)

2.3.底下可以再細分為
- complete defense
    - 在對抗樣本上達到原本的目標 with acceptable accuracy
- detection only
    - 對於前在對抗樣本做出拒絕，停止更進一步的processing

2.3.的差別
- modifying a network
    - training時，在原本的DNN架構/參數上做改變
- employing an 'add-on'
    - 保留原本的model，在testing再在後面加上external model

以下介紹都按照此分類架構：

## A. MODIFIED TRAINING/INPUT 修改訓練過程/ 輸入數據
### ==✱ brute-force adversarial training==
蠻力對抗訓練


#### 提出：對抗樣本可以用來提升adversarial training(or a network)
#### 做法：通過不斷輸入新類型的對抗樣本並執行對抗訓練，從而不斷提升網絡的魯棒性

因為必須要更多的training/data size因此稱之暴力法

在暴力法對抗訓練被視為 正規化網路(避免overfitting)
這樣做也增強了robustness

#### 效果：有論文指出，再多的資料量還是有方法可以攻擊

### ==✱ data compression as defense==
數據壓縮

許多分類模型用到的資料包含了JPEG格式的圖片

- [A study of the
effect of JPG compression on adversarial images.](https://arxiv.org/abs/1608.00853)
    - network: [OverFeat](https://zhuanlan.zhihu.com/p/66154322)
    - dataset: ImageNet
    - 提出：JPG壓縮實際上可以在很大程度上逆轉分類精度的下降，讓對抗樣本失敗。
    - 但本文也指出光是壓縮並不是一個有效的防禦方法。

- [Countering
adversarial images using input transformations](https://arxiv.org/abs/1711.00117)
    - [EYD note](https://zhuanlan.zhihu.com/p/46857716)
    - 被駁斥為混淆梯度
        - ![](https://i.imgur.com/lA0DBx2.png)
    - network: ResNet-50 model
    - dataset: ImageNet
    - 主要是透過對input image的轉換來減輕對抗樣本的影響。
    - 在餵進網路前先做轉換(*bit-depth reduction, JPEG compression, total variance minimization, and image quilting*)，得到一個trained CNN來自transformed images
    - 優勢：
        - non-differentiable nature
        - inherent randomness
        - difficult for an adversary to circumvent the defenses

- [Keeping the Bad Guys Out: Protecting and Vaccinating Deep Learning with JPEG Compression](https://arxiv.org/abs/1705.02900)
    - network: convolutional neural networks
    - dataset: CIFAR-10 & German Traffic Sign Recognition Benchmark (GTSRB)
    - JPEG壓縮的一個重要組成部分是它能夠去除圖像方形塊內的高頻信號分量。這樣的操作等效於圖像的選擇性模糊，有助於消除附加的擾動。
    - 此外，我們提出了一種基於集合的技術，該技術可以從給定的性能良好的DNN快速構建，並從經驗上展示出這種利用JPEG壓縮的集合如何在不要求模型知識的情況下保護模型免受多種類型的對抗。(此處用了FGSM和DeepFool)
    - 即使得到了不錯的防禦效果，但在如C&W這些比較強的攻擊方法便沒有多做分析

- [JPEG-resistant adversarial images]()
    - 指出了那些對抗樣本可以不受JPEG壓縮影響。

- Compression under Discrete Cosine Transform DCT 也被發現不足


#### 這些壓縮方法之缺點：
程度較大的壓縮常常也會讓分類失誤變高，程度過小的壓縮不足以移除對抗樣本

- [Enhancing robustness of machine learning systems via data transformations]()
    - 使用PCA來壓縮input data增強robustness，但[Feature squeezing mitigates
and detects carlini/wagner adversarial examples]()指出這樣的壓縮方法破壞了圖片的結構，會讓分類效果因此變差

### ==✱ foveation based defense==
基於中央凹機制的防禦

- [Foveation-based mechanisms alleviate adversarial examples](https://arxiv.org/abs/1511.06292)
    - network: AlexNet, GoogLeNet and VGG
    - dataset: ImageNet
    - generate adv samples: L-BFGS
    - [EYD note](https://zhuanlan.zhihu.com/p/49479448)
    - foveation mechanism
        - applying neural network in different regions of images
        - It is hypothesized that CNN-based classifiers trained on large datasets, such as ImageNet [11] are generally robust to scale and translation variations of objects in the images.
        - 基於以下假設：在大型數據集上訓練的基於CNN的分類器對圖像中對象的縮放和平移變化具有魯棒性，但對抗樣本沒有。
        - on L-BFGS & FGSM
        - 還沒有在更強的攻擊方法下呈現良好的防禦效力

### ==✱ data randomization and other methods==
數據隨機化方法及其他方法

- [Adversarial Examples for Semantic Segmentation and Object Detection](https://arxiv.org/abs/1703.08603)
    - network: [FCN](https://www.itread01.com/content/1547086456.html), AlexNet, VGG, ZFNet
    - dataset: PascalVOC
    - adv samples: Dense Adversary Generation(DAG)
    - 發現對對抗樣本進行隨機縮放會減少他的強度。
    - [code](https://paperswithcode.com/paper/adversarial-examples-for-semantic#code)
- [Learning Adversary-Resistant Deep Neural Networks](https://arxiv.org/abs/1612.01401)


也可以：
- adding random padding
- transform input data
- [data argumentation圖像增強](https://zhuanlan.zhihu.com/p/41679153)  (效果僅有些微)

使用兩個隨機化操作：
1）隨機調整大小（random resizing）；
2）隨機填充(random paddng)。
首先對輸入圖像的大小進行隨機調整（調整後大小隨機），然後在調整大小後的圖像周圍進行隨機填充零（隨機選擇填充位置）。

對抗攻擊從生成過程來看可以分為：
- 單步攻擊，只執行一步梯度計算：
    - （如FGSM）被證明具有更好的遷移能力，但是其攻擊性較差，可能不足以欺騙網絡。
- 迭代攻擊，進行多次迭代進行攻擊：
    - 從效果來看，迭代攻擊生成的對抗樣本容易過擬合到特定的網絡參數，遷移性較弱。

正是因為迭代攻擊的泛化能力不強，所以作者考慮低級圖像變換（例如，調整大小、填充、壓縮等）可能會破環迭代攻擊生成的對抗擾動的特定結構，從而很好的防禦對抗攻擊。

---

## B. MODIFYING THE NETWORK 修改網絡
完全防禦


### ==✱ deep contractive networks==
深度壓縮網絡

[Towards deep neural network architectures robust to adversarial examples](https://arxiv.org/abs/1412.5068)
提出方法：**深度壓縮網絡（Deep Contractive Networks）**
使用了類似CAE的平滑懲罰項，成功防禦L-BGFS [torch code(not original)](https://github.com/aaronmckinstry706/toward-robust-dnn)

觀察：若是將去噪AE堆疊在原本的網路上會使得網路更加脆弱

> [Contractive autoencoder](https://www.twblogs.net/a/5b8d077e2b71771883398862)是autoencoder的一個變種，其實就是在autoencoder上加入了一個規則項，它簡稱CAE，可以防止過擬合

### ==✱ gradient regularization/masking==
梯度正則化/ 遮罩

- [Improving the Adversarial Robustness and Interpretability of Deep Neural Networks by Regularizing their Input Gradients](https://arxiv.org/abs/1711.09404)
    - network: CNN
    - dataset: MNIST
    - generate adv samples: FGSM, JSMA, TGSM
    - 透過在gradient上的正規化，讓較小的對抗性擾動就不可能徹底改變訓練模型的輸出
    - 這種方法和brute-force結合會有很好的robustness
    - 但是這種方法也使得訓練複雜度增加
    - [tf code](https://github.com/dtak/adversarial-robustness-public)



### ==✱ defensive distillation==
防守性蒸餾

- [Distilling the Knowledge in a Neural Network](https://arxiv.org/abs/1503.02531)
    - [EYD note](https://zhuanlan.zhihu.com/p/37922148) 蒸餾法
    - dataset: MNIST, ASR, JFT
    - network: DNN
    - 提高網路的彈性去適應微小的擾動
    - C&W方法據稱可以成功攻破這種防禦機制
![](https://i.imgur.com/FIwuLkx.png)


### ==✱ biologically inspired protection==
生物啓發的防禦方法

- [Biologically inspired protection of deep networks from adversarial attacks](https://arxiv.org/abs/1703.09202)
    - network: MLP+CNN
    - dataset: MNIST
    - 觀察：Goodfellow等人對線性假設
    - 做法：使用高度非線性激活函數

Brendel和Bethge聲稱由於計算的數量限制，攻擊在生物學啟發的保護上失敗了。他們稱再次穩定計算可以成功攻擊受保護的網絡。

### ==✱ parseval networks==
帕網絡

- [Houdini: Fooling Deep Structured Prediction Models](https://arxiv.org/abs/1707.05373)
    - 以生成專門針對所考慮任務的最終績效指標而量身定制的對抗示例
    - 應用到語音識別，姿勢估計和語義分割等一系列應用
    - 提出：Parseval network
    - 做法：employ a layer-wise regularization by controlling the global **Lipschitz constant** of the network
    - 可以通過對這些功能保持較小的Lipschitz常數來克服小輸入擾動的魯棒性(我們可以將網路每層都是為函數)

> 對於函數y=f（x）在定義域為D上，如果存在L ∈R ,且L>0，對任意x1,x2 ∈D，有：
**|f(x1)-f(x2)|≤ L| x1-x2|；**
則稱L為f(x)在D上的[Lipschitz常數](https://blog.csdn.net/chaolei3/article/details/81202544)。
從這裡可以看出，Lipschitz常數並不是固定不變的，而是依據具體的函數而定


### ==✱ deepcloak==
- [DeepCloak: Masking Deep Neural Network Models for Robustness Against Adversarial Samples](https://arxiv.org/abs/1702.06763)
    - network: Residual network with 164 layers
    - dataset: CIFAR10
    - 做法：在output前插入masking層
    - 認為masking層中最主要的權重對應於網路中最敏感的特徵(對於對抗攻擊而言)，**使用一對原始圖像和對抗圖像進行訓練並對這些成對圖像的前一層的輸出特徵之間的差異進行編碼**，透過強制這些主要權重為零來掩蓋這些特徵
    - [torch code](https://paperswithcode.com/paper/deepcloak-masking-deep-neural-network-models#code)

### ==✱ miscellaneous approaches==
混雜方法


### ==✱ detection only approaches==
僅探測方法
#### ++SafetyNet++
[SafetyNet: Detecting and rejecting adversarial examples robustly](https://arxiv.org/abs/1704.00103)
> 提出假設：ReLU 對對抗樣本的模式與一般圖片的不一樣，用 SVM 實現



#### ++detector subnetwork++
[On Detecting Adversarial Perturbations](https://arxiv.org/abs/1702.04267)

提出：透過二元分類訓練而成的subnetwork，偵測input是否具有對抗擾動
作法：將此subnetwork加入網路層中，並使用對抗訓練(adversarial training)幫助偵測擾動

效果：FGSM, BIM and DeepFool

#### ++exlpoiting convolution filter statistics++ 
[Adversarial Examples Detection in Deep Networks with Convolutional Filter Statistics](https://arxiv.org/abs/1612.07767)
> 介紹了同 CNN 和統計學的方法做的級聯分類器模型在分辨對抗樣本上可以有 85% 的正確率


#### ++additional class augmentation++
[On the (Statistical) Detection of Adversarial Examples](https://arxiv.org/abs/1702.06280)
新增類別去分辨出所有的對抗樣本，也就是所有對抗樣本都必須被分為這一類

[Blocking Transferability of Adversarial Examples in Black-Box Learning Systems](https://arxiv.org/abs/1703.04318)
同上，並針對黑盒攻擊

---

## C. NETWORK ADD-ONS 使用附加網絡
### ==✱ defense against universal perturbations==
防禦通用擾動

- [Defense Against Universal Adversarial Perturbations](https://ieeexplore.ieee.org/document/8578455)
    - network: CaffeNet, VGG-F network and GoogLeNet
    - dataset: ILSVRC 2012
    - 提出：**Perturbation Rectifying Network (PRN)**
    - 做法：透過這樣額外的pre-input層糾正對抗樣本，使得classifier可以正確預測。
    - 其與targeted network(真正執行分類預測的網路)的參數是分開訓練的。透過單獨訓練的網路加在原本的網路之前達到防禦的目的。
> A separate detector is trained by extracting features from the input-output differences of PRN for the training images



### ==✱ gan-based defense==
基於 GAN 的防禦

- [Generative Adversarial Trainer: Defense to Adversarial Perturbations with GAN](https://arxiv.org/abs/1705.03387)
    - network: ConvNets with ReLUs
    - dataset: CIFAR-10 and CIFAR-100
    - generate perturbation: GAT 
    - 做法：同時訓練分類器和generator
    - generator：針對分類器網路之gradient生產擾動
    - classifier：辨識乾淨與對抗樣本
    - 效果：可以防禦FGSM

> In another GAN-based defense, Shenet al.[58] use the generator part of the network to rectify a perturbed image. Shen等[58]人使用網絡的生成器部分來修正一個受干擾的圖像。

- Defense-GAN: 被駁斥為混淆梯度
![](https://i.imgur.com/4EeKGM1.png)
(倒數第三行)

### ==✱ detection only approaches==
僅探測方法

#### ++Feature Squeezing++
[Feature Squeezing: Detecting Adversarial Examples in Deep Neural Networks](https://arxiv.org/abs/1704.01155)
做法：使用兩個額外的model，去減少圖像中每個像素的顏色位深度，並對圖像執行空間平滑，得出squeezed images。
當target network(classifier)對於originalimage和squeezed image的預測相差太大的時候，這image就被視為對抗樣本。

效果：除了能防禦許多經典的攻擊方法，在強大的攻擊方法例如C&W attack上也表現得不錯
#### ++MagNet++
[MagNet: a Two-Pronged Defense against Adversarial Examples](https://arxiv.org/abs/1705.09064)
[EYD notes](https://zhuanlan.zhihu.com/p/52735215)
提出：一個框架，其使用一個或多個額外的detectors去分辨圖片是乾淨或是受擾動過的。
training：框架學習乾淨圖片的manifold(流形)
testing：如果遇到圖片和乾淨圖片的manifold相去太遠則視為對抗樣本並拒絕。如果相去不遠但不是落在manifold上的話則是將其reform to lie on the manifold

其他：Carlini and Wagner 指出這樣的方法在稍為大些的擾動下就會detect失敗
#### ++Miscellaneous Methods++
其他方法


---

## References
- https://mayi1996.top/2019/01/15/%E7%AE%97%E6%B3%95/#13-foveation-based-defense
- https://www.twblogs.net/a/5b845c892b71775d1cd06e4f

---

## Other Notes

### Poisoning attack vs Adversarial attack
![](https://i.imgur.com/WlROXC6.png)
[ref](https://towardsdatascience.com/how-to-attack-machine-learning-evasion-poisoning-inference-trojans-backdoors-a7cb5832595c)

### published white-box defenses to adversarial examples
[This list](https://www.robust-ml.org/defenses/) contains published white-box defenses to adversarial examples that have been open-sourced, along with third-party analyses / security evaluations that have been open-sourced.
- [Obfuscated Gradients Give a False Sense of Security: Circumventing Defenses to Adversarial Examples](https://arxiv.org/abs/1802.00420) [//code](https://github.com/anishathalye/obfuscated-gradients)
- [On the Robustness of the CVPR 2018 White-Box Adversarial Example Defenses](https://arxiv.org/abs/1804.03286)
- [ICLR 2018七篇對抗樣本防禦論文被新研究攻破](https://www.jiqizhixin.com/articles/2018-02-03-4)
    - [Towards Deep Learning Models Resistant to Adversarial Attacks](https://openreview.net/pdf?id=rJzIBfZAb)
    - [CASCADE ADVERSARIAL MACHINE LEARNING REGULARIZED WITH A UNIFIED EMBEDDING](https://openreview.net/pdf?id=HyRVBzap-)

### [Is there any adversarial defense method that has successfully beaten or is robust to Carlini Wagner attacks ?](https://www.reddit.com/r/MachineLearning/comments/9mipdc/d_is_there_any_adversarial_defense_method_that/)
### other survey papers
- https://arxiv.org/pdf/1712.07107.pdf
    - 將防禦分成主動防禦和被動防禦，分別介紹了三種
    - **reactive 被動**
        - ++Adversarial Detecting：在testing的時候偵測++
        - ++Input Reconstruction：CAE, denoising AE, MagNet, PixelDefense++
        - ++Network Verification：++
        - checks the properties of a neural network: whether an input violates or satisfies the property. 
    - **proactive 主動**
        - ++Network Distillation：蒸餾法++
        - ![](https://i.imgur.com/zbrNyhA.png)
        - proved that using high-temperature softmax reduced the model sensitivity to small perturbations
        - ![](https://i.imgur.com/MNKuQej.png)
        - ++Adversarial (Re)training：使用對抗樣本訓練++
        - ++Classifier Robustifying++
- https://arxiv.org/pdf/1909.08072.pdf
    - ++1.Gradient Masking/Obfuscation++
        - DEFENSIVE DISTILLATION 
        - SHATTERED GRADIENTS 
        - STOCHASTIC/RANDOMIZED GRADIENTS 
        - EXPLODING & VANISHING GRADIENTS
        - GRADIENT MASKING/OBFUSCATION METHODS ARE NOT SAFE 
    - ++2.Robust Optimization++
        - REGULARIZATION METHODS：Penalize Layers’ Lipschitz Constant, Penalize Layers’ Partial Derivative (DCN)
        - ADVERSARIAL (RE)TRAINING 
    - ++3.Adversarial Examples Detection++
- [Review of Artificial Intelligence Adversarial Attack and Defense Technologies](https://pdfs.semanticscholar.org/4af6/c0c61bbaaca04d33deea73b69b8494e0c77e.pdf?_ga=2.40393186.1115732540.1575216216-396659802.1575216216)
    - 跟這篇幾乎一模一樣
- [CertifiedDefensesforDataPoisoningAttacks](https://papers.nips.cc/paper/6943-certified-defenses-for-data-poisoning-attacks.pdf)
