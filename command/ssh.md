## 设置 ssh-key 免密登录
参考 https://www.cnblogs.com/hanwen1014/p/9048717.html

1. 服务器生成密钥`ssh-keygen`,结果生成到 `~/.ssh`下:
```
root@MyServer:~/.ssh# ls
id_rsa  id_rsa.pub  known_hosts
```
2. 将本地 id_rsa.pub 文件的内容拷贝至远程服务器的 ~/.ssh/authorized_keys 文件

```
cat ~/.ssh/id_rsa.pub | ssh username@server.address.com 'cat >> ~/.ssh/authorized_keys'
```

## 配置 vscode ssh 免密




## 防止连接超时

1. 配置客户端： /etc/ssh/ssh_config 文件中添加`ServerAliveInterval 60`
2. 配置服务器： /etc/ssh/sshd_config 文件中添加
- ClientAliveInterval 600 数值是秒 可以随意设置
- ClientAliveCountMax 10 如果发现客户端没有响应，则判断一次超时，参数设置是允许超时次数
3. 应用设置:
- 服务器: `systemctl reload	sshd`


```
systemctl                   ##服务控制命令
systemctl start sshd        ##开启服务
systemctl stop sshd         ##关闭服务
systemctl restart	sshd	##重启服务
systemctl reload	sshd 	##重新加载服务配置  <===
```

## 端口映射

```
ssh -L <port>:localhost:<port> <username>@<server>
ssh -L 25000:localhost:25000 root@154.48.248.252
```