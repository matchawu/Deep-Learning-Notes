# 108-2 meeting note

## March
### 0312 lab

#### ► 論文討論

- Mei Chen Wu
    [Detection of Accounting Anomalies in the Latent Space using Adversarial Autoencoder Neural Networks](https://arxiv.org/abs/1908.00734?fbclid=IwAR1-ZM9xfXOrKQNm2g1X3FRuUhe0FONlPEFlJZ8BYx1vMxvS6C_mYVW_HMk)

- 吳姿妏
    [Data Poisoning Attack against Knowledge Graph Embedding](https://www.ijcai.org/Proceedings/2019/0674.pdf?fbclid=IwAR12aMre0dl-VJFoWT0WXMyZAkXsfJWIf7-39G38tw4S-ztb9eFWBJyJFKM)

- 郭家瑄


---

### 0305 lab

#### ► 論文討論

- 楊曜駿
    [Reasoning on Knowledge Graphs with Debate Dynamics](https://arxiv.org/abs/2001.00461)

- Archi Chou
    [HetGNN: Heterogeneous Graph Neural Network](https://dl.acm.org/doi/abs/10.1145/3292500.3330961?fbclid=IwAR36iEZJZjDxsSX89WZpDRHRS6LWdWt19QNj3FQeeR5HEl2S9C8SPS8rafo)

- ~~Mei Chen Wu
    Detection of Accounting Anomalies in the Latent Space using Adversarial Autoencoder Neural Networks~~



## February

### 0227 lab

#### ► 論文討論

- 楊雯婷
    Graph Few-shot Learning via Knowledge Transfer

- 吳宛儒 
    Knowledge Graph Alignment Network with Gated Multi-hop Neighborhood Aggregation

- 洪芝盈 
    Can deep learning predict risky retail investors? A case study in financial risk behavior forecasting



---

### 0224 group



---

### 0220 lab

#### ► 論文討論
note: [雲端筆記pdf](https://drive.google.com/file/d/1soKhwWVPT-mRxYPU1yXdf4aBVzEknqaH/view?usp=sharing)

- Fei-fan He
[FA3: Exploration-Exploitation in Reinforcement Learning](https://rlgammazero.github.io/?fbclid=IwAR0FP3FSxZF1-WjGTagE5huHRg_t_IuzgsKEL_ANkSZSgujk1IE74tDYDCk)

- 林昕靜
[Diachronic Embedding for Temporal Knowledge Graph Completion](https://grlearning.github.io/papers/41.pdf)

- 王亭云
[A Spatio-Temporal Graph Attention Network for Traffic Forecasting](https://arxiv.org/pdf/1911.13181.pdf)


---


### 0217 group

* me：
    * 簡短進度規劃 graphSAGE
* T：
    * AAAI 九月投稿
    * 多討論，比之前好更好就好
    * 報paper之前找學長姐聽過
    * 早睡早起多運動，健身房好臭
    * 看口試就是要看口委問什麼：有圖有表示，對應到亮點
    * 了解SOTA目前做的如何，但如果問題設定很不一樣，就可以擋掉這樣的問題
* others:
    * [graphSAGE](https://jian-tang.com/files/AAAI19/aaai-grltutorial-part2-gnns.pdf) ==巧莛==
        * graph embedding到底在learn什麼？
        * graph embedding:++找到vector代表node++
        * ++有connection的人越相似越好++
        * node的標註使他可以做分類(supervised)
        * 一開始有features或亂數產生embedding得到特徵
        * h^0^ 不會改，改的是 A(neighbor)、B(me)兩個network：**learn的是這兩個網路**
        * 拿別的h^1^ 來算自己的h^2^ --> predefine要算幾層、要多少neighbors
        * *positive negative去算loss*
    * KG (h,r,t)三者皆要embedding ==姿妏==
        * r(h)-->t  -->:接近於
        * h,t: entity r: relationship
        * transX 是在算這個embedding
        * 原本非KG的做法的問題：通常citation都是單向的，雙向幾乎沒有，所以如果一般的graph將有cite的兩個paper放在空間中相近的地方，很不合理
        * A-cite->B embedding後經過一個NN 出來0or1 確定是A cite B
        * 也就是r(A)->B 但r(B)->A不成立






