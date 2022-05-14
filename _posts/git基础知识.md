笔记包含git命令cmd命令等

[03]最小配置

查看global设置：`git config --global --list'

全局设置用户名，`!user.name`和`'xxx'`之间要加空格：`git config --global user.name "xxx"`

查看global下的user.name：`git config --global user.name`

[04]新建仓库

创建新的由git管理的仓库xx：git init xx

git接管原有仓库：git init

把xx加入暂存区：git add xx

查看工作目录和暂存区状态：git status

提交暂存区内容到当前分支,-m里是提交理由：git commit -m"xxx"

提交工作区内容到当前分支,-m里是提交理由：git commit -am"xxx"

查看git日志：git log

win系统拷贝文件不加双引号命令语法不正确，斜杠方向错误系统找不到指定文件：copy "..\0-material\readme"

[05]暂存区和工作区

把工作区中已被git管理的文件全部提交到暂存区：git add -u

清除暂存区，工作目录中的所有变更：git reset --hard

!用git更改文件名(git提供的改名简便方法，直接在暂存区内改变)：git mv readme readme.md

[07]git log版本管理的几种用法

当前分支演进历史：git log

所有分支演进历史：git log --all

图形化的整体演进树：git log --all --graph

简洁版日志，显示版本hash和提交时-m中的备注信息：git log --oneline

temp分支的演进历史：git log temp

!所有图形化的简版演进历史：git log --all --graph --oneline

当前分支最近4条日志：git log -n4

前两种的组合写法：git log -n4 --oneline

查看本地有多少分支：git branch -v

查看本地和远端所有的分支：git branch -av

从旧版本上建新分支temp，并进入新分支：git checkout -b temp hash标识值

把工作区的更改直接提交到版本历史库：git commit -am"xxx"

浏览器查看git log相关帮助：git help --web log

[08]gitk图形界面的版本管理
进入图形化版本管理工具：gitk

进入图形化版本管理工具，显示所有分支：gitk --all

[09].git目录下
切换到master分支：git checkout master

查看hash指向的文件的类型：git cat-file -t hash标识值

查看hash指向的文件的内容：git cat-file -p hash标识值

**
HEAD文件 内容是一个引用，指向当前使用分支的最新一次commit或某个不在分支内的commit(分离头指针状态)。

config文件 存放与此仓库相关的配置信息,即local信息。

refs文件夹 包含heads(分支们,存放了每个分支最新的commit的hash标识值)和tags(可当里程碑用：v1.0)。

objects文件夹 存放commit，tree，blob。(放入暂存区时就会存进来)

[10]git中的三个对象

commit包含了commit提交时产生的信息(parent author和-m中的信息)和工作目录中除了.git文件夹的快照(唯一一个tree)。

tree包含除了.git外的所有文件和文件夹，tree中包含tree，tree就是文件夹。

blob即文件。

三种对象都会有对应的hash值。

在git中，相同内容的文件就算文件名不同，仍然对应同一个blob。

[12]分离头指针(detached HEAD)

基于hash标识值代表的版本进入分离头指针状态：git checkout hash标识值

**
进入分离头指针状态后，做一些尝试性变更，切换到别的分支后，这些变更不会被保存。

没有和分支或tag挂钩的分离头指针会被git认为不重要，会被清除。

[13]HEAD和branch
比较两个commit之间的差异：git diff hash标识值1 hash标识值2

当前HEAD指向的commit和它的父commit之间的差异：git diff HEAD HEAD~1

笔记包含git命令cmd命令等

【14】删除分支

`git branch -d branchname`
未merged警告出现时，确认删除用-D;

【15】修改最新commit的message

`git log -n1`
显示最近一次commit提交;

`git commit --amend`
修改message并替换掉最近一次的commit，所以不会增加一次commit版本;
**
无法输入wq时，可以按一下ESC键，再输入2个大写的Z，就能保存并退出。

【16】修改旧commit的message

`git rebase -i fatherhashcode`
!是填入上一级commit的hash值，r(reword);
**
rebase是变基操作。

【17】多个连续commit合成成一个

`git rebase -i fatherhashcode`
!是填入所有commit上一级的hash值，选择一个pick，其余的s(squash);
【18】多个不连续的commit合成为一个
`git rebase -i fatherhashcode`
如果没有更上一级的commit，就进入最原始的commit，手动pick它，位置在要和它合并的commit(s)之前，最终产物的位置在pick的那个原commit上;

【19】对比暂存区和HEAD(当前分支中正在使用的commit)
`git diff --cached`
对比后需要再更改的，在工作区修改，再次add进暂存区。(cached:缓存);

【20】暂存区和工作区的比较

`git diff`
显示所有文件的差异;

`git diff -- readme.md`
只显示readme.md文件的差异,可加多个文件名;
**

工作区内的变更即还没有add进暂存区的内容。
已经add进暂存区的文件，工作区和暂存区内是相同的。
【21】把暂存区所有变更不保留，恢复到和HEAD相同

`git reset HEAD`
【22】工作区某个文件恢复到暂存区状态

`git checkout -- index.html`
!变更工作区用checkout，变更暂存区用reset。
【23】暂存区内部分文件撤销变更，回退为HEAD

`git reset HEAD -- styles\style.css`
可空格添加多个文件;
【24】删除本分支最近几次提交

`git reset --hard commit_hashcode`
HEAD指向，工作区，暂存区都改为指向指定commit;
**
并不是真正删除，只是不再在branch中显示。
后悔药：git reflog 查看命令历史, 记录了每次变更命令。

【25】比较两个commit之间差别

`git diff temp master`
比较两个分支最新commit之间差异;

`git diff temp master --index.html`
比较两个分支最新commit的index.html文件之间的差异;
**
上述命令可以用hashcode来比较任意两个commit间的差异。

【26】删除文件
`remove readme.md`
工作区删除;

`git rm readme.md`
暂存区删除;

【27】加塞了紧急任务时，暂存正在进行的任务

`git stash`
暂存此时的状态(stash:藏匿处);

`git stash list`
查看stash里存放的状态们;

`git stash apply`
恢复且不删除stash内容;

`git stash pop`
恢复且删除从stash末尾弹出的内容;

【28】哪些文件不被纳入版本控制系统
`mkdir doc`
当前目录下创建doc文件夹;

`echo "hi" > doc\readit`
在doc文件夹下新建文件readit并加入内容hi;
`remove -rf doc`

删除doc文件夹;
**
在.gitignore文件里配置不需要管理的文件种类，即git status时，不会监控这些文件的变更。
针对可以通过构建再复现的文件。

【29】将git仓库备份到本地

`git clone --bare path\.git ya.git`
用哑协议创建裸仓库ya.git;

`git clone --bare file:\\path\.git zhineng.git`
用智能协议创建裸仓库zhineng.git;

`git remote -v`
查看协作了哪些远端仓库;

`git remote add zhineng file:\\path\zhineng.git`
添加协作的远端仓库，取名为zhineng，添加后就可以向zhineng仓库push了;

`git push zhineng`
push到智能仓库;
**
包含本地(哑协议(进度不可见)/智能协议(进度可见，速度快))和网络(http/https/ssh)
! 裸仓库对代码平台的作用,参考：http://www.worldhello.net/gotgit/02-git-solo/100-git-clone.html#id4
**
辨析：

`git reset HEAD`
把暂存区所有变更不保留，恢复到和HEAD相同;

`git reset --hard HEAD`
工作区，暂存区都与HEAD同步。

笔记包含git命令git bash命令等

【33】本地仓库同步到github

`git remote -v`
查看与本地协作的远端仓库信息;

`git remote add 给远端仓库起的名字 复制ssh`
添加ssh对应的远端仓库;

`git fetch github master`
把远端仓库github的master分支fetch下来，会形成一颗独立的tree;

`git merge -h`
查看merge命令的帮助信息;

`git merge --allow-unrelated-histories github/master`
把fetch下来的master分支和本地当前分支master合并(两分支不是父子关系，所以合并需要添加 --allow-unrelated-histories);

`git push github --all`
把当前本地仓库push到远端仓库github;

`git push github master`
把当前本地仓库的master分支push到远端仓库github的master分支;

**
git bash的指令和mac终端相同。
-x多为操作性质指令，--x多为描述性质指令。

【34】同一分支上不同人修改了不同文件，时差的协作

`git clone sshkey` 创建出的新仓库名

`git checkout -b` 新建分支名(通常和后者取名相同) 远端分支名

`git push`
push到远端，在checkout那步已经把两个分支关联;

`git fetch github`
fetch下来与本地协作的远端仓库github;

`git merge` 远端仓库名/远端分支名
push时远端有本地未跟进的更新(先再次fetch得到更新，再merge);

**
在本地无法直接在clone下来的远程分支上做变更，只能基于远程分支建本地分支后，才能创建commit。
【35】不同人修改了同文件
`git pull`
开发前先和远端同步;

**
本地功能还没有开发完，不想做集成只想看和远端分支的差异，就可以先执行fetch。
【36】不同人更改了同一处引发冲突的处理
**
后更改的人需要先pull，把更新过的远端和本地融合，手动在编辑器里处理冲突，把更新commit后，即可再次push。

【39】禁止向与别人协作的分支push -f
git push -h
查看git push命令可加的后缀与作用;
**
本地分支与远端分支不是fast forward关系时，是不能push的。
但附加-f可以强制push，会导致远端对应分支的历史演变完全被本地替代。
【40】
**
公共分支严禁拉到本地rebase变基，即不要修改项目的历史版本。
**
git push -f 远端仓库名 hashcode:远端分支名
把本地hashcode对应的commit和它的历史演进强行push到指定远端分支上;
