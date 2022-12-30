## 10.1 可执行文件生成概述
- 程序的转换处理过程
	- 预处理
	- 编译
	- 汇编
	- 链接
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/compileprocess.png)

- 连接benifits
	- 模块化
	- 效率高

- 可执行文件的生成
	- 源程序文件分别转换(预处理，编译，汇编)
	- 可重定位目标文件(链接)
	- 可执行目标文件
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/link1.png)

- 连接过程的本质：可并相同的节
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/link2.png)

- 可执行文件的存储器映像
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/link3.png)


### 10.2 目标文件格式概述
- recap 源程序 ===> 可重定位目标文件 ===> 可执行目标文件

- 链接操作的步骤
	- 符号解析(Symbol resolution)
		- 程序中有定义和引用的符号(包括变量和函数等)
		- 编译器将定义的符号放在一个符号表(symbol table)中
		- 连接器将每个符号的引用都与一个确定的符号定义建立关联
	- 重定位
		- 合并相关.o 文件
		- 确定每个符号的地址
		- 在指令中填入新的地址

- 目标文件
	- type
		- 可重定位目标文件 .o
		- 可执行目标文件 a.out
		- 共享的目标文件 .so
	- cf 两种反汇编方式
```
objdump -d test.o	
```
地址从0开始

```
objdump -d test
```
地址为虚拟地址

	- 格式
		- Linux: ELF

### 10.3 ELF(Executable and Linkable Format)
- 链接视图（被链接）：可重定位目标文件 (Relocatable object files)

- 执行视图（被执行）：可执行目标文件（Executable object files）
