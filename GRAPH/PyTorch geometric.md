# PyTorch geometric

[documentation](https://pytorch-geometric.readthedocs.io/en/latest/index.html)

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

