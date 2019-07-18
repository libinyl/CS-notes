exec 函数族都是调用底层的`execve`.

```
int execve(const char *filename, char *const argv[],char *const envp[]);
```

此函数执行被参数`filename`指向的程序.后两个参数分别是参数列表和环境变量列表.

家族函数的区别:参考[回答](https://stackoverflow.com/a/47609180)

```c
// p:[x] 程序路径是 path
// v:[o] 参数通过 argv 数组传入
// e:[o] 环境变量从 envp 数组传入
int execve(const char *path, char *const argv[], char *const envp[]);

// p:[x] 程序路径是 path
// l:[o] 参数通过边长参数列表传入
// e:[x] 环境变量继承自调用者
int execl(const char *path, const char *arg0, ... /*, (char *)0 */);


// p:[x] 程序路径是 path
// l:[o] 参数通过变长参数列表传入
// e:[o] 环境变量从 envp 数组传入
int execle(const char *path, const char *arg0, ... /*, (char *)0, char *const envp[] */);


// p:[x] 程序路径是 path
// v:[o] 参数通过 argv 数组传入
// e:[x] 环境变量继承自程序调用者环境
int execv(const char *path, char *const argv[]);

// p:[o] 程序名由 file 给出,或者在 PATH 中搜索
// l:[o] 参数通过变长参数列表传入
// e:[x] 环境变量继承自调用者
int execlp(const char *file, const char *arg0, ... /*, (char *)0 */);

// p:[o] 程序名由 file 给出,或者在 PATH 中搜索
// v:[o] 参数通过 argv 数组传入
// e:[x] 环境变量继承自调用者环境
int execvp(const char *file, char *const argv[]);
```