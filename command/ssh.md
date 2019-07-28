## 设置 ssh-key 免密登录

1. `ssh-add ~/.ssh/id_rsa`
2. `cat ~/.ssh/id_rsa.pub | ssh username@server.address.com 'cat >> ~/.ssh/authorized_keys'`

## 防止连接超时

## 端口映射

```
ssh -L <port>:localhost:<port> <username>@<server>
ssh -L 25000:localhost:25000 root@154.48.248.252
```