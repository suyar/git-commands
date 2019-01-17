# Git Commands
> ### 开始使用git  

* 设置用户名  
`git config --global user.name "Your Name"`  
* 设置邮箱  
`git config --global user.email "email@example.com"`  
* 创建仓库（当前目录）  
`git init`  
* 添加文件  
`git add <file>` _添加指定文件_  
`git add .` _添加所有改变的文件_  
_注：如果add后又修改了文件，还要再add一次之后再commit_  
* 提交  
`git commit -m "提交说明"`  
* 查看状态  
`git status`  
* 查看修改  
`git diff <file>` _查看单个文件的更改_  
`git diff` _查看所有文件的更改_  
* 查看历史提交  
`git log`  
`git log --pretty=oneline` _一次提交显示为一行_  
`git blame <file>` _查看一个文件的修改记录(谁在什么事件修改了什么)_  
* 查看历史命令  
`git reflog`

> ### 版本控制  

* 版本回退  
`git reset --hard HEAD` _撤销所有未提交的操作，包括add_  
`git reset --hard HEAD^` _回退到上一个版本_  
`git reset --hard HEAD^^` _回退到上两个版本_  
`git reset --hard HEAD~100` _回退到上100个版本_  
`git reset --hard <commit>` _回退到指定版本_  
`git checkout -- <file>` _丢弃工作区的修改，如果文件add到了暂存区又做了修改，则恢复到暂存区，否则恢复到版本库的状态，如果文件删除了，则回复到版本库的文件_  
`git reset HEAD <file>` _把暂存区的修改撤销掉，重新放回工作区_  
_注：_  
_场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令 `git checkout -- <file>`_  
_场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令 `git reset HEAD <file>`，就回到了场景1，第二步按场景1操作_  
_场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退，不过前提是没有推送到远程库_  
* 删除/重命名  
`git rm <file>` _删除文件，尽管文件已经添加到暂存区(add)_  
`git rm --cached <file>` _把文件从版本库、暂存区删掉，但是保留硬盘文件_  
`git mv <file> <other file>` _重命名文件_  

> ### 远程仓库  

* 创建ssh密钥  
`ssh-keygen -t rsa -C "youremail@example.com"`  
_注：一路回车，在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人，复制内容，在github上添加_  
* 远程仓库  
`git remote add origin git@github.com:michaelliao/learngit.git` _关联远程仓库,远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库_  
`git push -u origin master` _我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令_  
`git push origin master` _把本地master分支的最新修改推送至GitHub_  
`git clone git@github.com:michaelliao/gitskills.git` _从远程仓库克隆，Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin_  
`git remote` _查看远程库的信息_  
`git remote -v` _查看远程库的详细信息_  
`git push origin master` _推送远程分支，就是把该分支上的所有本地提交推送到远程库_  
`git pull` _从远程库拉取_  
`git checkout -b <branch> origin/<branch>` _创建远程origin的branch分支到本地_  
`git branch --set-upstream <branch> origin/<branch>` _指定本地dev分支与远程origin/dev分支的链接_  
`git push origin --delete <branch>` _删除远程分支_  

> ### 分支管理  

* 创建分支  
`git checkout -b <branch>` _创建分支并切换过去，相当于执行了 `git branch <branch>` 和 `git checkout <branch>`_  
`git branch` _查看当前分支_  
`git checkout <branch>` _切换分支_  
`git merge <branch>` _合并分支到当前分支，有冲突修改后再add、commit_  
`git merge --no-ff -m "合并信息" <branch>` _禁止快速合并_  
`git branch -d <branch>` _删除分支_  
`git branch -D <branch>` _强行删除分支(未合并的分支)_  
* BUG分支  
`git stash` _把当前工作现场“储藏”起来，等以后恢复现场后继续工作_  
`git stash list` _查看stash_  
`git stash apply` _恢复现场_  
`git stash drop` _删除保存的stash_  
`git stash pop` _恢复并删除stash_  
`git stash apply stash@{0}` _多次stash，恢复指定的stash_  

> ### 标签管理  

* 创建标签  
`git tag <name>` _创建标签_  
`git tag` _查看所有标签_  
`git tag <name> <commit>` _在指定的版本版本id打标签_  
`git show <name>` _查看标签信息_  
`git tag -a <name> -m "说明" <commit>` _创建带有说明的标签_  
* 操作标签  
`git tag -d <name>` _删除标签_  
`git push origin <name>` _推送某个标签到远程仓库_  
`git push origin --tags` _一次性推送全部尚未推送到远程的本地标签_  
`git push origin :refs/tags/<name>` _删除远程标签(删除远程标签之前要先删除本地标签)_  

> ### 导出

`git archive -o /d/www/update.zip HEAD $(git diff HEAD HEAD^ --name-only)` _导出和上个版本差异的文件_  
`git archive -o /d/update/project.zip master -0` _导出纯净项目源码_  
`git config core.quotepath false` _如果导出的文件有中文显示成Unicode导致导出失败，配置这个_  

> ### 其他配置

`git config core.gitproxy=socks5://127.0.0.1:1080` _设置socket5代理_  
`git config core.filemode false` _忽略文件权限差异_  

