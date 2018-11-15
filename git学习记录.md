git status 查看版本状态是否更新

git diff 文件名    查看改文件变更内容

git log 查看所有commit版本变更信息

git log --pretty=oneline log简化版

HEAD指向的版本是当前版本，因此，git允许我们在版本的历史之间进行切换，使用命令 git reset HEAD commitID

git reset --hard HEAD^ 回滚到上一个版本  HEAD^^就是上上个版本 往上回滚100个版本就是HEAD~100

git log时 每次commit都有一个唯一ID 我们可以通过git reset --hard ID前几位  恢复回滚的事件(即恢复未回滚状态)

但是git log查看commitID是在当前窗口有效，当窗口关闭或者挂机后，通过git log就查看不到commitID了 这个时候可以通过git reflog来查看commitID 它记录了我们每一次命令

git rm 文件名  用于删除文件，如果是错误删除且之前有commit 可以用git reset --hard commitID进行回滚


#####分支管理

首先创建dev分支，然后切换到dev分支

git checkout -b dev【git checkout命令加上-b参数表示创建并切换】相当于以下两条命令：

git branch dev + git checkout dev 【新建分支dev + 切换分支到dev】

然后用git branch 查看当前分支，该命令会列出所有分支，当前分支前面会标一个 * 号

合并dev分支到master分支上：git merge dev

删除分支：git branch -d dev





