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
