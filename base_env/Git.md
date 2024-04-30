## 安装

```bash
apt-get install git
```

## 初始化
```bash
git init

git clone "https://xxxxxx"
```
## config
```bash
# 
git config -l

#
git config user.name "name"
git config user.email "email"

```

## 操作
```bash
git branch -r # 查看远程分支名

git status # 查看工作区代码相对于暂存区的差别
	-s # 输出简短信息

git add . # 将当前目录下修改的所有内容从工作区添加到暂存区
	-u # 只包含已跟踪的文件, 即修改和删除的文件, 不包括新增
	-a # 所有文件

git diff # 查看执行git status的结果的详细信息（已写入缓存与已修改但尚未写入缓存的改动的区别）
	--cached # 查看已缓存的改动
	--stat # 显示摘要而非整个diff

git diff HEAD # 查看已缓存的与未缓存的所有改动

git commit -m 'message' # 将暂存区内容添加到本地仓库
	-a # 可以绕过git add命令直接提交到本地仓库

git pull origin main # 将远程仓库main中的信息同步到本地仓库main中

git push origin main # 将本地仓库推送到远程服务器
	# 一般形式 git push <远程主机名> <本地分支名> <远程分支名> 
	# 如果远程分支被省略，则表示将本地分支推送到与之存在追踪关系的远程分支（通常两者同名），如果该远程分支不存在，则会被新建
	# 如果当前分支只有一个远程分支, 那么

```

`refs/for 的意义在于我们提交代码到服务器之后是需要经过code review 之后才能进行merge的，而refs/heads 不需要`

```sh
# 只克隆某个分支代码，不会下载整个git仓库
Git clone -b {dev} --single-branch
```
## 分支管理
```bash

git brach # 列出本地分支

git branch {branch_name} # 创建分支
git branch -d {branch_name} # 删除该分支

git checkout {branch_name} # 切换分支
git checkout -b {branch_name} # 创建新分支并立即切换到新分支下

git merge {newtest} # 合并分支，将newtest分支合并到主分支，
```

## 远程管理
```bash

ssh-keygen -t rsa -C "youremail@example.com" # 生成ssh公钥
ssh -T git@github.com # 验证是否成功

git remote add origin git@github.com:xxx/xxx.git # 添加一个新的远程仓库

git pull -u origin main # 

git fetch # 下载新分支

git push [alias] [branch] # 推送到远程仓库
```

## .gitignore
```bash
# 此为注释
*.a  # 忽略所有.a结尾的文件
!lib.a  # 但lib.a除外
/TODO  # 仅仅忽略项目根目录下的TODO文件，不包括subdir/TODO
build/  # 忽略build/ 目录下的所有文件，包括subdir/build/
doc/*.txt  # 会忽略 doc/notes.txt 但不包括doc/server/arch.txt

```






## FAQ

1. 内容已经修改并推送到了远端仓库，想要撤回，且不想要远端留下该条记录
	- 先回退本地修改记录，然后`git push --force`【会导致远端仓库不可逆，危险操作，谨慎使用，做好备份】

2. 独立子项目并保留提交记录
    - `git subtree split -P ${name of folder} -b ${new branch}`
    - 切换到新的分支
    - 推送到远端新仓库

3. 解决Windos下`git status`中文乱码
	- `git bash` 终端输入命令 `git config --global core.quotepath false`
	- 终端界面鼠标右击`Options-Text`选择`zh_CN`和`UTF-8`

4. 无法拉取github代码或提交
	fatal: unable to access 'https://github.com/wsnbabby/obsidian_wu.git/': Failed to connect to github.com port 443 after 21102 ms: Timed out

```bash
//取消http代理
git config --global --unset http.proxy
//取消https代理 
git config --global --unset https.proxy
```

5. 