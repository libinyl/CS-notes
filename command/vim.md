## 跳转到第 50 行
```
:50
```

## 复制粘贴
```
yy  复制
p   粘贴
```

## 删除全文

```
光标位于首行首列,dG
```

## 搜索

## vimrc

```
set nu
set mouse=a
set tabstop=4
set cursorline
syntax enable
set completeopt=longest,menu
set laststatus=2
```

- 竖直分屏 :vs [filename]
- 分屏跳转 ctrl w hjkl
- 退出分屏 quit
- 执行外部命令 :! gcc
- 打开终端 :term
- 关闭中断 :q
- 调整窗口大小 ctrl w +/-数字
- 关闭窗口  ctrl w c
- 剪切一行 dd
- 复制一行 yy
- 刷新 :e
- 切换到浏览模式 :Ex
- 浏览模式下创建新文件 %
- 浏览模式下创建新目录 d
- 折叠代码 zc
- 缩进

## 格式化代码

- 按两下小写g，即gg，定位光标到第一行。 
- 按住Shift+v，即大写V，进入可视化编辑的列编辑模式。 
- Shift+g，即大写G，选中整个代码。 
- 按下等号=，格式化所有代码。

vim - 的意思:

## 找不到折叠

 set fdm=indent