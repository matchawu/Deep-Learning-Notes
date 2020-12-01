# Normalization
`note`
`batchnorm` `instancenorm` `layernorm`

[0813-via](https://www.jiqizhixin.com/articles/2018-08-29-7)
[0816-via-很多東西統整!](https://mlexplained.com/2018/11/30/an-overview-of-normalization-methods-in-deep-learning/)
[0816-to read](https://arthurdouillard.com/post/normalization/)
[onenote](https://nctuitsc-my.sharepoint.com/personal/wwj_iim08g_o365_nctu_edu_tw/_layouts/15/WopiFrame.aspx?sourcedoc={4dc6c9b5-99be-4859-b1a2-5064c81d3714}&action=edit&wd=target%28Quick%20Notes.one%7Cced483ae-0112-42f3-91d4-7af9d136bc48%2F%E6%B7%B1%E5%BA%A6%E5%AD%B8%E7%BF%92%E4%B8%AD%E7%9A%84Normalization%E6%A8%A1%E5%9E%8B%5C%7C%20%E6%A9%9F%E5%99%A8%E4%B9%8B%E5%BF%83%7C6e7ead8c-88d9-4aef-9a79-4a0f5a2fd440%2F%29)

![](https://i.imgur.com/ubG63fZ.png)

## Normalization

## Batch Normalization
[李宏毅](https://www.youtube.com/watch?v=BZh1ltr5Rkg)

## Batch Norm 的四大罪状

### 局限 1：如果 Batch Size 太小，则 BN 效果明显下降。 

- 如果BATCH-SIZE太小，任務效果會不佳

太小的定義？
- (下圖)BatchSize 小于 8 的时候开始对分类效果有明显负面影响
- 小的batch size意味著樣本數少，無法得到有效統計量，也就是噪音太大。
> BN 是严重依赖 Mini-Batch 中的训练实例的，如果 Batch Size 比较小则任务效果有明显的下降。那么多小算是太小呢？图 10 给出了在 ImageNet 数据集下做分类任务时，使用 ResNet 的时候模型性能随着 BatchSize 变化时的性能变化情况，可以看出当 BatchSize 小于 8 的时候开始对分类效果有明显负面影响。

> 这个很好理解，这就类似于我们在做年均收入调查的时候，正好把你和马云放到一个 Batch 里算平均收入，那么当你为下个月房租发愁之际，突然听到你所在组平均年薪 1 亿美金时，你是什么心情，那小 Mini-Batch 里其它训练实例就是啥心情。 

![](https://i.imgur.com/0C8JdS5.png)

> 图 10. BN 的 Batch Size 大小对 ImageNet 分类任务效果的影响（From GN 论文） 

> - BN 的 Batch Size 大小设置是由调参师自己定的，调参师只要把 Batch Size 大小设置大些就可以避免上述问题。
> 
> - 但是有些任务比较特殊，要求 batch size 必须不能太大，在这种情形下，普通的 BN 就无能为力了。
    - 比如 BN 无法应用在 Online Learning 中，因为在线模型是单实例更新模型参数的，难以组织起 Mini-Batch 结构。 

### ==局限 2：对于有些像素级图片生成任务来说，BN 效果不佳== 

- 圖片分類任務：找出關鍵特徵就能正確分類
    - 粗度任務
    - 使用BN有好效果
- 輸出輸入都是圖片的任務：例如風格轉換應用
    - 像素級別
    - 使用BN有負面效果
    - 因為在同一個MINI-BATCH中有多張無關的圖片之間一同計算統計量，會減弱單張圖片本身可能帶有的特有的細節訊息

### 局限 3：RNN 等动态网络使用 BN 效果不佳且使用起来不方便 

> 对于 RNN 来说，尽管其结构看上去是个静态网络，但在实际运行展开时是个动态网络结构，因为输入的 Sequence 序列是不定长的，这源自同一个 Mini-Batch 中的训练实例有长有短。
> 
> 对于类似 RNN 这种动态网络结构，BN 使用起来不方便，因为要应用 BN，那么 RNN 的每个时间步需要维护各自的统计量，而 Mini-Batch 中的训练实例长短不一，这意味着 RNN 不同时间步的隐层会看到不同数量的输入数据，而这会给 BN 的正确使用带来问题。
> 
> 假设 Mini-Batch 中只有个别特别长的例子，那么对较深时间步深度的 RNN 网络隐层来说，其统计量不方便统计而且其统计有效性也非常值得怀疑。另外，如果在推理阶段遇到长度特别长的例子，也许根本在训练阶段都无法获得深层网络的统计量。
> 
> 综上，在 RNN 这种动态网络中使用 BN 很不方便，而且很多改进版本的 BN 应用在 RNN 效果也一般。 

### 局限 4：训练时和推理时统计量不一致 

> 对于 BN 来说，采用 Mini-Batch 内实例来计算统计量，这在训练时没有问题，但是在模型训练好之后，在线推理的时候会有麻烦。因为在线推理或预测的时候，是单实例的，不存在 Mini-Batch，所以就无法获得 BN 计算所需的均值和方差，一般解决方法是采用训练时刻记录的各个 Mini-Batch 的统计量的数学期望，以此来推算全局的均值和方差，在线推理时采用这样推导出的统计量。虽说实际使用并没大问题，但是确实存在训练和推理时刻统计量计算方法不一致的问题。 
> 
> 上面所列 BN 的四大罪状，表面看是四个问题，其实深入思考，都指向了幕后同一个黑手，这个隐藏在暗处的黑手是谁呢？**就是 BN 要求计算统计量的时候必须在同一个 Mini-Batch 内的实例之间进行统计，因此形成了 Batch 内实例之间的相互依赖和影响的关系**。
> 
> 如何从根本上解决这些问题？一个自然的想法是： **把对 Batch 的依赖去掉，转换统计集合范围。** 在统计均值方差的时候，不依赖 Batch 内数据，**只用当前处理的单个训练数据**来获得均值方差的统计量，这样因为不再依赖 Batch 内其它训练数据，那么就不存在因为 Batch 约束导致的问题。在 BN 后的几乎所有改进模型都是在这个指导思想下进行的。 
> 
> 但是这个指导思路尽管会解决 BN 带来的问题，又会引发新的问题，新的问题是：我们目前已经没有 Batch 内实例能够用来求统计量了，此时统计范围必须局限在一个训练实例内，一个训练实例看上去孤零零的无依无靠没有组织，怎么看也无法求统计量，***所以核心问题是对于单个训练实例，统计范围怎么算？***

![](https://i.imgur.com/G2eZ3ob.png)

## Layer Normalization


## Instance Normalization 
- Instance Normalization
- Conditional Instance Normalization
- [Adaptive Instance Normalization](https://arxiv.org/pdf/1703.06868.pdf)
### 應用領域

```
- style transfer
- GANs
```

### 使用原因
`0816`
[via](https://mlexplained.com/2018/11/30/an-overview-of-normalization-methods-in-deep-learning/)
> Originally devised for style transfer, the problem instance normalization tries to address is that the network should be agnostic to the contrast of the original image. Therefore, it is specific to images and not trivially extendable to RNNs.

整個網路應該對原本圖片之間的比較是未知的，也就是說input進來的這些圖片之間的差異，不該被網路所考量。
(和RNN所要考慮的不一樣，RNN需要考慮時序性的關係)

在style transfer上面，IN效果比使用BN還要好，也有將IN使用在GANs上的例子


`0813`
> 从上述内容可以看出，Layer Normalization 在抛开对 Mini-Batch 的依赖目标下，为了能够统计均值方差，很自然地把同层内所有神经元的响应值作为统计范围，那么我们能否进一步将统计范围缩小？
> 
![](https://i.imgur.com/OlgMByG.png)

#### CNN
> - 对于 CNN 明显是可以的，因为同一个卷积层内每个卷积核会产生一个输出通道，而每个输出通道是一个二维平面，也包含多个激活神经元，自然可以进一步把统计范围缩小到单个卷积核对应的输出通道内部。
> - 上图 展示了 CNN 中的 Instance Normalization，对于图中某个卷积层来说，每个输出通道内的神经元会作为集合 S 来统计均值方差

#### RNN MLP 無法做 IN
> - 对于 RNN 或者 MLP，如果在同一个隐层类似 CNN 这样缩小范围，那么就只剩下单独一个神经元，输出也是单值而非 CNN 的二维平面，这意味着没有形成集合 S，所以 RNN 和 MLP 是无法进行 Instance Normalization 操作
> 
> Instance Normalization 对于一些图片生成类的任务比如图片风格转换来说效果是明显优于 BN 的，但在很多其它图像类任务比如分类等场景效果不如 BN。

## Group Normalization
