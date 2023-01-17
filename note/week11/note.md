## 11.1 符号及符号表
https://github.com/kechenkristin/csapp/blob/main/note/week11/slides/11.1.pdf

### recap: 链接操作的步骤

### 符号的定义和引用
- 局部变量分配在栈中, 不会在过程外被引用, 因此不是符号定义
- 符号定义
	- 指被分配了存储空间
	- 函数名：代码所在区
	- 变量名：静态数据区
- 定义符号的值：其目标所在的首地址

![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/w11p1.png)

### 链接符号的类型
- Global symbols
- External symbols
- Local symbols(static)

### 目标文件中的符号表
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/w11p2.png)

### 符号解析(Symbol Resolution)+
- 目的：将每个模块**引用的符号**与某个目标模块中的**定义符号**建立关联

- 全局符号的强弱 
	- 强符号：函数名和已初始化的全局变量名
	- 弱符号：未初始化的全局变量名

- 解析规则
	- Rule1: 强符号不能多次定义
	- Rule2: 一强一弱按强
	- Rule3: 多弱择其一

- examples(slides)

- 多重定义全局符号的问题
	- 尽量避免使用全局变量
	- 尽量使用本地变量(static)
	- 全局变量要赋初值
	- 外部全局变量使用extern

## 11.2 静态链接和符号解析
https://github.com/kechenkristin/csapp/blob/main/note/week11/slides/11.2.pdf

### 静态链接对象
静态链接对象 = 多个可重定位目标模块(.o文件) + 静态库(标准库、自定义库) (.a文件，其中包含多个.o模块)

### 静态库
- 常用静态库
	- libc.a
	- libm.a

- 静态库的创建
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/w11p3.png)

![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/w11p4.png)

### 链接器中符号解析的全过程(important, slides)
**UDE**

### 链接顺序问题(slide)
