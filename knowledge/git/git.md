# git中文教程

https://git-scm.com/book/zh/v2

## 1. git配置命令

> 1. 查看版本 git --version 
> 2. 配置user信息 
>    1. git config --global user.name 'your_name'
>    2. git config --global user.name 'your_email@domain.com'
> 3. 显示配置config配置
>    1. git config --list --local 对当前仓库生效（缺省）生效优先级最高
>    2. git config --list --global 对当前用户所有仓库生效（常用）
>    3. git config --list --system 对系统所有登录的用户有效（很少）

##  2. 建 Git 仓库

> 1. ⽤ Git 之前已经有项⽬代码
>    1. $cd 路径
>    2. $ git init
> 2. 用git之前未创建项目代码
>    1. $ cd  某个文件夹
>    2. $ git init your_project 
>    3. $ cd your_project

## 3. git基本命令

> 1. 将工作区文件添加到暂存区
>    1. git add
>    2. git add -u 可以将git已经跟踪的修改文件全部add到暂存区
> 2. 将暂存区文件提交到仓库
>    1. git commit
>    2. git commit -am ""  = git add + git commit
>    3. git commit --amend 变更提交的信息，并将暂存区提交
> 3. 查看git日志
>    1. git log
>    2. git log --online 查看简洁版git日志
>    3. git log -n4 --online 查看最近四条简洁版git日志
>    4. git log --all 查看所以分支的日志
>    5. git log --all --graph 查看带版本图形化演进历史（这些参数都可以罗列增加）
> 4. 创建分支
>    1. git checkout -b A B 基于B分支创建A分支 
>    2. git branch -av 查看全部分支
>    3. git branch -d 删除分支
> 5. 查看差异
>    1. git diff 查看工作区和暂存区之间的差异
>    2. git diff --cached 查看暂存区和HEAD之间的差异
>    3. git diff 分支A 分支B  查看两个分支的差异（本质和commit点是一样的）
> 6. 取消变更（git status会有提示，请注意）
>    1. git reset HEAD 取消暂存区的变更 暂存区的文件恢复至工作区
>    2. git checkout -- filename 取消工作区的变更 工作区的文件恢复至暂存区

## 4. git小技巧

> 1. 文件名重命名 git mv readme readme.md
> 2. 分离头指针
>    1. git checkout  commit点 后 HEAD会处于分离头指针状态，detached HEAD
>    2. 这种状态下可以进行commit，但是当切换到分支上时，若未为此创建分支，之后git会将此commit点清理掉
> 3. 正确删除文件的方法 git rm readme



## 5. 探秘.git

> 1. HEAD文件
>
>    1. ref: refs/heads/main 当前指向的分支
>    2. $ cat refs/heads/main
>       0c9c6e15876e6e0a81314cde09bb67e3fa70963a commit点
>    3. $ git cat-file -t 0c9c6e15876 查看数字的类型
>       commit   commit点类型
>    4. $ git cat-file -p 0c9c6e15876 查看数字内存放的内容
>
> 2. config文件
>
>    1. 配置信息
>
> 3. objects核心内容
>
>    1. 内容：双字符文件夹+info+pack
>
>    2. 查看双字符文件夹中内容的类型：$ git cat-file -t 双字符+文件夹中文件内容
>
>       -r--r--r-- 1 zbw 197121 150 Jun 21 01:02 1e9e6abc3b255c3df7b3e8eb41e63eaac427d4
>
>       zbw@LAPTOP-6JBT8C4I MINGW64 /d/git/CLeetCodePlan/.git/objects/f9 (GIT_DIR!)
>       $ git cat-file -t f91e9e6abc3b2
>       tree
>
>    3. 查看内容$ git cat-file -p f91e9e6abc3b2
>       100644 blob 11f796f1cf17c287cc3c1643caaf55f07991f05f    01INIT.md
>
>       blob（只要任何文件的文件内容相同就是唯一的blob）
>
>    4. 查看blob内容，就是当时存储的内容
>
>       $ git cat-file -p  11f796f1cf17c287cc3c16
>
>       02 How to setup cpp on windows
>
>       1. VS and VS code
>
> 4. commit、tree、blob之间的关系
>
>    可以通过3中的命令查看
>
>    ![](D:\git\CLeetCodePlan\knowledge\git\git1.PNG)
>
> 5. 

## 6. git场景

> 1. 修改老的commit点的提交信息
>    1. git rebase -i 父commit点  交互变基
>    2. 将想变基的commit点修改为reword，wq！
>    3. 变更提交信息
> 2. 将连续多个commit点压缩成一个
>    1. git rebase -i 父commit点  交互变基
>    2. 将想变基的commit点修改为squash，wq！
>    3. 变更提交信息
> 3. 将间隔多个commit点压缩成一个
>    1. git rebase -i 父commit点  交互变基
>    2. 调整commit点顺序
>    3. 将想变基的commit点修改为squash，wq！
>    4. 变更提交信息
>    5. 不建议使用，毕竟很多commit点有耦合关系，冲突较多
> 4. 取消最近几次的提交
>    1. git reset --hard commit点   （危险）将HEAD指向commit点，同时将暂存区和工作区也恢复到commit点内容；这样真的会丢失commit点，所以使用时一定要注意
> 5. 临时开发紧急任务（将工作区和暂存区现场保存）
>    1. git stash 将工作区和暂存区现场保存至栈中
>    2. git stash list 查看栈中的信息
>    3. git status 查看工作区是干净的
>    4. 开发紧急任务
>    5. git stash apply 读出栈中内容恢复至工作区和暂存区
>    6. git stash pop 弹出栈中内容恢复至工作区和暂存区

## 7. 仓库备份

> 1. 常用的传输协议
>
> | 常用协议      | 语法格式                                     | 说明                     |
> | ------------- | -------------------------------------------- | ------------------------ |
> | 本地协议（1） | /path/to/repo.git                            | 哑协议                   |
> | 本地协议（2） | file:///path/to/repo.git                     | 智能协议                 |
> | http协议      | http://git-server.com:port/path/to/repo.git  | 平时接触到的都是智能协议 |
> | https协议     | https://git-server.com:port/path/to/repo.git | 平时接触到的都是智能协议 |
> | ssh协议       | user@git-server.com:path/to/repo.git         | ⼯作中最常⽤的智能协议   |

> 2. 哑协议与智能协议
>    1. 直观区别：哑协议传输进度不可见；智能协议传输可见；
>    2. 传输速度：智能协议比哑协议传输速度快（压缩打包）；
> 3. 

 

