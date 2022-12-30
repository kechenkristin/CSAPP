## Prenote
### Files
```shell
kristin@kristin-PC:~/study/csapp/labs/attacklab/target1$ ls
cookie.txt  ctarget  farm.c  hex2raw  README.txt  rtarget
```

- README.txt: A file describing the contents of the directory
- ctarget: An executable program vulnerable to code-injection attacks
- rtarget: An executable program vulnerable to return-oriented-programming attacks
- cookie.txt: An 8-digit hex code that you will use as a unique identifier in your attacks.
- farm.c: The source code of your target’s “gadget farm,” which you will use in generating return-oriented programming attacks.
- hex2raw: A utility to generate attack strings.

### getbuf()
Both CTARGET and RTARGET read strings from standard input. They do so with the function getbuf defined below:
```c
unsigned getbuf() {
	char buf[BUFFER_SIZE];
	Gets(buf);
	return 1;
}
```


## Level1

