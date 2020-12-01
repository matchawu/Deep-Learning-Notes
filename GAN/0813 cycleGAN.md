# 0813 cycleGAN
`experiments`

1.

|                | G             | D       |
| -------------- | ------------- | ------- |
| PARAMETERS     | 6,171,025     | 698,055 |
| DROPOUT        | NO            | 0,1,1,1 |
| NORMALIZATION  | INSTANCE NORM | NO NORM |

```
[Epoch 0/200] [Batch 0/4000] [D loss: 3.225699, acc:  15%] [G loss: 22.221811, adv: 2.360132, recon: 0.806711, id: 0.486132] time: 0:00:13.481804
```

2.
|                | G             | D       |
| -------------- | ------------- | ------- |
| PARAMETERS     | 6,171,025     | 698,055 |
| DROPOUT        | 1             | 0,1,1,1 |
| NORMALIZATION  | INSTANCE NORM | NO NORM |
```
[Epoch 0/200] [Batch 0/4000] [D loss: 1.304975, acc:  39%] [G loss: 26.520996, adv: 4.041301, recon: 0.835721, id: 0.893908] time: 0:00:15.905946
```

3.
|                | G             | D       |
| -------------- | ------------- | ------- |
| PARAMETERS     | 6,171,025     | 698,055 |
| DROPOUT        | 3             | 0,1,1,1 |
| NORMALIZATION  | INSTANCE NORM | NO NORM |
```
[Epoch 0/200] [Batch 0/4000] [D loss: 2.076398, acc:  26%] [G loss: 23.980339, adv: 2.986134, recon: 0.809952, id: 0.820672] time: 0:00:20.360793 
```

4.
|                | G             | D       |
| -------------- | ------------- | ------- |
| PARAMETERS     | 6,171,025     | 698,055 |
| DROPOUT        | 3             | 0,1,1,1 |
| NORMALIZATION  | INSTANCE NORM | NO NORM |
```
[Epoch 0/200] [Batch 0/400] [D loss: 2.189849, acc:  28%] [G loss: 25.381546, adv: 2.864056, recon: 0.905549, id: 0.766920] time: 0:00:28.729339
```


5.
|                | G             | D       |
| -------------- | ------------- | ------- |
| PARAMETERS     | 6,171,025     | 698,049 |
| DROPOUT        | 2             | 0       |
| NORMALIZATION  | INSTANCE NORM | NO NORM |
```
[Epoch 0/200] [Batch 0/400] [D loss: 0.490675, acc:  50%] [G loss: 19.871944, adv: 0.815638, recon: 0.814554, id: 0.743713] time: 0:00:18.993251 
```

6.
|                | G             | D       |
| -------------- | ------------- | ------- |
| PARAMETERS     | 6,171,025     | 698,049 |
| DROPOUT        | 0             | 0       |
| NORMALIZATION  | INSTANCE NORM | NO NORM |
```
[Epoch 0/200] [Batch 0/400] [D loss: 0.491104, acc:  50%] [G loss: 17.585930, adv: 0.840059, recon: 0.708906, id: 0.645417] time: 0:00:22.668045 
```

7.
|                | G             | D       |
| -------------- | ------------- | ------- |
| PARAMETERS     | 1,545,425     | 181,377 |
| DROPOUT        | 0             | 0       |
| NORMALIZATION  | INSTANCE NORM | NO NORM |
```
[Epoch 0/200] [Batch 0/400] [D loss: 0.487405, acc:  50%] [G loss: 18.293304, adv: 0.879647, recon: 0.754539, id: 0.778340] time: 0:00:56.545487
```