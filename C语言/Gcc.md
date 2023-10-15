
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
# 预处理（默认不会产生结果文件，需要指定）
gcc -E hello.c > hello.i

# 编译（自动生成hello.s文件）
gcc -S hello.i

# 汇编（自动生成hello.o文件）
gcc -c hello.s 

# 链接（默认生成a.out可执行文件, -o 指定名称）
gcc hello.o -o hello
```