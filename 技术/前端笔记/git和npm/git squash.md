gitlab上合并的时候，会勾上squash，但这时候因为提交记录的问题，导致squash失败，
所以要先在本地squash

我们有三个分支，master，develop以及feature特性分支，假定我们开发时使用的是feature分支，我们来这里查看提交记录
在master上新拉一个分支master-squash，将本地开发分支develop合并到master-squash，

git merge --squash develop
git commit -m '修复了xxx'
git push origin master

