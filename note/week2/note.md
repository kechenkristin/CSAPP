## 2.1 数制与编码
https://github.com/kechenkristin/csapp/blob/main/note/week2/slides/21.pdf
- 转换的概念在数据表示中的反映

- 信息的二进制编码
	- 机器级数据
		- 数值数据: 无符号整数, 带符号整数, 浮点数(实数)
		- 非数值数据: 逻辑数(位串), 西文字符，汉字
	- 01
	- reasons using binary
	- 真值&机器数
		- 真值：真正的值
		- 机器数: 用0和1编码的计算机内部的01序列

- 数值数据的表示(important)
	- 进位计数制
		- decimal, binary, octal, hexadecimal
		- 相互转换
	- 定，浮点表示(小数点)
		- 定点整数, 定点小数
		- 浮点数
	- 定点数的编码(正负号)
		- 原码 补码 移码 反码	

- 进位计数制
	- 进制表示
		- decimal
		- binary
		- octal
		- hexadecimal
	- 相互转换
		- decimal <===> binary  
	8421
		- decimal <===> octal

## 2.2 定点数的编码表示
https://github.com/kechenkristin/csapp/blob/main/note/week2/slides/22.pdf
- 原码(Sign and Magnitude)
- 补码 
	- modular 运算
	- 2's complement  
https://inst.eecs.berkeley.edu/~cs61c/sp22/pdfs/lectures/lec01.pdf  

![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/Cdata.png)

- C语言支持的基本数据类型
	- 整数类型
		- Unsigned integer
		- Signed integer
	- 实数类型
		- 单精度浮点
		- 双精度浮点
		- 拓展精度浮点

## 2.3 C语言中的整数
- Unsigned Integer
	- 机器中字的位排列顺序有两种方式
		- LSB
		- MSB
	- 编码中没有符号位
- Signed Integer
	- 0-positive	1-negative
	- 三种定点编码方式
		- Signed and magnitude(原码)  
定点小数，用来表示浮点数的尾数
		- Excess(biased) notion(移码)
定点整数，用于表示浮点数的阶(指数)
		- Two's complement(补码)

## 2.4 浮点数的编码表示
- IEEE754
- 机器数 ===> 真值
- 真值  ===> 机器数
- Normalized numbers
- represent 0
- represent +/ ∞
- NaN(Not a Number)
- Denorms

## 2.5 非数值数据的编码表示
- 逻辑数据
- 西文字符(ASCII)
- 汉字及国际字符的编码表示

## 2.6 数据宽度和存储容量的单位
- 数据的基本宽度
	- bit: 处理，存储，传输信息的最小单位
	- Byte
		- 存储器按字节编址
		- 最小可寻址单位(addressable unit)
		- LSB MSB
	- word

- 数据量的度量单位
	- KB	1KB = 2^10 Byte = 1024B
	- MB	1MB = 2^20 Byte = 1024KB
	- GB	1GB = 2^30 Byte = 1024MB
	- TB	1TB = 2^40 Byte = 1024GB


