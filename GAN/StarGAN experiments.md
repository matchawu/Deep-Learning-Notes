---
tags: stargan, experiment
---

# StarGAN experiments

### feedback
semi 未知的用同時刻已知且標好label的去做標籤

### code
using: PyTorch [github](https://github.com/yunjey/stargan)

## network architecture

### Generator 
`The number of parameters: 8430528`
#### Down-sampling
![](https://i.imgur.com/gr704ip.png)
#### Bottleneck
![](https://i.imgur.com/edrTBRQ.png)
#### Up-sampling
![](https://i.imgur.com/i6nvYNQ.png)


![](https://i.imgur.com/xWMTX0x.png)
![](https://i.imgur.com/T50dJhe.png)


### Discriminator
`The number of parameters: 44762048`

![](https://i.imgur.com/gjgdKd3.png)

![](https://i.imgur.com/cEYNiHT.png)


## samples
200,000張圖片

input/black/blonde/brown/gender/age
![](https://i.imgur.com/ZiBxz27.jpg)

## results
![](https://i.imgur.com/MPAVBf2.png)
![](https://i.imgur.com/qk6RnNy.png)
![](https://i.imgur.com/CU8Agn6.png)
![](https://i.imgur.com/7LxUYT6.png)

![](https://i.imgur.com/Leg2ONM.png)
![](https://i.imgur.com/UMiBfO8.png)
![](https://i.imgur.com/JW8WBt5.png)
![](https://i.imgur.com/eqRvLc4.png)
![](https://i.imgur.com/ANt1Fh8.png)
![](https://i.imgur.com/RjfXK96.png)
![](https://i.imgur.com/5eR1fzg.png)
![](https://i.imgur.com/6BII8j2.png)
![](https://i.imgur.com/lOPAFUo.png)
![](https://i.imgur.com/nJIYumv.png)
![](https://i.imgur.com/Sc3oKHO.png)
![](https://i.imgur.com/tubbvgK.png)
![](https://i.imgur.com/s5aYulS.png)

## cycleGAN pytorch
epoch 100/200
![](https://i.imgur.com/pKznyQp.png)
![](https://i.imgur.com/zJ8oeRO.png)
![](https://i.imgur.com/e2jwC84.png)
![](https://i.imgur.com/l5TvtIG.png)
![](https://i.imgur.com/0DWSnEc.png)

![](https://i.imgur.com/muY5ozh.png)
![](https://i.imgur.com/aeUNSZL.png)
![](https://i.imgur.com/eyQFaA3.png)
![](https://i.imgur.com/4H4wnvq.png)
![](https://i.imgur.com/nDshwul.png)



- [ ] try using own img to test StarGAN without labels
```
python main.py --mode test --dataset CelebA --image_size 128 --c_dim 5 
```
只是在main.py改動CelebA資料集的位置，置換成/img folder，如看看testing資料沒有標籤的情況下能不能拿去做testing(我猜是不行)
- [ ] if cannot, add img to some existing datasets and add labels in exiting .txt file
list_attr_celeba-bew.txt 最後面n張圖片改成自己所切好的128 * 128的圖片(需要跟celeba原本的大小一樣!!!)檔名要改好(照數字順序)(另外新增資料夾，不要把原本的更動//太多)
加註標籤，但不再拿去training，直接讓他跑testing
- [x] pretrained model + test 
```
python main.py --mode test --dataset CelebA --image_size 256 --c_dim 5
```
