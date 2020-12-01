---
tags: torch, gp, gradient penalty, l2, autograd
---


# Gradient Penalty
## TORCH.AUTOGRAD


[via](https://pytorch.org/docs/stable/_modules/torch/autograd.html)

```
def grad(outputs, inputs, grad_outputs=None,
            retain_graph=None, create_graph=False,
            only_inputs=True, allow_unused=False)
```
> 有關於L2的作法!!
![](https://i.imgur.com/GlkcowV.png)

#### Arguments
###### outputs (sequence of Tensor): 
    outputs of the differentiated function.
###### inputs (sequence of Tensor): 
    Inputs w.r.t. which the gradient will be
    returned (and not accumulated into ``.grad``).
###### grad_outputs (sequence of Tensor): 
    The "vector" in the Jacobian-vector product.
    Usually gradients w.r.t. each output. None values can be specified for scalar
    Tensors or ones that don't require grad. If a None value would be acceptable
    for all grad_tensors, then this argument is optional. Default: None.
###### retain_graph (bool, optional): 
    If ``False``, the graph used to compute the grad
    will be freed. Note that in nearly all cases setting this option to ``True``
    is not needed and often can be worked around in a much more efficient
    way. Defaults to the value of ``create_graph``.
###### create_graph (bool, optional): 
    If ``True``, graph of the derivative will
    be constructed, allowing to compute higher order derivative products.
    Default: ``False``.
###### allow_unused (bool, optional): 
    If ``False``, specifying inputs that were not
    used when computing outputs (and therefore their grad is always zero)
    is an error. Defaults to ``False``.
    
    
## TORCH.GRAD

```
def grad(outputs, inputs, grad_outputs=None, 
         retain_graph=None, create_graph=False,
         only_inputs=True, allow_unused=False)
```

#### Arguments
        outputs (sequence of Tensor): outputs of the differentiated function.
        inputs (sequence of Tensor): Inputs w.r.t. which the gradient will be
            returned (and not accumulated into ``.grad``).
        grad_outputs (sequence of Tensor): The "vector" in the Jacobian-vector product.
            Usually gradients w.r.t. each output. None values can be specified for scalar
            Tensors or ones that don't require grad. If a None value would be acceptable
            for all grad_tensors, then this argument is optional. Default: None.
        retain_graph (bool, optional): If ``False``, the graph used to compute the grad
            will be freed. Note that in nearly all cases setting this option to ``True``
            is not needed and often can be worked around in a much more efficient
            way. Defaults to the value of ``create_graph``.
        create_graph (bool, optional): If ``True``, graph of the derivative will
            be constructed, allowing to compute higher order derivative products.
            Default: ``False``.
        allow_unused (bool, optional): If ``False``, specifying inputs that were not
            used when computing outputs (and therefore their grad is always zero)
            is an error. Defaults to ``False``.
