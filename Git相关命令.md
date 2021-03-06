# Git 常用命令
1. 设置git
    ```bash
    设置git名字 git config --global user.name "BigFly"
    设置git邮箱 git config --global user.email "afforfun@outlook.com"
    ```
2. 远程仓库相关命令
    ```bash
    检出仓库：$ git clone git://github.com/jquery/jquery.git
    查看远程仓库：$ git remote -v
    添加远程仓库：$ git remote add [name] [url]
    删除远程仓库：$ git remote rm [name]
    修改远程仓库：$ git remote set-url --push[name][newUrl]
    拉取远程仓库：$ git pull [remoteName] [localBranchName]
    推送远程仓库：$ git push [remoteName] [localBranchName]
    ```
3. branch操作相关命令
    ```bash
    git branch #查看本地分支
    查看远程分支：$ git branch -r
    创建本地分支：$ git branch [name] 注意新分支创建后不会自动切换为当前分支
    切换分支：$ git checkout [name]
    创建新分支并立即切换到新分支：$ git checkout -b [name]
    
    删除分支：$ git branch -d [name] ---- -d选项只能删除已经参与了合并的分支，对于未有合并的分支是无法删除的。如果想强制删除一个分支，可以使用-D选项
    
    合并分支：$ git merge [name] ----将名称为[name]的分支与当前分支合并
    
    创建远程分支(本地分支push到远程)：$ git push origin [name]
    删除远程分支：$ git push origin :heads/[name]
 
    $ git push origin test:master         // 提交本地test分支作为远程的master分支 //好像只写这一句，远程的github就会自动创建一个test分支
    $ git push origin test:test              // 提交本地test分支作为远程的test分支
    如果想删除远程的分支呢？类似于上面，如果:左边的分支为空，那么将删除:右边的远程的分支。
    $ git push origin :test              // 刚提交到远程的test将被删除，但是本地还会保存的，不用担心
    ```
4. tag操作相关命令
    ```bash
    查看版本：$ git tag
    创建版本：$ git tag [name]
    删除版本：$ git tag -d [name]
    查看远程版本：$ git tag -r
    创建远程版本(本地版本push到远程)：$ git push origin [name]
    删除远程版本：$ git push origin :refs/tags/[name]
    ``` 