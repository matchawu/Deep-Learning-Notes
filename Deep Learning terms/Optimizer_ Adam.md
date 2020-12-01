---

tags: adam, optimizer

---



# Optimizer: Adam

[via!!!](https://www.jiqizhixin.com/articles/2017-07-12)
[via](https://pytorch.org/docs/stable/optim.html)
[lr decay](https://www.pytorchtutorial.com/pytorch-learning-rate-decay/)
[手動調整lr](http://www.spytensor.com/index.php/archives/32/)

### pytorch

```
torch.optim.Adam(params, lr=0.001, betas=(0.9, 0.999), eps=1e-08, weight_decay=0, amsgrad=False)
```

### 什么是param_groups?
optimizer通过param_group来管理参数组.param_group中保存了参数组及其对应的学习率,动量等等.所以我们可以通过更改param_group[‘lr’]的值来更改对应参数组的学习率。
```
def update_lr(self, g_lr, d_lr):
        """Decay learning rates of the generator and discriminator."""
        for param_group in self.g_optimizer.param_groups:
            param_group['lr'] = g_lr
```

### beta1,2
Adam 算法同時獲得了 AdaGrad 和 RMSProp 算法的優點。Adam 不僅如 RMSProp 算法那樣基於一階矩均值計算適應性參數學習率，它同時還充分利用了梯度的二階矩均值（即有偏方差/uncentered variance）。具體來說，算法計算了梯度的指數移動均值（exponential moving average），超參數 beta1 和 beta2 控制了這些移動均值的衰減率。

移動均值的初始值和 beta1、beta2 值接近於 1（推薦值），因此矩估計的偏差接近於 0。該偏差通過首先計算帶偏差的估計而後計算偏差修正後的估計而得到提升。如果對具體的實現細節和推導過程感興趣，可以繼續閱讀該第二部分和原論文。

![](https://i.imgur.com/bbtlUdx.png)

