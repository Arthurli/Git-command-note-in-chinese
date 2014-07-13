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

