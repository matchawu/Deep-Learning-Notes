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

