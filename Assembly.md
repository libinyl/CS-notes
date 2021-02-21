## 命令简介

命令 | 全称 | 含义
---|----|---
orl | or logical | 位或
movl | mov long | 字长传送 32 位
movw | mov word | 字传送 16 位
movb | mov byte | 字节传送 8 位

## 常用操作

- 启动保护模式

- 开启分页()

```x86asm
movl	%cr0, %eax
orl	$(CR0_PE|CR0_PG|CR0_WP), %eax
movl	%eax, %cr0
```

lgdt

## 知识点

intel 没有提供用 mov 改变 cs:ip 的功能.只能通过 jmp 来改变 cs 和 ip.

## 内联汇编

r | Register
--|---------
a | %eax, %ax, %al
b | %ebx, %bx, %bl
c | %ecx, %cx, %cl
d | %edx, %dx, %dl
S | %esi, %si
D | %edi, %di

test1