*注：本文进行的验证基于 linux 环境，（很）可能依赖编译器的实现，这里暂不深究*

## 多态的解释

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

**问题：当用基类（父类）引用派生类（子类）对象，并调用它们均定义的函数，最终哪个函数会被调用**

Java 作为一种纯面向对象语言，强调函数的可 **重写 (override)** 性，在上述代码情景下，父类变量会毋庸置疑地调用子类对象的 `foo()`.

![](/Java&#32;多态png)

而 C++, 如同它一贯的风格，面对这一问题时，也给出了可选项，也就是 **虚函数** 的概念，即函数前的 `virtual` 关键字。如果用 C++ 写上述代码，且没有 `virtual` 关键字，那么最终行为是 `A->foo()`, 没有体现多态的行为，最终会调用 `dosth1()`；而只有在 A 类中的 `foo` 前加上 `virtual` 关键字，才会体现上述与 Java 类似的行为，最终调用 `dosth2()`.

这也是应当把基类的析构函数定义为 `virtual` 的原因：当试图通过基类指针对其引用的派生类对象进行析构时，如果没有指定 `virtual`, 就会只调用基类的析构函数，而派生类的析构函数得不到调用，造成 Memory Leak.

从这个对比也可以看出，Java 的函数默认就是 `virtual` 的。也正因如此，Bjarne Stroustrup 也忠告从 Java 转到 C++ 的程序员："函数不再是默认 `virtual` 的了。并非每个类都必然被继承。" (*C++ 程序设计语言 1.3.4*)

`virtual` 像一个开关，从基类的视角告诉编译器: 请**延迟绑定**. 把变量与函数延迟绑定,才使得下面的函数成为可能:

```C++
void dispatch(Base *p)
{
    p->foo();// call virtual funcion
}
```

我们无需考察 `p` 变量的真实类型, 更不知道 `foo()` 的具体实现,这都依赖于我们的约定: 每个继承了 `Base` 的派生类, 都对`foo()`作出了与其类型相关的恰当的实现.




## 更多资料

- [The Java™ Tutorial: Overriding and Hiding Methods](https://docs.oracle.com/javase/tutorial/java/IandI/override.html)
- 
