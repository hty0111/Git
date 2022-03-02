把当前目录变为Git可以管理的仓库

```c
git init
```

添加文件到暂存区

```c
git add <文件名>
git add .		//提交所有新文件
git add -A		//提交所有变化
git add -u		//提交所有修改和删除的文件
```

提交文件到版本库

```c
git commit -m "提交信息"
```

查看状态：可以看到是否有未提交的文件

```c
git status
```

查看文件的修改情况

```c
git diff	//difference
```

查看提交日志

```c
git log
git log --pretty=oneline
```

回到某一版本

```c
git reset --hard HEAD^	//当前版本为HEAD，上上个版本为HEAD^^，上100个版本为HEAD~100
git reset --hard <版本号>
```

查看每一次命令：用于找寻版本号

```c
git reflog
```

丢弃工作区的修改：1. 工作区修改后未被添加到暂存区 2.添加到暂存区后又在工作区修改

让文件回到最近一次$commit/add$的状态

```c
git checkout -- <文件名>
```

丢弃暂存区的修改：把暂存区的版本会退到工作区

```c
git reset HEAD <file>
```

从版本库删除文件

```c
git rm <文件名>		//单个文件
git rm * -r			  //全部删除
git add .		      //手动删除后更新
git commit -m "删除文件"
```

关联GitHub远程库

```c
git remote add origin git@github.com:hty0111/<repo>.git	//远程库的名字为origin
```

把本地库内容推送到远程库

```c
git push -u origin master	//推送远程库origin的master分支
git push origin master
```

查看远程库信息

```c
git remote -v
```

解除本地和远程的绑定关系

```c
git remote rm origin
```

从远程库克隆本地库

```c
git clone git@server:<user>/<repo>.git
```

创建分支并切换

```v
git switch -c dev		//分支dev
git checkout -b dev
//相当于 git branch dev; git chechout dev
```

查看当前分支

```c
git branch
```

切换到已有分支

```v
git switch master
git checkout master
```

合并分支

```c
git merge dev	//合并dev到当前分支
```

不使用fast forward快速合并：在merge时生成新的commit，所以可以看到分支历史信息

```c
git merge --no-ff -m "info" dev
```

删除分支

```c
git branch -d dev	//已合并
git branch -D dev	//未合并
```

查看分支合并图

```c
git log --graph
```

储藏当前工作现场

```c
git stash
```

查看储藏区

```c
git stash list
```

恢复并删除储藏区内容

```c
git stash pop
//等价于 git stash apply; git stash drop
```

恢复指定的储藏区

```c
git stash apply stash@{0}
```

复制一个特定的提交到当前分支

```c
git cherry-pick <commit_id>
```

查看远程库信息

```c
git remote -v
```

创建远程的分支到本地

```c
git checkout -b dev origin/dev
```

建立本地分支和远程分支的链接

```c
git branch --set-upstream-to <branch-name> origin/<branch-name>
```

把分叉的提交历史整理成一条直线

```c
git rebase
```

查看所有标签

```c
git tag
```

打标签

```c
git tag <标签名>	//对当前分支的最新commit打标签
git tag <标签名> <commit_id>	//对特定版本打标签
git tag -a <标签名> -m "info"
```

查看标签信息

```c
git show <标签名>
```

删除本地标签

```c
git tag -d <标签名>
```

删除远程标签

```c
git push origin :refs/tags/<tagname>
```

推送标签到远程

```c
git push origin <标签名>	//推送某个标签
git push origin --tags	  //推送所有标签
```

强行添加gitignore忽略的文件

```c
git add -f <文件名>
```

查看被忽略原因

```c
git check-ignore -v <文件名>
```

避免被忽略

```c
//.gitignore文件
.*				//排除所有.开头的隐藏文件
!.gitignore		//不排除.gitignore
git -rm -r --cached	//清除添加gitignore之前已经被git跟踪的文件
```

给命令重命名

```c
git config --gobal alias.co checkout
//每个仓库的配置文件在.git/config中，每个用户的配置文件在主目录下的.gitconfig中
```

