初始化
git init 

添加文件到Git仓库
git add <file>    $ git add file1.txt
git commit -m <message>    $ git commit -m "add 3 files."

查看是否有文件修改
git status

查看修改内容
git diff

查看历史记录（退出方法：输入法英文状态下按字母Q键）
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
强制推送在后面加 -f，但是这会使库里原来的文件消失

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

当Git无法自动合并分支时，把Git合并失败的文件手动编辑为我们希望的内容，再提交。
查看合并情况：
git log --graph --pretty=oneline --abbrev-commit
--graph 可以看到合并图
--abbrev-commit 不显示完整的40字节十六进制提交对象名称，只显示部分前缀
-------------------------------------------------------------------------------------
分支管理策略
强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息
--no-ff参数，表示禁用Fast forward
git merge --no-ff -m "merge with no-ff" dev

你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
----------------------------------------------------------------------------------------------------
Bug分支（）

暂存工作区：
git stash

查看暂存内容
git stash list

取出暂存内容，并删除暂存区内容：
git stash pop

当手头工作没有完成，却需要临时修复bug时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场；
（用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；另一种方式是用git stash pop，恢复的同时把stash内容也删了）

赋值某一次commit到本分支：
git cherry-pick <commit>

在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

强行删除分支：
git branch -D <name>
开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。
-----------------------------------------------------------------------------------------
多人协作

查看远程库信息
git remote -v

推送分支，指定本地分支，Git就会把该分支推送到远程库对应的远程分支上：
git push origin master

要在dev分支上开发，方法：
（一）新建分支前，先拉取远程
git pull
然后创建远程origin的dev分支到本地：
git checkout -b dev origin/dev

（二）如果已经创建了分支dev，拉取远程可能是失败的
原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：
git branch --set-upstream-to=origin/dev dev
然后可以推送和拉取了；如果拉取后有冲突，先手动修改合并，在提交；

变基
git rebase
rebase操作可以把本地未push的分叉提交历史整理成直线；
rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。
--------------------------------------------------------------------------------------------
创建标签
git tag v1.0

查看所有标签
git tag

对某次提交打标签（commit id）
git tag v0.9 f52c633

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：
$ git tag -a v0.1 -m "version 0.1 released" 1094adb

查看标签信息
git show <tagname>

删除标签
git tag -d <tagname>

推送某个标签到远程，使用命令
git push origin <tagname>

一次性推送全部尚未推送到远程的本地标签：
$ git push origin --tags

如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
git tag -d v0.9
然后，从远程删除。删除命令也是push，但是格式如下：
$ git push origin :refs/tags/v0.9
------------------------------------------------------------------------------------
使用GitHub

访问bootstrap的项目主页https://github.com/twbs/bootstrap，点“Fork”就在自己的账号下克隆了一个bootstrap仓库，
然后，从自己的账号下clone：
git clone git@github.com:sufuzhi/bootstrap.git

如果你希望bootstrap的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。当然，对方是否接受你的pull request就不一定了。

如果你没能力修改bootstrap，但又想要试一把pull request，那就Fork一下我的仓库：https://github.com/michaelliao/learngit，创建一个your-github-id.txt的文本文件，写点自己学习Git的心得，然后推送一个pull request给我，我会视心情而定是否接受。

使用码云
上传自己的SSH公钥
创建一个新的项目
把它和码云的远程库关联：
git remote add origin git@gitee.com:sufuzhi/learngit.git

之后，就可以正常地用git push和git pull推送了！

如果在使用命令git remote add时报错：
git remote add origin git@gitee.com:liaoxuefeng/learngit.git
fatal: remote origin already exists.
这说明本地库已经关联了一个名叫origin的远程库，此时，可以先用git remote -v查看远程库信息：

如果是该远程库已指向GitHub。我们可以删除已有的GitHub远程库：
git remote rm origin
再关联码云的远程库

一个本地库能不能既关联GitHub，又关联码云：：

先删除已关联的名为origin的远程库：
git remote rm origin

然后，先关联GitHub的远程库（注意，远程库的名称叫github，不叫origin了。）：
git remote add github git@github.com:sufuzhi/learngit.git

再关联码云的远程库（远程库的名称叫gitee，不叫origin）：
git remote add gitee git@gitee.com:sufuzhi/learngit.git

git remote -v查看远程库信息，可以看到两个远程库：

如果要推送到GitHub，使用命令：
git push github master

如果要推送到码云，使用命令：
git push gitee master

码云也同样提供了Pull request功能，可以让其他小伙伴参与到开源项目中来。你可以通过Fork我的仓库：https://gitee.com/liaoxuefeng/learngit，创建一个your-gitee-id.txt的文本文件， 写点自己学习Git的心得，然后推送一个pull request给我，这个仓库会在码云和GitHub做双向同步。
-----------------------------------------------------------------------------
自定义Git

让Git显示颜色，会让命令输出看起来更醒目
git config --global color.ui true




















