## mac 下编译生成 linux 可执行的 elf 文件

```
brew install i386-elf-binutils
i386-elf-gcc -v
```

## 查看搜索路径

## mac 交叉编译

```
/usr/local/Cellar/i386-elf-gcc/9.1.0/bin/i386-elf-gcc
```

## 常用命令解释

选项 | 含义
---|---
-nostdinc | 不要在标准系统目录中寻找头文件.只搜索`-I'选项指定的目录(以及当前目录,如果合适).结合使用`-nostdinc'和`-I-'选项,你可以把包含文件搜索限制在显式指定的目录.

## 生命周期命令

命令 | 作用 | 后缀
---|----|---
-E | 预处理 | a.i
-S | 编译,生成汇编代码 | .S
-c | 汇编,生成二进制机器码 | .o
-o | 链接 | .out

## 编译 gcc 源码

--enable-languages=c++