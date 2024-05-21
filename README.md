![image](https://github.com/hty0111/Git/assets/87237878/0713bff8-1c89-44a3-bd1a-00435ba9e94e)# Git版本管理



## 廖雪峰 Git 教程 & Learn Git Branching

```shell
""" <ref>指的是所有可被git引用的位置，如HEAD/commit/branch/tag等 """

# 基本推送流程
git init                                                    # 初始化仓库
git add <file>                                              # 添加文件到暂存区
git add .                                                   # 提交所有新文件
git add -A                                                  # 提交所有变化
git add -u                                                  # 提交所有修改和删除的文件
git rm <file>                                               # 删除版本库的文件
git commit -m "<log>"                                       # 提交文件到版本库
git remote add origin git@github.com:hty0111/<repo>.git     # 远程库的名字为origin
git push -u/--set-upstream origin/[master] master           # 将本地的master分支推送远程库origin并关联
git push -f origin <local_branch>[:<origin_branch>]         # 强制推送本地src到远程dst

# 版本管理
git checkout HEAD~^2~2                                      # 将HEAD的位置从现在的HEAD上移一次+上移到第二个父节点+上移两次，checkout本质是移动HEAD指针
git reset --hard HEAD^                                      # 当前版本为HEAD，上上个版本为HEAD^^，上100个版本为HEAD~100
git reset --hard <version>                                  # 根据版本号回退
git reset HEAD <file>                                       # 丢弃暂存区的修改：把暂存区的版本会退到工作区
git revert <ref>                                            # 撤销某一次提交并更新（用于远程库）
git checkout -- [<file>]                                    # 让工作区（的文件）回到最近一次commit/add的状态
git update-ref -d HEAD                                      # 撤销第一次commit
git commit --amend -m "<commit>"                            # 修改当前提交的commit内容

# 分支管理
git branch                                                  # 查看分支
git branch <dev> [<ref>]                                    # （在指定的提交处）创建分支
git switch <dev> / git checkout <dev>                       # 切换分支
git switch -c <dev> / git checkout -b <dev>                 # 创建并切换分支
git branch -f <dev> <ref>                                   # 移动分支到指定位置
git branch -d <dev>                                         # 删除已合并分支
git branch -D <dev>                                         # 删除未合并分支
git merge <dev>                                             # 将指定分支复制到当前分支，会创建新的commit
git merge --no-ff -m "<log>" <dev>                          # 禁用fast forward则merge时会产生新的commit
git merge --no-ff --no-commit                               # 不生成提交，可以手动选择需要add的改动文件后再commit
git cherry-pick <ref>                                       # 复制一个特定的提交到当前分支
git rebase <dev1> [<dev2>]                                  # 把（dev2分支）当前分支往dev1分支上整理成一条直线
git rebase -i HEAD^                                         # 交互式整理历史，pick改成drop即删除提交，改成edit可以编辑commit信息。pick; drop; edit: git commit --amend -m <commit>; fixup
git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch <file>'   # 删除某个文件并重新生成commit（用于大文件）

# 远程仓库
git remote -v                                               # 查看远程库信息
git remote rm origin                                        # 解除本地和远程的绑定关系
git clone <url> [repo]                                      # 克隆到本地
git checkout -b <branch> origin/<branch>                    # 创建远程分支到本地
git branch -vv                                              # 查看本地分支和远程库关联情况
git branch -u/--set-upstream-to <branch> origin/<branch>    # 建立本地分支和远程分支的链接，注意与 git push -u 分支顺序相反
git pull origin <origin_branch>[:<local_branch>] [--rebase] # 抓取远程分支与本地当前/指定分支合并 == fetch + merge/rebase
git fetch origin <origin_ref>:<local_branch>                # 抓取远程分支ref位置未被本地branch分支包含的记录（不合并），若origin_ref为空，视为在本地新建local_branch
git merge origin/master -s ours --allow_unrelated_histories # 抓取远程分支后与本地分支合并
git push origin <local_ref>:<origin_branch>                 # 上传所有ref位置未被远程仓库branch分支包含的提交记录，若local_ref为空，视为删除远程仓库的origin_branch

# 子模块
git submodule add <url>                                     # 添加子模块，更新.gitmodules
git submodule update --init --recursive                     # 拉取所有子模块的内容
git clone <url> --recurse-submodules                        # 递归拉取所有子项目 == git clone + git submodule update --init --recursive
git submodule deinit <submodule> [--force]                  # 删除子模块信息，更新.git/config
git rm <submodule>                                          # 删除子模块文件夹，更新.gitmodules

# 日志和记录
git reflog                                                  # 查看每一次命令：用于找寻版本号
git status                                                  # 查看状态：可以看到是否有未提交的文件
git diff <file>                                             # 查看文件的修改情况
git log --graph --oneline --all                             # 查看所有分支的提交日志

# 储藏区
git stash                                                   # 储藏当前工作现场
git stash list                                              # 查看储藏区
git stash apply                                             # 恢复储藏区
git stash drop                                              # 删除储藏区
git stash pop                                               # 恢复并删除储藏区
git stash apply stash@{0}                                   # 恢复到指定的储藏区

# 标签
git tag                                                     # 查看所有标签
git show <tag>                                              # 查看标签信息
git tag <tag> [<ref>]                                       # 对某次提交打标签，默认是HEAD指向的位置
git tag <tag> <ref>                                         # 对特定版本打标签
git push origin <tag>                                       # 推送某个标签
git push origin --tags                                      # 推送所有标签
git tag -d <tag>                                            # 删除本地标签
git push origin :refs/tags/<tagname>                        # 删除远程标签
git describe <ref>                                          # 查找离ref(HEAD/commit/tag)最近的tag

# gitignore
git add -f <file>                                           # 强行添加gitignore忽略的文件
git check-ignore -v <file>                                  # 查看被忽略原因
git rm -r --cached <file>                                   # 清除添加gitignore之前已经被git跟踪的文件
!.gitignore                                                 # 避免被忽略

# 配置文件。C:\Users\HTY\.gitconfig; /home/hty/.gitconfig
git config --global color.ui true                           # 显示颜色
git config --global alias.<alias> <cmd>                     # 取别名
git config --global --unset alias.<alias>                   # 删除别名
git config --global alias.alias "! git config --get-regexp ^alias\. | sed -e s/^alias\.// -e s/\ /\ =\ /"
git config --global alias.lg "log --color --graph --pretty=format:'%C(auto)%h -%C(auto)%d %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --all"
```



## 版本管理策略

`master`分支用来更新大版本，`dev`分支用于开发。

```shell
*   5c6d6f7 (tag: v1.2, origin/master, master) add gun shift
|\
* \   75756af (tag: v1.1) add mahony
|\ \
| | | * 91ceea9 (HEAD -> dev) revise minipc
| | | * 968a5f0 fix minipc receive
| | | * ff359d5 revise can receive
| | | * 231b2d1 update mode task
| | |/
| | * 11926af add gun shift
| |/
| * 0b00845 add mahony
| * 6a174ec mahony
| * f6afc90 add can auto-retransmission; remove redundant timer
| * 46526d7 revise motor offset
|/
* 058ee4d v1.0
```

## 提交格式

```shell
<type>(<scope>): <subject>

1. feat：用于表示新增了一个功能或特性。
2. fix：用于表示修复了一个bug或问题。
3. docs：用于表示更新了文档或注释。
4. style：用于表示对代码风格进行了调整，如格式化代码、修改变量命名等。
5. refactor：用于表示对代码进行了重构，既不是新增功能也不是修复bug，而是对代码结构进行了调整。
6. test：用于表示添加或修改了测试代码。
7. chore：用于表示对构建过程或辅助工具的修改，如更新依赖库、配置文件等。


## 其他教程

[merge策略](https://zhuanlan.zhihu.com/p/192972614)

[版本管理策略](https://blog.csdn.net/yilishuku/article/details/119916978)
