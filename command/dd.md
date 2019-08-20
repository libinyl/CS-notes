## dd
```
//从 boot.bin 拷贝到 boot.img, 以 512byte 为一块,拷贝 1 块
dd if=boot.bin of=boot.img bs=512 count=1
```