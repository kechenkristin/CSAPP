## note
### 8.1 数组和指针类型的分配和访问
https://github.com/kechenkristin/csapp/blob/main/note/week8/slides/nju/81.pdf
- 数组元素在内存的存放和访问
	- eg short A[4]
	- 第i(0<=i<=3)个元素的地址计算公式**&A[0] + 2 * i**
	- 汇编指令 **movw(%edx, %ecx, 2), %ax**
		- 其中，ecx 为**变址(索引)寄存器**, 在循环体中增量
- 表格
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/Cdata.png)
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/arrayaddress2.png)
- 静态区
	- 可执行目标文件的数据段
	- 注意linux是小端对齐(详见实例)
- auto型
	- 栈
- 数组与指针
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/arrayaddress.png)
- 指针数组与多维数组
- 实例
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/arrayElement.png)

### 8.2 结构和联合数据类型的分配与访问 
https://github.com/kechenkristin/csapp/blob/main/note/week8/slides/nju/82.pdf
- 结构体
	- 结构体成员在内存的存放和访问 
		- 栈中的auto  ebp和esp定位
		- 静态区首地址是一个确定的静态区地址
		- 基址加偏移量
	- 作为入口参数
		- 按值传递
		- 按地址传递
- 联合体数据
	- 联合体各成员共享存储空间, 按最大长度成员所需空间大小为目标
	- 可实现对相同位序列进行不同数据类型的解释
	- 利用嵌套可定义链表结构
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/union.png)

### 8.3 数据的对齐存放 
https://github.com/kechenkristin/csapp/blob/main/note/week8/slides/nju/83.pdf
- Alignment
- 对齐方式的设定
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/unionexample1.png)
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/unionexample2.png)
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/unionexample3.png)

### 8.4 越界访问和缓冲区溢出攻击
https://github.com/kechenkristin/csapp/blob/main/note/week8/slides/nju/84.pdf  

https://www.cs.cmu.edu/afs/cs/academic/class/15213-f15/www/lectures/09-machine-advanced.pdf  

- 缓冲区溢出
	- 概念：数组存储区可看成一个缓冲区, 超越数组存储区的写入操作称为缓冲区溢出 
	- 原因：没有对栈中作为缓冲区的数组的访问进行越界检查
- 防范
	- Avoid overflow vulnerabilities in code
		- **fgets** instead of **gets**
		- **strncpy** instead of **strcpy**
		- don't use **scanf** with %s 
	- System Level Protections
		- Randomized stack offsets
		- Nonexecutable code segments
	- Stack Canaries can help(very safe)
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/canary1.png)
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/canary2.png)

- Return-Oriented Programming
