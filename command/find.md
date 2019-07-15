## 找到当前目录及子目录下所有可执行文件

linux:

```
find . -type f -executable -print
```

macos:

```
find . -type f -perm +111 -print
```