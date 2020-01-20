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
也用于恢复误删文件
git checkout -- <file>

删除文件
手动删除，然后 git rm <file> 或者 git add<file>，然后 git commit
----------------------------------------------------------------------------------------------
连接远程仓库

用户主目录下创建SSH Key（每台需要推送的电脑都要创建一个不同的key）
ssh-keygen -t rsa -C "youremail@example.com"

登陆GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容

把本地仓库关联远程仓库
git remote add origin git@github.com:sufuzhi/learngit.git
或
git remote add origin https://github.com/sufuzhi/learngit.git

推送（origin是远程库的名字，首次推送加 -u，以后可以不加）
git push -u origin master

快速克隆仓库
git clone git@github.com:sufuzhi/gitskills.git
----------------------------------------------------------------------------------------------
使用分支

创建分支
git branch <name>

切换分支：
git checkout <name>
或者
git switch <name>

创建+切换分支：
git checkout -b <name>
或者
git switch -c <name>

查看当前所有分支：
git branch

合并指定分支到当前分支
git merge <name>

删除指定分支
git branch -d <name>





