## 查看物理内存

```
pmemsave 0 0x08000000  meminit.dump
// linux
tac <(xxd -a -c 16 meminit.dump)>meminit.md
// mac
tail -r <(xxd -a -c 16 meminit.dump)>meminit.md
```

## kernel 的入口:

```
readelf -h obj/kern/kernel
0x10000c
```

tail -r <(xxd -a -c 16 meminit.dump)>meminit.md

## monitor [常用命令](https://en.wikibooks.org/wiki/QEMU/Monitor#info)

在 6.828 实验中,键入`Ctrl A,C`进入 qemu 监控模式.

命令 | 功能
---|---
info mem | 查看虚拟内存映射状态 | 
info registers | 查看 CPU 状态 |

