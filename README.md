<a href="https://996.icu"><img src="https://img.shields.io/badge/link-996.icu-red.svg" alt="996.icu" /></a>

# GitQuick

# Git简介

> git简单介绍 参见[廖雪峰Git](https://www.liaoxuefeng.com/wiki/896043488029600)

# 历史介绍

## Git诞生

Liuns在1991年创建了开源的Liunx，随后，全世界的开发者为Linux提供修改。当时有CVS和SVN，但是这些都是**集中式版本控制系统**，速度慢，必须要联网，所以Linus是通过手工方式合并代码。

2002年，Linux发展十年，代码量已经很大了，Linus很难再通过手工方式合并所有提交修改的代码，恰好当时有个商业的版本控制系统BitKeeper，愿意为Linux社区提供免费的版本控制使用权。

**2005**年，Linux社区有人试图破解BitKeeper的协议，被BitKeeper的东家BitMover公司发现了，所以收回了对社区的免费使用权。那怎么办呢？**Linus**花了两周时间自己用**C语言**写了一个**分布式版本控制系统**：**Git**！一个月之内，Linux的代码已经全部交给Git管理了。

**2008**年，**GitHub**网站上线了，它为开源项目免费提供Git储存，包括jQuery，PHP，Ruby等无数开源项目开始迁移至GitHub。

最初Git只能在Linux和Unix系统上跑，现在已经可以在Linux，Unix，Windows，Mac平台上跑了。

[Windows平台下载Git](https://git-scm.com/downloads)

[另一个下载地址](https://github.com/waylau/git-for-win)

CentOS7用`sudo yum install git`命令安装

Ubuntu用`sudo apt-get install git`命令安装

## 区别

集中实版本控制系统，就比如一个图书馆（中央储存库），你要修改一本书，必须先把书拿出来，修改，再将书放回图书馆。最大的毛病就是要先联网才能工作。并且由于中央储存库的存在，一旦中央储存库挂掉，那么所有人都无法工作。

分布式版本控制系统，就不必须有中央储存库，每个人的电脑上都是完整的版本库，但是为了方面多人协作，通常也有一台充当“中央储存库”的电脑，这它的存在仅仅是方便大家的修改，它挂掉了，任何一个人的电脑上都是完整的版本库。

另外Git还有及其优秀强大的分支管理。

## 使用

下载之后傻瓜式安装，然后在开始菜单里找到Git-Git Bash，点击打开后蹦出一个类似黑窗口的东西，就说明你已经安装成功了。

下面用于配置你全局（`--global`表示你这台机器上所有的Git仓库都会使用这个配置）的名字和Email。

（因为Git是分布式版本控制系统。所以每个机器必须自报家门，说下自己是谁，Email是啥）

```git
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```



在你电脑的任意一个（空）目录（无中文无空格）右键选择`Git Bash Here`，在弹出的窗口输入`git init`，然后你就会发现此目录下多了一个`.git`文件夹，这是用来管理版本的，千万不要改动。



## 注意

Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的。

对于二进制文件，Git只能追踪文件，不能跟踪文件变化，也就是只知道word、图片等从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。



[notepad++](https://notepad-plus-plus.org/)

## 名词解释

了解git之后，学习git命令之前，**一定**要先了解git的几个分区

### 工作区（Working Directory）

>  你在电脑里能看到的目录

[![mazgWF.png](https://s2.ax1x.com/2019/08/22/mazgWF.png)](https://imgchr.com/i/mazgWF)

### 版本库（Repository）

> 工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

版本库包含很多东西，最重要的是暂存区（stage或index）和Git创建的第一个分支`master`以及指向它的指针`HEAD`

[![mdSmT0.png](https://s2.ax1x.com/2019/08/22/mdSmT0.png)](https://imgchr.com/i/mdSmT0)

#### 暂存区

#### master分支

#### 指向master的指针HEAD

# 命令

## 提交

初始化Git仓库：`git init`

添加文件到Git仓库，分两步：

​	1、添加文件，可以添加多个文件：`git add <filename>`

​	2、提交文件，将添加的文件提交：`git commit -m <message>`

像打怪过关一样，你每通过一关，就自动把游戏状态存盘，万一某关没有通过，还能从最近的一关重新开始。

`git commit`就好比存盘，当你觉得修改文件到一定程度时，就存盘下。

[![mdS0pD.png](https://s2.ax1x.com/2019/08/22/mdS0pD.png)](https://imgchr.com/i/mdS0pD)

### 运行原理

`git add`将工作区所有修改提交到暂存区(stage)，`git commit`将暂存区的东西一次性提交到分支。

提交完成后，如果你没有再对工作区进行修改，那么工作区就是干净的。

```
$ git status
On branch master
nothing to commit, working tree clean
```

现在状态：

[![mdSLNV.png](https://s2.ax1x.com/2019/08/22/mdSLNV.png)](https://imgchr.com/i/mdSLNV)



`git status`：查看状态，具体：

- 查看工作区和分支（已提交）的区别，有无修改。
- 查看工作区和暂存区的区别，有无修改。

如果有文件被修改过，查看文件修改内容：`git diff <filename>`

或者 `git diff HEAD -- readme.txt `查看工作区和版本库里面（master分支）最新版本的区别

## 版本回退

假设你写了一个文件，提交了三次：

**查看从最近到最远的提交信息**：`git log`或` git log --pretty=oneline`查看简写信息：

```git
1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
e475afc93c209a690c39c13a46716e8fa000c366 add distributed
eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
```

版本号，信息

HEAD代表当前版本，上一个就是HEAD^，再上一个就是`HEAD^^`，往上一百个可以写为`HEAD~100`

现在，你在`append GPL`版本这里，**回退版本**：` git reset --hard HEAD^`或者`git reset --hard e475afc `

再用`git log`查看，只能查看两个版本的信息，因为**它只能看之前的版本**

**查看命令历史**：`git reflog`，确定要回到未来的哪个版本。



## 撤销修改

`git checkout -- readme.txt`：把readme.txt**在工作区的修改全部撤销**

回退到最近一次`git commit`或`git add`的状态



将暂存区的修改撤销掉，重新放回工作区。

`git reset HEAD readme.txt`

`HEAD`表示最新的版本



综上：

**假设你有一个更改，已经添加到暂存区，但是又发现错了。还没有提交，你需要将暂存区的内容回退到工作区再清空**

(已经git add 但还未git commit)

[![mw9N38.png](https://s2.ax1x.com/2019/08/22/mw9N38.png)](https://imgchr.com/i/mw9N38)

先将修改撤销，`git reset HEAD readme.txt`，现在暂存区的修改已经清空，修改已经恢复到工作区了。

丢弃工作区修改，`git checkout -- readme.txt`（丢弃工作区的修改，当然可以将修改直接**手工删除**，但是有时候我们记不清楚都修改了哪些，有时候我们忘记了上次提交的是什么样的了。这就是这个命令的解决范围，我们使用这个命令直接将工作区的修改丢弃至上次提交的版本）



# 总结

上述内容，我们已经学会了使用Git对一个文件进行时空穿梭，上述内容种，我们面对的是我们自己的本地库，只有一个master分支。拥有以上技能后，我们再也不用担心文件备份或丢失的问题。

但是这只是体现出来**版本控制系统**的*一小部分*，还没有体现出**分布式**这个大特点。



# 远程库

本地Git仓库，远程GitHub创建一个Git仓库。让这两个仓库进行远程同步。



在GitHub上，Create 一个repository后，我们就在GitHub上拥有一个仓库，这个仓库还是空的。我们可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后把本地仓库的内容推送到GitHub仓库上。



[![mwubTK.png](https://s2.ax1x.com/2019/08/22/mwubTK.png)](https://imgchr.com/i/mwubTK)



# 分支

> 假如你准备开发一个新功能，需要两周才能完成，第一周你写了50%的代码。如果立刻提交，由于代码还没写完，不完整的代码会导致别人不能干活，不能运行等问题。但是如果

假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。



？

我在本地开发，只提交到本地的master，不推送不就得了。





# git原理

HEAD指向当前分支（当前分支指向当前修改），所以说HEAD指向当前修改。



对于某一端仓库，本地仓库 或者 远程origin仓库来说：

## 我以为的

[![mw1axe.png](https://s2.ax1x.com/2019/08/22/mw1axe.png)](https://imgchr.com/i/mw1axe)

这样创建分支就是一件非常耗时耗力的工作。假如你现在再master分支的当前修改上，如果拟新建一个dev分支，就要做几件事：新建dev指针，然后将master分支的当前修改完全拷贝到dev分支的当前修改上，再将HEAD指向dev分支。

## 实际上的

### 新增分支

创建一个新的分支dev：git新建一个指针dev，指向master相同的提交；再将HEAD指向dev，就表示当前分支在dev上。

**git创建一个分支很快！创建指针，改变两个指针的指向。**工作区文件没有任何变化（上面也没有变化啊）。

[![mwdMYd.png](https://s2.ax1x.com/2019/08/22/mwdMYd.png)](https://imgchr.com/i/mwdMYd)

 

### 合并分支

假如在dev的工作完成了，需要将分支合并到master上。直接把master指向dev，就完成啦！！！

[![mwHKr6.png](https://s2.ax1x.com/2019/08/22/mwHKr6.png)](https://imgchr.com/i/mwHKr6)

### 删除分支

直接删除dev指针就行啦！！！

> 现在是不是感觉git这个设计理念非常的吊炸天？？？！！！这也是指针，C语言的魅力。



**廖雪峰原版**：

[![mwHGPH.png](https://s2.ax1x.com/2019/08/22/mwHGPH.png)](https://imgchr.com/i/mwHGPH)





### 命令实战

我们创建`dev`分支，然后切换到`dev`分支：

```
$ git checkout -b dev
```

用`git branch`命令查看当前分支：

```
$ git branch
* dev
  master
```

然后提交：

```
$ git add readme.txt 
$ git commit -m "branch test"
```

`dev`分支的工作完成，我们就可以切换回`master`分支：

```
$ git checkout master
```

现在，我们把`dev`分支的工作成果合并到`master`分支上：

```
$ git merge dev
```

（Fast-forward，这次合并是“快进模式”）

可以放心地删除`dev`分支了：

```
$ git branch -d dev
```

查看`branch`，就只剩下`master`分支了：

```
$ git branch
* master
```



**Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在`master`分支上工作效果是一样的，但过程更安全。**

### 小结

Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`

创建+切换分支：`git checkout -b <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`



# Git使用

> Git快速使用

#### 设置（重置）当前电脑上的git账户和邮箱

> global 全局

```
git config --global user.name "hanxu"
git config --global user.email "hanxu@do1.com.cn"
```

#### 生成公钥

```
ssh-keygen -t rsa -C "hanxu@do1.com.cn"
```

如果之前生成过ssh，那么这一步会出现提问：**是否覆盖之前的ssh?**

选择 y

生成的公钥文件在：C:\Users\123\\.ssh\id_rsa.pub 

#### 查看当前电脑上的git账户和邮箱

```
git config user.name
git config user.email
```

#### 重置电脑git账户信息 -unsure

```
git config –-system –-unset credential.helper
```

#### 记住git账户密码 -unsure

> 每次git clone都会让你输入账号和密码，执行：

```
git config --global credential.helper store
```







# 向GitHub推送代码

## 先有本地库，再有远程库

本地代码项目：myfile，

远程github创建仓库，不要勾选readme.md，啥都不要选，就写一个名字。

然后，开始：

```
F:
cd F:\\myfile
git bash here

git init
git add .
git commit -m "xxx" //提交到本地master分支

git remote add origin ssh地址  //关联远程库。远程库默认叫origin，可以修改，但没必要。
git push -u origin master //推送master分支所有内容。
//实际是把本地master分支推送到远程库的master分支
//由于远程库是空的，所以我们使用-u参数，将本地master和远程master分支关联起来。

//更新代码
git pull //先拉下来看下有无冲突
git add
git commit
git push origin master //把本地master分支的最新修改推送至GitHub。现在，你就拥有了真正的分布式版本库！
```



**分布式版本系统**的最大好处之一是**在本地工作**完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！**当没有网络的时候**，尽管修改你的文件，然后一次次`git add`和`git commit`添加，**提交到本地分支**(master)即可。**当有网络的时候**，再把本地提交**推送一下**(master)就完成了同步，真是太方便了！

[![mwubTK.png](https://s2.ax1x.com/2019/08/22/mwubTK.png)](https://imgchr.com/i/mwubTK)

> 为什么说是担任协作场景呢？因为这步骤只适合担任协作，更新文件。如果是多人协作，就存在一个问题：在阳光明媚的清晨，你拉下来代码之后，一顿乱改；同样，别人也拉下代码，一顿乱改。傍晚，你如果直接将本地推送到远程库，万一此时（你要推送，但还没有推送的时候），别人已经将他修改后的代码推送了，那么如果你这时候你直接推送你的代码，就会造成代码紊乱出错等问题。在多人协作种，正确的做法是：在每次推送代码之前，都先拉取一遍代码，拉取之后，将拉取得到的最新代码和你修改的代码进行整合，解决冲突（也可能那人和你修改了同一个地方），然后再推送。

## 先有远程库，后有本地库

github创建仓库：写名字，勾选readme.md文件，创建完成。

本地：选择一个目录（这个目录是否位空也不重要），直接`git bash here`，输入 `git clone ssh地址`，完成。不用`git init`

> Git支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快，且https协议每次推送都必须输入口令，麻烦。

