错误的分支名为bugfix
正确的分支名为bugfixOnRelease
先切换到bugfix分支
git checkout bugfix
打开错误分支上提交代码的log，复制第一条log的那个标识，比如d4961b51
git log --oneline  获取log hash
切换到正确的分支bugfixOnRelease
git checkout  bugfixOnRelease
把bugfix分支的commit修改应用到当前分支
git cherry-pick d4961b51 //git cherry-pick用于把另一个本地分支的commit修改应用到当前分支
推代码
git push
切回到提错代码的分支bugfix
git checkout bugfix
代码回退一层 
git reset --hard HEAD^
强推远端同步
git push -f origin bugfix
