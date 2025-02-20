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
