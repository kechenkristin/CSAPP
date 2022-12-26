## code
```c
#include <stdio.h>
#include <stdlib.h>
#include "support.h"
#include "phases.h"

/* 
 * Note to self: Remember to erase this file so my victims will have no
 * idea what is going on, and so they will all blow up in a
 * spectaculary fiendish explosion. -- Dr. Evil 
 */

FILE *infile;

int main(int argc, char *argv[])
{
    char *input;

    /* Note to self: remember to port this bomb to Windows and put a 
     * fantastic GUI on it. */

    /* When run with no arguments, the bomb reads its input lines 
     * from standard input. */
    if (argc == 1) {
        infile = stdin;
    }

    /* When run with one argument <file>, the bomb reads from <file> 
     * until EOF, and then switches to standard input. Thus, as you 
     * defuse each phase, you can add its defusing string to <file> and
     * avoid having to retype it. */
    else if (argc == 2) {
        if (!(infile = fopen(argv[1], "r"))) {
            printf("%s: Error: Couldn't open %s\n", argv[0], argv[1]);
            exit(8);
        }
    }

    /* You can't call the bomb with more than 1 command line argument. */
    else {
        printf("Usage: %s [<input_file>]\n", argv[0]);
        exit(8);
    }
/* Do all sorts of secret stuff that makes the bomb harder to defuse. */
    initialize_bomb();

    printf("Welcome to my fiendish little bomb. You have 6 phases with\n");
    printf("which to blow yourself up. Have a nice day!\n");

    /* Hmm...  Six phases must be more secure than one phase! */
    input = read_line();             /* Get input                   */
    phase_1(input);                  /* Run the phase               */
    phase_defused();                 /* Drat!  They figured it out!
                                      * Let me know how they did it. */
    printf("Phase 1 defused. How about the next one?\n");

    /* The second phase is harder.  No one will ever figure out
     * how to defuse this... */
    input = read_line();
    phase_2(input);
    phase_defused();
    printf("That's number 2.  Keep going!\n");

    /* I guess this is too easy so far.  Some more complex code will
     * confuse people. */
    input = read_line();
    phase_3(input);
    phase_defused();
    printf("Halfway there!\n");

    /* Oh yeah?  Well, how good is your math?  Try on this saucy problem! */
    input = read_line();
    phase_4(input);
    phase_defused();
    printf("So you got that one.  Try this one.\n");

    /* Round and 'round in memory we go, where we stop, the bomb blows! */
    input = read_line();
    phase_5(input);
    phase_defused();
    printf("Good work!  On to the next...\n");

    /* This phase will never be used, since no one will get past the
     * earlier ones.  But just in case, make this one extra hard. */
    input = read_line();
    phase_6(input);
    phase_defused();
    /* Wow, they got it!  But isn't something... missing?  Perhaps
     * something they overlooked?  Mua ha ha ha ha! */

    return 0;
}
```

## exercise

> objdump -S bomb  
> (gdb) disas function_name

### phase_1

#### code
##### phase_1
```asm
0000000000400ee0 <phase_1>:
  400ee0:	48 83 ec 08          	sub    $0x8,%rsp	// 设置栈帧
  400ee4:	be 00 24 40 00       	mov    $0x402400,%esi	// 将立即数$0x402400存入%esi寄存器
  400ee9:	e8 4a 04 00 00       	call   401338 <strings_not_equal>	// 调用string_not_equal函数
  400eee:	85 c0                	test   %eax,%eax
  400ef0:	74 05                	je     400ef7 <phase_1+0x17>		// 400ee0 + 0x17 = 400ef7
  400ef2:	e8 43 05 00 00       	call   40143a <explode_bomb>
  400ef7:	48 83 c4 08          	add    $0x8,%rsp
  400efb:	c3                   	ret  
```

##### string_not_equal
```asm
0000000000401338 <strings_not_equal>:
  401338:	41 54                	push   %r12
  40133a:	55                   	push   %rbp
  40133b:	53                   	push   %rbx
  40133c:	48 89 fb             	mov    %rdi,%rbx
  40133f:	48 89 f5             	mov    %rsi,%rbp
  401342:	e8 d4 ff ff ff       	call   40131b <string_length>
  401347:	41 89 c4             	mov    %eax,%r12d
  40134a:	48 89 ef             	mov    %rbp,%rdi
  40134d:	e8 c9 ff ff ff       	call   40131b <string_length>
```

##### string_length
```asm
000000000040131b <string_length>:
  40131b:	80 3f 00             	cmpb   $0x0,(%rdi)
  40131e:	74 12                	je     401332 <string_length+0x17>
  401320:	48 89 fa             	mov    %rdi,%rdx
  401323:	48 83 c2 01          	add    $0x1,%rdx
  401327:	89 d0                	mov    %edx,%eax
  401329:	29 f8                	sub    %edi,%eax
  40132b:	80 3a 00             	cmpb   $0x0,(%rdx)
  40132e:	75 f3                	jne    401323 <string_length+0x8>
  401330:	f3 c3                	repz ret 
  401332:	b8 00 00 00 00       	mov    $0x0,%eax
  401337:	c3                   	ret  
```

```
(gdb) x/s 0x402400
0x402400:	"Border relations with Canada have never been better."
```

### phase_2
#### codes

##### read_six_numbers
> (gdb) disas read_six_numbers
```asm
Dump of assembler code for function read_six_numbers:
   0x000000000040145c <+0>:	sub    $0x18,%rsp
   0x0000000000401460 <+4>:	mov    %rsi,%rdx
   0x0000000000401463 <+7>:	lea    0x4(%rsi),%rcx
   0x0000000000401467 <+11>:	lea    0x14(%rsi),%rax
   0x000000000040146b <+15>:	mov    %rax,0x8(%rsp)
   0x0000000000401470 <+20>:	lea    0x10(%rsi),%rax
   0x0000000000401474 <+24>:	mov    %rax,(%rsp)
   0x0000000000401478 <+28>:	lea    0xc(%rsi),%r9
   0x000000000040147c <+32>:	lea    0x8(%rsi),%r8
   0x0000000000401480 <+36>:	mov    $0x4025c3,%esi
   0x0000000000401485 <+41>:	mov    $0x0,%eax
   0x000000000040148a <+46>:	call   0x400bf0 <__isoc99_sscanf@plt>
   0x000000000040148f <+51>:	cmp    $0x5,%eax
   0x0000000000401492 <+54>:	jg     0x401499 <read_six_numbers+61>
   0x0000000000401494 <+56>:	call   0x40143a <explode_bomb>
   0x0000000000401499 <+61>:	add    $0x18,%rsp
   0x000000000040149d <+65>:	ret    
End of assembler dump.
```
##### phase_2

> (gdb) disas phase_2

```asm
Dump of assembler code for function phase_2:
   0x0000000000400efc <+0>:	push   %rbp
   0x0000000000400efd <+1>:	push   %rbx
   0x0000000000400efe <+2>:	sub    $0x28,%rsp
   0x0000000000400f02 <+6>:	mov    %rsp,%rsi
   0x0000000000400f05 <+9>:	call   0x40145c <read_six_numbers>
   0x0000000000400f0a <+14>:	cmpl   $0x1,(%rsp)
   0x0000000000400f0e <+18>:	je     0x400f30 <phase_2+52>
   0x0000000000400f10 <+20>:	call   0x40143a <explode_bomb>
   0x0000000000400f15 <+25>:	jmp    0x400f30 <phase_2+52>
   0x0000000000400f17 <+27>:	mov    -0x4(%rbx),%eax
   0x0000000000400f1a <+30>:	add    %eax,%eax
   0x0000000000400f1c <+32>:	cmp    %eax,(%rbx)
   0x0000000000400f1e <+34>:	je     0x400f25 <phase_2+41>
   0x0000000000400f20 <+36>:	call   0x40143a <explode_bomb>
   0x0000000000400f25 <+41>:	add    $0x4,%rbx
   0x0000000000400f29 <+45>:	cmp    %rbp,%rbx
   0x0000000000400f2c <+48>:	jne    0x400f17 <phase_2+27>
   0x0000000000400f2e <+50>:	jmp    0x400f3c <phase_2+64>
   0x0000000000400f30 <+52>:	lea    0x4(%rsp),%rbx
   0x0000000000400f35 <+57>:	lea    0x18(%rsp),%rbp
   0x0000000000400f3a <+62>:	jmp    0x400f17 <phase_2+27>
   0x0000000000400f3c <+64>:	add    $0x28,%rsp
   0x0000000000400f40 <+68>:	pop    %rbx
   0x0000000000400f41 <+69>:	pop    %rbp
   0x0000000000400f42 <+70>:	ret    
End of assembler dump.
```

#### log
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/lab2p2.png)
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/lab2p32.png)
1. 准备栈帧
2. 调用read_six_number函数,注意参数的摆放位置  
	- R[rsp] arg1, R[rsp]+4 arg2, R[rsp]+8 arg3 etc
3. 易知第一个参数是1
4. R[rbx]存放下一个参数的值, R[rbp]存放跳出循环的临界值 
5. (important), 该处就是更新的核心逻辑, 2*上一个参数
	

#### ans
1, 2, 4, 8, 16, 32

### phase_3
#### res
- 一些用到的gdb指令

运行单条机器指令
> (gdb) stepi

在单条机器指令处打断点
```
(gdb) b *(xxxxxxx)
```

打断正在执行的函数
> (gdb) finish

查看某个立即数
> (gdb) p 0x111

- imgs
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/switch.png)

![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/arguments.png)

![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/lab2p31.png)



#### codes
```asm
Dump of assembler code for function phase_3:
   0x0000000000400f43 <+0>:	sub    $0x18,%rsp
   0x0000000000400f47 <+4>:	lea    0xc(%rsp),%rcx
   0x0000000000400f4c <+9>:	lea    0x8(%rsp),%rdx
   0x0000000000400f51 <+14>:	mov    $0x4025cf,%esi
   0x0000000000400f56 <+19>:	mov    $0x0,%eax
   0x0000000000400f5b <+24>:	call   0x400bf0 <__isoc99_sscanf@plt>
   0x0000000000400f60 <+29>:	cmp    $0x1,%eax
   0x0000000000400f63 <+32>:	jg     0x400f6a <phase_3+39>
   0x0000000000400f65 <+34>:	call   0x40143a <explode_bomb>
   0x0000000000400f6a <+39>:	cmpl   $0x7,0x8(%rsp)
   0x0000000000400f6f <+44>:	ja     0x400fad <phase_3+106>
   0x0000000000400f71 <+46>:	mov    0x8(%rsp),%eax
   0x0000000000400f75 <+50>:	jmp    *0x402470(,%rax,8)
   0x0000000000400f7c <+57>:	mov    $0xcf,%eax
   0x0000000000400f81 <+62>:	jmp    0x400fbe <phase_3+123>
   0x0000000000400f83 <+64>:	mov    $0x2c3,%eax
   0x0000000000400f88 <+69>:	jmp    0x400fbe <phase_3+123>
   0x0000000000400f8a <+71>:	mov    $0x100,%eax
   0x0000000000400f8f <+76>:	jmp    0x400fbe <phase_3+123>
   0x0000000000400f91 <+78>:	mov    $0x185,%eax
   0x0000000000400f96 <+83>:	jmp    0x400fbe <phase_3+123>
   0x0000000000400f98 <+85>:	mov    $0xce,%eax
   0x0000000000400f9d <+90>:	jmp    0x400fbe <phase_3+123>
   0x0000000000400f9f <+92>:	mov    $0x2aa,%eax
   0x0000000000400fa4 <+97>:	jmp    0x400fbe <phase_3+123>
   0x0000000000400fa6 <+99>:	mov    $0x147,%eax
   0x0000000000400fab <+104>:	jmp    0x400fbe <phase_3+123>
   0x0000000000400fad <+106>:	call   0x40143a <explode_bomb>
   0x0000000000400fb2 <+111>:	mov    $0x0,%eax
   0x0000000000400fb7 <+116>:	jmp    0x400fbe <phase_3+123>
   0x0000000000400fb9 <+118>:	mov    $0x137,%eax
   0x0000000000400fbe <+123>:	cmp    0xc(%rsp),%eax
   0x0000000000400fc2 <+127>:	je     0x400fc9 <phase_3+134>
   0x0000000000400fc4 <+129>:	call   0x40143a <explode_bomb>
   0x0000000000400fc9 <+134>:	add    $0x18,%rsp
   0x0000000000400fcd <+138>:	ret    
End of assembler dump.
```

#### log

```shell
kristin@kristin-PC:~/study/csapp/labs/bomblab/bomb$ cat ans.txt 
Border relations with Canada have never been better.
1 2 4 8 16 32
test
```

```shell
(gdb) b phase_3
Breakpoint 1 at 0x400f43
(gdb) run ans.txt 
Starting program: /home/kristin/study/csapp/labs/bomblab/bomb/bomb ans.txt
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
Welcome to my fiendish little bomb. You have 6 phases with
which to blow yourself up. Have a nice day!
Phase 1 defused. How about the next one?
That's number 2.  Keep going!

Breakpoint 1, 0x0000000000400f43 in phase_3 ()
(gdb) stepi
0x0000000000400f47 in phase_3 ()
(gdb) 
0x0000000000400f4c in phase_3 ()
(gdb) 
0x0000000000400f51 in phase_3 ()
(gdb) 
0x0000000000400f56 in phase_3 ()
(gdb) 
0x0000000000400f5b in phase_3 ()
(gdb) 
0x0000000000400bf0 in __isoc99_sscanf@plt ()
(gdb) 
__GI___isoc99_sscanf (s=0x603820 <input_strings+160> "test", format=0x4025cf "%d %d") at ./stdio-common/isoc99_sscanf.c:24
24	./stdio-common/isoc99_sscanf.c: No such file or directory.
(gdb) 
0x00007ffff7de42d4	24	in ./stdio-common/isoc99_sscanf.c
(gdb) finish
Run till exit from #0  0x00007ffff7de42d4 in __GI___isoc99_sscanf (
    s=0x603820 <input_strings+160> "test", format=0x4025cf "%d %d")
    at ./stdio-common/isoc99_sscanf.c:24
0x0000000000400f60 in phase_3 ()
Value returned is $1 = 0
```

根据1及 gdb format=0x4025cf "%d %d" 可知，该 phase需要两个int  
根据参数的入口地址相关知识可知, 第一个参数存放在0x8(%rsp), 第二个参数存放在0xc(%rsp)  
根据2可知，第一个参数在1和7之间(1, 7)  
更改ans.txt  

```shell
kristin@kristin-PC:~/study/csapp/labs/bomblab/bomb$ cat ans.txt 
Border relations with Canada have never been better.
1 2 4 8 16 32
2 999
```

根据3及多个跳转指令可知，这是一个swithch-case结构, 根据第一个参数的值对第二个参数会有不同的指派  

- 当第一个参数为2时
```shell
(gdb) b *0x0000000000400f75
Breakpoint 1 at 0x400f75
(gdb) r ans.txt 
Starting program: /home/kristin/study/csapp/labs/bomblab/bomb/bomb ans.txt
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
Welcome to my fiendish little bomb. You have 6 phases with
which to blow yourself up. Have a nice day!
Phase 1 defused. How about the next one?
That's number 2.  Keep going!

Breakpoint 1, 0x0000000000400f75 in phase_3 ()
(gdb) stepi
0x0000000000400f83 in phase_3 ()	
// 0x0000000000400f83 <+64>:    mov    $0x2c3,%eax
(gdb) p 0x2c3
$1 = 707
```

- 当第一个参数为3时
```shell
Breakpoint 1, 0x0000000000400f75 in phase_3 ()
(gdb) stepi
0x0000000000400f8a in phase_3 ()	
//  0x0000000000400f8a <+71>:    mov    $0x100,%eax
(gdb) p 0x100
$1 = 256
```

- ps registers
	- eax/rax: 0<+19> ===> first arg<+46> ===> 根据第一个参数所赋的第二个参数的值<+57 ~ +118>
	- 0x8(%rsp): first arg
	- 0xc(%rsp): second arg

### phase_4
#### code
```asm
(gdb) disas phase_4
Dump of assembler code for function phase_4:
   0x000000000040100c <+0>:	sub    $0x18,%rsp
   0x0000000000401010 <+4>:	lea    0xc(%rsp),%rcx
   0x0000000000401015 <+9>:	lea    0x8(%rsp),%rdx
   0x000000000040101a <+14>:	mov    $0x4025cf,%esi
   0x000000000040101f <+19>:	mov    $0x0,%eax
   0x0000000000401024 <+24>:	call   0x400bf0 <__isoc99_sscanf@plt>
   0x0000000000401029 <+29>:	cmp    $0x2,%eax
   0x000000000040102c <+32>:	jne    0x401035 <phase_4+41>
   0x000000000040102e <+34>:	cmpl   $0xe,0x8(%rsp)
   0x0000000000401033 <+39>:	jbe    0x40103a <phase_4+46>
   0x0000000000401035 <+41>:	call   0x40143a <explode_bomb>
   0x000000000040103a <+46>:	mov    $0xe,%edx	// R[edx] = $0xe = 14
   0x000000000040103f <+51>:	mov    $0x0,%esi	// R[esi] = $0x0 = 0
   0x0000000000401044 <+56>:	mov    0x8(%rsp),%edi	// R[edi] = M[R[rsp]+0x8] = 第一个参数
   0x0000000000401048 <+60>:	call   0x400fce <func4>
   0x000000000040104d <+65>:	test   %eax,%eax
   0x000000000040104f <+67>:	jne    0x401058 <phase_4+76>
   0x0000000000401051 <+69>:	cmpl   $0x0,0xc(%rsp)
   0x0000000000401056 <+74>:	je     0x40105d <phase_4+81>
   0x0000000000401058 <+76>:	call   0x40143a <explode_bomb>
   0x000000000040105d <+81>:	add    $0x18,%rsp
   0x0000000000401061 <+85>:	ret    
End of assembler dump.
```



```asm
(gdb) disas func4
Dump of assembler code for function func4:
   0x0000000000400fce <+0>:	sub    $0x8,%rsp	
   0x0000000000400fd2 <+4>:	mov    %edx,%eax	// R[eax] = R[edx] = $0xe = 14
   0x0000000000400fd4 <+6>:	sub    %esi,%eax	// R[eax] = R[eax] - R[esi] = 14 - 0 = 14
   0x0000000000400fd6 <+8>:	mov    %eax,%ecx	// R[ecx] = R[eax] = 14
   0x0000000000400fd8 <+10>:	shr    $0x1f,%ecx	// 对R[ecx]的值逻辑右移31位
   0x0000000000400fdb <+13>:	add    %ecx,%eax	// R[eax] = R[eax] + R[ecx]
   0x0000000000400fdd <+15>:	sar    %eax		// R[eax] = R[eax] >> 1 = 7
   0x0000000000400fdf <+17>:	lea    (%rax,%rsi,1),%ecx	// R[ecx] = R[rax] + R[rsi] = 7 + 0 = 7
   0x0000000000400fe2 <+20>:	cmp    %edi,%ecx	// R[edi]存放第一个参数a
   0x0000000000400fe4 <+22>:	jle    0x400ff2 <func4+36>	// 若a>7则跳转至<+36>
   0x0000000000400fe6 <+24>:	lea    -0x1(%rcx),%edx
   0x0000000000400fe9 <+27>:	call   0x400fce <func4>
   0x0000000000400fee <+32>:	add    %eax,%eax
   0x0000000000400ff0 <+34>:	jmp    0x401007 <func4+57>
   0x0000000000400ff2 <+36>:	mov    $0x0,%eax	// 返回值为0
   0x0000000000400ff7 <+41>:	cmp    %edi,%ecx	// 再次比较第一个参数和R[edi]
   0x0000000000400ff9 <+43>:	jge    0x401007 <func4+57>	// if a <= 7, 跳出
   0x0000000000400ffb <+45>:	lea    0x1(%rcx),%esi	// R[esi]++
   0x0000000000400ffe <+48>:	call   0x400fce <func4>
   0x0000000000401003 <+53>:	lea    0x1(%rax,%rax,1),%eax
   0x0000000000401007 <+57>:	add    $0x8,%rsp
   0x000000000040100b <+61>:	ret    
End of assembler dump.
```

#### log

```
(gdb) b phase_4
Breakpoint 1 at 0x40100c
(gdb) r ans.txt 
Starting program: /home/kristin/study/csapp/labs/bomblab/bomb/bomb ans.txt
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
Welcome to my fiendish little bomb. You have 6 phases with
which to blow yourself up. Have a nice day!
Phase 1 defused. How about the next one?
That's number 2.  Keep going!
Halfway there!

Breakpoint 1, 0x000000000040100c in phase_4 ()
(gdb) stepi
0x0000000000401010 in phase_4 ()
(gdb) 
0x0000000000401015 in phase_4 ()
(gdb) 
0x000000000040101a in phase_4 ()
(gdb) 
0x000000000040101f in phase_4 ()
(gdb) 
0x0000000000401024 in phase_4 ()
(gdb) 
0x0000000000400bf0 in __isoc99_sscanf@plt ()
(gdb) 
__GI___isoc99_sscanf (s=0x603870 <input_strings+240> "test", format=0x4025cf "%d %d") at ./stdio-common/isoc99_sscanf.c:24
24	./stdio-common/isoc99_sscanf.c: No such file or directory.
(gdb) finish
Run till exit from #0  __GI___isoc99_sscanf (
    s=0x603870 <input_strings+240> "test", format=0x4025cf "%d %d")
    at ./stdio-common/isoc99_sscanf.c:24
0x0000000000401029 in phase_4 ()
Value returned is $1 = 0
```
##### phase_4
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/lab2p41.png)
1. 该phase需要两个int
- R[rsp] + 0x8 存放第一个参数
- R[rsp] + 0xc 存放第二个参数
2. R[eax] != 2
3. 第一个参数(R[rsp]+8) < 0xe(14)
4. 调用fun4之前寄存器中存储的值 
- R[edx] = $0xe = 14  
- R[esi] = $0x0 = 0  
- R[edi] = M[R[rsp]+0x8] = 第一个参数a  
5. 易知第二个参数是0

##### func4
![avatar](https://github.com/kechenkristin/imagesGitHub/blob/main/notes/csapp/lab2p42.png)
该段code是一段递归调用  
<+0>-<+17> 处设置了一些寄存器的值  
根据注释可知，临界值为7，故第一个参数是7

```shell
kristin@kristin-PC:~/study/csapp/labs/bomblab/bomb$ cat ans.txt 
Border relations with Canada have never been better.
1 2 4 8 16 32
3 256
7 0
kristin@kristin-PC:~/study/csapp/labs/bomblab/bomb$ bomb ans.txt 
Welcome to my fiendish little bomb. You have 6 phases with
which to blow yourself up. Have a nice day!
Phase 1 defused. How about the next one?
That's number 2.  Keep going!
Halfway there!
So you got that one.  Try this one.
```
