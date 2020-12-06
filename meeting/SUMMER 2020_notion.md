# SUMMER 2020

報paper的範例：

[AliNet-2](https://docs.google.com/presentation/d/12ZtA3nh-6KQ7S_wmhTIauKnbJz3U_Lz8gyMOc8U4wTU/edit#slide=id.g7e95d0ef1f_0_94)

[Adversarial Attack Tutorial - HackMD](https://hackmd.io/_m_DMm18QDKMGv2GxbrnIw?view)

[Attack組 論文&各種筆記 - HackMD](https://hackmd.io/iiKwIJUsSuKxs08kF7LxqQ?view&fbclid=IwAR0x8thg4UgjHXUvQ4pgabDL_96RBpbdmU3-yYhOkld2zI5VcTddEMsSmWk)

## 三種想法

---

1. 考量相同degree的prediction應該相同 ⇒ 
2. 套用在community detection上，model結果是屬於每群的機率
3. 用在RS上面，input可以是user&user+r或item&item+r，限制出來的rs結果要相似

## 大方向

---

1. 看VAT有沒有進化版，套用在graph上面
2. 將GraphVAT應用在RS上面，但可能model要變形比較多：如何放入KG(relation multi-hot)？將分類問題轉變成link prediction問題？

## 問題

---

1. 為甚麼不直接用AT就好？VAT的好處？
2. 可能可以改的地方：在算和neighbors的predictions相近與否的時候，可以讓有同樣label的neighbor所佔的權重較大
3. GCN aggregate的方式？在做node classification上的方式？
4. GCN GraphSAGE GNN 之 input output 數量 需要甚麼東西(e.g.A,D,X)
5. GraphVAT在訓練的時候是把每個node都下去train還是有sample？
6. 論文中好像有提到negative sample，是用在哪裡？
7. 泰勒為甚麼可以解決一階=0的問題？實際上code是怎麼運作的？d？
8. smoothness是在指甚麼？為甚麼這邊的node classification要強調smoothness但是一般的nc只計算CEloss？