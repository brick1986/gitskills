# gitskills

常用的命令：

git add <filename>    将本地修改增加到stage(暂存区)

git commit -m "message"  将stage里暂存的 修改 提交到本地分支

git checkout -- <filename>   丢弃本地未提交到stage的修改

git reset HEAD <filename>  回退到指定的版本号，HEAD表示最新的版本

git remote add origin git@github.com:brick1986/learngit.git    关联一个远程库

git push -u origin master     第一次推送master分支所有内容，-u参数 可以把本地分支和远程分支关联起来，之后推送可以简化命令

git push <origin> <master>    将本地分支的修改推送到远程库

git clone git@github.com:brick1986/gitskills.git   克隆一个远程仓库


分支相关命令：

git branch dev     创建一个叫 dev 的分支

git checkout dev   切换到 dev 分支

git checkout -b dev   创建dev分支并且切换到dev分支，是一个简写的命令，合并了创建和切换

git branch		查看当前所有分支，当前分支前会有一个*号

git merge <branch_name>  将指定分支branch_name合并到当前分支

git branch -d <branch_name>  删除指定分支

git branch -D <branch_name>  当要删除的分支包含为merge的内容时，-D参数可以强制删除指定分支

git log --graph    查看分支合并图

git status      查看当前分支状态


分支策略：

master 分支， 稳定，只用作发布版本

dev 分支， 不稳定，用做开发，频繁更新。 dev测试得到一个稳定版本，将dev合并到master上用作发布

成员分支， 每个用户的分支，开发完成后合并分支到 dev。 


Bug 分支：

git stash    储藏当前修改，执行完命令以后，当前分支处于clean状态，可以在原有版本上修改指定bug

git stash list   查看储藏的工作现场

git stash apply  恢复工作现场

git stash drop   删除储藏的工作现场

git stash pop    恢复工作现场并删除储藏

git stash apply stash@{0}	 多次储藏后，恢复指定的工作现场


多人协作：

git remote	    查看远程仓库信息

git remote -v   查看远程仓库详细信息

git push <origin> <master/dev> 		推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上

										1. master分支是主分支，因此要时刻与远程同步；

										2. dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

										3. bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

										4. feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
										
										
多人协作的一个示例：

1. 模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆：

	git clone git@github.com:michaelliao/learngit.git
	
2. 克隆完成，默认情况下，小伙伴只能看到master分支：

	git branch

3. 小伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支：

	git checkout -b dev origin/dev
	
4. 小伙伴可以在dev上继续修改，然后，时不时地把dev分支push到远程：

	git add env.txt
	
	git commit -m "add env"
	
	git push origin dev
	
5. 小伙伴已经向origin/dev分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送：

	git add env.txt
	
	git commit -m "add new env"

	git push origin dev
	
	这个时候提示了错误信息：
	To github.com:michaelliao/learngit.git
	 ! [rejected]        dev -> dev (non-fast-forward)
	error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
	hint: Updates were rejected because the tip of your current branch is behind
	hint: its remote counterpart. Integrate the remote changes (e.g.
	hint: 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.
	
6. 推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：

	git pull
	
	又提示了错误信息：
	There is no tracking information for the current branch.
	Please specify which branch you want to merge with.
	See git-pull(1) for details.

		git pull <remote> <branch>

	If you wish to set tracking information for this branch you can do so with:

		git branch --set-upstream-to=origin/<branch> dev
		
7. git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：

	git branch --set-upstream-to=origin/dev dev
	
8. 设置完链接，再pull：

	git pull
	
	提示了冲突的信息：
	Auto-merging env.txt
	CONFLICT (add/add): Merge conflict in env.txt
	Automatic merge failed; fix conflicts and then commit the result.
	
9. git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：

	git commit -m "fix env conflict"
	
	git push origin dev
	

总结流程，多人协作的工作模式通常是这样：

	a. 首先，可以试图用git push origin <branch-name>推送自己的修改；

	b. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

	c. 如果合并有冲突，则解决冲突，并在本地提交；

	d. 没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

	e. 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

	这就是多人协作的工作模式，一旦熟悉了，就非常简单。













