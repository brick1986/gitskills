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

git log --graph    查看分支合并图

git status      查看当前分支状态


分支策略：

master 分支， 稳定，只用作发布版本

dev 分支， 不稳定，用做开发，频繁更新。 dev测试得到一个稳定版本，将dev合并到master上用作发布

成员分支， 每个用户的分支，开发完成后合并分支到 dev。 1. edit on brick-branchxxxxxx
