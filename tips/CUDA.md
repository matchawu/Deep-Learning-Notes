# CUDA

`各種cuda問題`

## 指令



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