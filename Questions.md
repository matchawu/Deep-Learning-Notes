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

It is so weird.

