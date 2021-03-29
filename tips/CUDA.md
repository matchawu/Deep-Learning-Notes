# CUDA

`各種cuda問題`

[對應版本](https://www.tensorflow.org/install/source#linux)

## 指令

problem:

```
E: unable to locate package cuda
```

最後9.1裝起來會有問題因此還是先維持10.1。

問題應該是9.1只有Ubuntu 17.04的key，但我的server是16.04的，需要降其他packages的版本才不會有問題。

[參考還沒細看](https://comzyh.com/blog/archives/967/)

## 安裝

步驟：[link](https://towardsdatascience.com/setup-an-environment-for-machine-learning-and-deep-learning-with-anaconda-in-windows-5d7134a3db10)

1. Download Anaconda
2. Install Anaconda & Python
3. Start and Update Anaconda
4. Install CUDA Toolkit [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive) & cuDNN [cuDNN Download](https://developer.nvidia.com/rdp/cudnn-download)
5. Create an Anaconda Environment
6. Install Deep Learning API’s (TensorFlow & Keras)

---

### cuda 10.1 installation on Ubuntu 20.04

`實際上試過在18.04也是可行的`

[link](https://medium.com/@exesse/cuda-10-1-installation-on-ubuntu-18-04-lts-d04f89287130)

```
nvidia-smi # 此為driver，跑出來會跟安裝的版本沒對應，但最終去code確認torch是抓得到cuda的
```

```
nvcc -V # 此為compiler，
```

<img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201228140709148.png" alt="image-20201228140709148" style="zoom:80%;" />