# 問題紀錄

## TypeError

### Expected DataType for argument 'Tout' not torch.float32

型態問題，遇到這個問題的當下是因為我有torch也有keras的東西(不良行為)，因此有些東西需要先轉到numpy再挪用。

## RuntimeError

### CUDA error: device-side assert triggered

[LINK](https://blog.csdn.net/Geek_of_CSDN/article/details/86527107)

>  改為在CPU上運行：因為當模型在GPU上運行的時候其實是沒辦法顯示出真正導致錯誤的地方的（按照PyTorch Dev的說法：“Because of the asynchronous nature of cuda, the assert might not point to a full correct stack trace pointing to where the assert was triggered from.”即這是CUDA的特性，他們也沒辦法），所以可以通過將模型改成在CPU上運行來檢查出到底是哪裡出錯（因為CPU模式下會有更加細緻的語法/程序檢查）。但是這個方法通常是不可行的，因為可能訓練的網絡特別大，轉到CPU上訓練的話可能會花費很長時間，那麼就應該嘗試下面的方法。

## AttributeError

### module 'tensorflow' has no attribute 'get_default_graph 

[LINK](https://github.com/keras-team/keras/issues/12379)

![image-20210108211702244](C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20210108211702244.png)

簡單來說，把原本的 `from keras import xxx` 改成 `from tensorflow.keras import xxx` 即可。

## ImportError

### libcublas.so.10.0: cannot open shared object file: No such file

[LINK](https://blog.csdn.net/Jiaach/article/details/88418216)

> 原因為`tensorflow`版本與`CUDA`的版本不對應

查看CUDA版本：[*](https://blog.csdn.net/baidu_32936911/article/details/79774289)

```python
cat /usr/local/cuda/version.txt # cuda
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2 # cuDNN
```

查看tensorflow和CUDA版本的對應關係：

https://tensorflow.google.cn/install/source

