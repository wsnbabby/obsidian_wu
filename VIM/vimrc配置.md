
```vim
"传说中的去掉边框用下边这一句
set go=

"设置配色，这里选择的是desert，也有其他方案，在vim中输入:color 在敲tab键可以查看
color desert

"设置背景色，每种配色有两种方案，一个light、一个dark
set background=light

"打开语法高亮
syntax on

"显示行号
set number

"用空格键替换制表符
:set expandtab

"制表符占4个空格
set tabstop=4

"默认缩进4个空格大小
set shiftwidth=4

"增量式搜索
set incsearch

"高亮搜索
set hlsearch

"有时中文会显示乱码，用一下几条命令解决
let &termencoding=&encoding

set fileencodings=utf-8,gbk

```