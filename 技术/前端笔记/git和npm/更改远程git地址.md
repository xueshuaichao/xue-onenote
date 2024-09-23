公司的git库地址换了，我怎么更换本地本地库的git地址。

方法一 ： 通过命令直接修改远程仓库地址
git remote 查看所有远程仓库
git remote xxx 查看指定远程仓库地址
git remote set-url origin 你新的远程仓库地址

方法二： 先删除在添加你的远程仓库
git remote rm origin
git remote add origin 你的新远程仓库地址
