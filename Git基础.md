# Git基础
## 本地创建git
开始对某个项目使用git的时候使用,之后就会出现一个.git的文件，用来存储所有git相关的信息
	$ git init
之后我们来进行第一次提交
	$ git add *.c
	$ git add README
	$ git commit -m "First commit"
## 从服务器下载git
我们可以从服务器下载git程序
	$ git clone git://github.com/schacon/grit.git

## 我们来查看git状态
	$ git status
![][image-1]

## 让我们来跟踪一个文件
	$ git add README

## 查看已暂存和未暂存的更新
此命令比较的是工作目录中当前文件和暂存区域快照之间的差异
	$ git diff
若要看已经暂存起来的文件和上次提交时的快照之间的差异
	$ git diff --cached

## 提交
	$ git commit //进入vi填写comiit信息
	$ git commit -m "first commit" //直接commit
	$ git commit -a -m "first commit" //直接commit 所有已经跟踪的文件 不需要add

## 移除文件 移动文件
	$ rm grit.gemspec //删除新添加文件，之后需要add 删除操作
	$ git rm grit.gemspec
	$ git rm -f grit.gemspec //强力删除
	$ git rm --cached grit.gemspec //缓存区删除 工作区保存

	$ git mv grit.gemspec //移动文件

## 查看提交历史
	$ git log
	$ git log -p -2 //-p显示每次差异 -2显示最近2次
	$ git log --stat //仅改变增改行统计
	$ git log --pretty=oneline //比如用 oneline 将每个提交放在一行显示,这在提交数很大时非常有用。另外还有 short,full 和 fuller 可以用
	$ git log --pretty=format:"%h - %an, %ar : %s"

> 选项 说明  
> %H 提交对象(commit)的完整哈希字串 %h 提交对象的简短哈希字串  
> %T 树对象(tree)的完整哈希字串  
> %t 树对象的简短哈希字串  
> %P 父对象(parent)的完整哈希字串 %p 父对象的简短哈希字串
> %an 作者(author)的名字  
> %ae 作者的电子邮件地址  
> %ad 作者修订日期(可以用 -date= 选项定制格式) %ar 作者修订日期,按多久以前的方式显示  
> %cn 提交者(committer)的名字  
> %ce 提交者的电子邮件地址  
> %cd 提交日期  
> %cr 提交日期,按多久以前的方式显示  
> %s 提交说明

另外还有按照时间作限制的选项,比如 --since 和 --until。下面的命令列出所有最近 两周内的提交:
	git log --since=2.weeks

> 选项 说明  
> -(n) 仅显示最近的 n 条提交  
> --since, --after 仅显示指定时间之后的提交。 --until, --before 仅显示指定时间之前的提交。 --author 仅显示指定作者相关的提交。 --committer 仅显示指定提交者相关的提交。

## 撤销操作
	git commit --amend //撤销最后一次操作
	$ git reset HEAD benchmarks.rb //撤销已经暂存文件
	$ git checkout -- benchmarks.rb //回到以前的版本  这里还需要实验

## 远程仓库使用
	$ git remote //获取远程库的名字
	$ git remote -v //获取远程库地址
	$ git push origin master //推送到远程库
	$ git remote show origin //查看远程库信息
	git remote add pb git://github.com/paulboone/ticgit.git //添加远程库
	$ git remote rename pb paul //重命名
	$ git remote rm paul //删除
	$ git fetch \[remote-name]  //抓取远程库
	$ git pull //更新远程库代码

## 打标签 此处无兴趣










[image-1]:	git_lifecycle.tiff