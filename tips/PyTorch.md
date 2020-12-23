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







### Others

[DL寫過的自定義dataset](https://github.com/matchawu/DL_HW3/blob/master/GAN_source_code/main.py)

[Pytorch資料讀取(Dataset, DataLoader, DataLoaderIter)](https://www.itread01.com/content/1545234667.html)

### 轉來轉去 tensor轉numpy

[https://blog.csdn.net/pengge0433/article/details/79459679](https://blog.csdn.net/pengge0433/article/details/79459679)

## Adversarial using PyTorch

[https://adversarial-ml-tutorial.org/](https://adversarial-ml-tutorial.org/)