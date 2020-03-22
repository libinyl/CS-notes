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

- -v : 打印正在编译的包

## import path

假设模块 github.com/google/go-cmp 下有一个包 cmp,那么:

- module: github.com/google/go-cmp
- package: cmp
- 包的 import path: github.com/google/go-cmp/cmp
- 标准库里的包没有 import path

 contains a package in the directory cmp/. That package's import path is github.com/google/go-cmp/cmp. Packages in the standard library do not have a module path prefix.