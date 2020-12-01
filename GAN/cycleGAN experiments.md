# cycleGAN experiments

## datasets
- ukiyoe2photo
- vangogh2photo
- summer2winter_yosemite
- cartoon2animation


## 設定
- G,D的參數量
    - ver.1
        - G:6,171,025
        - D:662,981
    - ver.2
        - G:24,662,801
        - D:2,764,743
        - D-acc:78%-95%
- img_rows, img_cols
- (64,64,3)
- epochs
- batch_size
- batch
- sample_interval
- PatchGAN
- Normalization
- Dropout(rate)
- LeakyReLU(alpha=0.2)
- optimizer = Adam(0.0002, 0.5)
- loss_weights=[ 1, 1, 10, 10, 1, 1]
d,g,cycle,identity; mse,mae,mae

### D
![](https://i.imgur.com/wxdgTCA.png)

### G
![](https://i.imgur.com/1rb7xMD.png)

## ukiyoe2photo

### experiment 1:
`8/7`
> epochs:1000
> No dropout
> **BatchNormalization**

605
![](https://i.imgur.com/GiguqGN.png)
606
![](https://i.imgur.com/2vWEixF.png)

### experiment 2:
`8/7 part2`
> epochs:200
> **No dropout**
> **InstanceNormalization**
> 128 * 128

86
![](https://i.imgur.com/7oJVXNI.png)
70
![](https://i.imgur.com/HBrCcJ1.png)
193
![](https://i.imgur.com/Cadgxqo.png)


光線明顯的真實照片
195
![](https://i.imgur.com/Klo3KWc.png)

整體效果還是沒有很好
197
![](https://i.imgur.com/62sAiBI.png)

人像問題
189
![](https://i.imgur.com/OouLtdW.png)



### experiment 3:
`8/9 1724`
> epochs:1000
> **Dropout(0.5) * 2 on D**
> InstanceNormalization

#### results
989
![](https://i.imgur.com/eS6l95S.png)

人像在轉換上很容易失敗
842
![](https://i.imgur.com/vlDb5xN.png)
760
![](https://i.imgur.com/eLG70Fn.png)

小部分的人像比較不會受到影響
846
![](https://i.imgur.com/ATGKW6W.png)

### experiment 4:
`8/9 1941`
> epochs:500
> **Dropout(0.4)** * 2 on D
> InstanceNormalization

99
![](https://i.imgur.com/z0gwSHP.png)
429
![](https://i.imgur.com/rPvgwby.png)


### 問題
1. 人像(資料集內容物不同、色塊區分)
2. 夜間真實照片轉成浮世繪不太有效果

---


## vangogh2photo

### experiment 1:
`8/8 2217`
> epochs:1000
> **Dropout(0.4) * 2** on D
> InstanceNormalization
> 64 * 64

992
![](https://i.imgur.com/ZeUFcxU.png)


轉成真實照片時人像或物體會消失
967
![](https://i.imgur.com/7ajuoyY.png)

真實照片轉梵谷時邊界不明確上色會壞掉
987
![](https://i.imgur.com/k9TVDsw.png)


### experiment 2:
`8/9 2104`
> epochs:500
> **Dropout(0.5) * 2** on D
> InstanceNormalization
> 64 * 64

498
![](https://i.imgur.com/dKxjgQB.png)
461
![](https://i.imgur.com/ELS4I5w.png)
473
![](https://i.imgur.com/4ciBk53.png)



邊界不明確的原始圖片
474
![](https://i.imgur.com/ryxHZq7.png)

人像
496
![](https://i.imgur.com/GmT52GZ.png)
446
![](https://i.imgur.com/s6YsJmM.png)

黃色的天空or黃色的花
470
![](https://i.imgur.com/fgUZWZ6.png)


### experiment 3:
`8/9 2331`
> epochs:500
> **Dropout(0.5) * 1** on D
> InstanceNormalization
> 64 * 64

488
![](https://i.imgur.com/4qfGG3Y.png)

476
![](https://i.imgur.com/novq7tK.png)
450
![](https://i.imgur.com/0n4OKzm.png)

各種顏色的植物
473
![](https://i.imgur.com/dwM9OPe.png)
470
![](https://i.imgur.com/Smx45ND.png)

依舊失敗的人像
453
![](https://i.imgur.com/6QO5m9v.png)


### 問題
1. 人像(黃色的臉,以及多為黃色的背景/天空)
2. 植物顏色種類太多vs真實照片通常多為綠色

---

## summer2winter_yosemite

### experiment 1:
`8/10 0209`
> epochs:500
> **Dropout(0.5) * 1** on D
> **InstanceNormalization**
> 64 * 64

437
![](https://i.imgur.com/UGp6vOt.png)
435
![](https://i.imgur.com/qJXsIxP.png)

但大部分效果都很差
481
![](https://i.imgur.com/nInP5n3.png)
431
![](https://i.imgur.com/K7DKAN5.png)


### experiment 2:
`8/10 1122`
> epochs:500
> **No dropout**
> InstanceNormalization
> 64 * 64

499
![](https://i.imgur.com/tb12Wxw.png)
475
![](https://i.imgur.com/ALTsOgL.png)
462
![](https://i.imgur.com/BH8HGa5.png)

不夠明顯或失敗的例子
471
![](https://i.imgur.com/Kv2BXUG.png)
421
![](https://i.imgur.com/DbFXBVn.png)


### experiment 3:
`8/10 2348`
> epochs:500
> **Dropout(0.3) * 1** on D
> InstanceNormalization
> 64 * 64

487
![](https://i.imgur.com/zjBYCMT.png)
472
![](https://i.imgur.com/OV7iGcE.png)
465
![](https://i.imgur.com/0sWzebk.png)

不夠明顯的綠色/白色，不會被轉換(的感覺)

433
![](https://i.imgur.com/C75JW6l.png)
432
![](https://i.imgur.com/v0JdfcL.png)
427
![](https://i.imgur.com/vBFQeuo.png)

### 問題
1. 照片的明暗會影響(只轉換某種明確的白色、翠綠色)
2. 季節無關的顏色(假設照片中只有這些顏色)，不太具有轉換效果

---

## cartoon2animation

### experiment 1:
`8/8 1935`
> epochs:1000
> **Dropout(0.5) * 1** on D
> **InstanceNormalization**
> 64 * 64


### experiment 2:
`8/8 2221`
> epochs:1000
> **Dropout(0.5) * 2** on D
> InstanceNormalization
> 64 * 64

978
![](https://i.imgur.com/Bu6naFV.png)
968
![](https://i.imgur.com/YEIJ4en.png)
![](https://i.imgur.com/fTBYWAV.png)


352
![](https://i.imgur.com/NNqHKOu.png)
512
![](https://i.imgur.com/nRo2cwY.png)


卡通轉動漫人物失敗

### experiment 3:
`8/11 1418`
> epochs:500
> **Dropout(0.5) * 3** on D
> InstanceNormalization
> 64 * 64

111
![](https://i.imgur.com/9s3CCbo.png)
102
![](https://i.imgur.com/pnl7hj4.png)


### experiment 4:
`8/11 1830`
> epochs:500
> **Dropout(0.5) * 1** on **G**
> InstanceNormalization
> 64 * 64

60
![](https://i.imgur.com/QbR2Z19.png)
11
![](https://i.imgur.com/6FYku8l.png)

### 問題
1. 卡通轉動漫人物細節不清楚

## 未來
1. 修正上述問題
2. network
3. 原始paper code

## 對照
paper:
![](https://i.imgur.com/x0kAzKF.jpg)


## code
```
#!/usr/bin/env python
from __future__ import print_function, division
import scipy

from keras.datasets import mnist
from keras_contrib.layers.normalization.instancenormalization import InstanceNormalization
from keras.layers import Input, Dense, Reshape, Flatten, Dropout, Concatenate
from keras.layers import BatchNormalization, Activation, ZeroPadding2D
from keras.layers.advanced_activations import LeakyReLU
from keras.layers.convolutional import UpSampling2D, Conv2D
from keras.models import Sequential, Model
from keras.optimizers import Adam
import datetime
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt
import sys
from data_loader import DataLoader
import numpy as np

import tensorflow as tf
import os
os.environ["CUDA_VISIBLE_DEVICES"] = "0"
from keras.backend.tensorflow_backend import set_session
config = tf.ConfigProto()
config.gpu_options.per_process_gpu_memory_fraction = 0.8
set_session(tf.Session(config=config))

import os
if not os.path.exists("/mnt/sda/wwj0507/datasets"):
    os.makedirs("/mnt/sda/wwj0507/datasets")
os.chdir('/mnt/sda/wwj0507/datasets')


class CycleGAN():
    def __init__(self):
        # Input shape
        self.img_rows = 64
        self.img_cols = 64
        self.channels = 3
        self.img_shape = (self.img_rows, self.img_cols, self.channels)

        # Configure data loader
        self.dataset_name = 'cartoon2animation'
        self.data_loader = DataLoader(dataset_name=self.dataset_name,
                                      img_res=(self.img_rows, self.img_cols))
        

        # Calculate output shape of D (PatchGAN)
        patch = int(self.img_rows / 2**4)
        self.disc_patch = (patch, patch, 1)

        # Number of filters in the first layer of G and D
        self.gf = 32
        self.df = 64

        # Loss weights
        self.lambda_cycle = 10.0                    # Cycle-consistency loss
        self.lambda_id = 0.1 * self.lambda_cycle    # Identity loss

        optimizer = Adam(0.0002, 0.5)

        # Build and compile the discriminators
        self.d_A = self.build_discriminator()
        self.d_B = self.build_discriminator()
        self.d_A.compile(loss='mse',
            optimizer=optimizer,
            metrics=['accuracy'])
        self.d_B.compile(loss='mse',
            optimizer=optimizer,
            metrics=['accuracy'])

        #-------------------------
        # Construct Computational
        #   Graph of Generators
        #-------------------------

        # Build the generators
        self.g_AB = self.build_generator()
        self.g_BA = self.build_generator()

        # Input images from both domains
        img_A = Input(shape=self.img_shape)
        img_B = Input(shape=self.img_shape)
        

        # Translate images to the other domain
        fake_B = self.g_AB(img_A)
        fake_A = self.g_BA(img_B)
        # Translate images back to original domain
        reconstr_A = self.g_BA(fake_B)
        reconstr_B = self.g_AB(fake_A)
        # Identity mapping of images
        img_A_id = self.g_BA(img_A)
        img_B_id = self.g_AB(img_B)

        # For the combined model we will only train the generators
        self.d_A.trainable = False
        self.d_B.trainable = False

        # Discriminators determines validity of translated images
        valid_A = self.d_A(fake_A)
        valid_B = self.d_B(fake_B)

        # Combined model trains generators to fool discriminators
        self.combined = Model(inputs=[img_A, img_B],
                              outputs=[ valid_A, valid_B,
                                        reconstr_A, reconstr_B,
                                        img_A_id, img_B_id ])
        self.combined.compile(loss=['mse', 'mse',
                                    'mae', 'mae',
                                    'mae', 'mae'],
                            loss_weights=[  1, 1,
                                            self.lambda_cycle, self.lambda_cycle,
                                            self.lambda_id, self.lambda_id ],
                            optimizer=optimizer)        

    def build_generator(self):
        """U-Net Generator"""

        def conv2d(layer_input, filters, f_size=4):
            """Layers used during downsampling"""
            d = Conv2D(filters, kernel_size=f_size, strides=2, padding='same')(layer_input)
            d = LeakyReLU(alpha=0.2)(d)
            d = InstanceNormalization()(d)
            return d

        def deconv2d(layer_input, skip_input, filters, f_size=4, dropout_rate=0):
            """Layers used during upsampling"""
            u = UpSampling2D(size=2)(layer_input)
            u = Conv2D(filters, kernel_size=f_size, strides=1, padding='same', activation='relu')(u)
            if dropout_rate:
                u = Dropout(dropout_rate)(u)
            u = InstanceNormalization()(u)
            u = Concatenate()([u, skip_input])
            return u

        # Image input
        d0 = Input(shape=self.img_shape)

        # Downsampling
        d1 = conv2d(d0, self.gf)
        d2 = conv2d(d1, self.gf*2)
        d3 = conv2d(d2, self.gf*4)
        d4 = conv2d(d3, self.gf*8)

        # Upsampling
        u1 = deconv2d(d4, d3, self.gf*4)
        u2 = deconv2d(u1, d2, self.gf*2)
        u3 = deconv2d(u2, d1, self.gf)

        u4 = UpSampling2D(size=2)(u3)
        output_img = Conv2D(self.channels, kernel_size=4, strides=1, padding='same', activation='tanh')(u4)

        return Model(d0, output_img)

    def build_discriminator(self):

        def d_layer(layer_input, filters, f_size=4, normalization=True):
            """Discriminator layer"""
            d = Conv2D(filters, kernel_size=f_size, strides=2, padding='same')(layer_input)
            d = LeakyReLU(alpha=0.2)(d)
            d = Dropout(0.5)(d)
            d = Dropout(0.5)(d)
            if normalization:
                d = InstanceNormalization()(d)
            return d

        img = Input(shape=self.img_shape)

        d1 = d_layer(img, self.df, normalization=False)
        d2 = d_layer(d1, self.df*2)
        d3 = d_layer(d2, self.df*4)
        d4 = d_layer(d3, self.df*8)

        validity = Conv2D(1, kernel_size=4, strides=1, padding='same')(d4)

        return Model(img, validity)

    def train(self, epochs, batch_size=1, sample_interval=50):

        start_time = datetime.datetime.now()

        # Adversarial loss ground truths
        valid = np.ones((batch_size,) + self.disc_patch)
        fake = np.zeros((batch_size,) + self.disc_patch)
        print(789)
        for epoch in range(epochs):
            for batch_i, (imgs_A, imgs_B) in enumerate(self.data_loader.load_batch(batch_size)):
                print(7289)
                # ----------------------
                #  Train Discriminators
                # ----------------------

                # Translate images to opposite domain
                fake_B = self.g_AB.predict(imgs_A)
                fake_A = self.g_BA.predict(imgs_B)

                # Train the discriminators (original images = real / translated = Fake)
                dA_loss_real = self.d_A.train_on_batch(imgs_A, valid)
                dA_loss_fake = self.d_A.train_on_batch(fake_A, fake)
                dA_loss = 0.5 * np.add(dA_loss_real, dA_loss_fake)

                dB_loss_real = self.d_B.train_on_batch(imgs_B, valid)
                dB_loss_fake = self.d_B.train_on_batch(fake_B, fake)
                dB_loss = 0.5 * np.add(dB_loss_real, dB_loss_fake)

                # Total disciminator loss
                d_loss = 0.5 * np.add(dA_loss, dB_loss)


                # ------------------
                #  Train Generators
                # ------------------

                # Train the generators
                g_loss = self.combined.train_on_batch([imgs_A, imgs_B],
                                                        [valid, valid,
                                                        imgs_A, imgs_B,
                                                        imgs_A, imgs_B])

                elapsed_time = datetime.datetime.now() - start_time

                # Plot the progress
                print ("[Epoch %d/%d] [Batch %d/%d] [D loss: %f, acc: %3d%%] [G loss: %05f, adv: %05f, recon: %05f, id: %05f] time: %s " \
                                                                        % ( epoch, epochs,
                                                                            batch_i, self.data_loader.n_batches,
                                                                            d_loss[0], 100*d_loss[1],
                                                                            g_loss[0],
                                                                            np.mean(g_loss[1:3]),
                                                                            np.mean(g_loss[3:5]),
                                                                            np.mean(g_loss[5:6]),
                                                                            elapsed_time))

                # If at save interval => save generated image samples
                if batch_i % sample_interval == 0:
                    self.sample_images(epoch, batch_i)
                

    def sample_images(self, epoch, batch_i):
        os.makedirs('images/%s' % self.dataset_name, exist_ok=True)
        r, c = 2, 3

        imgs_A = self.data_loader.load_data(domain="A", batch_size=1, is_testing=True)
        imgs_B = self.data_loader.load_data(domain="B", batch_size=1, is_testing=True)

        # Demo (for GIF)
        #imgs_A = self.data_loader.load_img('datasets/apple2orange/testA/n07740461_1541.jpg')
        #imgs_B = self.data_loader.load_img('datasets/apple2orange/testB/n07749192_4241.jpg')

        # Translate images to the other domain
        fake_B = self.g_AB.predict(imgs_A)
        fake_A = self.g_BA.predict(imgs_B)
        # Translate back to original domain
        reconstr_A = self.g_BA.predict(fake_B)
        reconstr_B = self.g_AB.predict(fake_A)

        gen_imgs = np.concatenate([imgs_A, fake_B, reconstr_A, imgs_B, fake_A, reconstr_B])

        # Rescale images 0 - 1
        gen_imgs = 0.5 * gen_imgs + 0.5

        titles = ['Original', 'Translated', 'Reconstructed']
        fig, axs = plt.subplots(r, c)
        cnt = 0
        for i in range(r):
            for j in range(c):
                axs[i,j].imshow(gen_imgs[cnt])
                axs[i, j].set_title(titles[j])
                axs[i,j].axis('off')
                cnt += 1
        fig.savefig("images/%s/%d_%d.png" % (self.dataset_name, epoch, batch_i))
        plt.close()

if __name__ == '__main__':    
    gan = CycleGAN()
    gan.train(epochs= 100, batch_size=200, sample_interval=200)

```