# Type Casting in C

## 1 自动类型转换, Implicit conversions

自动类型转换分三种情况:

### 1.1 算数转换

包括 +-*/和符号运算

- 若参与运算的类型不同,则先转换为同一类型.
- 转换按数据长度增长(变"宽")的方向进行,以保证不降低精度.
  - 1.若字节数不同,则转换为字节数多的类型
  - 2.若字节数相同,但一种有符号另一种无符号,则转换为无符号类型.
  - 3.char 和 short 类型参与运算时,必须先转换为int 型.

具体提升路线:

```
long double
↑
double
↑
float
↑
unsigned long long
↑
long long
↑
unsigned long
↑
long
↑
int
```

### 1.2 赋值转换

- 赋值操作时,赋值运算符右边的数据必须转换为赋值号左边的数据.
- 如果右边的数据类型大于左边,则发生截断或舍入.
- 对于函数调用,如果函数有原型,那么对应的参数都被转换为对应参数的非完全限定名(`unqualified type`,即不包含 const,volite 的类型名,如`int`).

### 1.3 输出转换

## 2 强制类型转换

## 参考资料

[cppreference](https://en.cppreference.com/w/c/language/conversion)