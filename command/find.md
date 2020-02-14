## 找到当前目录及子目录下所有可执行文件

linux:

```
find . -type f -executable -print
```

macos:

```
find . -type f -perm +111 -print
```

## 找到当前目录下文件名包含 xx 的文件

find . -name '*xxx*'

https://www.cnblogs.com/shenqidu/p/10615593.html