# C5
## 5.1 程序转换概述
https://github.com/kechenkristin/csapp/blob/main/note/week5/slides/51.pdf

- 高级语言程序总是转换为机器代码才能在机器上执行
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/lantoas.png)

- 转换过程
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/compileprocess.png)

- 汇编指令
	- 编译
```
gcc -E test.c -o test.i
gcc -S test.i -o test.s
```
	- 反汇编
```
objdump -d test.o
```

- 两种目标文件
	- test.o: 可重定位目标文件(逻辑地址)
	- test: 可执行目标文件(真实地址)
	可执行文件的存储器映像

- ISA 
	- Instruction Set Architecture
	- Specification, 规定如何使用硬件
		- 指令格式 操作种类
		- 指令可以接受的操作数类型
		- 寄存器的名称、编号、长度、用途
		- 存储空间的大小和编址方式
		- 大端小端
		- 寻址方式
		- 程序计数器 条件码定义
	- relationship between ISA and MicroArchitecture(Organization)
	ISA是计算机组成的抽象

- Summary
	- 高级语言程序总是转换为机器代码才能在机器上执行  
	- 转换过程:预处理、编译、汇编、链接  
	- 机器代码是二进制代码,可DUMP为汇编代码表示  
	- ISA规定了一台机器的指令系统涉及到的所有方面  
	  	- 所有指令的指令格式、功能
		- 通用寄存器的个数、位数、编号和功能
		- 存储地址空间大小、编址方式、大/小端
		- 指令寻址方式


## 5.2

![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/address.png)
