master提交时间轴：    02
dev提交时间轴 .    : 01 .     03
执行 git merge dev，显示提交顺序： 01 02 03
执行 git rebase master变基，显示提交顺序： 02 01 03，此时还是在dev分支。这种方法可以解决sqush失败的问题。
