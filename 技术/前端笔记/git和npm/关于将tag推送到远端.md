查看文件状态 ：git status
切换分支 ：git checkout [分支名]
新增文件 ：git add [文件名]
新增所有文件 ：git add -all
删除文件 ：git rm [文件名]
提交代码到本地仓库 ：git commit -m "说明"
将本地仓库代码推送到远程 ：git push
代码回滚：(push前一定检查好，不然回滚有很多坑)
查看日志 ：git log
回滚到上一个版本 ：git reset --hard HEAD^
到指定版本 ：git reset --hard [commit hash]
创建分支
创建分支 ：git checkout -b [分支名]
删除分支 ：git branch -d [分支名]
推送分支到远程 ：git push origin [分支名]
关联远程分支 ：git push --set-upstream origin [分支名]
合并分支代码
整个分支合并：git checkout [被合并的分支名]
根据[需求|commit hash]合并：
  单个版本号合并：git cherry-pick [commit hash]
  多个版本号合并：git rebase   (好几种用法，自行百度)


对发布分支打tag(tag名请跟发布分支名保持一致)
打tag ：git tag -a [tag名] -m "此次tag备注"
同时我们也可以像特定的commit添加标签，使用该commit对应的SHA值即可
git tag -a <版本号> <SHA值> -m "<备注信息>"
比如 git tag -a 1.0.0 0c3b62d -m "Release Edition v1.0.0" 就是为SHA为0c3b62d的这次提交打了1.0发行版的tag

推送所有tag ：git push --tags
删除本地标签 ：git tag -d [tag名]


问题：Git本地没有push,本地仓库打了tag之后只把tag push了，远程仓库该tag下是最新的代码吗？

答案一：这个问题很好玩，也很简单，只要自己实际操作一把就可以发现，该 tag 下的代码是最新的。不过要搞明白为什么，还需要明白 Git 里的 对象 和 引用 这两个概念。
Git 一共有四种类型的对象：数据对象（blob object）、树对象（tree object）、提交对象（commit object）和 标签对象（tag object）。其中标签对象和提交对象非常类似，可以理解为是提交对象的一个引用。我们每次运行 git add 和 git commit 命令时，实际上是将被改写的文件保存为数据对象和树对象，并创建一个提交对象指向顶层的树对象，这些对象保存在 .git/objects 目录下。
其次，Git 一共有三种类型的引用：HEAD 引用、标签引用 和 远程引用，他们分别保存在 refs/heads、refs/tags 和 refs/remotes 三个目录下。HEAD 引用代表你创建的代码分支，标签引用代表你创建的所有标签。你可以打开三个目录下的文件看看，实际上就是一个纯文本文件，里面记录着提交对象（或标签对象）的 SHA-1 哈希值，代表这个引用指向哪一次提交。
所以，当你推一个 tag 到远程仓库时，是在远程仓库的 refs/tags 目录下创建一个标签引用，它要指向一个提交对象，而这个对象由于你还没 push，也会打包发送到服务器上。但是，由于 HEAD 引用并没有更新，所以随便 checkout 到哪个分支都看不到这次提交，只有 checkout 到指定的 tag，才能看到这次提交。

答案二：
是最新的。
git add .
git commit -m 'test'
git tag 'v1.0.0'
git push --tags
如果你是这么操作的，那么远程仓库中，注释为test的提交只会出现在 tag v1.0.0中
