## 廖雪峰 Git教程

```shell
git init	# 初始化仓库
git add <file>	# 添加文件到暂存区
git add .		# 提交所有新文件
git add -A		# 提交所有变化
git add -u		# 提交所有修改和删除的文件
git rm <file>	# 删除版本库的文件
git commit -m "<log>"	# 提交文件到版本库
git remote add origin git@github.com:hty0111/<repo>.git	# 远程库的名字为origin
git push -u origin master	# 将本地的master分支推送远程库origin并关联

git clone	# 克隆到本地
git checkout -b <branch> origin/<branch>	# 创建远程分支到本地
git branch --set-upstream-to <branch> origin/<branch>	# 建立本地分支和远程分支的链接
git pull	# 抓取远程分支

git add -f <file>	# 强行添加gitignore忽略的文件
git check-ignore -v <文件名>	# 查看被忽略原因
git -rm -r --cached	# 清除添加gitignore之前已经被git跟踪的文件
!.gitignore		# 避免被忽略

git status		# 查看状态：可以看到是否有未提交的文件
git diff <file>	# 查看文件的修改情况
git log --graph --pretty=oneline --abbrev-commit	# 查看提交日志
git rebase	# 把分叉的提交历史整理成一条直线

git reflog	# 查看每一次命令：用于找寻版本号
git reset --hard HEAD^		# 当前版本为HEAD，上上个版本为HEAD^^，上100个版本为HEAD~100
git reset --hard <version>	# 根据版本号回退
git reset HEAD <file>		# 丢弃暂存区的修改：把暂存区的版本会退到工作区
git checkout -- [<file>]	# 让工作区（的文件）回到最近一次commit/add的状态

git remote -v	# 查看远程库信息
git remote rm origin	# 解除本地和远程的绑定关系

git branch	# 查看分支
git branch <dev>	# 创建分支
git switch <dev> / git checkout <dev>	# 切换分支
git switch -c <dev>	/ git checkout -b <dev>	# 创建并切换分支
git branch -d <dev>	# 删除已合并分支
git branch -D <dev>	# 删除未合并分支
git merge <dev>		# 将指定分支合并到当前分支
git merge --no-ff -m "<log>" <dev>	# 禁用fast forward则merge时会产生新的commit

git stash	# 储藏当前工作现场
git stash list	# 查看储藏区
git stash apply # 恢复储藏区
git stash drop  # 删除储藏区
git stash pop	# 恢复并删除储藏区
git stash apply stash@{0}	# 恢复到指定的储藏区
git cherry-pick <commit_id>	# 复制一个特定的提交到当前分支

git tag		# 查看所有标签
git show <tag>	# 查看标签信息
git tag <tag>	# 对当前分支的最新commit打标签
git tag <tag> <commit_id>	# 对特定版本打标签
git push origin <tag>	# 推送某个标签
git push origin --tags	# 推送所有标签
git tag -d <tag>	# 删除本地标签
git push origin :refs/tags/<tagname>	# 删除远程标签

git config --global color.ui true	# 显示颜色
git config --global alias.<alias> <cmd>	# 取别名
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
