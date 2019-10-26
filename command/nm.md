# nm: 用于查看二进制文件的符号表

名字来自于"name list".

## 符号类型说明

大写是全局变量,小写是局部变量(non-external).

类型 | 说明
---|---
A | 该符号的值是绝对的，在以后的链接过程中，不允许进行改变。这样的符号值，常常出现在中断向量表中，例如用符号来表示各个中断向量函数在中断向量表中的位置。
B | 该符号的值出现在非初始化数据段(bss)中。例如，在一个文件中定义全局static int test。则该符号test的类型为b，位于bss section中。其值表示该符号在bss段中的偏移。一般而言，bss段分配于RAM中
C | 该符号为common。common symbol是未初始话数据段。该符号没有包含于一个普通section中。只有在链接过程中才进行分配。符号的值表示该符号需要的字节数。例如在一个c文件中，定义int test，并且该符号在别的地方会被引用，则该符号类型即为C。否则其类型为B。
D | 该符号位于初始话数据段中。一般来说，分配到data section中。例如定义全局int baud_table[5] = {9600, 19200, 38400, 57600, 115200}，则会分配于初始化数据段中。
G | 该符号也位于初始化数据段中。主要用于small object提高访问small data object的一种方式。
I | 该符号是对另一个符号的间接引用。
N | 该符号是一个debugging符号。
R | 该符号位于只读数据区。例如定义全局const int test[] = {123, 123};则test就是一个只读数据区的符号。注意在cygwin下如果使用gcc直接编译成MZ格式时，源文件中的test对应_test，并且其符号类型为D，即初始化数据段中。但是如果使用m6812-elf-gcc这样的交叉编译工具，源文件中的test对应目标文件的test,即没有添加下划线，并且其符号类型为R。一般而言，位于rodata section。值得注意的是，如果在一个函数中定义const char *test = “abc”, const char test_int = 3。使用nm都不会得到符号信息，但是字符串“abc”分配于只读存储器中，test在rodata section中，大小为4。
S | 符号位于非初始化数据区，用于small object。
T | 该符号位于代码区text section。
U | 该符号在当前文件中是未定义的，即该符号的定义在别的文件中。例如，当前文件调用另一个文件中定义的函数，在这个被调用的函数在当前就是未定义的；但是在定义它的文件中类型是T。但是对于全局变量来说，在定义它的文件中，其符号类型为C，在使用它的文件中，其类型为U。
V | 该符号是一个weak object。当一个已定义的弱符号被连接到一个普通定义符号，普通定义符号可以正常使用，当一个未定义的弱对象被连接到一个未定义的符号，弱符号的值为0.
W | The symbol is a weak symbol that has not been specifically tagged as a weak object symbol.
- | 该符号是a.out格式文件中的stabs symbol。
? | 该符号类型没有定义

## 常用

按地址逆序输出: `nm -n -r kernel`

把不可读的符号名转为可读符号名: `-C`