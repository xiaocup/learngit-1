Gitee的操作

## 1 Git 简介

GIt是目前世界上最先进的分布式版本控制系统

>  版本控制系统
>
> 一种文件管理系统，任何被它管理的文件内容发生任何变化它都能被记录下来，

版本控制的两个功能

- 跟踪文件的变根
- 并行开发，有效地解决版本的同步以及不同开发者之间的开发通信问题



Git是Linus 开发的一个分布式版本控制系统，使用c语言开发



## 2 版本控制系统的分类

- 集中式	 CSS SVN(修复了CSS的一些不稳定问题)
- 分布式 Git 



集中式版本控制系统的特点

有一个中央服务器，版本库存储在中央服务器上，如果需要更改版本库的内容，必须先从中央服务器获取版本库

缺点

- 必须联网

- 中央服务器要是出了问题，所有人都没法干活了

原理

![image-20210427185148451](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210427185148451.png)



分布式版本控制系统的特点

每台电脑都有一个完整的版本库，通常也有一台充当中央服务器的电脑，方便其他用户交换修改版本库

- 不需要联网
- 强大的分支管理

原理

![image-20210427185158325](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210427185158325.png)



## 3 Git的安装









## 4 Git的工作模式

>  版本库 一个目录该目录下的所有文件都会被Git管理起来

1 创建版本库

git init   进入在对应目录下使用该命令

```
 git init
```

会生成一个.git目录这个目录是Git来跟踪管理版本库的，如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见

2 将文件添加到版本库中

1 首先将文件复制到版本库的目录中

2 **使用git add命令 把文件修改添加到版本库中的暂存区中**

```
git add //文件名
git add . //提前当前目录下的所有文件到暂存区
git add *  //提交所有位置未提交的文件到暂存区
```

3 使用git commit -m  本次提交的说明，将暂存区的内容提交到当前本地仓库中

```
 git commit -m "wrote a readme file"
```

git commit 会把所有添加到版本库的文件，添加到版本库中

![image-20210427195316242](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210427195316242.png)

注意 

- 如果工作区中有一个A文件，前面已经提交暂存区的A 并且提交到了仓库中，此时对A进行修改，那么可以不用add 到暂存区， 可以直接commit到本地仓库
- 如果工作区中有一个A文件，修改提交到了A，在提交时候，修改了A那么commit不会提交第二次的修改

4 git status  查看工作区文件的状态

- Untracked files 

  git diff 查看修改文件的内容

![img](file:///D:\etempfile\1632078935\Image\C2C\@$EMPKIL5NE9J6C}XD4M4QM.png)



## 5  版本回退

Git也是一样，每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为`commit`一旦你把文件改乱了，或者误删了文件，还可以从最近的一个`commit`恢复，然后继续工作，而不是把几个月的工作成果全部丢失。



1 git log 显示从最近到最远的提交日志

  git log 显示提交日志的精简版

![image-20210427192541441](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210427192541441.png)

2 git reset --hard HEAd^ 回退到前一个版本

- git中 HEAD表示当前的版本，HEAD^表示上一个版本，HEAD^^表示上上个版本，HEAD~100 回退到往上100个版本
- git reset 版本号 也可以回退，但是不会把磁盘中的文件

3 git reset --hard commentid  回退到指定id的版本，可以回到未来的版本

- 只需要写commentid的前几个字符就可以了

```
git reset --hard HEAD  ac5f4 
```

4 git reflog 查看缩略版的提交信息   可以用于回退时忘记commentid 

```0
git reflog
```

5 绑定用户名和Email 

- git config --global user.name  用户名（键）

- git config --global user.email

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。

> 注意git config命令的–global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

6 git config -l 查看全局配置

```
git config -l
```



7 git rm 文件名 删除版本库中文件，

```
git rm 文件名
```

- 注意git rm删除工作区的文件，这个文件还必须提交到本地仓库，才能完全删除

可以使用rm 文件名 删除磁盘中的文件

**注意使用 git rm 文件名，删除文件后**，不能简单使用git checkout filename 恢复删除的文件，但是rm  文件名 可以恢复

**解决**

git checkout -- HEAD

8 git chekout 文件名  从本地仓库取出

```
git checkout filename
git chekout * //本地仓库修改的所有文件内容，覆盖到工作区的磁盘文件
```

- cat filename 查看文件内容

如果对文件进行了修改，并且提交到了暂存区，那么git chekout filename,不能覆盖工作区的文件

## 6 工作区和暂存区

- 工作区
  - 就是你初始化目录为版本库的那个目录
  - .git 为版本库
- 暂存区 
  - 版本库中有暂存区，以及Git为我们自动创建第一个分支Master ，以及指向`master`的一个指针叫`HEAD`。

git add 的原理

![image-20210427200624729](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210427200624729.png)

git commit 的原理

![image-20210427200640423](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210427200640423.png)



## 7 管理修改

git 监控的是文件的修改，每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。



**2 撤销修改**

1 git checkout -- filename 

- 撤销对工作区的修改
  - 这里面有两种情况，一种情况工作区修改了文件，还没提交到暂存区，现在撤销修改到版本库一样的状态
  - 修改了文件，并添加到了暂存区，如果再次修改文件，则回退到添加到暂存区的状态
  - **其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。**

2 git reset HEAD file 

- 把暂存区的修改撤销掉，重新放到工作区
- 注意此时工作区的修改不会撤销

小结 git reset 即可以回退版本，也可以暂存区的修改撤销掉，重新放回工作区

3 git reset --hard^HEAD 回退到上一个版本 

- 如果提交到了本地仓库，则可以使用git reset --hard HEAD^  回退到上一个版本，会撤销工作区的修改
- 使用git reset HEAD^  会撤销到上个版本对工作区的修改，但是不会撤销工作区的修改 继续使用git checkout -- file 撤销对工作区的修改

**注意 如果提交到远程仓库后就不能撤回了**

3 删除文件

1 使用 rm filename 删除工作区的文件

- 注意不会删除版本库中的文件
- 如果不小心删除错了，可以使用 git checkout -- file 撤销修改

2 git rm filename 确认删除版本库中的文件

- 确认删除后，还要提交删除修改 git commit

git checkout HEAD -- file 撤销对文件的修改 

## 8 远程仓库

远程仓库是提供一个供其他用户拉去其他用户修改，以及供给其他用户提交自己修改的一个仓库

GitHub 提供了一个免费的远程仓库,GitHUB 使用SSH加密协议，与本地仓库进行数据传输，因此需要在本机配置SSH

1 创建SSH KEY 

（1）打开Shell（Windows下打开Git Bash），创建SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可 

不需要设置密码

（2 ）查看用户主目录是否有.ssh文件夹，里面是否有`id_rsa`和`id_rsa.pub`这两个文件，前者是私钥后者是公钥

（3） 在github添加公钥

![image-20210428090454048](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210428090454048.png)

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。



**1 git remote add origin（远程仓库的名字）**  git@github.com:xiaocup/shiyanlou-code-.git

建立本地仓库与远程仓库的管理



2 git push -u origin  master  推送当前master 分支（本地仓库）的内容到远程仓库,

- 加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

- 以后推送就可以使用 git push origin master



3 SSH警告

当你第一次使用Git的`clone`或者`push`命令连接GitHub时，会得到一个警告：

```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入`yes`回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

```
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
```



GitHub GitLAB 都是远程仓库，公司一般都会搭建自己的远程仓库 GitLAB



### 删除远程库

1 git remote -v 查看远程仓库的信息

```
 git remote -v
```

2 git remote 查看远程仓库有哪些

```
git remote 
```



3 git remote rm origin 需要删除的远程仓库名

```
$ git remote rm origin
```



4 git push 远程仓库名  要提交的分支

- 如果远程仓库有的内容有，而本地仓库没有，那么推送会报错
- 解决 
  - 1 强制推送  git push -f 远程仓库名 要推送的分支
  - 2 
    - 1 先git pull 远程仓库  本地分支
    - 2 再 git push 远程仓库 本地分支

5 git pull 远程仓库名 本地分支 

- 将远程仓库

6 git push -f 远程仓库名 要提交的分支  

- 强制推送本地仓库的内容，覆盖到原有的仓库



**删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。**

Git 最大的好处，现在不用联网，也可以在本机上进行工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步

3 注意如果本地仓库添加多个远程仓库，那么git remote add 远程仓库名

远程仓库名应该不一样





**2 从远程仓库克隆**

1 git clone git@github.com:michaelliao/gitskills.git clone一个本地仓库



2 GitHub给出的地址不止一个，还可以用`https://github.com/michaelliao/gitskills.git`这样的地址。实际上，Git支持多种协议，默认的`git://`使用ssh，但也可以使用`https`等其他协议。

使用`https`除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`。



## 9 分支管理

**1 分支的作用** 

当大家一起来开发维护一个项目时，我们每天都会对文件进行更改，那么我们每个人的更改都是相互独立的，我们并不知道对方做了什么，而且我们也不希望自己的工作做到一半时会被别人添加进新的东西，那么此时如果我们创建一个属于自己的分支，在自己的分支上干活，直到你认为做好了然后提交上去，这不就解决了相互影响的问题了嘛。

2 Git的分支，创建与切换都更加块，相比其他版本控制管理系统



`HEAD`指向的就是当前分支。



### 1 分支常用命令

 主干和分支

可以在版本库中创建许多的分支版本库，

master 表示当前文件夹是一个主干，`git commit`只负责把暂存区的修改提交了



1 创建一个分支

git branch 分支名

```
git branch head
```

`master`分支是一条线，`master`指向最新的提交，然后使用一个`HEAD`指针指向`master`，每一次的提交，都会让`master`分支线变长

![image-20210428192146087](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210428192146087.png)

2 显示所有分支

```
git branch
```

3 切换分支

```
git checkout 分支名
```

4  创建并切换分支

```
git checkout -b 分支名
```

在分支上修改代码，并不会再主干上修改同样的代码，因此需要将分支上的代码合并到主干上面。

5 合并分支

```
git merge 分支名A
```

将分支A上的内容合并到当前分支上去

- 合并到分支到master上面后，其他分支不会受到master合并后的更新

-创建当前的分支会默认拉去master下面的分支

![image-20210428192240811](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210428192240811.png)

6 删除分支

```
git branch -d 分支名
```



- 注意创建分支，还有其他的命令

1 创建并切换分支

```
git switch  -c 分支名
```

2  切换分支

```
git switch master
```



分支也和主干一样，也拥有同样的内存结构，即工作区，暂存区，本地仓库



### 2 解决冲突

1 当分支修改了一部分主分支上面的内容，然后提交修改，然后切换到主分支上面去，修改分支修改的那部分内容，进行提交，如果此时主分支合并分支那么就会造成冲突



2 解决冲突的办法

手动修改冲突的内容，然后在master分支进行提交



**3 git log --graph 查看分支合并图**



**实例**

1 准备新的`feature1`分支

```
git switch -c feature1
```

修改`readme.txt`最后一行，改为

```
Creating a new branch is quick AND simple.
```

2 在`feature1`分支上提交：

```
$ git add readme.txt
$ git commit -m "AND simple"
```

3 切换到`master`分支：

```
$ git switch master

Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
  Git还会自动提示我们当前master分支比远程的master分支要超前1个提交。
```

4 在`master`分支上把`readme.txt`文件的最后一行改为：

```
Creating a new branch is quick & simple.
```

5 提交：

```
$ git add readme.txt 
$ git commit -m "& simple"
[master 5dc6824] & simple
 1 file changed, 1 insertion(+), 1 deletion(-)
```

![image-20210428194807617](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210428194807617.png)

这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突

```
$ git merge feature1

Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Git告诉我们，`readme.txt`文件存在冲突，必须手动解决冲突后再提交。`git status`也可以告诉我们冲突的文件：

```
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

可以直接查看readme.txt的内容：

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> feature1
```

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，我们修改如下后保存：

```
Creating a new branch is quick and simple.
```

再提交：

```
$ git add readme.txt 
$ git commit -m "conflict fixed"
[master cf810e4] conflict fixed
```



### 3 分支管理策略

分支管理策略主要指的是Git在分支进行合并时的策略，一般有三种模式

- fast-forward (ff)

- –no-ff
- *--squash*





1 fast-forward 

Git 合并两个分支时，如果顺着一个分支走下去可以到达另一个分支的话，那么 Git 在合并两者时，只会简单地把指针右移，叫做“快进”（fast-forward）

![image-20210429084328366](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210429084328366.png)

![image-20210429084530538](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210429084530538.png)



- 特点 删除分支后会丢失分支信息
- 合并后的分支不会有分支历史，看不出来合并

2 –no-ff

关闭fast-forward模式，在提交的时候，会创建一个merge的commit信息，然后合并的和master分支
merge的不同行为，向后看，其实最终都会将代码合并到master分支，而区别仅仅只是分支上的简洁清晰的问题

- 特点 合并后能看出分支合并的历史

![image-20210429084715932](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210429084715932.png)



3 --squash

把一些不必要commit进行压缩，比如说，你的feature在开发的时候写的commit很乱，那么我们合并的时候不希望把这些历史commit带过来，于是使用–squash进行合并，此时文件已经同合并后一样了，但不移动HEAD，不提交。需要进行一次额外的commit来“总结”一下，然后完成最终的合并。

- 特点 合并后不会产生新的commit信息，HEAD指针不移动

- 解决了分支合并后，分支上做了过多提交信息的问题，不会吧分支提前的问题带过来



在实际开发中，我们应该按照几个基本原则进行分支管理：

1 首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本平时不能在上面干活；

2 干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

3 你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

![image-20210429085023041](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210429085023041.png)

### 4 Bug分支



 Bug分支管理

当出现Bug时，我们通常创建一个分支，来进行处理Bug，处理完成后，再合并分支



为了解决，有时候在Bug分支，工作还未完成，没有提交，然后又要去master分支，解决bug，那么就需要保存Bug分支的现场



1 git stash 保存分支的工作现场

```
git stash
```

2 git statsh apply 恢复当前分支的工作现场

```
 git statsh apply
```

- 注意恢复后，保存的现场不会被删除掉，需要调用 git stash drop

3 git stash drop 删除当前分支的现场

```
 git stash drop
```



4 恢复并删除当前分支的现场 git stash pop

```
git stash pop
```

5 git stash list 查看分支的现场

```
git stash list
```

6 git  cherry-pick commitid 能复制一个另一分支特定的提交到当前分支

因为master分支，修改了Bug，其他分支上的Bug依旧存在，为了不重复修复bug可以使用该命令

```
 git cherry-pick 4c805e2
```



### 5 Feature分支

1 当需要添加一个新的功能的时候，不希望因为一些实验性质的代码，把主分支搞乱了

**所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。**



**2 git branch -D 分支名 强行删除一个未合并的分支**

**具体实例**

现在，你终于接到了一个新任务：开发代号为Vulcan的新功能，该功能计划用于下一代星际飞船。

于是准备开发：

```
$ git switch -c feature-vulcan
Switched to a new branch 'feature-vulcan'
```

5分钟后，开发完毕：

```
$ git add vulcan.py

$ git status
On branch feature-vulcan
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   vulcan.py

$ git commit -m "add feature vulcan"
[feature-vulcan 287773e] add feature vulcan
 1 file changed, 2 insertions(+)
 create mode 100644 vulcan.py
```

切回`dev`，准备合并：

```
$ git switch dev
```

一切顺利的话，feature分支和bug分支是类似的，合并，然后删除。

但是！

就在此时，接到上级命令，因经费不足，新功能必须取消！

虽然白干了，但是这个包含机密资料的分支还是必须就地销毁：

```
$ git branch -d feature-vulcan
error: The branch 'feature-vulcan' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
```

销毁失败。Git友情提醒，`feature-vulcan`分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用大写的`-D`参数。。

现在我们强行删除：

```
$ git branch -D feature-vulcan
Deleted branch feature-vulcan (was 287773e).
```



### 6 多人协作

**git pull  会拉取远程仓库的所有分支**

**git pull origin master 只会拉取远程仓库的origin master 分支**





1 git remote 显示有哪些分支

```
git remote
```

2 git remote -v 显示分支的详细信息包括权限

```
git remote -v
```

3 推送分支 推送分支到远程仓库

```
git push 远程仓库名 master(要推送分支) 
```

分支推送问题， ，哪些分支需要推送，哪些不需要呢？

- `master`分支是主分支，因此要时刻与远程同步；
- `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！



2 **抓取分支**

1 git clone git@github.com:michaelliao/learngit.git

- 克隆远程仓库到本地 **实际上Git自动把本地的`master`分支和远程的`master`分支对应起来了，并且，远程仓库的默认名称是`origin`。**

2创建远程`origin`的`dev`分支到本地，并建立关联

```
git checkout -b dev origin/dev
```



3 指定本地分支与远程分支的连接

```
$ git branch --set-upstream-to=origin/dev(远程分支) dev(本地分支)
```



常见问题解决

```
fatal: 'origin/dev' is not a commit and a branch 'dev' cannot be created from
```

就是远程仓库有dev分支，但是你clone的时候是不会有远程的dev分支的

应该先拉取

```
git pull 
```

2 git pull 时报错  no tracking information

```
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
```

未建立与本地dev分支与远程dev分支的关联，因此pull失败



3 多人写作产生的冲突

如果一个人修改了本地仓库的内容，并提交推送到了远程仓库，然后你同时修改了本地仓库和前面那个人的同一个文件，提交推送会报异常，这是需要拉取远程仓库的文件，这是会产生分支合并冲突需要手动解决冲突，并进行提交

### 7 Rebase

![image-20210429105735660](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210429105735660.png)

HEAD-》dev 表示当前版本库的分支为 dev,提交位置为 38048af

origin /dev 表示当前远程库dev分支的提交位置为  91700e2



## 11 Git的常见错误

1 拉去错误

![image-20210428203811923](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210428203811923.png)

两个分支是两个不同的版本，具有不同的提交历史，因此拒绝合并

解决办法

```
$git pull origin master --allow-unrelated-histories
```



2 git rebase 把分叉的提交历史“整理”成一条直线看上去更直观

缺点 本地的分叉提交已经被修改了



2 推送本地仓库到远程仓库出错

![image-20210428204755286](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210428204755286.png)

原因， 远程仓库和本地仓库不一致，需要先从本地仓库拉取远程仓库

```
git pull orgin master
git push orgin master
```

git merge 和 git rebase的区别

1. 可以看出merge结果能够体现出时间线，但是rebase会打乱时间线。
2. 而rebase看起来简洁，但是merge看起来不太简洁。
3. 最终结果是都把代码合起来了，所以具体怎么使用这两个命令看项目需要

1 原来的图

![image-20210429110703835](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210429110703835.png)

2 git merge 后

![image-20210429110716906](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210429110716906.png)

3 git rebase 后

![image-20210429110731772](C:\Users\liujian\AppData\Roaming\Typora\typora-user-images\image-20210429110731772.png)

git pull相当于是git fetch + git merge



## 10 标签管理

**通常发布一个版本的时候，都会在版本库中打一个标签**

**标签就是版本库中的一个快照，它就是指向某个commit的指针**

之所以引入tag的原因，是commit的 id太长了不好记忆





1 创建标签 （给指定的提交id 打上标签）

- 1 切换到要打标签的分支上 
- 2 git tag 标签名 

```
git tag v1.0 [commentid] 
```

- 默认标签是打在最新提交的commitId上的

2 git tag 查看标签名有哪些

```
git tag
```

3 git show tagname 查看标签的详细信息

```
git show v0.1
```

4 git tag -a tagname -m commentid 说明文字

```
 git tag -a v0.1 -m "version 0.1 released" 1094adb
```



2 标签的管理

1 推送一个标签到远程仓库

```
git push origin 标签名
```

2 推送所有标签到远程仓库

```
git push orgin --tags 
```

3 删除本地标签

```
git tag -d 标签名
```

4 删除远程标签

- 1 先删除本地标签

- 2 从远程删除

  - ```
    git push origin :refs/tags/标签名
    ```









## 12 Github 与Gitee

### 1 使用Github

​	Github是一个免费开源的远程仓库，通过GitHub，既可以让别人参与你的开源项目，也可以参与别人的开源项目。



## 2 参与一个开源项目的步骤

 1 访问项目主页点“Fork”就在自己的账号下克隆了一个bootstrap仓库

- 在自己仓库下创建bootstarp仓库，自己才能修改

2 修复bug，然后推送到远程仓库

3 向开源项目提交pull request





## 13 Git每天工作内容

1 早上 git pull 远程仓库

2 git add newfile.java

3 git diff 

4 git commit -m "mesage"

5 git status 

6 git push remote master