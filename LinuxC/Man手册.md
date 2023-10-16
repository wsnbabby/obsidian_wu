
## 安装

有些系统未自带完整的man手册，可以自行安装

```bash
# ubunut
sudo apt-get install manpages-de manpages-de-dev manpages-dev glibc-doc manpages-posix-dev manpages-posix

# 中文包
sudo apt-get install manpages-zh
```

### 查看中文手册

`man -M /usr/share/man/zh_CN/ 2 read`

### 自定义一个查看中文man的命令

在`~/.bashrc`中添加`alias cman='man -M /usr/share/man/zh_CN'`



## 常用man命令

- man -f read # 查看命令所在章节