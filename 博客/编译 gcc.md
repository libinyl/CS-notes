apt source libstdc++6   // 获取源码

不要在源代码目录下执行 configure

https://gcc.gnu.org/wiki/InstallingGCC

http://web.mit.edu/darwin/src/modules/gcc3/libstdc++-v3/docs/html/install.html

~/Documents/testgcccode/libstdc++code/gcc-8-8.3.0/objdir$     $PWD/../gcc-8.3.0/configure --prefix=/home/u1804/Documents/mystdlibc++ --enable-language=c++ -enable-cxx-flags="-g3 -O0"

约 18:29 开始编译.

现在快 10 分钟了.

应该是 make -j 4

18:36 开始

51 未结束 56 未结束 1902 未结束

19:22 未结束

从源代码找包:

dpkg -S /usr/include/stdlib.h
得到 动态库为 libc6-dev


