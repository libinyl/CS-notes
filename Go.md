## 命令解释

go 环境: https://howistart.org/posts/go/1/

## 调试

go build -gcflags "all=-N -l" xxx
dlv --listen=:2345 --headless=true --api-version=2 --accept-multiclient exec ./xxx

## 代码组织

模块化: https://segmentfault.com/a/1190000018536993

```
$ go list -m all

$ go list -m -json all # json 格式输出
{
        "Path": "golang.org/x/text",
        "Version": "v0.3.0",
        "Time": "2017-12-14T13:08:43Z",
        "Indirect": true,
        "Dir": "/Users/lishude/go/pkg/mod/golang.org/x/text@v0.3.0",
        "GoMod": "/Users/lishude/go/pkg/mod/cache/download/golang.org/x/text/@v/v0.3.0.mod"
}
{
        "Path": "rsc.io/quote",
        "Version": "v1.5.2",
        "Time": "2018-02-14T15:44:20Z",
        "Dir": "/Users/lishude/go/pkg/mod/rsc.io/quote@v1.5.2",
        "GoMod": "/Users/lishude/go/pkg/mod/cache/download/rsc.io/quote/@v/v1.5.2.mod"
}
```

包: 同一个包下的源文件一起编译,每个源文件的符号对同包其他文件可见.

模块: 一个模块包含多个相关的包.

sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt update
sudo apt install golang-go

https://thenewstack.io/understanding-golang-packages/

## array

https://blog.csdn.net/xiangxianghehe/article/details/78356355

```go
func arrayinit() {
	var a [2]string // 声明长度，不指定元素
	a[0] = "abc"
	a[1] = "cba"

	arr1 := [2]int{3}       // 声明长度，指定部分元素
	arr1 = [2]int{3, 4}     // 声明长度，指定全部元素
	arr1 = [...]int{1, 2}   // 不声明长度，指定全部元素
	arr2 := [...]int{99: 1} // 不声明长度，指定全部元素

	fmt.Printf("%T", arr1)
	fmt.Printf("%T", arr2)
}
```

## slice

```go

```

## go command

go build:

go get: 

- -d 只下载不安装
- -f 只有在你包含了 -u 参数的时候才有效，不让 -u 去验证 import 中的每一个都已经获取了，这对于本地 fork 的包特别有用
- -fix 在获取源码之后先运行 fix，然后再去做其他的事情
- -t 同时也下载需要为运行测试所需要的包
- -u 强制使用网络去更新包和它的依赖包 下载丢失的包，但不会更新已经存在的包
- -v 显示执行的命令

go clean

go clean -modcache

## import path

假设模块 github.com/google/go-cmp 下有一个包 cmp,那么:

- module: github.com/google/go-cmp
- package: cmp
- 包的 import path: github.com/google/go-cmp/cmp
- 标准库里的包没有 import path

 contains a package in the directory cmp/. That package's import path is github.com/google/go-cmp/cmp. Packages in the standard library do not have a module path prefix.

 ## go env



## 语法

声明 slice

 ```go
letters := []string{"a", "b", "c", "d"}
var s []byte
s = make([]byte, 5, 5)
 ```

## make

参数: 类型, 长度,预留空间长度

map只能为slice, map, channel分配内存，并返回一个初始化的值。首先来看下make有以下三种不同的用法：

1. make(map[string]string)

2. make([]int, 2)

3. make([]int, 2, 4)


1. 第一种用法，即缺少长度的参数，只传类型，这种用法只能用在类型为map或chan的场景，例如make([]int)是会报错的。这样返回的空间长度都是默认为0的。

2. 第二种用法，指定了长度，例如make([]int, 2)返回的是一个长度为2的slice

3. 第三种用法，第二参数指定的是切片的长度，第三个参数是用来指定预留的空间长度，例如a := make([]int, 2, 4), 这里值得注意的是返回的切片a的总长度是4，预留的意思并不是另外多出来4的长度，其实是包含了前面2个已经切片的个数的。所以举个例子当你这样用的时候 a := make([]int, 4, 2)，就会报语法错误。

## build

go build -o 目标文件名 


## mod

更新

 go get -u xxx
 