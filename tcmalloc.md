##  tcmalloc

全称: thread cache malloc

内存分配按大小分为三类:

- 小对象分配,(0, 256KB]
- 中对象分配,(256KB,1MB]
- 大对象分配,(1MB, +∞)

1. 整个虚拟地址空间分为 n 个 page,每个 page 默认 8KB
2. 连续的几个 page 称为 1 个 span.