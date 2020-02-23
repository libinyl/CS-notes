## 命令解释

### go build
### go install
### go run

go 环境: https://howistart.org/posts/go/1/

## 代码组织

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