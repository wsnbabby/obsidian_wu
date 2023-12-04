## fopen

```C
#include <stdio.h>

FILE *fopen(const char *pathname, const char *mode);

FILE *fdopen(int fd, const char *mode);

FILE *freopen(const char *pathname, const char *mode, FILE *stream);
```

mode参数说明

- 'r'  ：只读，文件不存在报错，定位到文件开始处
- 'r+' ：读写，文件不存在报错，定位到文件开始处
- 'w'  ：只写，文件不存在创建，文件存在则清空，定位到文件开始处
- 'w+' ：读写，文件不存在创建，文件存在则清空，定位到文件开始处
- 'a'  ：只写，文件不存在创建，定位到文件结尾
- 'a+' ：读写，文件不存在创建，定位到文件结尾

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
 #include <stdio.h>

int fgetc(FILE *stream);

// 宏，与fgetc相同
int getc(FILE *stream);

// 从指定的流 stream 读取一行，并把它存储在str所指向的字符串内。当读取(n-1)个字符时，或者读取到换行符时，或者到达文件末尾时，它会停止
char *fgets(char *s, int size, FILE *stream);

// 从STDIN(标准输入)获取并返回下一个字符,如果到达文件尾返回EOF
int getchar(void);

// 从STDIN(标准输入)读取字符并把它们加载到_str_(字符串)里,直到遇到新行(\n)或到达EOF. 新行字符翻译为一个null中断符. gets()的返回值是读入的字符串,如果错误返回NULL
char *gets(char *str);

// 普通文件输入流可以使用ungetc放回一个字符，但是一次只能够放回一个，必须要等到放回的字符读出来之后再才能接着放回一个字符
int ungetc(int c, FILE *stream);
```
## fput

```C
#include <stdio.h>

int fputc(int c, FILE *stream);

int fputs(const char *s, FILE *stream);

int putc(int c, FILE *stream);

int putchar(int c);

int puts(const char *s);
```



## fscanf

## fprintf

## fread

## fwrite



# 文件定位

>每个流都有相关联的文件位置（file position），打开文件时会将文件位置设置在文件开始处（追加模式会设置在文件末尾），后续的读写操作会自动推进

三种宏：
- SEEK_SET 文件起始处
- SEEK_CUR 文件当前位置
- SEEK_END 文件末尾

## fseek

```C
int fseek(FILE *stream, long offset, int whence);
```

## fgetpos

## fsetpos

## ftell

## rewind


