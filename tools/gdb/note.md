## GDB

### man gdb
Here are some of the most frequently needed GDB commands:

       break [file:][function|line]
           Set a breakpoint at function or line (in file).

       run [arglist]
           Start your program (with arglist, if specified).

       bt  Backtrace: display the program stack.

       print expr
           Display the value of an expression.

       c   Continue running your program (after stopping, e.g. at a
           breakpoint).

       next
           Execute next program line (after stopping); step over any function
           calls in the line.

       edit [file:]function
           look at the program line where it is presently stopped.

       list [file:]function
           type the text of the program in the vicinity of where it is
           presently stopped.

       step
           Execute next program line (after stopping); step into any function
           calls in the line.

       help [name]
           Show information about GDB command name, or general information
           about using GDB.

       quit
       exit
           Exit from GDB.

       For full details on GDB, see Using GDB: A Guide to the GNU Source-Level
       Debugger, by Richard M. Stallman and Roland H. Pesch.  The same text is
       available online as the "gdb" entry in the "info" program.


### codes
```c
#include<stdio.h>

int main() {
        int arr[4] = {1, 2, 3, 4};
        int i = 0;
        for (i = 0; i < 4; i++) {
                printf("%d\n", arr[i]);
        }       
        return 0;
}
```

### gdb pratical
#### basic usage(run and quit)
- step1 compile(gcc)
> gcc -g
-g 参数代表可以调试

- step2 启动gdb调试工具，加载要执行的目标文件
// 启动gdb 调试工具，并加载程序
> gdb 可执行目标文件  

or 
> gdb  
> file 可执行的目标文件

- step3 设置断点
// 在main函数入口处设置断点
> break main
or  
> b main  

// 在源程序test.c的第三行处设置断点
> break test.c:3
or 
> b main

- step4 启动程序运行
// 程序会在断点处停下
> run	

- step5 查看程序运行时的当前状态
> p

- 退出gdb
> quit

```
(gdb) list
1	#include<stdio.h>
2	
3	int main() {
4		int arr[4] = {1, 2, 3, 4};
5		int i = 0;
6		for (i = 0; i < 4; i++) {
7			printf("%d\n", arr[i]);
8		}
9		return 0;
10	}
(gdb) b main
Breakpoint 1 at 0x1175: file test.c, line 3.
(gdb) b 4
Breakpoint 2 at 0x1184: file test.c, line 4.
(gdb) info b
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x0000000000001175 in main at test.c:3
2       breakpoint     keep y   0x0000000000001184 in main at test.c:4
(gdb) r
Starting program: /home/kristin/study/csapp/tools/gdb/pratical/a.out 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, main () at test.c:3
3	int main() {
(gdb) n

Breakpoint 2, main () at test.c:4
4		int arr[4] = {1, 2, 3, 4};
(gdb) p &arr[0]
$2 = (int *) 0x7fffffffdf10
(gdb) p &arr[1]
$3 = (int *) 0x7fffffffdf14
```
