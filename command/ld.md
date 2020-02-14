# ld

选项    作用
-N  设置 text 段和 data 段可以被读写;不将 data 段设置为页对齐;

-L -rpath
https://stackoverflow.com/a/8482308

-L: 用于链接时 ld 寻找库的路径
-rpath: 嵌入到二进制文件中的路径,用于运行时寻找库

	gcc	-Wl,-Bstatic \
			-la \
			-lb \
			-lc \
			-Wl,-Bdynamic \
			-ld \
			-le 

## 静态库命名规则

```
lib + <library name> + .a
```

## 静态库与动态库的对比

1. 当客户端二进制文件链接静态库时不会把整个静态库内容链接进来,只会链接目标文件中必要的符号.最小粒度是目标文件.
2. 动态库的最小粒度是符号.
3. 静态库的符号不会作为全局可见的符号保留,而是会变成私有符号



## 动态库文件名规则

```
lib + <library name> + .so + <version info>

其中 version info = M.m.p

简记为妈卖批

M: 主办版本号
m: 次版本号
p: 补丁版本号
```


## 动态库的 soname

```
lib + <library name> + .so + <library Major (主要)version digit(s)>
```

如 libz.so.1.2.3.4 的 soname 是 libz.so.1

soname 由链接器嵌入到 elf 文件库的 elf 字段中.可以用 readelf -d xxx 来查看.


## 关于 -L 和 -l

-L 和 -l 用于指定**构建时**库文件路径.区别于**运行时**.

如果只链接, 不需要-Wl

gcc main.o -L../sharedlib -lworkingdemo -o demo

如果编译+链接,则需要-Wl

gcc -Wall -fPIC main.cpp -Wl,-L../sharedlib -Wl,-lworkingdemo -o demo



## -l 选项实际做了什么?

-L 仅在链接阶段起作用,之后不再起任何作用

-l 传递的参数会被嵌入到二进制的库文件中,并在运行时发挥作用.

参考: 高级C/C++ 编译技术(中文版), p102~p103

https://stackoverflow.com/a/6578558

处理过程:-Wl,--verbose

https://stackoverflow.com/a/31370503

https://stackoverflow.com/a/28088356

https://stackoverflow.com/a/14330267

You can pass a list of options to the linker using "-Wl".

    #cgo LDFLAGS: -Wl,-Bstatic -ldep1 -ldep2 -Wl,-Bdynamic

That will statically link libdep1 and libdep2, while leaving the rest