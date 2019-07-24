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
										
										














