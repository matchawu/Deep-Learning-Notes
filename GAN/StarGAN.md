# StarGAN
multi-domain image-to-image translation

{%pdf https://arxiv.org/pdf/1711.09020.pdf %}

## Abstract

- 兩個以上的domain之間相互轉換
- StarGAN只用一個model
    - multiple datasets with different domains within a single network
    - flexibly transalting an input image to any desired target domain

## Introduction

### 用詞
* **attribute**
    * 屬性
    * e.g.髮色、性別或年齡
    * hair color, gender or age
* **attribute value**
    * 屬性的某種值
    * particular value of an attribute
        * black/brown/blond for hair color
        * female/male for gender
* **domain**
    * 具有同樣attribute value的圖片集合
    * a set of images sharing the same attribute value
        * *images of women*

### datasets
- CelebA: 
    - 40 labels
    - `5_o_Clock_Shadow Arched_Eyebrows Attractive Bags_Under_Eyes Bald Bangs Big_Lips Big_Nose Black_Hair Blond_Hair Blurry Brown_Hair Bushy_Eyebrows Chubby Double_Chin Eyeglasses Goatee Gray_Hair Heavy_Makeup High_Cheekbones Male Mouth_Slightly_Open Mustache Narrow_Eyes No_Beard Oval_Face Pale_Skin Pointy_Nose Receding_Hairline Rosy_Cheeks Sideburns Smiling Straight_Hair Wavy_Hair Wearing_Earrings Wearing_Hat Wearing_Lipstick Wearing_Necklace Wearing_Necktie Young `
- RaFD: 
    - 8 labels for 臉部表情

> 我們可以訓練多種domain來自不同的datasets，例如我們可以改變CelebA的圖片上的表情利用我們在RaFD資料及上學到的資料
We can further extend to training multiple domains from different datasets, such as jointly training CelebA and RaFD images to change a CelebA image’s facial expression using features learned by training on RaFD

### 現有技術的限制與問題
> 目前現有的model對於multi-domain image translation是沒效率也不有效的。
> [cycleGAN](https://hackmd.io/rHnLs0j1SDWIrR0e5r8sZQ)

- *沒效率*是因為如果要轉k個domains，就需要k(k-1)個generators。
    - ![](https://i.imgur.com/XJinkOX.png)
        - *translate among 4 domains*

- *不有效*是因為即使有global features from all domains，但每個generators還是沒辦法徹底利用整個training data，而只能從所有k個中的**2個domain**來學習。
    - 這樣也限制了generated images的品質表現。

    - 也因為每一個dataset是*partially labeled* 部分標記，所以不能jointly training damains from different datasets。 (3.2)

### StarGAN如何做
> our model takes in training data of multiple domains, and learns the mappings between all available domains using only a single generator.

![](https://i.imgur.com/mPbu8TV.png)

> generator要學習的並不是一個fixed translation(e.g.black-to-blond hair)

#### generator input: image & domain information
- 目標：學習如何將input圖片有彈性地轉換到相對應的target domain
    - 使用 **label (e.g., binary or one-hot vector)** 去表示domain information
    - training時隨機產生一個target domain label 
    - 在testing的時候就可以控制(選擇)domain label，使圖片能夠轉換到任何我們想要的domain

#### joint training between domains of different datasets(multi-domain image translation across different datasets)
- 在domain label的表示上，使用**mask vector**
    - 忽略未知的label，只關注某個dataset的label
    - 利用從RaFD學來的特徵，可以做到合成臉部表情(在celebA的圖片上)

### contributions
1. multi-domains mappings learning 
    ***only a single generator and a discriminator***
2. mask vector can control all available domain labels
3. better then baseline models

## Related Works
- Conditional GAN
- Image-to-Image Translation

---


## StarGAN

![](https://i.imgur.com/PPpFwbl.png)

### 3.1. Multi-Domain Image-to-Image Translation 

> 在G的輸入中添加目標領域信息，即把圖片翻譯到哪個領域這個信息告訴生成模型。
> D除了具有判斷圖片是否真實的功能外，還要有判斷圖片屬於哪個類別的能力。這樣可以保證G中同樣的輸入圖像，隨著目標領域的不同生成不同的效果
> 除了上述兩樣以外，還需要保證圖像翻譯過程中圖像內容要保存，只改變領域差異的那部分。圖像重建可以完整這一部分，圖像重建即將圖像翻譯從領域A翻譯到領域B，再翻譯回來，不會發生變化。
> 

![](https://i.imgur.com/PTapg9f.png) 
G要學會轉換input圖片x到output圖片y，附帶條件：domain label c
target domain label c 在訓練時是隨機產生的(使G可以彈性地轉換input圖片)
> train G to translate an input image x into an output image y *conditioned on the target domain label c*. We *randomly generate* the target domain label c so that G learns to flexibly translate the input image

![](https://i.imgur.com/NfAIH95.png)
也使用了一個輔助的classifier，讓一個D可以控制多個domains
也就是說D可以產出probability distributions over both sources and domain labels
> We also introduce an auxiliary輔助 classifier that allows a single D to control multiple domains. That is, our D produces probability distributions over both sources and domain labels
![](https://i.imgur.com/9UZBCe8.png)

- **Adversarial Loss**
    - ![](https://i.imgur.com/4g7ZIBo.png)
    - generated images vs real images能做區分
    - (G:input image x & target domain label c)
    - D: real or fake images
    - Dsrc(x) as a probability distribution over sources given by D

- **Domain Classification Loss**
    - 訓練D的時候，使用真實圖像在原始領域進行，訓練G的時候，使用生成的圖像在目標領域進行
    - 1 : **real image,original domain**
        - a domain classification loss of *real* images used to optimize D
        - （x,c'）是訓練集給定的
        - 真實圖片x(D的input x)能被分類到相關分布c'
        - ![](https://i.imgur.com/WaGRRfo.png)
    - 2 : **fake image,target domain**
        - 確定同樣的輸入圖片input x 在和不同的輸入target domain一起input到G的時候，G會產生不一樣的結果
        -  domain classification loss of *fake* images used to optimize G
        -  G(x,c)這張假圖片可以被分類到相關分布c
        -  x:G's input image, c:G's input domain information 
        - ![](https://i.imgur.com/e6BylWq.png)

- **Reconstruction Loss**
    - translated images preserve the content of its input images *while changing only the domain-related part* of the inputs
    - apply "**cycle consistency loss**"
    - ![](https://i.imgur.com/CfGRC7m.png)
    - G takes in the translated image G(x;c) and the original domain label c' as input 
    -  tries to reconstruct the original image x
        - loss: **L1 norm**

++使用同一個generator兩次，第一次將圖片轉成對應target domain的圖片，第二次由轉換出來的圖片重構回原本的圖片。++

- Full Objective
    - ![](https://i.imgur.com/v9KFpBU.png)
- hyper-parameters:
    - ![](https://i.imgur.com/qm5fTKG.png)**cls**:domain classification loss 相對於ad-loss的重要性
    - ![](https://i.imgur.com/KuBx8Eo.png)**rec**:reconstruction losses 相對於ad-loss的重要性
        - We use cls = 1 and rec = 10 

### 3.2. Training with *Multiple Datasets* 

*the label information is only partially known to each dataset*
兩個不同的datasets所含有的label種類可能是不一樣的

CelebA裡面含有頭髮顏色、性別等label，但並沒有臉部表情例如喜悅、悲傷等等(但RaFD有)

這樣會造成問題：在將translated image重構回原本的input image x 的時候，++我們需要完整的information on label vector c'++

- **Mask Vector : m**
    - *ignore unspecified labels and focus on the explicitly known label provided by a particular dataset*
    - **m** : 以n維one-hot vector去表示是哪個資料集
    - **n** : 使用的資料集數量
    - ![](https://i.imgur.com/OEuN19d.png)
        -  []: refers to concatenation
        - **ci** : 第i個dataset的labels(a vector)
    - The vector of the *known* label ci can be represented as either **a binary vector for binary attributes** or **a one-hot vector for categorical attributes**
    - the remaining n-1 *unknown* labels we simply assign zero values

- Training Strategy
    - G的架構和訓練一個dataset的時候一樣
    - 只有input label c~的**維度**不一樣
    - 也會將auxiliary classifier延伸，使D可以產生probability distributions over labels *for all datasets*
    - where the D tries to minimize ***only the classification error associated to the known label***

> For example, when training with images in CelebA, D minimizes ***only classification errors for labels related to CelebA attributes***, and not facial expressions related to RaFD.

- D learns all of the discriminative features for both datasets
- G learns to control all the labels in both datasets

![](https://i.imgur.com/JxHstzl.png)


## Implementation

### Improved GAN Training
> stabilize the training process
> generate higher quality images


Wasserstein GAN objective with gradient penalty 
![](https://i.imgur.com/Vfs2tpc.png)
[x](https://hackmd.io/em5VjC7RQjiuG0IABKxFAA?view)


### Network Architecture

> Adapted from **CycleGAN**, network composed of ++two convolutional layers++ with the stride size of two for downsampling, ++six residual blocks++, and ++two transposed convolutional layers++ with the stride size of two for upsampling.

> We use ++[instance normalization](https://hackmd.io/7rIAk8SkSKqpKpuENK6l_Q?view)++ for the ++generator++ but no normalization for the discriminator

> We leverage ++PatchGANs++ for the ++discriminator++ network, which classifies whether local image patches are real or fake. 


## Experiments

### 5.2. Datasets

- CelebA
> 202,599張名人的圖片, 每一張標註有40個binary attributes
> 128x128 
> 隨機取2000張做為test set其他的當作training
> 7 domains using the following attributes: 
> hair color (black, blond, brown), gender (male/female), and age (young/old). 

- RaFD
> 4,824張圖片(collected from 67 participants) 
> Each participant makes 8 facial expressions in 3 different gaze directions, which are captured from 3 different angles. 
> 128x128



### 5.3. Training
- Adam 
    - beta1 = 0.5 
    - beta2 = 0.999
For data augmentation we flip the images horizontally with a probability of 0.5
- 1 G update after 5 D updates 
- batch size = 16
- For experiments on CelebA, we train all models 
    - learning rate = 0.0001 for the first 10 epochs 
    - linearly decay the learning rate to 0 over the next 10 epochs
- To compensate for the lack of data, when training with RaFD 
    - we train all models for 100 epochs 
    - with a learning rate of 0.0001 
    - apply the same decaying strategy over the next 100 epochs

### 5.4. Experimental Results on CelebA 

![](https://i.imgur.com/L6dN1x7.png)

### 5.5. Experimental Results on RaFD

![](https://i.imgur.com/1gHUsQ2.png)

### 5.6. Experimental Results on CelebA+RaFD 

![](https://i.imgur.com/rHjXAP5.png)

## Conclusion

- using a single generator and a discriminator
    - scalable image-to-image translation model among multiple domains 
- higher visual quality
    - compared to baseline models
- simple mask vector 
    - utilize multiple datasets with different sets of domain labels

## reference
https://ptorch.com/news/116.html
https://blog.csdn.net/stdcoutzyx/article/details/78829232
https://juejin.im/post/5cf27a2151882544401f96f1
https://www.cnblogs.com/Thinker-pcw/p/9785379.html
[kami note](https://web.kamihq.com/web/viewer.html?state=%7B%22ids%22%3A%5B%221JTd68FXr-pXIzlq6GbrIuXIMa7AsLmEM%22%5D%2C%22action%22%3A%22open%22%2C%22userId%22%3A%22110423678406540730896%22%7D&filename=null)

## 其他類似或衍生方法
- GANimation:
    - https://arxiv.org/pdf/1807.09251.pdf
    - https://github.com/albertpumarola/GANimation
    - https://www.linkresearcher.com/theses/f7f02040-dbbb-46f3-9fe5-8329e99020fd
    - starGAN產生的結果是離散的，這裡產生的是GIF
    - 引入A和C
        - A: attention
        - C: RGB著色image

![](https://i.imgur.com/ZqLosIu.jpg)


- STARGAN-VC: 
    - NON-PARALLEL MANY-TO-MANY VOICE CONVERSION USING STAR GENERATIVE ADVERSARIAL NETWORKS
    - http://www.kecl.ntt.co.jp/people/kameoka.hirokazu/publications/Kameoka2018SLT12_published.pdf
    - 將starGAN用在語音上

- Non-Parallel Many-to-Many Cross-Lingual Voice Conversion Project Report
    - http://web.stanford.edu/class/cs224n/reports/custom/15722889.pdf

- SemiStarGAN: 
    - Semi-Supervised Generative Adversarial Networks for Multi-Domain Image-to-Image Translation
    - http://iagentntu.github.io/people/pdf/Hsu_ACCV18_SemiStarGAN.pdf
    - 由於先天具有完整標註的資料集很難取得因此加入Y model去做semi的starGAN
    - domain classification 輔助unlabeled data做self-ensembling