# PyTorch

### reshape

```python
torch.reshape(c,(5,2))
```

### where

和np.where不同之處在於：輸入的三個參數皆須為Tensor形式 [link](https://blog.csdn.net/xijuezhu8128/article/details/86590562)

```python
# torch.where
mask_true = torch.where(torch.isnan(y_true), torch.full_like(y_true, 0), torch.full_like(y_true, 1))
# np.where
mask_true = np.where(np.isnan(y_true), 0, 1)
```

### cat

add item to Tensor [link](https://stackoverflow.com/questions/61101919/how-can-i-add-an-element-to-a-pytorch-tensor-along-a-certain-dimension)

```python
new_edges = torch.cat((edges, edge_add), axis=1) # add edge
```

### gather



### 取得gradients

```python
torch.autograd.grad(<填寫loss>, <對誰微分>, retain_graph=True)[0]
```

另外，餵進去model的input需要設定為`requires_grad = True`才可以取得gradients

```python
X = Variable(X , requires_grad = True)
```

### torch.dtype

[link](https://pytorch.org/docs/stable/tensor_attributes.html)

### network parameters

PyTorch取得整個網路Net()的參數的方法如下：

```python
for p in net.parameters():
    print(p)
    # or do something you want
```

為此對整個Net()的參數做了L2 norm：

```python
l2_norm = 0.0
for p in model.parameters():
    l2_norm += torch.norm(p, 2) # torch.norm(sth, p) p代表L幾
```



### Others

[DL寫過的自定義dataset](https://github.com/matchawu/DL_HW3/blob/master/GAN_source_code/main.py)

[Pytorch資料讀取(Dataset, DataLoader, DataLoaderIter)](https://www.itread01.com/content/1545234667.html)

### 轉來轉去 tensor轉numpy

[https://blog.csdn.net/pengge0433/article/details/79459679](https://blog.csdn.net/pengge0433/article/details/79459679)

## Adversarial using PyTorch

[https://adversarial-ml-tutorial.org/](https://adversarial-ml-tutorial.org/)

## Tensorflow to PyTorch

[tensorflow改寫為pytorch的方法總結](https://blog.csdn.net/lrt366/article/details/96211913)