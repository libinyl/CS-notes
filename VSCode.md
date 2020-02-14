## 通用设置
```json
{
    "workbench.colorTheme": "Visual Studio Light",
    "workbench.startupEditor": "newUntitledFile",
    "window.zoomLevel": -1,
    "git.autofetch": true,
    "files.autoSave": "afterDelay",
    "explorer.openEditors.visible": 0,
    "editor.fontSize": 16,
    "editor.renderControlCharacters": true,
    "editor.showFoldingControls": "always",
    "editor.minimap.enabled": false,
    "workbench.useExperimentalGridLayout": true,
    "workbench.sideBar.location": "right",
    "workbench.tree.indent": 20,
    "workbench.editor.closeOnFileDelete": true,
    "workbench.editor.highlightModifiedTabs": true
}
```


## C++

{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "${workspaceFolder}/include",
                ..
            ],
            "defines": [],
            "compilerPath": "/opt/rh/devtoolset-2/root/usr/bin/gcc",
            "cStandard": "c11",
            "cppStandard": "c++14",
            "intelliSenseMode": "clang-x64"
        }
    ],
    "version": 4
}


includePath: 设定为 makefile 里的-I
browsepath: 

https://code.visualstudio.com/docs/cpp/faq-cpp

## 快捷键

功能 | 按键
---|---
显示侧边栏 | Cmd B
跳转到符号 | Cmd T
新建窗口   | sft Cmd N
折叠代码块

## 路径配置

