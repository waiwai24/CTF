# fd



## 1.前置知识

### 1.1 文件描述符fd

内核(kernel)利用文件描述符(file descriptor)来访问文件。文件描述符是非负整数。打开现存文件或新建文件时，内核会返回一个文件描述符。读写文件也需要使用文件描述符来指定待读写的文件

| 文件描述符 | 用途     | stdio流 |
| ---------- | -------- | ------- |
| 0          | 标准输入 | stdin   |
| 1          | 标准输出 | stdout  |
| 2          | 标准错误 | stderr  |

### 1.2 read()

```c
头文件：#include <unistd.h>
定义函数：ssize_t read(int fd, void * buf, size_t count);
```

* read()会把参数fd 所指的文件传送count 个字节到buf  指针所指的内存中. 若参数count 为0, 则read()不会有作用并返回0. 返回值为实际读取到的字节数, 如果返回0,  表示已到达文件尾或是无可读取的数据,此外文件读写位置会随读取到的字节移动
* fd=0，代表标准输入流

### 1.3 atoi()

```c
int atoi(constchar*str)
```

该函数返回转换后的长整数，如果没有执行有效的转换，则返回零

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
   int val;
   char str[20];
   
   strcpy(str, "98993489");
   val = atoi(str);
   printf("字符串值 = %s, 整型值 = %d\n", str, val);

   strcpy(str, "runoob.com");
   val = atoi(str);
   printf("字符串值 = %s, 整型值 = %d\n", str, val);

   return(0);
}
字符串值 = 98993489, 整型值 = 98993489
字符串值 = runoob.com, 整型值 = 0

```



## 2.pwn

查看文件权限，发现只能查阅fd.c：

```c
char buf[32];
int main(int argc, char* argv[], char* envp[]){
        if(argc<2){
                printf("pass argv[1] a number\n");
                return 0;
        }
        int fd = atoi( argv[1] ) - 0x1234;
        int len = 0;
        len = read(fd, buf, 32);
        if(!strcmp("LETMEWIN\n", buf)){
                printf("good job :)\n");
                system("/bin/cat flag");
                exit(0);
        }
        printf("learn about Linux file IO\n");
        return 0;

}
```

* `!strcmp("LETMEWIN\n", buf）= 1` 即可，即buf=LETMEWIN
  * s1>s2,返回1
  * s1=s2，返回0
  * s1<s2,返回-1
* buf由read输入，使fd=0，即可stdin
* 0x1234=4660,则运行fd时输入参数4660即可使fd为0，然后再标准输入LETMEWIN即可获得flag

flag：mommy! I think I know what a file descriptor is!!
