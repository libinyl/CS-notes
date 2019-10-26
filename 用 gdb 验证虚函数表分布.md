## 前注

- *注 1: 本文暂不考察编译时多态/静态派发, 即函数重载或泛型编程*
- *注 2: 验证基于 64-bit linux 环境，（很）可能依赖编译器的实现，这里暂不深究*
- *注 3: 由于水平实在有限, 本文远未结束, 当前大概是 v0.1 的样子, 待日后更新*


## 多态的简单解释

面向对象程序设计的核心思想是数据抽象，继承和动态绑定，也就是所谓的多态。不管哪种语言，多态特性使得我们可以一定程度上忽略一些对象在类型方面的区别，对他们进行统一操作。

当引入继承的概念后，派生类（或子类）仍然可以定义与基类的签名（等特征）相同的函数。例如：

```Java
/* pseudo code */
class  A{
    void foo(){
        dosth1();
    }
}

class B extends A{
    void foo(){
        dosth2();
    }
}

main()
{
    A a = new B;
    a.foo();    /* dosth1() or  dosth2()? */
}
```

**问题：当用基类（父类）引用派生类（子类）对象，并调用它们均定义的函数，最终谁会被调用?**

Java 作为一种纯面向对象语言，强调函数的可 **重写 (override)** 性，在上述代码情景下，父类变量会毋庸置疑地调用子类定义的 `foo()`.

![](/images/Java&#32;多态.png)

而 C++, 如同它一贯的风格，面对这一问题时，也给出了**可选项**，也就是 **虚函数** 的概念，即函数前的 `virtual` 关键字。如果用 C++ 写上述代码，且没有 `virtual` 关键字，那么最终行为是 `A::foo()`, 没有体现多态的行为，最终会调用 `dosth1()`；而只有在 A 类中的 `foo` 前加上 `virtual` 关键字，才会体现上述与 Java 类似的行为，最终调用 `dosth2()`.

这也是应当把基类的析构函数定义为 `virtual` 的原因：当试图通过基类指针对其引用的派生类对象进行析构时，如果没有指定 `virtual`, 就会只调用基类的析构函数，而派生类的析构函数得不到调用，造成 Memory Leak.

从这个对比也可以看出，Java 的函数默认就是 `virtual` 的。也正因如此，Bjarne Stroustrup 也忠告从 Java 转到 C++ 的程序员："函数不再是默认 `virtual` 的了。并非每个类都必然被继承。" (*C++ 程序设计语言 1.3.4*)

`virtual` 像一个开关，从基类的视角告诉编译器: 请**动态绑定**. 把变量与函数在运行时动态绑定,才使得下面的函数意图成为可能:

```C++
void dispatch(Base *p)
{
    p->foo();// call virtual funcion
}
```

我们的约定: 每个继承了 `Base` 的派生类, 都对虚函数 `foo()` 作出了与其类型相关的恰当的实现. 我们无需考察 `p` 变量的具体派生类型, 也不需要知道 `foo()` 的具体实现, 对于`p->foo()`的具体调用将在运行时根据 p 所指的对象的类型信息动态决定. 

那么 C++ 怎样存储对象的类型信息, 以实现动态绑定? 当我们用一个基类指针调用某个函数时,程序怎样确定这个函数到底是调用基类中定义的,还是某个派生类中覆盖的呢? 再换句话说,怎样解析(resolve)出一个函数名所绑定的实现?

## 虚函数表与虚指针

很多前辈给出了清晰易懂的解释, 如陈皓大大十多年前的[文章](https://coolshell.cn/articles/12165.html).

这里重新介绍一下. 虚函数表机制是是大多数 C++ 实现动态派发的手段. 每个包含虚函数的类对应一张虚函数表, 每个元素的值是此类的虚函数的地址. 比如对于下面的代码:


```C++
// test.cpp
#include <iostream>

class Base
{
public:
    virtual void Foo()
    {}
    virtual void FooNotOverridden()
    {}
};

class Derived: public Base
{
public:
    void Foo()
    {}
};

int main()
{
    Base p1, p2;
    Derived d1, d2;

    std::cout << "done" << std::endl;
}
```

`Base`类定义了两个虚函数, `Derived`类继承了`Base`类,并重写了其中的`Foo`函数, 直接继承了`FooNotOverridden`函数.与虚函数相关的指向关系如下图:

![](/images/虚函数表.png)

## 用 gdb 验证虚函数表分布

事实上在与其他动态库链接之前, 编译器就已经就已经预备好了虚函数表/指针/类型信息的 *符号*. 

用`g++ -c`对 `test.cpp` 只编译不链接,并用 `nm -n -r -C` 查看其符号表:

```
//g++ -c test.cpp -o test.o && nm -n -r -C test.o
// 按符号地址降序排序

// ...省略...
0000000000000000 V vtable for Derived
0000000000000000 V vtable for Base
0000000000000000 V typeinfo name for Derived
0000000000000000 V typeinfo name for Base
0000000000000000 V typeinfo for Derived
0000000000000000 V typeinfo for Base
// ...省略...
0000000000000000 W Derived::Foo()
0000000000000000 W Base::Foo()
0000000000000000 W Base::FooNotOverridden()
0000000000000000 T main
// ...省略...
```

可以看到, 编译器为每个包含虚函数的类预留了`vtable`,`typeinfo name`,`typeinfo`的符号,地址是 0,类型均为 *V*, 即 *weak object*, 属尚未定义的符号. 有关 nm 输出的解释,请参考 [这里](https://sourceware.org/binutils/docs/binutils/nm.html). 这篇[博客](https://www.howtoforge.com/linux-nm-command/)也非常适合学习使用 `nm` 工具.

光从链接前的结果看到的内容很有限.现在我们用正常编译文件, 并查看其符号表:

```
// g++ -g -O0 test.cpp -o test && nm -n -r -C test
// 按符号地址降序排序
0000000000202138 B _end
...
0000000000202010 D _edata
0000000000202010 B __bss_start
0000000000202008 D __dso_handle
0000000000202000 W data_start
0000000000202000 D __data_start
...
0000000000201d78 V typeinfo for Base
0000000000201d60 V typeinfo for Derived
0000000000201d40 V vtable for Base
0000000000201d20 V vtable for Derived
...
0000000000000c79 V typeinfo name for Base
0000000000000c70 V typeinfo name for Derived
...
0000000000000bc6 W Derived::Foo()
0000000000000bba W Base::FooNotOverridden()
0000000000000bae W Base::Foo()
...
0000000000000aca T main
...
00000000000009c0 T _start
0000000000000938 T _init
// 其他尚未定义,等待链接动态库的符号
                 U vtable for __cxxabiv1::__si_class_type_info@@CXXABI_1.3
                 U vtable for __cxxabiv1::__class_type_info@@CXXABI_1.3
                 ...
```

注意到,`vtable` 等解析信息已经有了初步的地址,但尚未初始化.下面将此文件运行, 考察它们的关系:

```
// g++ -g -O0 test.cpp -o test && gdb test


```



## 附 A: 一些工具和选项

**c++filt**

 用于把编译器生成的符号名称解释(demangle)为可读名称.如 `_ZTS4Base => typeinfo name for Base`

其他命令的相关类似功能:

- `nm -C`
- `objdump -C`,
- `gdb set print demangle on`,`set print asm-demangle on`

**gdb的一些选项**

- -x: 

**hexdump**

用于以指定进制查看文件的实际内容.




## 附 B: 参考资料

- [The Java™ Tutorial: Overriding and Hiding Methods](https://docs.oracle.com/javase/tutorial/java/IandI/override.html)
- [Itanium C++ ABI](http://itanium-cxx-abi.github.io/cxx-abi/)
- [Shahar Mike's Web Spot: C++ vtables - Part 1 - Basics](https://shaharmike.com/cpp/vtable-part1/)
- [Linux Audit: The 101 of ELF files on Linux: Understanding and Analysis](https://linux-audit.com/elf-binaries-on-linux-understanding-and-analysis/#what-is-an-elf-file)
- [HowtoForge: Linux nm Command Tutorial for Beginners (10 Examples)](https://www.howtoforge.com/linux-nm-command/)
- [Stack Overflow: What does “symbol value” from nm command mean?](https://stackoverflow.com/questions/1863613/what-does-symbol-value-from-nm-command-mean)
- [MartinKysel.com: Demystifying Virtual Tables In C++ – Part 3 Virtual Tables](https://www.martinkysel.com/demystifying-virtual-tables-in-c-part-3-virtual-tables/)
- [Wikipedia: Virtual method table](https://en.wikipedia.org/wiki/Virtual_method_table)