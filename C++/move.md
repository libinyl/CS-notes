## 移动语义,右值引用,完美转发,类型推导

## 何时应用移动语义提高性能?

很多情况会发生对象拷贝,这其中很多情况对象拷贝后就销毁了.此时的移动会提升性能.

右值引用只能绑定在右值上.例如:

```C++
int i = 42;
int &r = i;     // 正确, 左值引用绑定在左值上
int &&r = i;    // 错误, 右值引用不能绑定在左值上
int &&rr = r;   // 错误, 虽然r 是右值引用类型,但 r 本身是左值,不可以用右值引用类型的 rr 来绑定.

const int &r = 42;  //正确,可以把一个 const 引用绑定在右值上
```

当看到一个右值引用时,我们知道:

- 所引用的对象即将被销毁

## move:将左值转换为右值

```C++
int i = 1;
int &&r = std::move(i); //move 之后,不可再使用 i. 不能对 i 的值做任何假设. 但可以对其赋新值.
```

调用 move 意味着一种承诺: 不再读取它,但可能写入它.

## 移动构造,移动赋值

移动构造,移动赋值不应分配任何新内存.

## 模板类型推断, 引用折叠

1.没有 const 的 模板类型参数 T

```C++
template <typename T> void f1(T &p); // 参数必须是左值
int i = 1;
const int j = 1;
f1(i);  // T 是 int
f1(j);  // T 是 const int
f1(5);  // 错误,不可传入左值
```

2.有 const 的 模板类型参数 T

```C++
template <typename T> void f2(const T &p); // 参数可以是 const 或非 const 左值,也可以是右值,即任何对象.
int i = 1;
const int j = 1;
```

3.引用折叠

对于模板类型右值引用参数:T&&,可以接受任意类型.

比如对于

```C++
template<typename T>
void f(T&& t);
```

**如果调用形式为`f(1);` ,  那么:**

`T` 被推断为 `int&&` 类型, `T&&` 被推断为 `int&& &&` 类型, 折叠为 `int&&` 类型.

**如果调用形式为 `int i = 1; f(i);` , 那么:**

`T` 被推断为 `int&` 类型, `T&&` 被推断为 `int& &&` 类型, 折叠为 `int&` 类型.


对于

```C++
template<typename T>
void f(T& t);
```

**如果调用形式为`f(1);` ,  那么:**

`T` 被推断为 `int` 类型, `T&` 被推断为 `int&` 类型, 未发生折叠.

**如果调用形式为 `int i = 1; f(i);` , 那么:**

`T` 被推断为 `int&&` 类型, `T&&` 被推断为 `int&& &` 类型, 折叠为 `int&` 类型.


- 所有右值引用折叠到右值引用上仍然是一个右值引用。（A&& && 变成 A&&）
- 所有的其他引用类型之间的折叠都将变成左值引用。 （A& & 变成 A&; A& && 变成 A&; A&& & 变成 A&）