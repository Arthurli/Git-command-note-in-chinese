# GIT分支
新建分支
	$ git branch testing
	$ git branch -d testing //删除分支 如果没有合并则失败 -D强制删除
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

