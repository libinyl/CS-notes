## Go 的内置类型和内置函数有哪些?

参考: https://golang.org/pkg/builtin/

## go 的工程环境及常用变量

参考 https://www.programming-books.io/essential/go/gopath-goroot-gobin-d6da4b8481f94757bae43be1fdfa9e73

- 查看当前 go 变量:`go env`
- `go get`命令会把下载的包放置在`GOPATH`下.
- `GOROOT`即 go 的安装位置,go标准库位于此,通常无需改变
- `GOPATH`: go工程根目录的集合.我认为应当每次构建的时候手动 export,如`export GOPATH=~/goyard/calcproj`

## 语法简记

数组声明

