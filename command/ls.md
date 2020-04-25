## ls

## 结尾标志位,indicator含义:

```
ls -F appends symbols to filenames. These symbols show useful information about files.

@ means symbolic link (or that the file has extended attributes).
* means executable.
= means socket.
| means named pipe.
> means door.
/ means directory.
```

## 以友好格式显示时间

 export TIME_STYLE='+%Y-%m-%d %H:%M:%S'

## 时间

默认是 mtime 

- modification time (mtime，修改时间) 
  - 当该文件的“内容数据”更改时，就会更新这个时间。内容数据指的是文件的内容，而不是文件的属性。 
- status time（ctime，状态时间）
  - 当该文件的”状态（status）”改变时，就会更新这个时间，举例来说，更改了权限与属性，就会更新这个时间。 
- access time（atime，存取时间）：
  - 当“取用文件内容”时，就会更新这个读取时间。举例来说，使用cat去读取 ~/.bashrc，就会更新atime了。

[root@web10 ~]# ls -l --time=ctime install.log
-rw-r--r-- 1 root root 33386 2011-11-29 install.log
[root@web10 ~]# ls -l --time=atime install.log
-rw-r--r-- 1 root root 33386 07-13 16:02 install.log


## 按时间排序

## 按名称排序