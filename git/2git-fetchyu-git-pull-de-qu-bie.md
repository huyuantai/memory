
# Git fetch 自己手动合并 

git fetch origin master:tmp 
//在本地新建一个temp分支，并将远程origin仓库的master分支代码下载到本地temp分支
git diff tmp 
//来比较本地代码与刚刚从远程下载下来的代码的区别
git merge tmp
//合并temp分支到本地的master分支
git branch -d temp
//如果不想保留temp分支 可以用这步删除


# Git pull 自动合并

git pull <远程主机名> <远程分支名>:<本地分支名>
//取回远程主机某个分支的更新，再与本地的指定分支合并。