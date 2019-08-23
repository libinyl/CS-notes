显示文件夹结构:
```shell
while true;do tree;sleep 1;clear;done
```
等价于
```
watch -n 1 tree
```


## 清空文件
```
> hello.txt
```

## 基础

变量取值: ${i}

## 前台与后台

把当前进程放到后台运行: `ctrl z`

查看后台任务: `jobs`

与最近的后台任务切换: `fg`

杀死后台进程: kill %[后台job号]



## 环境变量加载顺序

![bash脚本加载顺序](/images/bash启动顺序.png)
