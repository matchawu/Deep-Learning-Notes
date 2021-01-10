# RL Graph Adversarial Training

> 碩論的部分......

## 1/7 discussion

- 怎麼講故事：
  - novelty
    - 可以套用在各個embedding methods上的AT方法 (e.g. baselines加了我的AT會有提升)
  - contributions
    - 同時考量nodes & edges perturbations
  - 以adversarial training為必要再延伸 or adversarial training是我的proposed methods的一部份？
  - 看許多篇何向南的前面把不同的東西(e.g. RL & graph)兜起來的講法
  - 為何我的solution可以，別人的不行/別人的missing，設計的架構有cover到我自己講的問題
- 如何設計experiments

- RL
  - action
    - 應該是一次就選兩個點，e.g. softmax結果sample兩個點，反正prob大的被選到的機率比較大。
    - `選第二個點之前不需要動到embedding`
    - `一次trajectory結束以後，應該要回到原始的edges_index`
    - node features是否有可能一起在這個步驟做，或是交替做
  - 一次選兩個點的寫法
  - 何向南兜起來QQ
  - 改善RL結果(不知道在爛什麼)