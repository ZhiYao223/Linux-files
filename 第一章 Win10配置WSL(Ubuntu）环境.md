# 第一章

## 一、WSL

- Windows Subsystem for Linux

1. 是用于Windows系统之上的Linux子系统，作用很简单，可以在Windows系统中获得Linux系统环境，并完全直连计算机硬件，无需通过虚拟机硬件。

2. 简而言之，Windows的WSL功能，可以无需单独虚拟一套硬件设备，就可以直接使用主机的物理硬件，构建Linux操作系统，并不会影响Windows系统本身的运行。

## 二、Linux目录结构

### 1. Linux路径的描述方式

- 在Linux系统中，路径之间的层级关系，使用‘ / ’来表示。
- 开头的‘ / ’表示根目录
- 后面的‘ / ’表示层级关系
- /usr/bin/test.txt

![image-20240417191102326](C:\Users\zhiyao\AppData\Roaming\Typora\typora-user-images\image-20240417191102326.png)

### 2. Windows路径的描述方式

- 在Windows系统中，路径之间的层级关系，使用‘ \ ’来表示。

- D: 表示D盘

- ‘ \ ’ 表示层级关系

- D:\software\vscode\test.txt

  ![image-20240417191035497](C:\Users\zhiyao\AppData\Roaming\Typora\typora-user-images\image-20240417191035497.png)

## 三、Linux命令入门

### 2.1 Linux命令基础

学习Linux，本质上是学习在命令行下熟练使用Linux的各类命令。

- 命令行：即Linux终端(Terminal)，是一种命令提示符页面。

- 命令：即Linux程序，一个命令就是一个Linux的程序。命令没有图形化页面，可以在命令行提供字符化的反馈。

  ![image-20240417192320415](C:\Users\zhiyao\AppData\Roaming\Typora\typora-user-images\image-20240417192320415.png)

### 2.2 ls命令入门

