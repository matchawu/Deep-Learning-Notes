# [GraphSAGE](https://web.kamihq.com/web/viewer.html?state=%7B%22ids%22%3A%5B%221vuuTYujX4EkMv9Y2oBkox5IWaidTwF9P%22%5D%2C%22action%22%3A%22open%22%2C%22userId%22%3A%22110423678406540730896%22%7D&filename=graphsage-nips17.pdf)
> Inductive Representation Learning on Large Graphs

[TOC]

## ABSTRACT

> *Instead of training individual embeddings for each node, we learn a function that generates embeddings by sampling and aggregating features from a node’s local neighborhood.*

## INTRODUCTION

- 過去的作法
> *previous works have focused on embedding nodes from a single fixed graph*
> 

> *directly optimize the embeddings for each node using matrix-factorization-based objectives, and do not naturally generalize to unseen data, since they make predictions on nodes in a single, fixed graph*
> 

> *equiring additional rounds of gradient descent before new predictions can be made*
> 

- ++GraphSAGE++
    - generalization的能力：對於各種features有same form
        - leverage node features (e.g., text attributes, node profile information, node degrees) in order to learn an embedding function that generalizes to unseen nodes. 
        - 可用在沒有node feature的graph上：simultaneously learn the topological structure of each node’s neighborhood as well as the distribution of node features in the neighborhood
    - train **aggregator functions**: learn to aggregator feature information from a node's local neighborhood (from a different number of hops, or search depth)
        - can be unsupervised or fully supervised


## RELATED WORK
### Factorization-based embedding approaches

### Supervised learning over graphs

### Graph convolutional networks




## PROPOSED METHOD
- 學習目標：如何aggregate feature information from a node's local neighborhood
- 1/ 先介紹graphSAGE如何產生node enbeddings(假設參數已學好)
- 2/ 再來說明如何更新graphSAGE的參數*standard stochastic gradient descent and backpropagation techniques*

### ▲ Embedding generation (forward propagation)
參數固定，訓練embedding

**K個aggregator functions**：從節點鄰居整合資訊，得到了a set of **weight matrices: W^k**：propagate information between different layers of the model or “search depths”

![](https://i.imgur.com/znIC6pU.png)

> at each iteration, or search depth, nodes aggregate information from their local neighbors, and as this process iterates, nodes incrementally漸進 gain more and more information from further reaches of the graph. 

經過遞迴，node會接收更廣更遠的graph資訊。


1/先去


### ▲ parameters of GraphSAGE

### ▲ aggregator architectures
- no natural ordering (unordered set of vectors)
- aggregator function would be symmetric (invariant to permutations of its inputs)
- arbitrarily ordered node neighborhood feature sets
![](https://i.imgur.com/dr06nqe.png)
* graph embedding到底在learn什麼？ ==0217 meeting==
    * graph embedding:++找到vector代表node++
    * ++有connection的人越相似越好++
    * node的標註使他可以做分類(supervised)
    * 一開始有features或亂數產生embedding得到特徵
    * h^0^ 不會改，改的是 A(neighbor)、B(me)兩個network：**learn的是這兩個網路**
    * 拿別的h^1^ 來算自己的h^2^ --> predefine要算幾層、要多少neighbors
    * *positive negative去算loss*
#### ++mean++
elementwise mean of the vectors in all v's neighbors
![](https://i.imgur.com/xNmV6Ym.png)

##### convolutional *from GCN*
> *The mean aggregator is nearly equivalent to the convolutional propagation rule used in the transductive GCN framework [17].*
> 

#### ++LSTM++
* 比mean好在：larger expressive capability
* but not inherently symmetric

> *an unordered set by simply applying the LSTMs to a **random permutation** of the node’s neighbors*

#### ++pooling++
![](https://i.imgur.com/OGUykUo.png)



## EXPERIMENTS

### ▲ citation and reddit data

### ▲ protein-protein interactions

### ▲ runtime and parameter sensitivity

### ▲ summary comparison between the different aggregator architectures



## THEORETICAL ANALYSIS


## CONCLUSION


## references
* [Graph Neural Network：GraphSAGE 算法原理，實現和應用](https://flashgene.com/archives/58728.html)
* [GraphSAGE: GCN落地必讀論文](https://zhuanlan.zhihu.com/p/62750137)
* [AAAI 2019](https://jian-tang.com/files/AAAI19/aaai-grltutorial-part2-gnns.pdf)


## code
[original](https://github.com/williamleif/GraphSAGE)

### 特點
> *GraphSage can be viewed as a stochastic generalization of graph convolutions, and it is especially useful for massive, dynamic graphs that contain rich feature information.*
> 

- 可針對沒有node features的圖來做：
    - now includes optional "identity features" that can be used with or without other node attributes

- GraphSage is intended for use on large graphs (>100,000) nodes.

### folder
- example_data
    - protein-protein interaction data (PPI)
    - 3 training graphs + one validation graph and one test graph

### requirements
```
$ pip install -r requirements.txt
```
other: [Docker](https://github.com/williamleif/GraphSAGE)

### Running the code
- files: contain example usages of the code
    - example_unsupervised.sh
        - sets a very small max iteration number, which can be increased to improve performance
    - example_supervised.sh
- if: not require generalizing to unseen data
    - set "--identity_dim" flag to a value in the range [64,256]
        - This flag will make the model embed unique node ids as attributes, which will increase the runtime and number of parameters but also potentially increase the performance. 
        - Note that you should set this flag and not try to pass dense one-hot vectors as features (due to sparsity).

> Note: For the PPI data, and any other multi-ouput dataset that allows individual nodes to belong to multiple classes, it is necessary to set the --sigmoid flag during supervised training. By default the model assumes that the dataset is in the "one-hot" categorical setting.
> 

