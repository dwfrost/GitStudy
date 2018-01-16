# GitStudy



从头开始复习git，熟悉git常见指令，安装，操作等

## 安装

### Mac

有两种方法

- brew安装git


> brew官网 https://brew.sh/
>
> brew使用教程 http://blog.csdn.net/andanlan/article/details/51589800

- Xcode安装git

> Xcode7.0后的版本默认安装了git，在终端直接输入git，看是否已安装。

### Windows

> git官网 https://git-scm.com/book/zh/v1/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git

##命令

### 创建版本库

`git init`    创建仓库

`git add file`	添加到git中（放入暂存区）

`git add .	`	一次性全部添加到暂存区

`git commit -m 'commit description'`	提交修改好的文件到本地

`git log`	打印提交日志

`git log —oneline`	打印提交日志的简写版

### 版本管理

`git reset —hard HEAD^`	回滚到上一个版本（HEAD代表当前版本，HEAD^代表上一个版本，HEAD^^代表上两个版本，依次类推）

`git reflog`	查看用户所有的提交记录

`git reset —hard 1231234（提交id`）回滚到1231234的提交版本

`git checkout — file` 	放弃工作区中对file文件的修改,不论暂存区是否有该文件的修改记录，即该命令不会放弃暂存区的修改，**只放弃工作区的修改**

`git reset HEAD file` 	放弃暂存区的内容(即放弃上一次add的内容)，退回到工作区，此时的工作区并不是最新版本，而是在最新版本的基础上用户修改过的内容

### 关联远程仓库

已github为例，假设有两种情况：

1.本地已有git仓库或项目文件，想在github进行关联

- 在github新建项目，不要勾选`Initialize this repository with a README`，默认创建即可
- 关联github，在本地仓库终端输入`git remote add origin git@github.com:dwfrost/GitStudy.git `,注意origin后的内容(SSH)可以从github上复制
- 推送内容到github `git push -u origin master`

2.本地是空文件，想从已有的github项目克隆

- 打开github项目，复制SSH
- 在本地仓库终端输入`git clone git@github.com:dwfrost/GitStudy.git`
- 如果是加入已有的项目，需要检出目标分支到本地，以便推送时本地分支和远程分支同名

### 分支管理

`git branch`	查看当前所在的分支

#### 创建	

`git branch dev`	创建dev分支

#### 切换

`git checkout dev`		切到dev分支

`git checkout -b dev`	创建并切换到dev分支

#### 合并

`git merge dev`	将dev分支合并到当前分支

#### 删除

`git branch -d dev`	删除dev分支(合并后才能删除，且当前分支不能为dev)

`git branch -D dev`	没有合并时，强制删除dev分支

#### 暂存

`git stash`	将修改内容（stash）移到贮藏区

`git stash list`	查看贮藏区的内容（stash）

恢复贮藏区有2种办法：

1.`git stash apply`恢复贮藏区，但贮藏区依旧保留修改内容（stash），如果想删除，使用`git stash drop`

2.`git stash pop`恢复贮藏区的同时删除修改内容（stash）

#### 推送

`git push origin dev`	将dev分支推送到远程仓库（origin）的dev分支上

### 标签管理

`git tag v1.0`	新建标签

`git tag`	查看标签

`git show v1.0`	查看标签信息

`git tag v0.9 7ff4f56`	给某次提交打上标签

`git tag -a v0.9 -m "version 0.9 released" 7ff4f56` `-a`后面是标签名，`-m`后面是标签说明

`git tag -d v1.0`删除标签

## 远程仓库

### 关联SSH

常见的远程仓库有github,码云等，为了方便本地和远程提交代码，需要配置SSH加密，如下：

1.创建SSH key。

创建前，看一下有没有。在用户目录下（mac），终端输入`ls -ah`查看隐藏文件，发现存在`.ssh`文件夹，`cd .ssh`->`open .`，看到存在`id_rsa`和`id_rsa.pub`两个文件，说明已经有了SSH key。

如果没有，就需要创建。

`$ ssh-keygen -t rsa -C "youremail@example.com"`

一路回车，创建成功。

2.添加公钥

`id_rsa`:密钥是用户保管的

`id_rsa.pub`:公钥是放在远程仓库，用于和密钥配对使用。

复制`id_rsa.pub`文件中的内容，打开github，在账户管理选项中添加SSH key。

## 概念

### 工作区

工作区就是git能够管理到的工作区域，也就是该仓库下的所有文件，包括正在修改的和已经存在的文件。

### 暂存区

暂存区是git记录的修改状态，用户在工作区修改文件后，可以用`git add file`将文件修改放入暂存区。

注意，如果用户没有把修改操作放入暂存区，然后直接提交，那git是不会提交用户的操作的，**git只提交暂存区中的修改操作**。所以在开发过程中，我们通常如下操作：

```
* 写代码，写代码……

 * 一个小功能或模块完成，直接提交

 * 如果代码不多，先放入暂存区，然后接着写代码
 * 觉得ok了，放入暂存区，不ok千万别放

* 所有的改动一次性提交

```

另外，如果暂存区存在文件，是不能直接`pull`分支的。

## 举个栗子

### 删除文件

- `git rm file`	相当于 `rm file`，然后`git add file`
- 是否真的删除？
- 是，`git commit -m 'delete file'`
- 否，`git reset HEAD file` + `git checkout -- file`

### 多人协作

- 查看远程库信息，使用`git remote -v`；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；如果使用sourcetree，右键origin，选择检出分支，即可在本地复制远程分支。
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。