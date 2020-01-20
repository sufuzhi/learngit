初始化
git init 

添加文件到Git仓库
git add <file>    $ git add file1.txt
git commit -m <message>    $ git commit -m "add 3 files."

查看是否有文件修改
git status

查看修改内容
git diff

查看历史记录
git log
让记录显示的有条理
git log --pretty=oneline

版本回退（回退几个版本，最后的数字就是几）
git reset --hard HEAD~1

还可以往前设置版本（最后的字符串就是版本id号的一部分）
git reset --hard 1094a

查看之前的每一次命令（如果不知道版本id号了，可以这样查看）
git reflog