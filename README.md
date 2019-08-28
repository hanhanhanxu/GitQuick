# GitQuick
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

本地：选择一个目录（这个目录是否位空也不重要），直接`git bash here`，输入 `git clone ssh地址`，完成。不用`git init`（不用吗？试一试）

> Git支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快，且https协议每次推送都必须输入口令，麻烦。

