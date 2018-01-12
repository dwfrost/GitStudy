# GitStudy



从头开始复习git，熟悉git常见指令，安装，操作等

##命令

git init    创建仓库

git add file	添加到git中（但没有提及到本地，只是放入暂存区）

git commit -m 'commit description'	提及修改好的文件到本地

git log	打印提交日志

git log —oneline	打印提及日志的简写版

git reset —hard HEAD^	回滚到上一个版本（HEAD代表当前版本，HEAD^代表上一个版本，HEAD^^代表上两个版本，依次类推）

git reflog	查看用户所有的提交记录

git reset —hard 1231234（提交id）回滚到1231234的提交版本

## 概念

### 工作区

工作区就是git能够管理到的工作区域，也就是该仓库下的所有文件，包括正在修改的和已经存在的文件。

### 暂存区

暂存区是git记录的修改状态，用户在工作区修改文件后，可以用`git add file`将文件修改放入暂存区。

注意，如果用户没有把修改操作放入暂存区，然后直接提交，那git是不会提交用户的操作的，**git只提交暂存区中的修改操作**。

另外，如果暂存区存在文件，是不能直接更新分支的。