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

## 某文件的修改历史

```
git log filename
```

## 跟踪关系
```
// 查看跟踪关系
git branch -vv
// 设置跟踪关系
git branch --set-upstream-to=远端库名/远端分支名 本地分支名
```

## 重置

软重置到某一版本:
```
git reset hash值
```

## 分支
```
//查看所有分支
git branch -a 
//切换远程分支
git checkout -b 本地分支名 远程库/远程分支名
```

## 对比远程与本地的差异
```
git fetch origin
git log master..origin/master
```

## Git warning: push.default is unset; its implicit value is changing
