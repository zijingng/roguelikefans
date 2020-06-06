---
typora-root-url: ..\..\static

title: "将 Visual Studio Code 的集成终端设置为 MSYS2"
date: 2020-06-03T23:23:40+08:00
author: ""
cover: ""
tags: ["VS Code", "MSYS2"]
keywords: []
description: ""
showFullContent: false
---
###### 1. 打开用户设置文件
- 点击Visual Studio Code左下角`管理`图标，点击`设置`，然后点击右上角`打开设置 (json)`。

- 或者使用快捷键 `Ctrl+Shift+P` 打开命令面板，搜索设置，选择`首选项: 打开设置 (json)`。
###### 2. 修改设置文件
添加以下配置：
```json
{
    // ...其他配置
    "terminal.integrated.shell.windows": "C:\\msys64\\usr\\bin\\bash.exe",
    "terminal.integrated.shellArgs.windows": [
        "--login",
    ],
    "terminal.integrated.env.windows": {
        "CHERE_INVOKING": "1",
        "MSYSTEM": "MINGW64",
    },
}
```