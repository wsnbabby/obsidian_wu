
### 编译流程

- 源文件
- 预处理
- 编译
- 汇编
- 链接
- 可执行文件
### 命令

```bash
# 一步搞定
gcc hello.c
```

```bash
# 预处理（PreProcess Only 默认不会产生结果文件，需要指定）
gcc -E hello.c > hello.i

# 编译（Compile Only 自动生成hello.s文件）
gcc -S hello.i

# 汇编（Compile and assemble 自动生成hello.o文件）
gcc -c hello.s 

# 链接（默认生成a.out可执行文件, -o 指定名称）
gcc hello.o -o hello
```

### 多文件编译过程

```C
// myhead.h
#ifndef MYHEAD_H
#define MYHEAD_H

int myfunc(int a);

#endif
```
>`MYHEAD_H`中下划线, 属于编程风格的内容，对程序没有影响。不用下划线也可以，用几个下划线也由个人习惯。

```C
// myhead.c
#include <stdio.h>

int myfunc(int a) {
	printf("call myfunc, argv=%d\n", a);
	return a;
}
```

```C
// main.c

#include <stdio.h>
#include "myhead.h"

int main() {
	printf("start to call myfunc\n");
	int a = myfunc(3);
	
	return 0;
}
```

> 假设现在有 main.c  myhead.h myhead.c三个文件，myhead.h声明了方法，myhead.c中定义了方法实现；main.c为主函数入口且用到了myhead.c中的方法。编译过程：`gcc main.c myhead.c -o main`