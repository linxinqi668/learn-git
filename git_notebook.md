- git init
  创建一个本地仓库

- git add file1.txt file2.txt
  添加file1.txt file2.txt的修改到暂存区，如果添加了未追踪的文件，就会把文件状态修改为追踪。

- git commit -m "version name"
  整合新的修改，产生一个新的版本

- git reset --hard HEAD^ 或者

  git reset --hard commit-id
  回退到上一个版本，实际上就是修改HEAD指针，同时修改文件。

- git reflog
  查看使用过的所有命令，每一次commit命令前都会有commit-id，可以通过这个来查找git log中显示不出来的commit-id。

- 暂存区的概念
  通俗的说，修改发生时保存在工作区，git add负责提交修改到暂存区，所以暂存区就是用来存储跟踪的文件的修改的。 git commit负责整合修改，产生新的版本，并且把新版本添加到分支上。

- git checkout -- <file_name or path>
  "--" is very important
  用于撤销在最近一次commit或者add后的所有修改。只影响被追踪的文件。
  实际上是用版本库中的文件替换本地文件，所以不仅可以用来撤销修改，也可以用来恢复文件。

- git reset HEAD <file_name>
  将file提到到暂存区的修改退回到工作区。

- 撤销修改总结:
  1. 撤销工作区的修改，使用git checkout
  2. 撤销提交到暂存区的修改，使用git reset HEAD file_name
  3. 撤销提交到分支的修改，直接git reset --hard HEAD^回到上一个版本

- git rm file_name -f + git commit -m "xxx"
  删除版本库中的文件
  也可以手动使用rm删除文件然后再git add，因为删除也是修改。

- git remote add origin ***git@server-name:path/repo-name.git***
  example: git@github.com:linxinqi668/learn-git.git
  斜体部分就是一个地址。添加一个远程仓库，并且命名为origin，可以添加多个。

- git push -u origin master
  推送master分支到名为origin的远程仓库的master分支，-u表示关联两个分支。

- git push origin master
  有了-u之后，提交master分支到origin仓库，就会自动到达origin的master分支，因为这俩关联啦。

- git clone git@github.com:linxinqi668/repo_name
  克隆远程仓库，形成一个本地仓库.

- 关于分支的指令
  1. git branch branch_name
     创建一个分支
     
  2. git switch branch_name
     切换到一个分支，新版的git适用
     
  3. git switch -c branch_name
     创建一个新的分支并且完成切换
     
  4. git merge branch_name
     合并某个分支到当前分支，合并就是字面意思。
     注意可能会失败，因为可能会文件存在冲突，比如说两个分支都修改了同一个文件的同一个位置。解决办法就是先git merge，然后再手动修改（merge）冲突文件，再提交，新的版本就是我们期望的合并后的样子。说白了没法合并的文件手动处理，处理完提交的操作就相当于完成合并。
     
     可选参数 --no-ff 表示不使用快速合并。同时最好加上-m选项写一下描述信息。
     快速合并时git log --graph看不到被合并的分支，只会看到合并后master分支到达的版本号。而--no-ff会看到合并了哪一个分支。
     
  5. git branch -d branch_name
     删除一个分支
     
  6. 对分支的理解，或者说对git的理解
     .git这个文件是非常重要的，包含了本地仓库的一切信息。首先一定有一个类似于链表的结构，每一个节点都是一个版本。然后每一个分支都是一个指针，指向一个节点（版本）。可以把分支指针看做是段寄存器，而head指针就用于段内偏移。指针虽然移动了，但是节点仍然会被保存在.git中（个人猜测）。而工作区的样子会随着指针的移动而变化。
     
  7. git branch
     查看当前所有的分支，以及所在分支。
     
  8. git log --graph
     利用图的形式表示版本变化。
  
  9. 分支策略：
     master分支用来发布正式版本。日常开发在dev分支进行。脑子里面要有那个分支图的图像。

