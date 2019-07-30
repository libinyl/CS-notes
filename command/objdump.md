
## 查看 file header :
```
root@MyServer:~/6828/lab# objdump -f obj/kern/kernel

obj/kern/kernel:     file format elf32-i386
architecture: i386, flags 0x00000112:
EXEC_P, HAS_SYMS, D_PAGED
start address 0x0010000c
```

## 查看所有 section 信息:

```
root@MyServer:~/6828/lab# objdump -s obj/kern/kernel |grep Contents
Contents of section .text:
Contents of section .rodata:
Contents of section .stab:
Contents of section .stabstr:
Contents of section .data:
Contents of section .bss:
Contents of section .comment:
```
## 查看特定 section 信息:

```
root@MyServer:~/6828/lab# objdump -s -j.stab obj/kern/kernel

obj/kern/kernel:     file format elf32-i386

Contents of section .stab:
 f0101f9c 01000000 0000be04 fb180000 01000000  ................
 f0101fac 64000000 000010f0 12000000 84000000  d...............
 f0101fbc 0c0010f0 00000000 44002c00 0c0010f0  ........D.,.....
 f0101fcc 00000000 44003900 150010f0 00000000  ....D.9.........
 (省略类似内容)
```

## 查看所有 header 信息

```
root@MyServer:~/6828/lab# objdump -x obj/kern/kernel

obj/kern/kernel:     file format elf32-i386
obj/kern/kernel
architecture: i386, flags 0x00000112:
EXEC_P, HAS_SYMS, D_PAGED
start address 0x0010000c

Program Header:
    LOAD off    0x00001000 vaddr 0xf0100000 paddr 0x00100000 align 2**12
         filesz 0x0000718d memsz 0x0000718d flags r-x
    LOAD off    0x00009000 vaddr 0xf0108000 paddr 0x00108000 align 2**12
         filesz 0x0000a948 memsz 0x0000a948 flags rw-
   STACK off    0x00000000 vaddr 0x00000000 paddr 0x00000000 align 2**4
         filesz 0x00000000 memsz 0x00000000 flags rwx

Sections:
Idx Name          Size      VMA       LMA       File off  Algn
  0 .text         00001831  f0100000  00100000  00001000  2**4
                  CONTENTS, ALLOC, LOAD, READONLY, CODE
  1 .rodata       0000075c  f0101840  00101840  00002840  2**5
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  2 .stab         000038f5  f0101f9c  00101f9c  00002f9c  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  3 .stabstr      000018fc  f0105891  00105891  00006891  2**0
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  4 .data         0000a300  f0108000  00108000  00009000  2**12
                  CONTENTS, ALLOC, LOAD, DATA
  5 .bss          00000648  f0112300  00112300  00013300  2**5
                  CONTENTS, ALLOC, LOAD, DATA
  6 .comment      00000035  00000000  00000000  00013948  2**0
                  CONTENTS, READONLY
SYMBOL TABLE:
f0100000 l    d  .text	00000000 .text
f0101840 l    d  .rodata	00000000 .rodata
f0101f9c l    d  .stab	00000000 .stab
f0105891 l    d  .stabstr	00000000 .stabstr
f0108000 l    d  .data	00000000 .data
f0112300 l    d  .bss	00000000 .bss
00000000 l    d  .comment	00000000 .comment
00000000 l    df *ABS*	00000000 obj/kern/entry.o
f010002f l       .text	00000000 relocated
f010003e l       .text	00000000 spin
00000000 l    df *ABS*	00000000 entrypgdir.c
(省略...)
```

## 只查看 section header 的内容

```
root@MyServer:~/6828/lab# objdump -h obj/kern/kernel

obj/kern/kernel:     file format elf32-i386

Sections:
Idx Name          Size      VMA       LMA       File off  Algn
  0 .text         00001831  f0100000  00100000  00001000  2**4
                  CONTENTS, ALLOC, LOAD, READONLY, CODE
  1 .rodata       0000075c  f0101840  00101840  00002840  2**5
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  2 .stab         000038f5  f0101f9c  00101f9c  00002f9c  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  3 .stabstr      000018fc  f0105891  00105891  00006891  2**0
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  4 .data         0000a300  f0108000  00108000  00009000  2**12
                  CONTENTS, ALLOC, LOAD, DATA
  5 .bss          00000648  f0112300  00112300  00013300  2**5
                  CONTENTS, ALLOC, LOAD, DATA
  6 .comment      00000035  00000000  00000000  00013948  2**0
                  CONTENTS, READONLY
```

## 查看反汇编代码

```
f0100008:   fe 4f 52                decb   0x52(%edi)
f010000b:   e4                      .byte 0xe4
obj/kern/kernel:     file format elf32-i386


Disassembly of section .text:

f0100000 <_start+0xeffffff4>:
f0100000:   02 b0 ad 1b 00 00       add    0x1bad(%eax),%dh
f0100006:   00 00                   add    %al,(%eax)
f0100008:   fe 4f 52                decb   0x52(%edi)
f010000b:   e4                      .byte 0xe4

f010000c <entry>:
f010000c:   66 c7 05 72 04 00 00    movw   $0x1234,0x472
f0100013:   34 12
f0100015:   b8 00 00 11 00          mov    $0x110000,%eax
f010001a:   0f 22 d8                mov    %eax,%cr3
f010001d:   0f 20 c0                mov    %cr0,%eax
f0100020:   0d 01 00 01 80          or     $0x80010001,%eax
f0100025:   0f 22 c0                mov    %eax,%cr0
f0100028:   b8 2f 00 10 f0          mov    $0xf010002f,%eax
f010002d:   ff e0                   jmp    *%eax

f010002f <relocated>:
f010002f:   bd 00 00 00 00          mov    $0x0,%ebp
f0100034:   bc 00 00 11 f0          mov    $0xf0110000,%esp
f0100039:   e8 56 00 00 00          call   f0100094 <i386_init>
(省略...)
```

## 查看 debug 信息

```
objdump -g
```

## 查看符号表信息

```
oot@MyServer:~/6828/lab# objdump -t obj/kern/kernel

obj/kern/kernel:     file format elf32-i386

SYMBOL TABLE:
f0100000 l    d  .text	00000000 .text
f0101840 l    d  .rodata	00000000 .rodata
f0101f9c l    d  .stab	00000000 .stab
f0105891 l    d  .stabstr	00000000 .stabstr
f0108000 l    d  .data	00000000 .data
f0112300 l    d  .bss	00000000 .bss
00000000 l    d  .comment	00000000 .comment
00000000 l    df *ABS*	00000000 obj/kern/entry.o
(省略...)
```

## 查看与 stab 相关的段信息

```
objdump -G
```

## 查看调试信息,以类似 C 语言的语法输出

```
objdump -g
```

## 反汇编

```
obj -d
```