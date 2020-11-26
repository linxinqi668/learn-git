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

- git reset HEAD <file_name>
  将file提到到暂存区的修改退回到工作区。

- 撤销修改总结:
  1. 撤销工作区的修改，使用git checkout
  2. 撤销提交到暂存区的修改，使用git reset HEAD file_name
  3. 撤销提交到分支的修改，直接git reset --hard HEAD^回到上一个版本

