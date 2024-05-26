# collission

## 1.源码

```c
#include <stdio.h>
#include <string.h>
unsigned long hashcode = 0x21DD09EC;
unsigned long check_password(const char* p){
	int* ip = (int*)p;
	int i;
	int res=0;
	for(i=0; i<5; i++){
		res += ip[i];
	}
	return res;
}

int main(int argc, char* argv[]){
	if(argc<2){
		printf("usage : %s [passcode]\n", argv[0]);
		return 0;
	}
	if(strlen(argv[1]) != 20){
		printf("passcode length should be 20 bytes\n");
		return 0;
	}

	if(hashcode == check_password( argv[1] )){
		system("/bin/cat flag");
		return 0;
	}
	else
		printf("wrong passcode.\n");
	return 0;
}

```

## 2.pwn

分析发现这题与md碰撞并没有关系，只需要输入一个20个字符（20bytes）的字符串，使20个字符分割成5个整数（4bytes），sum后与hashcode相等即可查看flag

* 0x21DD09EC=568,134,124=113,626,825*4+113,626,824
* 06 C5 CE C9，06 C5 CE C8
* p32(0x06C5CEC9)
  Out[]: b'\xc9\xce\xc5\x06'
* p32(0x06C5CEC8)
  Out[]: b'\xc8\xce\xc5\x06'
* 拼接：\xc9\xce\xc5\x06\xc9\xce\xc5\x06\xc9\xce\xc5\x06\xc9\xce\xc5\x06\\xc8\xce\xc5\x06
* 运行：./col \`python -c 'print "\xc9\xce\xc5\x06\xc9\xce\xc5\x06\xc9\xce\xc5\x06\xc9\xce\xc5\x06\xc8\xce\xc5\x06"'`

flag：daddy! I just managed to create a hash collision :)



## 3.tips

* `''` 单引号，转义其中的所有变量为单纯的字符串

* `""` 双引号，保留其中的变量属性，不进行转义处理

* ```
  python -c <command>
  ```

  执行 *command* 中的 Python 代码

* `0x` 用于表示整数值的十六进制形式，通常用于整数或指针等数据类型。

* `\x` 用于表示字符的十六进制值，通常用于字符串或字符常量中。
