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


## 预定义变量

参考: https://www.gnu.org/software/make/manual/html_node/Implicit-Variables.html

