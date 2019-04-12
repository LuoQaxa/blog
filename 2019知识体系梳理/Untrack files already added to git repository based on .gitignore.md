1. 确保`.gitignore`已经提交
2. 删除掉本地仓库的所有记录`git rm -r --cached .`
3. 重新添加所有的文件`git add .`
4. `git commit -m ".gitignore fix"`

现在仓库就会应用新的`.gitingore`文件的配置的所有文件，可以推到远程仓库


[参考](http://www.codeblocq.com/2016/01/Untrack-files-already-added-to-git-repository-based-on-gitignore/)