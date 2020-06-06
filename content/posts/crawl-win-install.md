---
typora-root-url: ..\..\static

title: "在Windows下编译DCSS"
date: 2020-06-02T21:45:42+08:00
author: ""
cover: ""
tags: ["DCSS", "MSYS2"]
keywords: []
description: "在 Windows MSYS2 环境下编译 DCSS。"
showFullContent: false
---
###### 1. 下载安装 MSYS2

   https://msys2.github.io/

   推荐安装64位 MSYS2。

###### 2. 运行 MSYS2 MinGW 64-bit

   *请不要运行 MSYS2 MinGW 32-bit 或 MSYS2 MSYS。*

###### 3. 更新核心软件包

   在 MSYS2 MinGW 64-bit 命令行运行：

   ```bash/shell
   pacman -Syu
   ```

   安装完成后需要重启 MSYS2 命令行。

###### 4. 更新全部软件包

   ```bash/shell
   pacman -Su
   ```

###### 5. 安装 git 和基础开发软件包

   ```bash/shell
   pacman -S base-devel git
   ```

###### 6. 安装 MinGW64 编译工具链

   ```bash/shell
   pacman -S mingw-w64-x86_64-toolchain
   ```

   到这一步开发环境就建好了！

###### 7. 安装 PyYAML

   ```bash/shell
   pacman -S mingw64/mingw-w64-x86_64-python3-pip
   pip install pyyaml
   ```

   或

   ```bash/shell
   pacman -S mingw-w64-x86_64-python3-yaml
   ```

###### 8. 克隆 crawl 源代码

   ```bash/shell
   cd ~
   
   git clone https://github.com/crawl/crawl.git
   
   cd crawl/crawl-ref/source
   
   git submodule update --init
   ```

###### 9. 编译 crawl

   - 编译命令行版本：

      ```bash/shell
      make
      ```

   - 编译图形版本：

      ```bash/shell
      make TILES=y
      ```

   - 编译 debug 版本：

      在命令最后加入目标 `debug`，例如：

      ```bash/shell
      make debug
      ```

   - 利用 CPU 多线程加速编译：

      ```bash/shell
      make -j [线程数]
      ```

###### 10. 运行 crawl
   - 在文件管理器中 `C:\msys64\home\用户名\crawl\crawl-ref\source` 路径下双击 `crawl.exe` 即可运行。

   - 或者在 MSYS2 命令行中运行，命令行版本：

      ```sh
      start crawl
      ```

   - 图形版本：

      ```sh
      ./crawl.exe
      ```

