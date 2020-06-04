---
typora-root-url: ..\..\static

title: "在Windows下编译DCSS"
date: 2020-06-02T21:45:42+08:00
author: ""
cover: ""
tags: ["DCSS"]
keywords: []
description: "在Windows MSYS2环境下编译DCSS。"
showFullContent: false
---
###### 1. 下载安装MSYS2

   https://msys2.github.io/

   推荐安装64位MSYS2。

###### 2. 运行MSYS2 MinGW 64-bit

   *请不要运行MSYS2 MinGW 32-bit或MSYS2 MSYS。*

###### 3. 更新核心软件包

   在MSYS2 MinGW 64-bit命令行运行：

   ```bash/shell
   pacman -Syu
   ```

   安装完成后需要重启MSYS2命令行。

###### 4. 更新全部软件包

   ```bash/shell
   pacman -Su
   ```

###### 5. 安装git和基础开发软件包

   ```bash/shell
   pacman -S base-devel git
   ```

###### 6. 安装MinGW64编译工具链

   ```bash/shell
   pacman -S mingw-w64-x86_64-toolchain
   ```

   到这一步开发环境就建好了！

###### 7. 安装PyYAML

   ```bash/shell
   pacman -S mingw64/mingw-w64-x86_64-python3-pip
   pip install pyyaml
   ```

   或

   ```bash/shell
   pacman -S mingw-w64-x86_64-python3-yaml
   ```

###### 8. 克隆crawl源代码

   ```bash/shell
   cd ~
   
   git clone https://github.com/crawl/crawl.git
   
   cd crawl/crawl-ref/source
   
   git submodule update --init
   ```

###### 9. 编译crawl

   - 编译命令行版本：

      ```bash/shell
      make
      ```

   - 编译图形版本：

      ```bash/shell
      make TILES=y
      ```

   - 编译debug版本：

      在命令最后加入目标`debug`，例如：

      ```bash/shell
      make debug
      ```

   - 利用CPU多线程加速编译：

      ```bash/shell
      make -j [线程数]
      ```

###### 10. 运行crawl
   - 在文件管理器中`C:\msys64\home\用户名\crawl\crawl-ref\source`路径下双击`crawl.exe`即可运行。

   - 或者在MSYS2命令行中运行，命令行版本：

      ```sh
      start crawl
      ```

   - 图形版本：

      ```sh
      ./crawl.exe
      ```

