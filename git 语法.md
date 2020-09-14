# git 简易使用

[book](https://git-scm.com/book/zh/v2)

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects


```bash
git <command> [<revision>...] -- [<file>...]

git [--version] [--help] [-C <path>] [-c <name>=<value>] [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path] [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare] [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>] <command> [<args>]
```

* `git <command> --help` 打开对应命令的文档 `C:\Program Files\Git\mingw64\share\doc\git-doc` 为文档位置  `git add --help`
* `git <command> -help` 在命令行中显示对应的语法 `git add -help`
* `git help` 等同于 `git --help`
* `git -help` 显示git的语法


git-命令格式 `<file>`最好加双引号括住 否则，如果文件名有关键字（如git）会出错

#### git工具

* git bash
* sourcetree
* sublime + git 插件
* eclipse + EGIT == HBuilder + EGIT 可以直接看某个文件历史纪录+对比

### 安装好git后,打开 Git Bash

#### git 全局设置

* **git config --global**

    ```bash
    git config --global <配置名称> <配置的值>
    ```

    * --global参数，所有的Git仓库都会使用这个配置

    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "email@example.com"
    git config --global core.autocrlf false #忽略换行方式
    ```





#### git init 创建版本库

* `cd <Path>` 切换到目录
* `mkdir <Folder>` 新建文件夹
* `pwd` 用于显示当前目录路径

* **git add**

    ```bash
    git add <file>
    ```

    * file : 将工作库的`<file>`文件添加到暂存区

    ```bash
   git add -A   # 添加所有改动
   git add *    # 添加新建文件和修改，但是不包括删除
   git add .    # 添加新建文件和修改，但是不包括删除
   git add -u   # 添加修改和删除，但是不包括新建文件
    ```

* **git commit**

    ```bash
    git commit -m "xxx" 将暂存区的所有内容提交到当前分支
    ```

* git status

    查看版本库状态

    ```bash
    git status
    ```
* git diff

    查看变更内容

    ```bash
    git diff <revision> -- <file>
    ```

    * `<revision>`默认是当前版本
    * `<file>`默认时全部已经修改文件

    ```bash
    git diff 33ee1e2 234ab1b 对比两个版本有什么不同

    git diff 33ee1e2 234ab1b -- "./learn20180223/day3/express_API.md" 对比两个版本这个文件的区别；如果只写一个版本就是工作区和所写版本的区别
    ```

    ```bash
    $ git diff HEAD -- "git 语法.txt" #查看工作区与版本区当前版本(最后一次提交)区别
    ```

    git diff 是工作区和暂存区的区别
    git diff HEAD 是工作区和版本区当前版本的区别哦

    怎么看这些区别，就是版本1通过-+代码的方式变成版本2 版本1最好是旧版本 版本2忽略的话就是工作区

* **git log**

    查看提交历史（默认显示3个历史 enter显示更多，q退出，vim语法 一直enter可以一直显示到最初）

    ```bash
    git log [<options>] [<revision range>] [[--] <path>…​]
    ```

    * `<options>`

        * `-p`,`-patch`,`-u` 按补丁格式显示每个更新之间的差异。显示每次提交的内容差异
        * `--word-diff`	按 word diff 格式显示差异。
        * `--stat`	显示每次更新的文件修改统计信息。
        * `--shortstat`	只显示 --stat 中最后的行数修改添加移除统计。
        * `--name-only`	仅在提交信息后显示已修改的文件清单。
        * `--name-status`	显示新增、修改、删除的文件清单。
        * `--abbrev-commit`	仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。简化commit id
        * `--relative-date`	使用较短的相对时间显示（比如，“2 weeks ago”）。
        * `--graph`	显示 ASCII 图形表示的分支合并历史。
        * `--pretty`	使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，* fuller 和 format（后跟指定格式）。oneline：一行显示
        * `--oneline`	--pretty=oneline --abbrev-commit 的简化用法。
        * `-<number>`,`-n <number>`,`--max-count=<number>` 只显示最近的`<number>`次提交
        * `--since`, `--after` 仅显示指定时间之后的提交。 --since=2008-10-01 , --since 2008-10-01 , --since="2008-10-01" 
        * `--until`, `--before` 仅显示指定时间之前的提交。--before=2008-11-01
        * `--author` 仅显示指定作者相关的提交。--author=gitster , --author gitster
        * `--committer` 仅显示指定提交者相关的提交。

    * `<revision range>`



    * `<path>`

        路径，可以多个路径。如果只关心某些文件或者目录的历史提交，可以在 git log 选项的最后指定它们的路径。 因为是放在最后位置上的选项，所以用两个短划线（--）隔开之前的选项和后面限定的路径名。当出现混淆时，路径可能需要加上`--` 前缀以将 `<options>` 区分开


    ``` bash
    #例子
    git log #查看全部文件提交历史
    git log test/test.html #查看 test/test.html 提交历史
    git log -p test/test.html #查看 test/test.html 提交历史详情（包含文件差异）
    git log --pretty=oneline #查看全部文件提交历史,每个记录以一行的方式简化，
    git log --graph #查看分支合并图
    git log --graph --pretty=oneline --abbrev-commit #查看分支合并图 一行显示 简化commit id --pretty=oneline一行显示 ; --abbrev-commit 简化commit id**
    git log --graph --oneline #查看分支合并图 一行显示 简化commit id ；显示效果同上面命令
    git log --graph --oneline --since=2019-06-02 --author=ccc #查看ccc自20190602的提交记录
    ```

    [git log](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2)

```
git reset --hard HEAD^ 回退到上一个版本
	HEAD当前版本 HEAD^上一个版本 HEAD^^上上一个版本 HEAD~100上100个版本 可以小写（head）
git reset --hard commit_id 回退到指定<commit id>的版本
git reflog 查看命令历史 会显示<commit id>，可以用来回退到未来版本
```

```
git checkout -- <file> 丢弃工作区的修改 --好重要(其实好像没有都可以)，没有--就变成了“切换到另一个分支”的命令
git reset <revision> <file> 丢弃工作区的修改 --好重要(其实好像没有都可以)，没有--就变成了“切换到另一个分支”的命令
	/*
		git reset --mixed：此为默认方式，不带任何参数的git reset，即时这种方式，它回退到某个版本，只保留源码，回退commit和index信息
	    git reset --soft：回退到某个版本，只回退了commit的信息，不会恢复到index file一级。如果还要提交，直接commit即可
	    git reset --hard：彻底回退到某个版本，本地的源码也会变为上一个版本的内容，此命令 慎用！
	*/
```

删除文件
	git rm <file> 在版本库删除指定文件  删除完之后直接git commit -m "XXX"
		/*
			rm 删除文件
		*/

远程仓库
	ssh-keygen -t rsa -C "youremail@example.com"  创建SSH key。 在用户主目录里找到.ssh目录 id_rsa.pub是公钥


* **git remote**

    ``` bash
    git remote [-v | --verbose]
    git remote add [-t <branch>] [-m <master>] [-f] [--tags | --no-tags] [--mirror=<fetch|push>] <name> <url>
    git remote rename <old> <new>
    git remote remove <name>
    git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
    git remote [-v | --verbose] show [-n] <name>
    git remote prune [-n | --dry-run] <name>
    git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)...]
    git remote set-branches [--add] <name> <branch>...
    git remote get-url [--push] [--all] <name>
    git remote set-url [--push] <name> <newurl> [<oldurl>]
    git remote set-url --add <name> <newurl>
    git remote set-url --delete <name> <url>
    ```

    * `-v`, `--verbose` Be a little more verbose and show remote url after name. NOTE: This must be placed between `remote` and `subcommand`. 稍微冗长一点，并在名字后显示远程网址。注意：必须放在remote和子命令之间。

    ``` bash
    git remote #查看远程仓库列表
    git remote -v #查看远程仓库列表，信息多点
    ```

    子命令

    -  `git remote add <name> <url>` 添加远程版本库，可添加多个仓库

	    + <url> github的远程库路径都为 git@github.com:<远程帐号库>/<仓库名>.git

        ``` bash
		git remote add origin git@github.com:cccikov/learnGit.git
		git remote add mayun git@gitee.com:cccikov/company-admin.git
        ```

    - `git remote set-url [--push] <name> <newurl> [<oldurl>]`  更改远程的URL

	    `git remote set-url origin http://192.168.0.202:9099/xiaoyun/admin_mobile.git `可以切换远程库




* **git push**

	git push -u origin master 将本地库推送到远程库 -u参数时第一次推送的时候，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来。将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。
	如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push。
		以后可以不加-u参数
		git push origin master
		可以简写为
		git push origin 或者 git push

* **git pull**

	git pull origin 从远程库(origin)获取并合并到当前本地本地分支 等价于 git push

	git pull origin master:my_test 将远程库(origin)的master分支拉取并合并到本地的my_test分支上。

	git pull origin master 将远程库(origin)的master分支拉取并合并到当前分支上(所以要注意了，如果当前分支不是master，会将当前分支合并成master那样，慎用)。

* **git clone**

	git clone <url> 克隆远程库

	git支持多种协议:

    1. ssh协议 git clone git@github.com:cccikov/cccgit.git

        ssh 协议需要 ssh 公钥，但是一旦添加到远程库中，就可以直接拉取代码；不需要登录。适合私人电脑，公司电脑。

	2. https协议 git clone https://github.com/cccikov/cccgit.git

        https 每次拉取和推送都需要输入账号密码登录（虽然电脑可能会记住密码）


-------------------

## 分支作用

在Git里，这个分支叫主分支，即master分支。
分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

* `git branch` 查看分支
* `git branch <name>` 创建分支
* `git checkout <name>` 切换分支
* `git checkout -b <name>` 创建+切换分支
* `git merge <name>` 合并某分支到当前分支
    - git merge --abort
    - git merge --–no-ff

    git merge --no-ff -m "merge with no-ff" dev   --no-ff参数，强制禁用Fast forward模式

* `git branch -d <name>` 删除分支
* `git log --graph` 查看分支合并图

    **`git log --graph --pretty=oneline --abbrev-commit`  `--pretty=oneline`一行显示 ; `--abbrev-commit`简化commit id**

在实际开发中，我们应该按照几个基本原则进行分支管理：

* 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
* 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
* 你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

-----------------

## 分离头指针

在"分离头指针"模式下进行的提交除了使用提交的ID来访问之外，不能通过master分支或者其他分支访问到，如果这个提交时master分支所需要的，那么该如何处理呢？如果使用git reset命令把master分支重置到该测试提交的分支上，那么会丢掉master指向的当前的提交。使用git merge合并操作可以两者兼顾。

```
git checkout -b dev 4159f67  将版本回退到4159f67，并在这里创建一个新的 dev 分支，因为HEAD在dev分支上，所以HEAD不是是分离的
git checkout 4159f67 将版本回退到4159f67，但是HEAD是分离的。将HEAD移动到 4159f67 commit id 版本 位置，但是HEAD处于分离状态
git reset 4159f67 将代码重置到4159f67版本
```

-----------------

## 三棵树

理解 reset 和 checkout 的最简方法，就是以 Git 的思维框架（将其作为内容管理器）来管理三棵不同的树。 “树” 在我们这里的实际意思是 “文件的集合”，而不是指特定的数据结构。 （在某些情况下索引看起来并不像一棵树，不过我们现在的目的是用简单的方式思考它。）

Git 作为一个系统，是以它的一般操作来管理并操纵这三棵树的：

| 树                | 用途                              |
|:-----------------:|:----------------------------------|
| HEAD              | 上一次提交的快照，下一次提交的父结点 |
| Index             | 预期的下一次提交的快照              |
| Working Directory | 沙盒                              |

* HEAD

    HEAD 是当前分支引用的指针，它总是指向该分支上的最后一次提交。 这表示 HEAD 将是下一次提交的父结点。 通常，理解 HEAD 的最简方式，就是将它看做 你的上一次提交 的快照。

* index

    索引是你的 预期的下一次提交。 我们也会将这个概念引用为 Git 的 “暂存区域”，这就是当你运行 git commit 时 Git 看起来的样子。

    Git 将上一次检出到工作目录中的所有文件填充到索引区，它们看起来就像最初被检出时的样子。 之后你会将其中一些文件替换为新版本，接着通过 git commit 将它们转换为树来用作新的提交。

* Working Directory

    最后，你就有了自己的工作目录。 另外两棵树以一种高效但并不直观的方式，将它们的内容存储在 .git 文件夹中。 工作目录会将它们解包为实际的文件以便编辑。 你可以把工作目录当做 沙盒。在你将修改提交到暂存区并记录到历史之前，可以随意更改。


### 未收录

* git checkout -b master --track mayun/master 检出远程分支
* git checkout -b master 新建master分支
* git checkout master 切换/检出远程分支（只有一个远程线有这个分支时）

git branch --set-upstream-to=origin/master master

git pull origin master --allow-unrelated-histories

<remote>/<branch>表示远程分支

git log origin/z_ccc --graph --oneline  查看远程库log

git log --all 查看库全部分支的log

git log origin --graph --oneline --all -10 --date-order 按时间排序
git log origin --graph --oneline --all -10 --topo-order 按层级排序

跟踪
git push -u mayun z_ccc
git checkout --track origin/master
git branch -u mayun/master
git branch --set-upstream-to=mayun/master
git branch --set-upstream-to mayun/master
跟踪后 git push 就会自动提交到对应的远程库


git pull = git fetch + git merge
    
    git fetch ssh
    git fetch origin
    git fetch origin master

git push -u
等同于
git push --set-upstream


git branch --all 全部分支
git branch 本地分支（本地已经检出的分支）

git branch -d test -f
    -f --force

git push -u mayun z_ccc -f 
    forced update

git branch -vv 查看本地分支及追踪的分支

git branch -a 查看远程分支

git revert
    合并分支的提交 -m 是 -mainline 的简写

git reflog

git cherry-pick commit_id
git cherry-pick --abort 
git cherry-pick 18e1a32...cae91f8   相当于(A B] 不包含A
git cherry-pick 18e1a32^...cae91f8  相当于[A B] 包含A

git merge --abort


git tag -d $(git tag -l)

git push http --delete $(git tag -l)

