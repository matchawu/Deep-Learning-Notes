---
tags: pytorch, torch
---

# PyTorch

## Adam 

[Optimizer: Adam](/bnKaitOMQaqgfemSnDkfSg)

## Gradient Penalty

[Gradient Penalty](/pvW9iHylT1mZqTIl0rgtaQ)

## x = x.view(x.size(0), -1)
[via](https://blog.csdn.net/whut_ldz/article/details/78882532)

這句話一般出現在model類的forward函數中，具體位置一般都是在調用分類器之前。分類器是一個簡單的nn.Linear()結構，輸入輸出都是維度為一的值，x = x.view(x.size(0), -1) 這句話的出現就是為了將前面多維度的tensor展平成一維。

![](https://i.imgur.com/fahDoOH.png)

上面是個簡單的網絡結構，包含一個卷積層和一個分類層。forward()函數中，input首先經過卷積層，此時的輸出x是包含batchsize維度為4的tensor，即(batchsize，channels，x，y)，x.size(0)指batchsize的值。x = x.view(x.size(0), -1)簡化x = x.view(batchsize, -1)。
view()函數的功能根reshape類似，用來轉換size大小。x = x.view(batchsize, -1)中batchsize指轉換後有幾行，而-1指在不告訴函數有多少列的情況下，根據原tensor數據和batchsize自動分配列數。

## torch
[PyTorch中文文檔](https://pytorch-cn.readthedocs.io/zh/latest/package_references/torch/)

### torch.pow() vs **
> ** is same as .pow()???

```
torch.pow(input, exponent, out=None)
```

* 参数：
    * input (Tensor) – 输入张量
    * exponent (float or Tensor) – 幂值
    * out (Tensor, optional) – 输出张量

![](https://i.imgur.com/LPfD9Zf.png)

### torch.sum()
```
torch.sum(input, dim, out=None) → Tensor
```

* 参数：
    * input (Tensor) – 输入张量
    * dim (int) – 缩减的维度
    * out (Tensor, optional) – 结果张量

![](https://i.imgur.com/a8ZXImN.png)

### torch.size()

```
torch.Size([0])
```
A tensor of this size is 1-dimensional but has no elements
```
torch.Size([1])
```
It is 1 dimensional and has one element


### torch.zeros()
```
torch.zeros(*sizes, out=None) → Tensor
```

* 参数:
    * sizes (int...) – 整数序列，定义了输出形状
    * out (Tensor, optional) – 结果张量

![](https://i.imgur.com/H9CGurc.png)


### torch.nn.functional.binary_cross_entropy_with_logits
`torch.nn.functional.binary_cross_entropy_with_logits(input, target, weight=None, size_average=True)` 
input - 任意形状的变量
target - 与输入形状相同的变量
weight（可变，可选） - 手动重量重量，如果提供重量以匹配输入张量形状
size_average（bool，可选） - 默认情况下，损失是对每个小型服务器的观察值进行平均。然而，如果字段sizeAverage设置为False，则相应的损失代替每个minibatch的求和。默认值：True


### torch.optimizer(自訂).step()
進行單次優化：所有的optimizer都實現了step()方法，這個方法會更新所有的參數。它能按兩種方式來使用：
```
optimizer.step()
```
這是大多數optimizer所支持的簡化版本。
一旦梯度被如backward()之類的函數計算好後，我們就可以調用這個函數。

![](https://i.imgur.com/SOOQic1.png)

註：
一開始會先自己定義好g或d的optimizer
```
self.g_optimizer = torch.optim.Adam(self.G.parameters(), self.g_lr, [self.beta1, self.beta2])
self.d_optimizer = torch.optim.Adam(self.D.parameters(), self.d_lr, [self.beta1, self.beta2])
```

### tensor(自訂).item()
可以將tensor轉為值輸出，用在列印log或output的時候


### torch.cat()

```
torch.cat(inputs, dimension=0) → Tensor
```
torch.cat()可以看做 torch.split() 和 torch.chunk()的反操作。
![](https://i.imgur.com/SgeNowE.png)
参数:

inputs (sequence of Tensors) – 可以是任意相同Tensor 类型的python 序列
dimension (int, optional) – 沿着此维连接张量序列。

### view()
類似reshape
view(* args) → Tensor
返回一个有相同数据但大小不同的tensor。
返回的tensor必须有与原tensor相同的数据和相同数目的元素，但可以有不同的大小。
一个tensor必须是连续的contiguous()才能被查看。
-1代表由別的維度決定它的維度大小
![](https://i.imgur.com/e4uc6HM.png)



### repeat()和expand()
[PyTorch 常用方法總結4：張量維度操作（拼接、維度擴展、壓縮、轉置、重複……）](https://zhuanlan.zhihu.com/p/31495102)
#### repeat()
![](https://i.imgur.com/sUBFefQ.png)

![](https://i.imgur.com/0QuGP2I.png)
#### expand()
![](https://i.imgur.com/XexomWs.png)
