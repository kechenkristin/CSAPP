### 3.7.1 真值与机器数

```c
#include "stdio.h"
void main( )
{
int ai = 100, bi = 2147483648, ci = -100;
unsigned au = 100, bu = 2147483648, cu = -100;
printf("ai=%d, bi=%d, ci=%d \n", ai, bi, ci);
printf("au=%u, bu=%u, cu=%u \n", au, bu, cu);
}
```
[!avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/w2p1.png)

- summary  
	- 带符号整数 : char、short、int、long  
		- 补码
	- 无符号整数：unsigned
		- binary
	- 浮点数 
		- IEEE754 (符号阶码尾数)

### 3.7.2 数据的宽度与存储
- 数据存储的宽度
[!avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/Cdata.png)

- 数据存储的排列方式(大小端)

- 数据存储的对齐方式

### 3.7.3 数据类型的转换
- 整数之间的数据类型转换
C语言中, 整数的赋值不是在真值上复制，而是在机器数上的赋值
设a有n位, b有m位, b = a
	- n = m 
	- n < m : 符号扩展或零扩展
	- n > m : 截断

- 整数与浮点数之间的转换

### 3.7.4 整数加减运算

### 3.7.5 浮点数的表示与运算(important 看slides)
