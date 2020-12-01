# Daily

Iterative Graph Adversarial Training with Generative Perturbations

tags: ```lab``` ```2020``` ```August```

- [元大](/iM_lboSGTXWzIBbGupbQ2g)
- [HackMD -- LaTeX 語法與示範](/vJlEs9wcTc-eE9rfjTPbzA?both)
- [chiwei](https://hackmd.io/@applemaster/BJDo3oCgP)
- [對照組實驗(何向南、SVAT OVAT)](https://docs.google.com/spreadsheets/d/1_vNZXMDKKCyYl0X6YyPbe9j0Aarkm4nczVmaS0I9wlI/edit?fbclid=IwAR35A63OLY7vWx1lrfDqwqnaaJJF0em4j-K5xEZqEurbGLn7QKgjGTXbcYo#gid=0)

---

想：

- [x] 摘要與標題
- [x] 實驗留至多2~3個
- [ ] epsilon的gamma暴力取
- [x] ifgsm的每一步用不同的量
- [ ] sample min max 合理選擇
- [ ] chapter 3



---

## August 26
- [x] 二階鄰居 
- [x] 二階鄰居實驗，權重：[0.75,0.25]、[0.5,0.5]
- [x] sample
- [ ] nn.Parameter

## August 25
- [x] 加入i-fgsm在rg上
- [ ] rv是否適合加？
- [ ] sample
- [ ] 想其他方法
[語法對照](https://blog.csdn.net/cetrol_chen/article/details/89415226)


## August 24
- [transductive vs inductive](https://www.zhihu.com/question/68275921)
- 元大畫圖ver 1
- 要做的
    - epsilon
    - rg iterative
    - sampling strategy


## August 19
- [ ] 鄰居改法ver1: 先同類，再找max KL鄰居
- [x] epsilon在loss上的限制：
    - -FLAGS.gamma * tf.nn.l2_loss(e)
    - 先初步做一版，用l2 reg的想法，希望epsilon越大越好
- [x] attacked accuracy
    - 攻擊的r來自CE loss不是KL loss，這部分重做
## August 18
- [ ] 鄰居attention
- [x] cora, citeseer以外的資料集：Pumbed
- chiwei:
    - 報那篇RL的paper
    - 跑Polblogs
- 討論元大做法

## August 17
- [x] 跑實驗、調參 
    - [實驗與調參紀錄](https://docs.google.com/spreadsheets/d/1E_zDZFmmZbvwB497QzDEIgbNCX6_g7q0jRnVAHF9cGE/edit#gid=2116586390)
    - [更改epsilon_log](https://drive.google.com/drive/folders/1VTxkUhs6yD-8l6DJYqjrCy7cm8FWUMAB)
- [x] 寫x,x+r的部分
    - GCN x,x+r acc
        - 改code: alpha=0, beta=0(不看reg項)
        - 但gat_loss = True
        - 看純GCN model對x+r的acc
    - GAT x,x+r acc
        - 改code: alpha=0(不看reg項)
        - gat_loss = True
        - 看GAT model對x+r的acc
- [ ] 鄰居帶有Attention
    - [參考](https://www.tensorflow.org/versions/r1.15/api_docs/python/tf/keras/layers/Attention?hl=zh-cn)



## August 16
### [cora]
#### 看自己logits & labels：雖然效果不錯，但是收斂速度比較慢。
```
Epoch:236
Test set results: cost= 1.33159 accuracy= 0.83500 time= 0.36599
```

![](https://i.imgur.com/8mdohl7.png)



## August 14

[0814 進度報告](/L2lMtxPMRiyJjxvnnS-GAA)

- [ ] attack 實驗對照組: 只需改inputs即可
- [ ] epsilon 

## August 11
## August 10
- [x] 更改元大PPT
- [x] paper: [Adversarial Transformations for Semi-Supervised Learning](https://www.notion.so/Adversarial-Transformations-for-Semi-Supervised-Learning-a88557c507ad4c968f3226878c8a3679)
- [ ] 改向南code
- [ ] 確認姿妏學姊code

## August 7
- [x] 寫Introduction
- [x] 元大rehearsal
- [x] 討論架構
- [x] 交Introduction

## August 6
- [x] 寫Introduction
- [x] 討論架構

## August 5
- [x] 跑[對照組實驗(何向南、SVAT OVAT)](https://docs.google.com/spreadsheets/d/1_vNZXMDKKCyYl0X6YyPbe9j0Aarkm4nczVmaS0I9wlI/edit?fbclid=IwAR35A63OLY7vWx1lrfDqwqnaaJJF0em4j-K5xEZqEurbGLn7QKgjGTXbcYo#gid=0)
- [x] Latent Adversarial Training of Graph Convolution Networks
- [x] GCN smoothness 假設
- [x] 可能的架構
- [x] 寫Introduction
- [x] 跑&改GCN

## August 4

- [x] 了解Link prediction based on GNN建立subgraph的方式
- [x] 推薦系統閱讀：KGAT

### Graph Defense
:::spoiler on structure
- Adversarial Training Methods for Network Embedding
    - DeepWalk
- Adversarial Robustness of Similarity-Based Link Prediction
    - Bayesian
- Adversarial Attack on Graph Structured Data
    - RL 
- Topology Attack and Defense for Graph Neural Networks: An Optimization Perspective
    - GNN
:::
:::spoiler on attribute
- [Latent Adversarial Training of Graph Convolution Networks](https://www.notion.so/2020-08-05-Latent-Adversarial-Training-of-Graph-Convolution-Networks-278792ab44f743908df71b2294233d00)
    - GCN based
    - 在latent H上面加入擾動，比起在raw features上擾動，會更有generalization
- GraphDefense: Towards Robust Graph Convolutional Networks
- 【對照】[Batch Virtual Adversarial Training for Graph Convolutional Networks](https://www.notion.so/Batch-virtual-adversarial-training-for-graph-convolutional-networks-dbf8320758554240b0ba6e5d9007269d)
    - GCN based
    - semi-supervised
    - 改良VAT，提出
        - sample-based VAT
        - optimizier-based VAT
- Virtual Adversarial Training on Graph Convolutional Networks in Node Classification
    - 同向南大大的
- Adversarial Defense Framework for Graph Neural Network
    - GNN based
    - DefNet
:::

## August 3
[Notion](https://www.notion.so/2402e3ec941a451f83790900a0f774da?v=0b66402e223e4caeb66909d631ef38e6)
:::spoiler 在AT上找在VAT之後的手法
- [ ] [Bidirectional Adversarial Training for Semi-Supervised Domain Adaptation](https://www.notion.so/Bidirectional-Adversarial-Training-for-Semi-Supervised-Domain-Adaptation-a0efd0b7e9d94f61acdc8e3df850a0bd)
    - 改良VAT
- [ ] [Mutual Improvement Between Temporal Ensembling and Virtual Adversarial Training](https://www.notion.so/Mutual-Improvement-Between-Temporal-Ensembling-and-Virtual-Adversarial-Training-80cbdfaee5ea4c0e8e29cef2798657d0)
    - 改良VAT：更改產生擾動的方式並加快訓練速度
    - 引入ensemble的方式訓練
- [ ] [Adversarial Training and Robustness for Multiple Perturbations](https://www.notion.so/Adversarial-Training-and-Robustness-for-Multiple-Perturbations-92af7a7e830044c39e3fad572a8b72be)
    - different types of perturbations simultaneously：gradients當作一種攻擊形式，同時還考量了其他種不同的可能的攻擊形式，一起做AT
- [ ] Fast is better than free: Revisiting adversarial training
    - 用FGSM跟random initialized的方式解決AT高成本問題。
- [ ] [Adversarial Training for Free!](https://www.notion.so/Adversarial-Training-for-Free-a0c023b770074b7c858d92d0919f275c)
    - 每個mini-batch只算一個gradients去做，而不是針對每一個樣本都算獨自的gradients，減少計算量
- [ ] [Transferable Adversarial Training: A General Approach to Adapting Deep Classifiers](https://www.notion.so/Transferable-Adversarial-Training-A-General-Approach-to-Adapting-Deep-Classifiers-e1ff90f9429d46b6bf924e1056c7dce3)
    - domain adaption/類似GAN的架構去做AT
- [ ] [Defense Against Adversarial Attacks Using Feature Scattering-based Adversarial Training](https://www.notion.so/Defense-Against-Adversarial-Attacks-Using-Feature-Scattering-based-Adversarial-Training-ecfab7dabc414a03896fa77c99fa51a5)
    - 大致上概念類似，也是在X上面加擾動，遞迴式地加
- [ ] [Adversarial Transformations for Semi-Supervised Learning](https://www.notion.so/Adversarial-Transformations-for-Semi-Supervised-Learning-a88557c507ad4c968f3226878c8a3679)
    - 改動epsilon的限制方式
- [ ] [On the Convergence and Robustness of Adversarial Training](https://www.notion.so/On-the-Convergence-and-Robustness-of-Adversarial-Training-2295162a4ffe4334bc7bafb193bcd19e)
    - ICML/改善AT的運算 dynamic PGD
- [ ] [Adversarial Transformations for Semi-Supervised Learning](https://www.notion.so/Adversarial-Transformations-for-Semi-Supervised-Learning-ffe290ff33774f21ac3c01f6bf20056d)
    - 改善VAT/數學
- [ ] [Bilateral Adversarial Training: Towards Fast Training of More Robust Models Against Adversarial Attacks](https://www.notion.so/Bilateral-Adversarial-Training-Towards-Fast-Training-of-More-Robust-Models-Against-Adversarial-Atta-c532d605268246e3bcd0022ab5660fa8)
    - ICCV/數學式很多 求adv的方式不太一樣/但概念類似
- [ ] [Joint Energy-Based Models for Semi-Supervised Classification](https://www.notion.so/Joint-Energy-Based-Models-for-Semi-Supervised-Classification-734b1cd69fd44fa5be3b93dc3483fcee)
:::

#### others
- [x] link prediction 現有的code之input output
- [ ] 找VAT以後的papers 可能和Graph結合的方式
- [ ] 找attack on graph-based RS的可能加入VAT的方式


## July 31
[Notion整理表格](https://www.notion.so/216808441d1946f48878c64c8ab090d4?v=236abf26a48d4e5c8fe527f20c75d031)

#### 何向南GraphVAT用到的方法
- [x] [VAT](https://www.notion.so/VAT-a96b359bc1064e028c730f31242c0800)

#### 何向南的另一篇：關於adv RS
- [x] [Adversarial Personalized Ranking for Recommendation](https://www.notion.so/Adversarial-Personalized-Ranking-for-Recommendation-7fbba1eabd1e43d6ab158cc5348cdc6a)

#### Recommendation System

- [x] [RippleNet](https://www.notion.so/RippleNet-d6860f1f1e7b47b8a0d4c1a369170a01)
- [x] [KGCN](https://www.notion.so/KGCN-3446823d934f4956b84c5e515f2d76da)
- [x] [MKR](https://www.notion.so/MKR-40679c0cb7aa43b08afde212c940c237)

#### Link Prediction
- [x] [Link Prediction Based on Graph Neural Networks](https://www.notion.so/Link-Prediction-Based-on-Graph-Neural-Networks-891950ef524249ecab94d612ae54eed4)


:::spoiler 討論可能的方向
1. 看VAT有沒有進化版，套用在graph上面
2. 將GraphVAT應用在RS上面，但可能model要變形比較多：如何放入KG(relation multi-hot)？將分類問題轉變成link prediction問題？
:::

:::spoiler 待解決的問題
1. 為甚麼不直接用AT就好？VAT的好處？
2. 可能可以改的地方：在算和neighbors的predictions相近與否的時候，可以讓有同樣label的neighbor所佔的權重較大
3. GCN aggregate的方式？在做node classification上的方式？
4. GCN GraphSAGE GNN 之 input output 數量 需要甚麼東西(e.g.A,D,X)
5. GraphVAT在訓練的時候是把每個node都下去train還是有sample？
6. 泰勒為甚麼可以解決一階=0的問題？實際上code是怎麼運作的？d？
7. smoothness是在指甚麼？為甚麼這邊的node classification要強調smoothness但是一般的nc只計算CEloss？
:::

## July 30

- [x] [口試委員意見](https://www.notion.so/60b7443a49a04a17860b94bfffae7dd1)
- [x] 論文閱讀筆記：
[Graph Adversarial Training: Dynamically Regularizing Based on Graph Structure by 何向南](https://www.notion.so/Graph-Adversarial-Training-Dynamically-Regularizing-Based-on-Graph-Structure-9e3c50ba30c24145b8d3eaebbd2e6f5b)
- [x] 跑code
- [x] 討論

:::spoiler 想法
1. ~~考量相同degree的prediction應該類似~~
2. 套用在community detection上，model結果是屬於每群的機率
3. 用在RS上面，input可以是user&user+r或item&item+r，限制出來的rs結果要相似
:::

### Graph - survey papers
- [Graph embedding techniques, applications, and performance: A survey](https://www.notion.so/Graph-embedding-techniques-applications-and-performance-A-survey-6d449d8471bd40718d01953d9c52ab7b)
- [其他Notion筆記](https://www.notion.so/Graph-Survey-082961acc09144638d575a0fd2200f9b)

### Attack on graph - survey Papers
survey papers and notes
- [x] [A Survey of Adversarial Learning on Graph](https://www.notion.so/A-Survey-of-Adversarial-Learning-on-Graph-6b4fd28929914199910e60b37f1d5186)
- [x] [Adversarial Attack and Defense on Graph Data: A Survey](https://www.notion.so/Adversarial-Attack-and-Defense-on-Graph-Data-A-Survey-14e897cd03fe4747943cf3811c422e86)
- [ ] [Adversarial Attacks and Defenses on Graphs: A Review and Empirical Study]()

### Attack on graph papers with code
[Notion閱讀整理表格](https://www.notion.so/5b6ad6f41d3340e8bb77afbc724a2855?v=b647868aeb664cea87a3be4f0f687310)：整理了有code的attack on graph的papers，以及他們的分類以及手法。


問題：定義perturbation的方式為統一，且單一種方式不會多方驗證。攻擊只在乎攻擊成功率而不在乎效率問題。

### Embedding methods
[Notion閱讀整理表格](https://www.notion.so/c9806a164fd242e49036e40be20d9301?v=681d79694dc74c20a5c1b5cc6b53fab2)：整理了目前常見的graph embedding手法。

### Attack on graph-based recommendation system papers
- [Poisoning attacks to graph-based recommender systems](https://www.notion.so/Poisoning-attacks-to-graph-based-recommender-systems-b99403c741694e589418aad82ebaa07e)
    - 加入fake users, 對filler items評分使得target items能在推薦清單中越前面越好
- [A robust hierarchical graph convolutional network model for collaborative filtering](https://www.notion.so/A-robust-hierarchical-graph-convolutional-network-model-for-collaborative-filtering-8d266b6a22c3445cae1531985970cbee)
    - 更改GCN的架構，讓不同階層鄰居表示個別輸出再concat成為一條embedding；引入dropout和attention解決over-fitting和over-smoothing的問題([如何解決over-smoothing](https://www.zhihu.com/question/346942899))
- [Gcn-based user representation learning for unifying robust recommendation and fraudster detection](https://www.notion.so/Gcn-based-user-representation-learning-for-unifying-robust-recommendation-and-fraudster-detection-76a818bf6c07418c81ffa3684cd40083)

















---

[推薦系統on graph](https://zhuanlan.zhihu.com/p/66521058)

[KDD CUP](https://www.biendata.xyz/competition/kddcup_2020/)

