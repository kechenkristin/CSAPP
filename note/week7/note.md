## 过程调用的机器级表示

### 7.1 
https://github.com/kechenkristin/csapp/blob/main/note/week7/slides/nju/71.pdf
- PQ过程 

- IA-32 寄存器使用规定
	- 调用者保存寄存器: EAX EDX ECX
	- 被调用者保存寄存器: EBX ESI EDI
	- 帧指针寄存器(当前栈帧的底部): EBP
	- 栈指针寄存器(当前栈帧的顶部): ESP

- 过程调用过程中栈和栈帧的变化

- 可执行文件的存储器映像

- 过程(函数)的结构
	- 准备阶段
		- 形成帧底: push指令和move指令
		- 生成栈帧(若需要): sub指令或and指令
		- 保存现场(如果有被调用者保存寄存器): move指令
		- 每个过程开始的两条指令
```
pushl %ebp
movl %esp, %ebp
```
	- 过程(函数)体
		- 分配局部变量空间, 并赋值
		- 具体处理逻辑, 如果遇到函数调用时
			- 准备参数: 将实参送到栈帧入口参数处
				- 在被调用函数中，使用**R[ebp]+8, R[ebp]+12, R[ebp]+16**作为有效地址来访问函数的入口参数
			- CALL指令: 保存返回地址并转被调用函数
		- 在EAX中准备返回参数
	- 结束阶段
		- 退栈: leave指令 或 pop指令
		- 取返回地址返回: ret指令

- 过程调用参数传递举例
	- 按地址
	- 按值

- 递归
	

### 7.2 选择和循环结构的机器值表示
https://github.com/kechenkristin/csapp/blob/main/note/week7/slides/nju/72.pdf
- if-else
- switch-case
- for loop
```
for (init; test; update)
	body
```
===>
```
init;
while (test) {
	body
	update
}
```

