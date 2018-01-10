# GitStudy



从头开始复习git，熟悉git常见指令，安装，操作等

##命令

git init    创建仓库

git add	添加到git中（但没有提及到本地，只是放入暂存区）

git commit -m 'commit description'	提及修改好的文件到本地

git log	打印提交日志

git log —oneline	打印提及日志的简写版

git reset —hard HEAD^	回滚到上一个版本（HEAD代表当前版本，HEAD^代表上一个版本，HEAD^^代表上两个版本，依次类推）

git reflog	查看用户所有的提交记录

git reset —hard 1231234（提交id）回滚到1231234的提交版本