##  coredump 限制
```
//查看限制
ulimit -a
//临时取消限制
ulimit -c unlimited
//永久取消限制
/etc/security/limits.conf
```

## 调试 coredump

```
gdb 可执行文件 core文件
```