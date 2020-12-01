# Deep Generative Models for Graph Generation

## Deep Generative Models
- Goal
- application for graph generation
    - social network
    - molecules

## 3 types of deep generative models
1. VAEs
2. GANs
3. Deep Auto-regressive Models

### 1.VAEs
- encoder
- decoder
- max: likelihood logp(x)
- max: variational lower-bound L(,,)
- L(,,):reconstruction ,regularization

### 2.GANs

### 3.Deep Auto-regrssive Models
e.g. RNN,and...
[paper:pixelRNN](http://proceedings.mlr.press/v48/oord16.pdf)
[paper:pixelCNN](https://papers.nips.cc/paper/6527-conditional-image-generation-with-pixelcnn-decoders.pdf)
[paper:WaveNet](https://pdfs.semanticscholar.org/df04/02517a7338ae28bc54acaac400de6b456a46.pdf?_ga=2.66084654.1055029080.1563951171-363824254.1563951171)

- Pixel RNN & Pixel CNN
    - image generated pixel by pixel
    - NN is used to model the conditional distribution
- WaveNet
    - p(x)=!!!

### Challenges for graph generation
1. ==graph structures & sizes are different==
2. ==no order (between nodes)==
3. ==discrete==

---

## GraphVAE
[paper](https://arxiv.org/pdf/1802.03480.pdf)
- input
    - graph G=(A,E,F)
        - A:adjacency matrix
        - E:edge attribute matrix
        - F:node attribute matrix
- encoder
    - graph NN + gated pooling => graph representation
- (probabilistic graph) decoder
    - output: G~ = (A~,E~,F~)
        - probabilistic fully connected graph 
        - (of a predifined maximun size: k nodes)
    - 分別model existence of nodes, edges, and their attributes
        - existence of nodes: bernoulli variables (0,1)
        - edges attributes: multinomial variables
        - nodes attributes: multinomial variables
    - 需要做graph matching
        - A~ node probabilities & edge probabilities
        - E~ probabilities for edge attributes
        - F~ probabilities for node attributes
    - taking edge-wise, node-wise argmax in A~,E~,F~

### Limitations
- must predifined ==max size==
- requires ==Graph Matching==

## JTVAE
[paper](https://arxiv.org/pdf/1802.04364.pdf)

## MolGAN
[paper](https://arxiv.org/pdf/1805.11973.pdf)
- implicit
- likelihood-free
- combined with RL
    - generator:
    - discriminator:
    - reward network:
- advantage:
    - no graph matching
- limitations:
    - max size should be predifined

## GCPN
[paper](https://cs.stanford.edu/people/jure/pubs/gcpn-neurips18.pdf)
- molecule generation as sequential decisions
    - add nodes and edges
    - a Markov decision process
- Goal: discover molecules that optimize desired properties while incorporating chemical rules
- GCPN is a general model for goal-directed graph generation with RL
    - optimize adversarial loss & domain-specific rewards(with policy gradients)
    - acts in an environment that incorporates domain-specific rules
### graph generation as MDP
> what is MDP?
> 馬可夫鏈決策過程
> https://www.cnblogs.com/jinxulin/p/3517377.html
> https://blog.techbridge.cc/2018/10/27/intro-to-mdp-and-app/
> 
![](https://i.imgur.com/u4SbmWD.png)

- State space
- Action space
    - a set of atoms to be added
        - connecting a new one to a node in Gt
        - connecting existing nodes in Gt
- State transition dynamics
    - 規範domain-specific rules
    - 只會carry out那些符合規範的actions
    - infeasible actions by the policy network會被拒絕，state保持不變
- Reward design
    - Final Reward
        - sum: domain-specific rewards的總和
        - 包含: final preoperty scores, penalization of unrealistic molecules, adversarial rewards
    - Intermediate Reward
        - step-wise的
        - validity rewards &
        - adversarial rewards
- GCPN: graph convolutional policy network
    - *compute node embeddings with neural message passing algorithms*
    - Action Prediction
        - selection (2 nodes)
        - prediction (edge type)
        - prediction (termination)
        - ![](https://i.imgur.com/8tj367t.png)


## Data sets

- ZINC
- RESULTS
    - reconstruction and validity
    - property optimization
    - property targeting
    - constrained property optimization
- generated molecules


## summary

## references



