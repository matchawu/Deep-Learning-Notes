# Tips for Improving GAN
`瞭解問題在哪`

### Note
- 一開始D就要到100%
    - if not 給D多點參數
    - G loss 若越來越大代表已經沒有學習的餘地了
- D可能會慢慢到100%，代表G被打趴了
    - 給G多點參數
- 如果中途出現模糊或是壞掉
    - 就可以停下來了
- D不要使用normalization
    - 因為normalize會遺失資訊

### 參考資料
* ICCV 2017:訓練GAN的16個技巧
    * https://blog.csdn.net/xiaolouhan/article/details/84106629
* Tensorflow中learning rate decay的奇技淫巧
    * https://zhuanlan.zhihu.com/p/32923584