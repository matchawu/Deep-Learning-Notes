# PyTorch geometric

[documentation](https://pytorch-geometric.readthedocs.io/en/latest/index.html)

### Installation

```
pip install torch-sparse
pip install torch-cluster
pip install torch-spline-conv
pip install torch-geometric
```

也可以等run出來的error在看要裝其中哪幾個就好

### Customized Dataset

```python
graph = dataset[0]
new_graph = Data(edge_index=new_edges, 
                 test_mask=graph.test_mask, 
                 train_mask=graph.train_mask, 
                 val_mask=graph.val_mask, 
                 x=graph.x, 
                 y=graph.y)
```

---

### GCN training - node classification on Cora dataset

