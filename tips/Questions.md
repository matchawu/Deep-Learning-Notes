# Questions

[![hackmd-github-sync-badge](https://hackmd.io/G7GFTPnNSXOH4iEq87a0tA/badge)](https://hackmd.io/G7GFTPnNSXOH4iEq87a0tA)


### Cannot git clone
![](https://i.imgur.com/YuRFJUk.png)

Solution([via](https://medium.com/@mhagemann/how-to-fix-ssh-permission-denied-with-git-clone-f669b65f90ac)):
1. Generate ssh key from typing command `ssh-keygen` in Git Bash
3. Find `id_rsa.pub` file and copy the key
4. Paste it on GitHub settings>SSH keys & GPG keys
5. Try again `git clone`

### Command not found
![](https://i.imgur.com/KCJIJtr.png)

Solution [via](https://gist.github.com/evanwill/0207876c3243bbb6863e65ec5dc3f058)

1. find make command file at 

### make command not succeed and show some certain commands not found 

First, check out the Makefile. In my experience, the `$CUDA_HOME` mentioned in my Makefile but actually it is undefined. So I have to first define it in command line like `CUDA_HOME=/usr/local/bin/` or whatever you want it to be. Then, `make` it again.

### Networkx version

Meeting `AttributeError: Graphs has no attribute node`, and all the solutions on-line said it would be fine after you reinstall networkx v2.3, however, it didn't work for me. After several detours, the problem solved after installing network v1.11.

- The problem occurred when I try to run the code https://github.com/Hanjun-Dai/graph_adversarial_attack
- I create virtual environment first, and it contains Python2.7, which is suit to the .whl torch vision mentioned in the respository.
- And the problem occurred!
- Finally it's solved and the environment is built in Python 3.6, torch 0.3.1, and networkx 1.11.

### Visual Studio Code - ssh connect to server

To my surprise, this bothered me twice this summer. So I have to clarify the steps  as a record.

- Install Windows SSH Client in Settings
- Set up the SSH keys: https://www.footmark.info/linux/centos/windows-ssh-nopassword-linux/
- Get `id_rsa.pub`  (your public key in your computer), and authorize it on the server which you feel like connecting to. After finishing it, you could connect to server without password.
- ref: https://xenby.com/b/220-%e6%95%99%e5%ad%b8-%e7%94%a2%e7%94%9fssh-key%e4%b8%a6%e4%b8%94%e9%80%8f%e9%81%8ekey%e9%80%b2%e8%a1%8c%e5%85%8d%e5%af%86%e7%a2%bc%e7%99%bb%e5%85%a5

### LeetCode無法登入問題：使用Cookie登入

link: https://zhuanlan.zhihu.com/p/119999079

### Anaconda 無法順利安裝

發現：安裝流程跑完以後再開始功能表看不到Anaconda Prompt

可能造成原因：reinstall或是uninstall的時候出現未知問題

解決方法：在安裝檔上右鍵用系統管理員執行，就可以了