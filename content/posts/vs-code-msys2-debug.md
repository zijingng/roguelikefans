---
typora-root-url: ..\..\static

title: "Visual Studio Code 集成 MSYS2 make 和 gdb"
date: 2020-06-06T11:10:04+08:00
author: ""
cover: ""
tags: ["VS Code", "MSYS2", "DCSS"]
keywords: []
description: " "
showFullContent: false
---
###### 在Visual Studio Code中配置 MSYS2 make 任务
- 按照[将 Visual Studio Code 的集成终端设置为 MSYS2](/posts/vs-code-msys2)设置 VS Code 终端。
- 如果你运行 `make` 的工作区文件夹下没有 `.vscode/tasks.json` 文件，新建一个这样的文件。
- 在 `.vscode/tasks.json` 文件中加入配置，以 DCSS `debug` 为例：
```json
{
    "version": "2.0.0",
    "tasks": [
        // ...其他任务
        {
            "type": "shell",
            "label": "make debug -j12 TILES=y",
            "command": "make",
            "args": [
                "debug",
                "-j12",
                "TILES=y"
            ],
            "options": {
                "cwd": "crawl-ref/source",
            },
            "problemMatcher": {
                "base": "$gcc",
                "fileLocation": ["relative", "${workspaceRoot}/crawl-ref/source"]
            },
            "group": "build"
        },
    ]
}
```
- 使用快捷键 `Ctrl+Shift+B` 或点击菜单栏 `终端 - 运行任务...` 运行 `make debug -j12 TILES=y` 任务。
###### 在 Visual Studio Code 中配置 MSYS2 gdb 调试
- 使用快捷键 `Ctrl+Shift+X` 或点击左侧扩展图标打开扩展界面，搜索和安装 `C/C++` 扩展。
- 如果你运行 `gdb` 调试的工作区文件夹下没有 `.vscode/launch.json` 文件，新建一个这样的文件。
- 在 `.vscode/launch.json` 文件中加入配置，以 DCSS `debug` 为例：
```json
{
    "version": "0.2.0",
    "configurations": [
        // ...其他配置
        {
            "name": "(gdb) Windows 上的 Bash 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceRoot}/crawl-ref/source/crawl.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceRoot}/crawl-ref/source/",
            "environment": [],
            "externalConsole": false,
            "pipeTransport": {
                "debuggerPath": "/usr/bin/gdb",
                "pipeProgram": "C:\\msys64\\usr\\bin\\bash.exe",
                "pipeArgs": ["-c"],
                "pipeCwd": ""
            },
            "sourceFileMap": {
                "/home/用户名/crawl": "${workspaceRoot}"
            },
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            // 如果要先编译再调试, 加入:  
            // "preLaunchTask": "make debug -j12 TILES=y"
        }
    ]
}
```
- 使用快捷键 `F5` 或点击菜单栏`运行 - 启动调试`开始调试。