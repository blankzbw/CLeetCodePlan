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
>    ![](https://github.com/blankzbw/CLeetCodePlan/blob/main/knowledge/git/git1.PNG)
>
> 5. 

## 6. git场景

> 1. 修改老的commit点的提交信息
>
>    1. git rebase -i 父commit点  交互变基
>    2. 将想变基的commit点修改为reword，wq！
>    3. 变更提交信息
>
> 2. 将连续多个commit点压缩成一个
>
>    1. git rebase -i 父commit点  交互变基
>    2. 将想变基的commit点修改为squash，wq！
>    3. 变更提交信息
>
> 3. 将间隔多个commit点压缩成一个
>
>    1. git rebase -i 父commit点  交互变基
>    2. 调整commit点顺序
>    3. 将想变基的commit点修改为squash，wq！
>    4. 变更提交信息
>    5. 不建议使用，毕竟很多commit点有耦合关系，冲突较多
>
> 4. 取消最近几次的提交
>
>    1. git reset --hard commit点   （危险）将HEAD指向commit点，同时将暂存区和工作区也恢复到commit点内容；这样真的会丢失commit点，所以使用时一定要注意
>
> 5. 临时开发紧急任务（将工作区和暂存区现场保存）
>
>    1. git stash 将工作区和暂存区现场保存至栈中
>    2. git stash list 查看栈中的信息
>    3. git status 查看工作区是干净的
>    4. 开发紧急任务
>    5. git stash apply 读出栈中内容恢复至工作区和暂存区
>    6. git stash pop 弹出栈中内容恢复至工作区和暂存区
>
> 6. 多人协作场景
>
>    1. 两个人修改不同文件先后提交,git可以自动合并
>       1. 第一个人git add + git commit +git push
>       2. 第二个人git add + git commit +git push（报错nofast）+git pull（git fetch+git merge)
>    2. 两个人修改相同文件不同位置，git可以自动合并
>       1. 第一个人git add + git commit +git push
>       2. 第二个人git add + git commit +git push（报错nofast）+git pull（git fetch+git merge)
>    3. 两个人修改相同文件相同位置，git不可以自动合并
>       1. 第一个人git add + git commit +git push
>       2. 第二个人git add + git commit +git push（报错nofast）+git pull（git fetch+git merge)（报错冲突）+解决冲突+git commit + git push
>    4. 一个人修改文件名，一个人基于之前的名称修改内容，git可以自动合并
>       1. 第一个人git add + git commit +git push
>       2. 第二个人git add + git commit +git push（报错nofast）+git pull（git fetch+git merge)
>    5. 两个人同时修改文件名，git不可以自动合并
>       1. 第一个人git add + git commit +git push
>       2. 第二个人git add + git commit +git push（报错no fastforward）+git pull（git fetch+git merge)（报错冲突）+解决冲突+git rm +git add + git commit + git push
>
> 7. 危险性极大的命令
>
>    1. git reset --hard commit点,然后git push -f  会导致远端的commit点丢失掉；
>
>    2. 公共分支禁止进行变基操作，这样会修改掉历史信息；如果A变基了，B进行push时就容易报错,导致解决起来非常的麻烦
>
>       ![rejected]   test_rebase_inter -> test_rebase_inter (non-fast-forward)
>
>       error: faild to push some  refs to "git@github.com:XXX/xx.git"
>
>       hint : Updates were rejectes because the tip of your current branch is behind
>
>       hint : its remote counterpart.Integrate the remote changes(e.g.
>
>       hint : 'hit pull ...') before pushing again.
>
>       hint : See the 'Note about fast-forward' in 'git push --help' for details.

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
>
>    1. 直观区别：哑协议传输进度不可见；智能协议传输可见；
>    2. 传输速度：智能协议比哑协议传输速度快（压缩打包）；
>
> 3. 备份
>
>    1. 哑协议克隆不带工作区的裸仓库
>
>       $ git clone --bare  /d/git/CLeetCodePlan/.git ya.git
>       Cloning into bare repository 'ya.git'...
>       done.
>
>    2. 哑协议克隆整个仓库（包括工作区）
>
>       $ git clone  /d/git/CLeetCodePlan/.git ya
>       Cloning into bare repository 'ya'...
>       done.
>
>    3. 智能协议克隆不带工作区的裸仓库
>
>       $ git clone  --bare file:///d/git/CLeetCodePlan/.git zhineng.git
>       Cloning into bare repository 'zhineng.git'...
>       remote: Enumerating objects: 81, done.
>       remote: Counting objects: 100% (81/81), done.
>       remote: Compressing objects: 100% (65/65), done.
>       remote: Total 81 (delta 23), reused 19 (delta 3), pack-reused 0
>       Receiving objects: 100% (81/81), 177.99 KiB | 6.84 MiB/s, done.
>       Resolving deltas: 100% (23/23), done.
>
>    4. 智能协议克隆整个仓库（包括工作区）
>
>       $ git clone  file:///d/git/CLeetCodePlan/.git zhineng
>       Cloning into 'zhineng'...
>       remote: Enumerating objects: 81, done.
>       remote: Counting objects: 100% (81/81), done.
>       remote: Compressing objects: 100% (65/65), done.
>       Receiving objects:  58% remote: Total 81 (delta 23), reused 19 (delta 3), pack-reused 0
>       Receiving objects: 100% (81/81), 177.99 KiB | 7.12 MiB/s, done.
>       Resolving deltas: 100% (23/23), done.
>
> 4. 远端仓库
>
>    1. 增加远端仓库
>
>       $git remote add zhineng  file:///d/git/test/zhineng.git
>
>    2. 查看增加的仓库
>
>       $ git remote -v
>       origin  git@github.com:blankzbw/CLeetCodePlan.git (fetch)
>       origin  git@github.com:blankzbw/CLeetCodePlan.git (push)
>       zhineng file:///d/git/test/zhineng.git (fetch)
>       zhineng file:///d/git/test/zhineng.git (push)
>
>    3. 在本地仓库提交一个commit点
>
>       $ git commit -m "uodate git"
>       [main 61f5ef0] uodate git
>        1 file changed, 19 insertions(+)
>
>    4. 将commit点推送到远端
>
>       $ git push zhineng
>       Enumerating objects: 9, done.
>       Counting objects: 100% (9/9), done.
>       Delta compression using up to 8 threads
>       Compressing objects: 100% (5/5), done.
>       Writing objects: 100% (5/5), 822 bytes | 822.00 KiB/s, done.
>       Total 5 (delta 3), reused 0 (delta 0), pack-reused 0
>       To file:///d/git/test/zhineng.git
>          b6986d9..61f5ef0  main -> main
>
>    5. 查看远端仓库commit信息
>
>       $ git log
>       commit 61f5ef0b1ed37ba351eaaf7556d68fea758d8a95 (HEAD -> main)
>       Author: blankzbw <zhengbowen963@163.com>
>       Date:   Fri Jul 16 00:26:36 2021 +0800
>
>       update git
>
>       由于创建的是裸仓库，所以只更新commit点，不会更新工作区文件
>
>    6. 一路验证.git里面存的内容
>
>    7. $ git cat-file -p 61f5ef0b1ed37ba351eaaf7556d68fea758d8a95
>       tree 23da1fe2f115126103d33969ed63e555847e04dc
>       parent b6986d9c3ae60edb864fb401bf93d11ae8acf53b
>       author blankzbw <zhengbowen963@163.com> 1626366396 +0800
>       committer blankzbw <zhengbowen963@163.com> 1626366396 +0800
>
>       uodate git
>
>       zbw@LAPTOP-6JBT8C4I MINGW64 /d/git/test/zhineng.git (BARE:main)
>       $ git cat-file -p  23da1fe2f115126103d33969ed63e555847e04dc
>       100644 blob c6127b38c1aa25968a88db3940604d41529e4cf5    .gitignore
>       100644 blob 261eeb9e9f8b2b4b0d119366dda99c6fd7d35c64    LICENSE
>       100644 blob eb485661d7acbbdc167426d869fc7dd61964f205    README.md
>       040000 tree 1467a07cba0a8fa4612dc84702e990403cc09f53    knowledge
>       040000 tree a0244e39aaafc8a38c4c705bc9352ffb308de293    leetcode
>       040000 tree cd83f81f1bf934b5a70bfb638e5bad58f1bbd159    vscode_setting
>
>       zbw@LAPTOP-6JBT8C4I MINGW64 /d/git/test/zhineng.git (BARE:main)
>       $ git cat-file -p  1467a07cba0a8fa4612dc84702e990403cc09f53
>       100644 blob 9cb3de0033db6fb482a389859b9d0c10576a4528    README.md
>       040000 tree aa839ef85c33867690ac46a2d66e4713b972f30f    cplusplus
>       040000 tree db163afff9a49da223c7a2b24deebee495d900f7    git
>
>       zbw@LAPTOP-6JBT8C4I MINGW64 /d/git/test/zhineng.git (BARE:main)
>       $ git cat-file -p   db163afff9a49da223c7a2b24deebee495d900f7
>       100644 blob 05c6077d090d608fabd30baf42c6f2ac21580c36    git.md
>       100644 blob 01148c407531e545007d65f2b446ee4a91e04bb3    git1.PNG
>
>       zbw@LAPTOP-6JBT8C4I MINGW64 /d/git/test/zhineng.git (BARE:main)
>       $ git cat-file -p   05c6077d090d608fabd30baf42c6f2ac21580c36
>
>       git中文教程
>
>       https://git-scm.com/book/zh/v2
>
>       1. git配置命令

## 8. 远端仓库

1. 合并分支 git merge
2. 拉取远端分支 git fetch
3. 拉取远端分支到本地并合并分支 git pull =  git fetch + git merge
4. 合并两个没有关系的远端分支和本地分支git merge --allow-unrelated-histories github/master
5. 推送到远端仓库 git push github/master

## 9. 开发工作流

> 1. 主干开发（google采用）
>
>    ![](https://github.com/blankzbw/CLeetCodePlan/blob/main/knowledge/git/git2.PNG)
>
> 2. git flow开发
>
>    ![](https://github.com/blankzbw/CLeetCodePlan/blob/main/knowledge/git/git_flow.PNG.PNG)
>
> 3. GitHub flow开发
>
>    ![](https://github.com/blankzbw/CLeetCodePlan/blob/main/knowledge/git/githubflow.PNG)
>
> 4. gitlab flow（带生产分支）
>
>    ![](https://github.com/blankzbw/CLeetCodePlan/blob/main/knowledge/git/gitlabflow.PNG)
>
> 5. gitlab flow（带环境分支）
>
>    ![](https://github.com/blankzbw/CLeetCodePlan/blob/main/knowledge/git/gitlabflow1.PNG)
>
> 6. gitlab flow（带发布分支）
>
>    ![](https://github.com/blankzbw/CLeetCodePlan/blob/main/knowledge/git/gitlabflow2.PNG)
