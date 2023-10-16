## fopen
### 方法

```C
#include <stdio.h>

FILE *fopen(const char *pathname, const char *mode);

FILE *fdopen(int fd, const char *mode);

FILE *freopen(const char *pathname, const char *mode, FILE *stream);
```

### mode

- r  ：只读，文件不存在报错，定位到文件开始处
- r+ ：读写，文件不存在报错，定位到文件开始处
- w  ：只写，文件不存在创建，文件存在则清空，定位到文件开始处
- w+ ：读写，文件不存在创建，文件存在则清空，定位到文件开始处
- a  ：只写，文件不存在创建，定位到文件结尾
- a+ ：读写，文件不存在创建，定位到文件结尾

> 字符串 mode 也可以包含字母 `b`  作为最后一个字符，或者插入到上面提到的任何双字符的字符串的两个字符中间。
> 
> 这样只是为了和  ANSI X3.159-1989 (`ANSI C`) 标准严格保持兼容，没有实际的效果；
> 
> 在所有的遵循 POSIX 的系统中，`b`都被忽略，包括 Linux。(其他系统可能将文本文件和二进制文件区别对待，如果在进行二进制文件的 I/O，那么添加 `b` 是个好主意，因为你的程序可能会被移植到非 Unix 环境中。)


## fclose

```C
int fclose(FILE *stream);
```

## fget

```C
int fclose(FILE *stream);
```

## fput
```C
int fputc(int c, FILE *stream);

int fputs(const char *s, FILE *stream);

int putc(int c, FILE *stream);

int putchar(int c);

int puts(const char *s);
```

## fgets


## fputs

## fscanf

## fprintf


## fread

## fwrite