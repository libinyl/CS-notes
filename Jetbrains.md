## 快捷键

功能 | 快捷键
---|----
查看宏替换的结果  | Ctrl + J
跳转到某文件 | Sft Cmd N
跳转到某符号 | Sft Opt Cmd Nq

## clion 

### debugger 显示数组内容

如 对于`int arr[]{1, 2, 3, 4, 5, 6};`

则需要在 watcher 里添加 `(int(*)[5])arr` 才能正常显示