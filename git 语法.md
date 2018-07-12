```bash
git <command> [<revision>...] -- [<file>...]
```
git-命令格式 `<file>`最好加双引号括住 否则，如果文件名有关键字（如git）会出错

#### git工具

* git bash
* sourcetree
* sublime + git 插件
* eclipse + EGIT == HBuilder + EGIT 可以直接看某个文件历史纪录+对比

### 安装好git后,打开 Git Bash

#### git 全局设置

```bash
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
git config --global core.autocrlf false 忽略换行方式
```

--global参数，所有的Git仓库都会使用这个配置

```bash
git config --global <配置名称> <配置的值>
```


#### git init 创建版本库

* `cd <Path>` 切换到目录
* `mkdir <Folder>` 新建文件夹
* `pwd` 用于显示当前目录路径

```bash
git add <file> 将工作库<file>文件添加到暂存区
```

* `git add -A`   // 添加所有改动
* `git add *`    // 添加新建文件和修改，但是不包括删除
* `git add .`    // 添加新建文件和修改，但是不包括删除
* `git add -u`   // 添加修改和删除，但是不包括新建文件


```bash
git commit -m "xxx" 将暂存区的所有内容提交到当前分支
```

```bash
git status 版本库状态
```

```bash
git diff <revision> -- <file> 查看变更内容 <revision>默认是当前版本 默认时全部已经修改文件
```

`$ git diff HEAD -- "git 语法.txt"` 查看工作区与版本区当前版本区别

```bash
git log 查看全部文件提交历史（默认显示3个历史 enter显示更多 一直enter可以一直显示到最初）
```

```bash
commit 3628164fb26d48395383f8f31179f24e0882e1e0    <commit id>
Author: Michael Liao <askxuefeng@gmail.com>		   <author>
Date:   Tue Aug 20 15:11:49 2013 +0800			   <date>

	append GPL									   <描述信息>
```

	git log <path>+<file> 查看指定文件提交历史（enter显示更多）   git log test/test.html
	git log -p <path>+<file> 查看指定文件提交历史详情（enter显示更多）   git log -p test/test.html
	git log --pretty=oneline 每个记录以一行的方式简化，查看全部文件提交历史
		/*
			3628164fb26d48395383f8f31179f24e0882e1e0 append GPL				<commit id> + <描述信息>
		*/

	git reset --hard HEAD^ 回退到上一个版本
		HEAD当前版本 HEAD^上一个版本 HEAD^^上上一个版本 HEAD~100上100个版本 可以小写（head）
	git reset --hard commit_id 回退到指定<commit id>的版本
	git reflog 查看命令历史 会显示<commit id>，可以用来回退到未来版本

	git checkout -- <file> 丢弃工作区的修改 --好重要(其实好像没有都可以)，没有--就变成了“切换到另一个分支”的命令
	git reset <revision> <file> 丢弃工作区的修改 --好重要(其实好像没有都可以)，没有--就变成了“切换到另一个分支”的命令
		/*
			git reset --mixed：此为默认方式，不带任何参数的git reset，即时这种方式，它回退到某个版本，只保留源码，回退commit和index信息
		    git reset --soft：回退到某个版本，只回退了commit的信息，不会恢复到index file一级。如果还要提交，直接commit即可
		    git reset --hard：彻底回退到某个版本，本地的源码也会变为上一个版本的内容，此命令 慎用！
		*/

删除文件
	git rm <file> 在版本库删除指定文件  删除完之后直接git commit -m "XXX"
		/*
			rm 删除文件
		*/

远程仓库
	ssh-keygen -t rsa -C "youremail@example.com"  创建SSH key。 在用户主目录里找到.ssh目录 id_rsa.pub是公钥

	git remote add origin git@github.com:<远程帐号库>/<仓库名>.git 添加远程版本库
	git push -u origin master 将本地库推送到远程库 -u参数时第一次推送的时候，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来。将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。
	如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push。
		以后可以不加-u参数
		git push origin master
		可以简写为
		git push origin 或者 git push

	git pull origin 从远程库(origin)获取并合并到当前本地本地分支 等价于 git push

	git pull origin master:my_test 将远程库(origin)的master分支拉取并合并到本地的my_test分支上。

	git pull origin master 将远程库(origin)的master分支拉取并合并到当前分支上(所以要注意了，如果当前分支不是master，会将当前分支合并成master那样，慎用)。


	git clone <url> 克隆远程库
		git支持多种协议 ssh协议 git clone git@github.com:cccikov/cccgit.git
						https协议 git clone https://github.com/cccikov/cccgit.git

分支作用
	在Git里，这个分支叫主分支，即master分支。
	分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。
	git branch 查看分支
	git branch <name> 创建分支
	git checkout <name> 切换分支
	git checkout -b <name> 创建+切换分支
	git merge <name> 合并某分支到当前分支
		git merge --no-ff -m "merge with no-ff" dev   --no-ff参数，强制禁用Fast forward模式
	git branch -d <name> 删除分支

	git log --graph 查看分支合并图
**`git log --graph --pretty=oneline --abbrev-commit`  `--pretty=oneline`一行显示 ; `--abbrev-commit`简化commit id**

在实际开发中，我们应该按照几个基本原则进行分支管理：
	首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
	那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
	你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
	所以，团队合作的分支看起来就像这样：
