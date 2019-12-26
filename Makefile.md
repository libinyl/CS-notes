## 参考

https://www.cnblogs.com/LoTGu/p/5936465.html

## 选项


- -p :打印规则

## makefile 搜索顺序

- GNUmakefile(不推荐)
- Makefile(推荐,位置接近文件夹顶端,接近README)
- makefile

## 特殊符号

特殊符号 | 含义
-----|---
$< | 第一个依赖文件名
$^ | 所有依赖文件名
$@ | 目标文件名称
$(@D) |表示"\$@"的目录部分(不以斜杠作为结尾)，如果"\$@"值是"dir/foo.o"，那么"\$(@D)"就是"dir"，而如果"$@"中没有包含斜杠的话，其值就是"."（当前目录） 。
$? | 当前目标所依赖的文件列表中比当前目标文件还要新的文件


## 百分号特殊符号

%.o : %.cc

## 预定义变量

参考: https://www.gnu.org/software/make/manual/html_node/Implicit-Variables.html

## 模板

```
TARGET:=simplest
OBJ:= simplest.o


LD :=ld
NASM:=nasm

LD_FLAGS 	:=
NASM_FLAGS	:= -f elf64

$(TARGET): $(OBJ)
	$(LD) $(LD_FLAGS) $^ -o $@

$(OBJ): simplest.asm
	$(NASM) $(NASM_FLAGS) -g $^ -o $@

clean:
	rm -rf $(TARGET) $(OBJ)
```

## 常见命令解析

OBJS := $(patsubst %.cc, %.o, $(SRCS))

把 SRCS 里的所有 .cc 文件名替换为.o 结尾并赋给 OBJS

LIBOBJS := $(filter-out .objs/main.o, $(OBJS))

去掉 OBJS 中所有符合中间模式的值,赋给LIBOBJS

$(wildcard *.c)

获取当前目录.c 文件列表


ranlib 更新库索引表

patsubst
