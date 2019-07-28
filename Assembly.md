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