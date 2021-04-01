## Git 学习心得

### 一、Git诞生

很多人都知道，Linus在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件了。

Linus虽然创建了Linux，但Linux的壮大是靠全世界热心的志愿者参与的，这么多人在世界各地为Linux编写代码，那Linux的代码是如何管理的呢？

事实是，在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码！

你也许会想，为什么Linus不把Linux代码放到版本控制系统里呢？不是有CVS、SVN这些免费的版本控制系统吗？因为Linus坚定地反对CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和Linux的开源精神不符。

不过，到了2002年，Linux系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。

安定团结的大好局面在2005年就被打破了，原因是Linux社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了（监控工作做得不错！），于是BitMover公司怒了，要收回Linux社区的免费使用权。

Linus可以向BitMover公司道个歉，保证以后严格管教弟兄们，嗯，这是不可能的。实际情况是这样的：

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。

Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。

历史就是这么偶然，如果不是当年BitMover公司威胁Linux社区，可能现在我们就没有免费而超级好用的Git了。





### 二、集中式和分布式

Linus一直痛恨的CVS及SVN都是集中式的版本控制系统，而Git是分布式版本控制系统，集中式和分布式版本控制系统有什么区别呢？

集中式版本控制系统，版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。

![central-repo](https://www.liaoxuefeng.com/files/attachments/918921540355872/l)

集中式版本控制系统最大的毛病就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在互联网上，遇到网速慢的话，可能提交一个10M的文件就需要5分钟，这还不得把人给憋死啊。

那分布式版本控制系统与集中式版本控制系统有何不同呢？首先，分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

和集中式版本控制系统相比，分布式版本控制系统的安全性要高很多，因为每个人电脑里都有完整的版本库，某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就可以了。而集中式版本控制系统的中央服务器要是出了问题，所有人都没法干活了。

在实际使用分布式版本控制系统的时候，其实很少在两人之间的电脑上推送版本库的修改，因为可能你们俩不在一个局域网内，两台电脑互相访问不了，也可能今天你的同事病了，他的电脑压根没有开机。因此，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。


![distributed-repo](https://www.liaoxuefeng.com/files/attachments/918921562236160/l)

当然，Git的优势不单是不必联网这么简单，后面我们还会看到Git极其强大的分支管理，把SVN等远远抛在了后面。

CVS作为最早的开源而且免费的集中式版本控制系统，直到现在还有不少人在用。由于CVS自身设计的问题，会造成提交文件不完整，版本库莫名其妙损坏的情况。同样是开源而且免费的SVN修正了CVS的一些稳定性问题，是目前用得最多的集中式版本库控制系统。

除了免费的外，还有收费的集中式版本控制系统，比如IBM的ClearCase（以前是Rational公司的，被IBM收购了），特点是安装比Windows还大，运行比蜗牛还慢，能用ClearCase的一般是世界500强，他们有个共同的特点是财大气粗，或者人傻钱多。

微软自己也有一个集中式版本控制系统叫VSS，集成在Visual Studio中。由于其反人类的设计，连微软自己都不好意思用了。

分布式版本控制系统除了Git以及促使Git诞生的BitKeeper外，还有类似Git的Mercurial和Bazaar等。这些分布式版本控制系统各有特点，但最快、最简单也最流行的依然是Git！

### 三、Git命令

1. `git config --global user.name "Your Name"`、`git config --global user.email "Your Email"`

注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

2. `git init`

通过`git init`命令把这个目录变成Git可以管理的仓库

3. `git add <file>`：把文件添加到仓库。

4. `git add . `：把所有修改或者添加的文件添加到仓库。

5. `git commit -m <message>`：对本次提交内容做出说明。

6. `git status`：查看被修改或者被添加的文件，随时掌握工作区的状态。

7. `git diff`：查看修改内容。

   - `git diff HEAD -- <file>`：查看工作区和版本库里最新版本的区别。

8. `git reset --hard <commit_id>`：穿梭历史版本（回退到历史版本）。

   - `HEAD`表示当前版本
   - `HEAD^`表示上一个版本

9. `git log`：查看提交历史，便于找到回退版本。

10. `git reflog`：产看历史命令，便于回到未来的某个版本。

11. `git checkout`：用版本库里的版本替换工作区的版本

    - 注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！

12. `git remote add origin git@server-name:path/repo-name.git`：关联远程仓库。

13. `git push -u origin master`：第一次推送master分支的所有内容。

14. `git push origin master`：第一次推送后，可以使用此命令推送最新修改。

15. `git clone`：克隆远端仓库

    - Git支持多种协议，包括`https`，但`ssh`最快

16. `git branch`：查看分支

17. `git branch <name>`：创建分支

18. `git checkout -b <name>`/`git switch -c <name>`：创建+切换分支

    - 切换分支使用`git checkout <branch>`，而前面讲过的撤销修改则是`git checkout -- <file>`，同一个命令，有两种作用，确实有点令人迷惑。

      实际上，切换分支这个动作，用`switch`更科学。因此，最新版本的Git提供了新的`git switch`命令来切换分支

19. `git merge <name>`：合并某分支到当前分支（Fast forward 模式）

20. `git merge --no-ff -m "merge with no-ff" <name>`：禁用Fast forward 模式合并

    - 合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

21. `git branch -d <name>`：删除分支

22. `git log --graph`：查看分支合并图

23. `git log --graph --pretty=oneline --abbrev-commit`：查看合并分支图（带参数）

24. `git stash`：储存当前工作

25. `git stash apply`：恢复stash，stash内容并不删除

26. `git stash drop`：删除stash内容

27. `git stash pop`：恢复的同时删除stash内容

28. `git stash list`：查看stash内容

29. `git cherry-pick <id>`：复制一个特定的提交到当前分支

30. `git branch -D <name>`：强行删除一个分支（没有被合并过的分支）

31. `git push origin <branch-name>`：推送自己分支的修改

32. `git pull`：拉取内容

    - 如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`

33. `git remote -v`：查看远程库信息

34. `git checkout -b branch-name origin/branch-name`：本地创建和远程分支对应的分支（本地和远程分支的名称最好一致）

35. `git branch --set-upstream branch-name origin/branch-name`：建立本地分支和远程分支的关联

36. `git rebase`：可以把本地未push的分叉历史整理成直线

    - rebase的目的是使我们在查看历史提交的变化时更容易，因为分叉的提交需要第三方对比

37. `git tag <tagname>`：用于新建一个标签，默认为HEAD，也可以制定一个commit id

38. `git tag -a <tagname> -m "dasdsak" <commit-id>`：指定标签信息

39. `git tag`：查看所有标签

    - 注意：标签总是和某个commit挂钩。如果这个commit既出现在master分支上，又出现在dev分支上，那么在这亮哥分支上都可以看到这个标签

40. `git show <tagname>`：查看tag说明文字

41. `git push origin <tagname>`：推送一个本地标签

42. `git push origin --tags`：推送全部未推送过的本地标签

43. `git tag -d <tagname>`：删除一个本地标签

44. `git push origin :refs/tags/<tagname>`：删除远程分支