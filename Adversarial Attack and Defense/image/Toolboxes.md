# Toolbox

# AdvBox

在Python 3.7下，git clone AdvBox，並pip install paddlepaddle即可使用。

先訓練模型，再攻擊。

# ART

安裝：[https://github.com/IBM/adversarial-robustness-toolbox/wiki/Get-Started#setup](https://github.com/IBM/adversarial-robustness-toolbox/wiki/Get-Started#setup)

直接跑setup.py build/install會有UnicodeDecodeError：沒有解決

後來方法：新增一個環境(mm)，在上面跑pip install adversarial-robustness-toolbox，可以成功

# [FoolBox](https://github.com/bethgelab/foolbox)

安裝：新增環境(foolbox)，在上面跑 pip install foolbox 即可使用