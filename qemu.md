## 查看物理内存
pmemsave 0 0x0A000000  mem.dump
tac <(xxd -a mem.dump)>mem.md