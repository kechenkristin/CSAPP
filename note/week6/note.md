## C6

### 程序由指令序列组成
- 指令如何执行
	- 根据EIP取指令
	- 指令译码
	- 取操作数
	- 指令执行
	- 回写结果
	- 修改EIP的值	

### 6.1 传送指令
https://github.com/kechenkristin/csapp/blob/main/note/week6/slides/nju/61.pdf
- 通用数据传送指令
	- mov 一般传送
	- push/pop 出栈/入栈
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/push.png)
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/pop.png)
- 地址传送指令
		- lea
- 输入输出指令 in/out
- 标志传送指令

### 6.2 定点算术运算指令
https://github.com/kechenkristin/csapp/blob/main/note/week6/slides/nju/62.pdf
- 加减运算 add/sub
- 增1/减1 inc/dec
- 取负运算 neg
- 比较运算 cmp
- 乘除运算 mul/div

### 6.3 按位运算指令
https://github.com/kechenkristin/csapp/blob/main/note/week6/slides/nju/63.pdf
- 逻辑运算
	- not 非
	- and 与
	- or 或
	- xor 异或
	- test  与操作测试，仅影响标志
- 移位运算
	- shl/shr 逻辑左/右移
	- sal/sar 算术左/右移
	- ps. 逻辑 vs 算术移位  
https://blog.csdn.net/zzldm/article/details/53410280#:~:text=%E9%80%BB%E8%BE%91%E5%8F%B3%E7%A7%BB%E5%B0%B1%E6%98%AF%E4%B8%8D,2%E7%9A%84n%E6%AC%A1%E6%96%B9%E3%80%82  
	- 按位运算指令举例
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/example.png)

- 浮点处理指令(了解) 6.5
https://github.com/kechenkristin/csapp/blob/main/note/week6/slides/nju/65.pdf
- MMX及SSE指令(了解) 6.6
https://github.com/kechenkristin/csapp/blob/main/note/week6/slides/nju/66.pdf
