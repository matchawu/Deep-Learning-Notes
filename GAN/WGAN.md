# WGAN
[ref](https://medium.com/@falconives/day-59-wasserstein-gan-wgan-b31adb226aea)

[hyl video](https://www.youtube.com/watch?v=3JP-xuBJsyc)

https://cloud.tencent.com/developer/article/1164051

![](https://i.imgur.com/Ubc0n0R.png)
![](https://i.imgur.com/S0sqGvh.png)

### WGAN的主要貢獻如下：
1. 彻底解决GAN训练不稳定的问题，不再需要小心平衡生成器和判别器的训练程度
2. 基本解决了collapse mode的问题，确保了生成样本的多样性
3. 训练过程中终于有一个像交叉熵、准确率这样的数值来指示训练的进程，这个数值越小代表GAN训练得越好，代表生成器产生的图像质量越高（如题图所示）
4. 以上一切好处不需要精心设计的网络架构，最简单的多层全连接网络就可以做到

### 相比起原版的GAN，WGAN其實只做了四項更動：
1. 判别器最后一层去掉sigmoid
2. 生成器和判别器的loss不取log
3. 每次更新判别器的参数之后把它们的绝对值截断到不超过一个固定常数c
4. 不要用基于动量的优化算法（包括momentum和Adam），推荐RMSProp，SGD也行


#### 待看
https://read01.com/zh-tw/5ABJ4P.html#.XVLprugzZPZ

#### SAVE
https://zhuanlan.zhihu.com/p/29394257
https://blog.csdn.net/qq_25737169/article/details/78857788
https://zhuanlan.zhihu.com/p/25071913
https://blog.csdn.net/Invokar/article/details/88917214