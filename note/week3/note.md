## 3.1 数字逻辑电路基础
https://inst.eecs.berkeley.edu/~cs61a/fa20/assets/slides/14-Circuits_full.pdf  
https://github.com/kechenkristin/csapp/blob/main/note/week3/slides/31.pdf  
- 布尔代数
	- 与 或 非
	- 真值表
- 逻辑门电路 
	- 一位/n位 逻辑门电路
	- 组合/时序逻辑电路（根据电路是否具有存储功能） 
	- 功能部件
		- 一些具有特定功能的组合逻辑部件
		- 译码器、编码器、多路选择器、加法器
		- 实现过程
			- 用一个真值表描述功能部件的输入和输出关系
			- 根据真值表确定逻辑表达式
			- 根据逻辑表达式实现逻辑电路
- 多路选择器
- 一位加法器
- n位加法器
- n位带标志加法器
- n位整数加/减运算器
- 算术逻辑部件(ALU)
	- **基本**算术运算&逻辑运算
	-  核心电路: **带标志加法器**
	- 输出: 和/差 & 标志信息
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/ALU.png)

## 3.2 从C表达式到逻辑电路
https://github.com/kechenkristin/csapp/blob/main/note/week3/slides/32.pdf
- C语言程序中的基本数据类型、基本运算类型
	- 基本数据类型
		- 无符号数(二进制位串) 带符号整数(补码)
		- 浮点数(IEEE 754标准)
		- 位串、字符串(ASCII码)
	- 基本运算类型
		- 算术(+ - * / % > < >= <= == !=)
		- 按位(| & ~ ^)
		- 逻辑(|| && !)
		- 移位(<< >>)
		- 拓展和截断
- 高级语言程序中的运算
	- 表达式 ===> 执行指令 ===> 运算电路
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/arthemetic.png)

## 3.3 C语言中的各类运算
https://github.com/kechenkristin/csapp/blob/main/note/week3/slides/33.pdf  
- 算术运算
	- 无符号数、带符号整数、浮点数的+ - * / %
- 按位运算
	- 用途: 掩码
	- 操作: | & ~ ^ 
	- 实例: 从数据y中提取低位字节, 并使高字节为0 ===> &
- 移位运算
	- 用途	
		- 提取部分信息
		- 扩大/缩小248倍
	- 操作
		- 
