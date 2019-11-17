# ttcp

- ttcp -r: 默认在 5001 端口等待数据
- ttcp -t 对端 ip: 向对端 ip 发送数据,默认buffer长度:65536byte=64KB, 默认buffer数量: 8192=8K 即总共 64K*8K=512MB 的数据

- -l 指定 buffer 长度
- -n 指定 buffer 数量