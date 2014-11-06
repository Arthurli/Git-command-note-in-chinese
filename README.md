# GIT 学习从此处开始
## Git的一些概念
首先一点就是git这种版本控制区别于SVN的很重要的一点就是它 **保存的是文件的快照**，而不是保存文件的修改，这样做的好处是不用每次都把所有的修改都计算一遍，不好的地方当然就是git库的大小，空间换时间吗...  

Git还有一个概念感觉就是其实不存在本质上的本地和远程的区别，当然这是我自己瞎想的，其实感觉就是一个个git的镜像，区别是从这个镜像获取修改还是，把修改push到哪个镜像

“Git 使用 SHA-1 算法计算数据的校验和，通过对文件的内容或目录的结构计算出一个 SHA-1 哈希值，作为指纹字符串。该字串由 40 个十六进制字符（0-9 及 a-f）组成”,git就是这样检验文件是否被修改过的。

关键的是记住一个概念，在GIT本地的代码有三个区域，分为已提交(committed),已修改(modified)和已暂存(staged),这也就是我们在本地代码修改的三种状态。 

## Git 的安装和帮助
	$ git config //git 相关的设置，会优先查询本地 .git/config 文件
	$ git help <verb>
	$ git <verb> --help 
	$ man git-<verb>
	
# Git基础
## 一次简单的git操作

	$ git init // 在当前路径下初始化git库，生成.git文件
	$ git add *.c // 使用add方法把文件的修改移动到暂存区 
	$ git add README
	$ git commit -m "First commit" // 把暂存取得得修改提交
	
	$ git clone git://github.com/schacon/grit.git // 从服务器克隆git,会在当前路径生成文件夹grit,当然也可以在最后加上文件夹名，则生成对应的文件夹保存git
	$ git clone git://github.com/schacon/grit.git GitCode
	 /**
	  *git clone 支持多种传输协议，例如ssh,git,https... 当然也支持本地克隆
	  */

## 我们来查看git状态

在这里再说说git的文件状态，如下图所示，文件又多出了两个状态，未被跟踪和未修改，其中未被跟踪的意思就是git不会记录该文件的修改
在这里再说下 `git add` 命令，在没有跟踪的事后这个命令会跟踪该文件或者该目录，否则会把该文件的修改放置到暂存区 
 
	 $ git status  // 查看当前文件的修改状态

![](IMG/git_lifecycle.tiff)

## 让我们来忽略一些文件
在根目录我们可以创建一个`.gitignore`的文件来设置忽略的文件  
文件 .gitignore 的格式规范如下：
> * 所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。
> * 可以使用标准的 glob 模式匹配。 
> * 匹配模式最后跟反斜杠（/）说明要忽略的是目录。 
> * 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。 

那么什么是 glob 模式呢：[百度百科](http://baike.baidu.com/view/4019153.htm) 
看个例子就什么都知道了

>  # 此为注释 – 将被 Git 忽略  
>  *.a       # 忽略所有 .a 结尾的文件  
>  !lib.a    # 但 lib.a 除外  
>  /TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO  
>  build/    # 忽略 build/ 目录下的所有文件  
>  doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
 
## 查看文件差异
此命令比较的是本地暂存文件修改,commits,分支等不同情况下文件的差异

	$ git diff //查看修改文件和原始文件的差别
	$ git diff --cached //已经暂存起来的文件和上次提交时的快照之间的差异

	

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

	$git commit --amend //撤销最后一次操作
	$ git reset HEAD benchmarks.rb //撤销已经暂存文件
	$ git checkout -- benchmarks.rb //回到以前的版本  这里还需要实验

## 远程仓库使用

	$ git remote //获取远程库的名字
	$ git remote -v //获取远程库地址
	$ git push origin master //推送到远程库
	$ git remote show origin //查看远程库信息
	$ git remote add pb git://github.com/paulboone/ticgit.git //添加远程库
	$ git remote rename pb paul //重命名
	$ git remote rm paul //删除
	$ git fetch \[remote-name]  //抓取远程库
	$ git pull //更新远程库代码

## 打标签 此处无兴趣


# GIT分支
新建分支

	$ git branch testing
	$ git branch -d testing //删除分支 如果没有合并则失败 -D

强制删除
新建分支之后不会切换到新建分支中去需要切换到分支中去

	$ git checkout testing

之前的两个步骤也可以合并成为一个命令

	$ git checkout -b testing

分支合并 

	$ git merge testing

查看分支最后一次提交信息

	$ git branch -v
    
查看已经与当前分支合并的分支或者没有合并的分支

	$ git branch --merged
	$ git branch --no-merged
	
	
	
	##GIT 衍合

rebse就是把抛弃原始提交 在原有基础上发现不同 进行修改(这点说的有点纠结)

	$ git checkout 001
	$ git rebase mastar

合并commit

如果你使用git做版本控管，在一個branch上開發一段時間後，commits看起來又多又雜亂，這個時候你可能會需要整理你的commits，將多個commits合併成1個，而git提供了一個指令可以幫助你完成這件事情：git rebase -i

一個簡單的範例，目標是： 將原本git log
	
	a
	b1
	b2
变成
  
	a
	b
###Step1：$ git rebase -i <不變動的commit的SHA-1>
例如此例就是a的SHA-1 (可用git log查看該commit的版本號)

	$ git rebase -i 49687a0a646954afdf3f4dae1f914ea793341ea2
按下enter後會進到編輯模式

###Step2：squash

pick 033beb4 b1
pick d426a8a b2

	# Rebase 49687a0..d426a8a onto 49687a0
	#
	# Commands:
	#  p, pick = use commit
	#  r, reword = use commit, but edit the commit message
	#  e, edit = use commit, but stop for amending
	#  s, squash = use commit, but meld into previous commit
	#  f, fixup = like "squash", but discard this commit's log message
	#  x, exec = run command (the rest of the line) using shell
	#
	# If you remove a line here THAT COMMIT WILL BE LOST.
	# However, if you remove everything, the rebase will be aborted.
	#
分成兩個區塊：第一是rebase interactive要執行的指令，第二是每個指令的簡單說明(‘#’後的是注解)。在這個例子裡面，我們至少要搞懂以下兩個：

	pick 033beb4 b1
	squash d426a8a b2
也就是將d426a8a這個版本的commit併到版本號033beb4的commit，對應我們的例子，就是將b2合併到b1這個commit。

在編輯完成後按下esc，打上:wq 儲存離開。

###Step3：接著輸入新的commit message
剛進來這個畫面，它會告訴你原本兩個commit messages分別是b1和b2，現在你要輸入新的commit message，也就是b，建議可以把原本的訊息註解掉。

	b
	# This is a combination of 2 commits.
	# The first commit's message is:
	# b1
	#
	# This is the 2nd commit message:
	#
	# b2
	#
	# Please enter the commit message for your changes. Lines starting
	# with '#' will be ignored, and an empty message aborts the commit.
	# Not currently on any branch.
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       modified:   a.txt
	#
編輯完成後一樣儲存離開。沒意外的話，會出現這樣的訊息：Successfully rebased and updated refs/heads/develop.。最後可以用git log這個指令來檢驗commits是不是變成我們要的樣子：

	-> % git log
	commit 27a1ff53137c6a35da1a83f4aa9ab7f652a5b4b2
	Author: ChiaChia Lee <spiderman0103@gmail.com>
	Date:   Fri Dec 30 15:07:38 2011 +0800

	    b

	commit 49687a0a646954afdf3f4dae1f914ea793341ea2
	Author: ChiaChia Lee <spiderman0103@gmail.com>
	Date:   Fri Dec 30 15:07:29 2011 +0800

	    a

