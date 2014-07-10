# GIT分支
新建分支
	$ git branch testing
	$ git branch -d testing //删除分支
新建分支之后不会切换到新建分支中去需要切换到分支中去
	$ git checkout testing
之前的两个步骤也可以合并成为一个命令
	$ git checkout -b testing

分支合并 
	$ git merge testing