---
title: CycleGAN
tags: Templates, Talk
description: View the slide with "Slide Mode".
---

<style>
code.blue {
  color: #35DFD6 !important;
}
code.orange {
  color: #FCB133 !important;
}
code.green {
  color: #B3F235 !important;
}
code.red {
  color: #F824A1 !important;
}
code.yellow{
  color: #F8E924 !important;
}
</style>


# CycleGAN
> Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks

<!-- Put the link to this slide here so people can follow -->
                    - slide: https://reurl.cc/Yyapa

---

## Introduction

---

![](https://i.imgur.com/eqztDDA.png)

---

- <code class="green">Image-to-image translation</code> is a class of vision and graphics problems where the goal is to learn *the mapping* between an input image and an output image *using a training set of aligned image pairs*.

- [pix2pix](https://blog.csdn.net/gdymind/article/details/82696481)
- [play](https://affinelayer.com/pixsrv/)


---

- GAN
![](https://i.imgur.com/z7KwcFB.png)
- pix2pix
![](https://i.imgur.com/7RJ447R.png)


---

- image-to-image translation
![](https://i.imgur.com/DnFvh9e.png) 

---

- However, obtaining paired training data can be *difficult and expensive*.

---

- <code class="red">*unpaired*</code> image-to-image translation
![](https://i.imgur.com/4PMQIk9.png) 

---

![](https://i.imgur.com/tdcFdWz.png)



---

- We assume there is some <code class="red">*underlying relationship*</code> between the domains – for example, that they are two different renderings of the same underlying world – and seek to learn that relationship.

---

- Although we lack supervision in the form of paired examples, we can exploit supervision <code class="yellow"> *at the level of sets*</code>: 
    - we are given one set of images in domain X and a different set in domain Y .

---

## Architecture

---

![](https://i.imgur.com/qfBUaQ2.png)

---

- two mapping:
    - <code class="blue">G : X → Y</code>
    - <code class="blue">F : Y → X</code>
- two adversarial discriminators:
    - <code class="yellow">Dx</code>
        - {x} : true x
        - {F(y)} : fake x
    - <code class="yellow">Dy</code>
        - {y} : true y
        - {G(x)} : fake y

---

## Loss Function

---

![](https://i.imgur.com/qfBUaQ2.png)


---

- <code class="orange">adversarial losses</code>
    - matching the distribution of generated images to the data distribution in the target domain

1. <code class="blue">G : X → Y</code> and its discriminator <code class="yellow">DY</code>
    ![](https://i.imgur.com/o0gh1CG.png)
2. <code class="blue">F : Y → X</code> and its discriminator <code class="yellow">DX</code>
    ![](https://i.imgur.com/LuXVD4T.png)

---

- <code class="blue">cycle consistency loss</code>
    - prevent the learned mappings G and F from contradicting each other

    - forward cycle consistency
      ![](https://i.imgur.com/R8pebZl.png)
    - backward cycle consistency
      ![](https://i.imgur.com/NIP5X4t.png)
![](https://i.imgur.com/dxDdZzF.png)

---

![](https://i.imgur.com/mXrLzHo.png)

---

- <code class="green">identity loss</code>
    - preserve the *color* of the input paintings
    - identity function: f(x)=x

```
parser.add_argument('--lambda_identity', type=float, default=0.5, help='use identity mapping. Setting lambda_identity other than 0 has an effect of scaling the weight of the identity mapping loss. For example, if the weight of the identity loss should be 10 times smaller than the weight of the reconstruction loss, please set lambda_identity = 0.1')
```

---

![](https://i.imgur.com/w1xgJTR.png)

---

![](https://i.imgur.com/eh1yW3A.png)

---

![](https://i.imgur.com/yyNrmJr.png)

---

## Full Objective Function

---

- The [original paper](http://openaccess.thecvf.com/content_ICCV_2017/papers/Zhu_Unpaired_Image-To-Image_Translation_ICCV_2017_paper.pdf) only mentioned adversarial and cycle consistency loss.

---

- Objective function
![](https://i.imgur.com/ixqrZaY.png)
- where <code class="yellow">λ</code> controls the *relative importance* of the two objectives

---

### Tricks

---

#### Network Structure
- Generator
    ![](https://i.imgur.com/gCGexFU.png)
    - *using ResNet*

---

#### Network Structure
- ResNet
    ![](https://i.imgur.com/QFCO7Vr.png)


---

#### Network Structure
- Discriminator
    ![](https://i.imgur.com/JnNe84x.png)
    - *using PatchGAN*

---

#### Network Structure
- PatchGAN
    ![](https://i.imgur.com/hbfdfas.png) 
    - *faster, fairer, better results*


---

#### Training Details
- Replace the negative log likelihood objective by <code class="red">a least square loss</code>
    ![](https://i.imgur.com/wWd3rZF.png)
    - *This loss performs more stably during training and generates higher quality results.*

---

#### Training Details
- Update the discriminators DX and DY <code class="red">using a history of generated images</code> rather than the ones produced by the latest generative networks. 
- We keep an <code class="orange">image buffer </code> that stores the 50 previously generated images.
    - *In order to reduce model oscillation*


---

## Implementations

---

![](https://i.imgur.com/VS1xe3S.png)

---

![](https://i.imgur.com/aFxlSsS.png)

---

![](https://i.imgur.com/be6VeZe.jpg)


---

![](https://i.imgur.com/mWtb1m7.png)

---

## Limitations

---

- We have also explored tasks that require <code class="blue">geometric changes</code>, with little success.

---

![](https://i.imgur.com/PsLwn5e.png)

---

## Other

---

### Some results...

---

#### horse2zebra
![](https://i.imgur.com/oceGR4D.png) ![](https://i.imgur.com/N3MmaQA.png)


---

#### ukiyoe2photo
![](https://i.imgur.com/695fVXj.png) ![](https://i.imgur.com/lxaOppw.png)

---

[details](https://hardikbansal.github.io/CycleGANBlog/)
[notes](https://hackmd.io/rHnLs0j1SDWIrR0e5r8sZQ?view)


---

## The End