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
git reset --hard HEAD^（Windows上这样写不合适）
因为Windows上cmd控制台中换行符默认是^，而不是\ ，所以有两种替代写法：
加引号：git reset --hard "HEAD^"
加一个^：git reset --hard HEAD^^

还可以往前设置版本（最后的字符串就是版本id号的一部分）
git reset --hard 1094a

查看之前的每一次命令（如果不知道版本id号了，可以这样查看）
git reflog

把暂存区的修改撤销掉（unstage），重新放回工作区（HEAD表示最新的版本。）：
git reset HEAD <file>

丢弃工作区的内容，恢复到最近一次git commit或git add时的状态（一定要有 -- ，而且后面有空格）
git checkout -- <file>


















