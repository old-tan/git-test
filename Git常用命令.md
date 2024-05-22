### 分支相关
1. git branch <branch-name> 本地创建分支
2. git push origin <branch-name> 推送本地分支到远端
3. git pull origin <branch-name> 拉取远端<branch-name>分支内容到本地当前分支
4. git branch --set-upstream-to=origin/<branch-name> <branch-name>  本地分支与远端分支关联
5. git branch -d <branch-name> 删除本地分支
6. git push origin -d <branch-name> 删除远端分支
7. git branch --unset-upstream <branchname> 删除本地分支关联
8. git branch -D dev # 删除本地dev分支
9. git push origin -d dev # 删除远程dev分支
10. git fetch orgin test 拉取远端分支到本地
11. git checkout -b test origin/test 创建并切换到本地分支 与 远端分支关联

### 暂存区
1. git stash 储存当前工作
2. git stash save <message> 存储当前工作并添加message
3. git stash pop 恢复的同时删除stash内容（缓存堆栈中第一个stash）
4. git stash apply 恢复指定stash，默认恢复第一条，指定恢复：git stash apply <stash@{0}> ，stash内容并不删除（将缓存中的stash多次应用到工作目录中）
5. git stash list 查看stash内容
6. git stash drop 删除stash内容

### git add
1. git add . // 所有
2. git add *.txt // 匹配 .txt
3. git add a.txt b.js c.vue // 某些文件
4. git add /src // /xxx 目录下

### git 合并分支中某一次提交
1. git cherry-pick <hash> 某一次hash
2. git cherry-pick <xxx> xxx分支的最新一次提交
3. git cherry-pick <hasha> <hashb>  合并 多次提交的 hash 串连

### commit 相关
#### 撤销 commit
##### git reset --soft HEAD^
1. --mixed 
意思是：不删除工作空间改动代码，撤销commit，并且撤销git add . 操作
这个为默认参数,git reset --mixed HEAD^ 和 git reset HEAD^ 效果是一样的。
2. --soft  
不删除工作空间改动代码，撤销commit，不撤销git add . 
3. --hard
删除工作空间改动代码，撤销commit，撤销git add . 

#### git commit 注释写错修改
git commit --amend
此时会进入默认vim编辑器，修改注释完毕后保存就好了。

### git 更新 gitignore 并使其生效
1. git rm -r --cached .  #清除缓存
2. git add . #重新trace file
3. git commit -m "update .gitignore" #提交和注释
4. git push origin master #可选，如果需要同步到remote上的话

### 版本回退
1. git log #查看历史记录
2. git log --pretty=oneline #美化历史记录
3. git reset --hard HEAD^ #回退到上一个版本
4. git reset --hard 1094a #会退到指定版本 1094a【指定commit id即版本号】
5. git push -f | git push -f origin <branch name>#强制推送到远端分支
6. git reflog #记录历史命令