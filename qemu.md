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