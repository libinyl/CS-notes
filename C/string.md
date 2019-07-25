## memset

原型：

```
void *memset(void *s, int c, size_t n);
```

解释：

把`s`指向的`n`个字节都用常量`c`来填充,最后返回指向`s`指向的区域的指针.