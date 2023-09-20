git branch <branch-name> 本地创建分支
git push origin <branch-name> 推送本地分支到远端
git pull origin <branch-name> 拉取远端<branch-name>分支内容到本地当前分支
git branch --set-upstream-to=origin/<branch-name> <branch-name>  本地分支与远端分支关联
git push origin -d <branch-name> 删除远端分支
git branch --unset-upstream <branchname> 删除本地分支关联
git fetch orgin test 拉取远端分支到本地
git checkout -b test origin/test 创建并切换到本地分支 与 远端分支关联