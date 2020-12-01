# Attack & Defense on Graphs with RL

[![hackmd-github-sync-badge](https://hackmd.io/_33QK2LYQZmEivFdvq2kwA/badge)](https://hackmd.io/_33QK2LYQZmEivFdvq2kwA)


### [Adversarial Attack on Graph Structured Data](https://arxiv.org/pdf/1806.02371.pdf)

選定兩個node(由Q1,Q2個別完成)

![](https://i.imgur.com/9Q65e8K.png)

---

### [Attacking Graph Convolutional Networks via Rewiring](https://arxiv.org/pdf/1906.03750.pdf)
```GCN``` ```Attack```
- State Space
    - The state space of the environment consists of all the intermediate graphs generated after all the possible rewiring operations.

- Action Space 
    - The action space consists of all the valid rewiring operations as defined in Definition 1.
    - Note that the valid action space is dynamic when the state changes, as the k-th hop neighbors are different in different states.

- State Transition Dynamics 
    - Given an action (rewiring operation) at = {vf ir, vsec, vthi} at state st. The next state st+1 is achieved by deleting the edge between vf ir and vsec in the current state st and adding an edge to connect vf ir with vthi.

- Reward Design 
    - The main goal of the attacker is to make the classifier f(·) predict a different label than originally predicted. We also encourage the attacker to take as few actions as possible so that the modification to the graph structure is minimal. Thus, we assign a positive reward when the attack is successful and assign a negative reward for each action step taken.

![](https://i.imgur.com/1LDRiGT.png)

---

### [Reinforcement Learning-based Black-Box Evasion Attacks to Link Prediction in Dynamic Graphs](https://arxiv.org/pdf/2009.00163.pdf)
Arxiv 
```dynamic graphs``` ```GCN``` ```link prediction```


---

### [Semantic-preserving Reinforcement Learning Attack Against Graph Neural Networks for Malware Detection](https://arxiv.org/pdf/2009.05602.pdf)
Arxiv
```malware detection``` 


---

### [Non-target-specific Node Injection Attacks on Graph Neural Networks: A Hierarchical Reinforcement Learning Approach](https://faculty.ist.psu.edu/vhonavar/Papers/www20.pdf)
WWW 


---

### [Enhancing Graph Neural Network-based Fraud Detectors
against Camouflaged Fraudsters]()