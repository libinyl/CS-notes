
## remote

修改 origin:

```
git remote origin set-url [url]
```

## 回退单个文件

```
git checkout origin/master [filename]
```

## 冲突标记

```
本地
<<<<<< HEAD:file.txt
Hello world
=======
Goodbye
>>>>>> 77976da35a11db4580b80ae27e8d65caf5208086:file.txt
其他人
```