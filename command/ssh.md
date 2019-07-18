## 设置 ssh-key 免密登录

1. `ssh-add ~/.ssh/id_rsa`
2. `cat ~/.ssh/id_rsa.pub | ssh username@server.address.com 'cat >> ~/.ssh/authorized_keys'`