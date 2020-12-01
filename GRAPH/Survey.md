# Survey
[list](https://github.com/ChandlerBang/awesome-graph-attack-papers)

## GCN
####  [🍨 A Robust Hierarchical Graph Convolutional Network Model for Collaborative Filtering](https://arxiv.org/pdf/2004.14734.pdf)
- GCN
- Collaborative Filtering
- KEYWORDS: Recommender Systems, Collaborative Filtering, Graph Convolutional Networks
- 提出原本GCN的缺陷：
    - 用fixed-length vectors去存不同階層鄰居=>可以attention來解決 
- ![](https://i.imgur.com/3fTLAaG.png)

#### [🍨 Tensor Graph Convolutional Networks for Multi-relational and Robust Learning](https://arxiv.org/pdf/2003.07729.pdf)
- GCN
- 多圖做semi-supervised classification
- ![](https://i.imgur.com/kgC69fG.png)
- ![](https://i.imgur.com/IB9eVAu.png)

#### [Topological Effects on Attacks Against Vertex Classification](https://arxiv.org/pdf/2003.05822.pdf)
- GCN


#### [All You Need is Low (Rank): Defending Against Adversarial Attacks on Graphs](https://dl.acm.org/doi/pdf/10.1145/3336191.3371789)
- GCN

#### [Edge Dithering for Robust Adaptive Graph Convolutional Networks](https://arxiv.org/pdf/1910.09590.pdf)
- GCNs


#### [GraphSAC: Detecting anomalies in large-scale graphs](https://arxiv.org/pdf/1910.09589.pdf)
- ???


#### [🍨 Robust Graph Convolutional Networks Against Adversarial Attacks](http://pengcui.thumedialab.com/papers/RGCN.pdf)
- GCN
- ![](https://i.imgur.com/he5cHUM.png)

#### [🍨 19.Adversarial Examples on Graph Data: Deep Insights into Attack and Defense](https://arxiv.org/pdf/1903.01610.pdf)
- GCNs
- ![](https://i.imgur.com/WJCpRb3.png)

#### [🍨 Power up! Robust Graph Convolutional Network against Evasion Attacks based on Graph Powering](https://arxiv.org/pdf/1905.10029.pdf)
- [note](https://web.kamihq.com/web/viewer.html?source=extension_pdfhandler&extension_handler=extension_open_button&file=https%3A%2F%2Farxiv.org%2Fpdf%2F1905.10029.pdf)
- GCNs




#### [Latent Adversarial Training of Graph Convolution Networks]()
- 在latent上面攻擊


#### [Graph Adversarial Training: Dynamically Regularizing Based on Graph Structure]()
- 何向南



## GNN

- Robust Collective Classification against Structural Attacks
    - http://www.auai.org/uai2020/proceedings/119_main_paper.pdf
    - not learning
- GNNGuard: Defending Graph Neural Networks against Adversarial Attacks
    - https://arxiv.org/pdf/2006.08149.pdf
    - GNN
- Robust Graph Representation Learning via Neural Sparsification
    - https://proceedings.icml.cc/static/paper_files/icml/2020/2611-Paper.pdf
    - GNN
    - ![](https://i.imgur.com/TLNNkP9.png)
- Graph Structure Learning for Robust Graph Neural Networks
    - https://arxiv.org/pdf/2005.10203.pdf
    - GNN
- EDoG: Adversarial Edge Detection For Graph Neural Networks
    - https://www.osti.gov/servlets/purl/1631086
    - GNN
- Towards an Efficient and General Framework of Robust Training for Graph Neural Networks
    - https://arxiv.org/pdf/2002.10947.pdf
    - GNNs
- How Robust Are Graph Neural Networks to Structural Noise? 
    - https://arxiv.org/pdf/1912.10206.pdf
    - GNNs
- Robust Graph Neural Network Against Poisoning Attacks via Transfer Learning
    - https://arxiv.org/pdf/1908.07558.pdf
    - GNNs


- 20.Topology Attack and Defense for Graph Neural Networks: An Optimization Perspective
    - GNNs

## RL
- Robust Detection of Adaptive Spammers by Nash Reinforcement Learning
    - https://arxiv.org/pdf/2006.06069.pdf
    - Nash RL
    - ![](https://i.imgur.com/AvqQSDT.png)


---

## A Survey of Adversarial Learning on Graph

### Adversarial Training
#### training with adversarial goals
:::spoiler **Graph Adversarial Training: Dynamically Regularizing Based on Graph Structure** [➔](https://arxiv.org/pdf/1902.08226.pdf)
- authors
    - Fuli Feng, Xiangnan He, Jie Tang, and Tat-Seng Chua. 2019.
- 何向南
:::



##### [🍧 Virtual adversarial training on graph convolutional networks in node classification](https://arxiv.org/pdf/1902.11045.pdf)
- Ke Sun, Zhouchen Lin, Hantao Guo, and Zhanxing Zhu. 2019. Virtual adversarial training on graph convolutional networks in node classification. InChinese Conference on Pattern Recognition and Computer Vision (PRCV). Springer, 431–443. 
- 看不出來與向南的差異


##### [🍧 Topology Attack and Defense for Graph Neural Networks: An OptimizationPerspective](https://arxiv.org/pdf/1906.04214.pdf)
- Kaidi Xu, Hongge Chen, Sijia Liu, Pin-Yu Chen, Tsui-Wei Weng, Mingyi Hong, and Xue Lin. 2019. Topology Attack and Defense for Graph Neural Networks: An OptimizationPerspective. arXiv preprint arXiv:1906.04214(2019). 
- [note](https://web.kamihq.com/web/viewer.html?source=extension_pdfhandler&extension_handler=extension_open_button&file=https%3A%2F%2Farxiv.org%2Fpdf%2F1906.04214.pdf)
- [code](https://github.com/KaidiXu/GCN_ADV_Train)


#### training with adversarial examples
:::spoiler Can Adversarial Network Attack be Defended? [➔](https://arxiv.org/pdf/1903.05994.pdf)
- authors
    - Jinyin Chen, Yangyang Wu, Xiang Lin, and Qi Xuan. 2019.
- [note](https://web.kamihq.com/web/viewer.html?source=extension_pdfhandler&extension_handler=extension_open_button&file=https%3A%2F%2Farxiv.org%2Fpdf%2F1903.05994.pdf)
- GNNs，但裡面都在講GCNs???!
- Methods
    - Global Adversarial Training (Global-AT).
        - ![](https://i.imgur.com/wWHkUV1.png)
    - Target Label Adversarial Training (Target-AT)
        - (protect the target labeled nodes from attack)-> only focus on the target labeled nodes in Ts
    - Smooth Defense
        - 蒸餾法 把GCN的output變得更generalized才不會在遇到perturbations的時候會受到影響很大
:::



:::spoiler ☑ Batch Virtual Adversarial Training for Graph Convolutional Networks [➔](https://arxiv.org/pdf/1902.09192.pdf)
- authors
    - ZhijieDeng,YinpengDong,andJunZhu.2019.
- 之前暑假有看過
- [note](https://web.kamihq.com/web/viewer.html?source=extension_pdfhandler&document_identifier=1Pmk3ZkhGzX0O3Fcn1aNSWXYHeUFIR7SF)
- [note2](https://www.notion.so/Batch-virtual-adversarial-training-for-graph-convolutional-networks-dbf8320758554240b0ba6e5d9007269d)
:::


:::spoiler ☒ **Adversarial personalized ranking for recommendation** [➔]()
- authors
    - XiangnanHe,ZhankuiHe,XiaoyuDu,andTatSengChua.2018
:::
 
:::spoiler ☑ **GraphDefense: Towards Robust Graph Convolutional Networks** [➔](https://arxiv.org/pdf/1911.04429.pdf) 
- authors
    - Xiaoyun Wang, Xuanqing Liu, and Cho-Jui Hsieh. 2019. 
- [note](https://web.kamihq.com/web/viewer.html?source=extension_pdfhandler&extension_handler=extension_open_button&file=https%3A%2F%2Farxiv.org%2Fpdf%2F1911.04429.pdf)
- original GCN limitation: 
    - 1) inefficient in large dataset, -> GraphSAGE: neighborhood sampling, 
    - 2) perturbations 
- ![](https://i.imgur.com/jrnpm21.png)
- training T次，每次隨機選一部份作為adv一部份維持clean，透過以下loss function去訓練更新分類器f
- ![](https://i.imgur.com/kn3GJc4.png)
- 主要解決
    - 1) large dataset
    - 2) transferability: train test沒有連結、不是同個connected component的問題(進而使得AT效果有限)
:::

### Node Classification Attack
### Defense
