# template

## problem

- 现状: C++有严格的类型检查, 对于只能处理特定类型的数据,而实际情况无法处理多种类型.如:
- 诉求: 同一个函数可以处理多种类型的数据.


```C++
int min(int a,int b)
{
    return a<=b?a:b;
}
min(3,5); // 3
min(13,8); // 8
min(1.9, 3.7); // 1?
```