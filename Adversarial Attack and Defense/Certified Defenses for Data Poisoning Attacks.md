---
tags: paper
---


# Certified Defenses for Data Poisoning Attacks 


## Abstract

對於廣泛的攻擊種類，建立一個loss的上界


## Introduction

攻擊者僅需新增一個使用者帳戶就可以做到data poisoning attack
目前大多專注於分類問題，有以下研究：
Biggio et al. (2012)
Xiao et al., 2012; 2015b; Newell et al., 2014; Mei and Zhu, 2015b; Burkard and Lagesse, 2017; Koh and Liang, 2017

有時候能夠顯著地降低分類器的準確度

也有特別針對某種攻擊法的防禦：Laishram and Phoha, 2016

很少有經過壓力測試(few have been stress-tested against a determined attacker)

也不能夠僅依賴實驗上的成功就能確保在面對新的攻擊方法時他能夠成功
而且可能的攻擊方法可能是幾乎無限的(near-limitless)

提出一個framework
1. 移除可行集合外的異常值
(remove outliers residing outside a feasible set)
2. 最小化margin-based loss
(minimize a margin-based loss on the remaining data)

產生估計的上界對於任何poisoning attack
並基於兩個假設：
1. train test的distribution是接近的
2. outlier removal不會嚴重更改乾淨資料的分布

為上限建立對偶節並使用結果升成與上限幾乎匹配的候選攻擊
上限和攻擊都是透過有效的在線學習演算法生成的

考量兩個instantiations:
1. outlier detector是獨立訓練的，並且不能被受汙染的資料影響到
2. data poisoning也可以攻擊outlier detector

上述兩種情況都已binary SVMs分析，但我們的framework也是用在multi-class情況上。

![](https://i.imgur.com/ceYX69e.png)


## Problem Setting
input ![](https://i.imgur.com/bDnKIZn.png)
output ![](https://i.imgur.com/2ct14Tv.png)
![](https://i.imgur.com/2oIXYj0.png)
(although most of our analysis holds for arbitrary Y)

![](https://i.imgur.com/1mqd8DJ.png) 是非負的convex loss function
e.g. 線性分類with hinge loss:
![](https://i.imgur.com/hUeBXK3.png)



