![](/360/学习/前端/2016/笔记/trees.png)

##基本
working dir -> index(stage) -> HEAD

git add <file>...  添加（stage）到暂存区（Index）


git status: 仓库当前状态

git diff: 修改的内容

git commit: 就好比RPG游戏的存档，可以读取。

git log <-n>: 历史记录

git log --pretty=oneline 文件名: 某个文件的提交历史

HEAD:指针，指向的是当前分支的当前版本

##时光穿梭
如果想回退版本，可以用git reset

git reset --hard HEAD^:回退到上一个版本（也可以写作git reset --hard HEAD~1  数字任意，从上一个版本开始数，超出总数报错，没效果）

git reset --hard <commit>:同上，回退到某一版本。（会丢弃本地修改）

git reflog:每一次的命令记录

git checkout <commit> <file> 某个文件回退到某个版本 （工作区，会丢弃本地修改）

git checkout -- file: 丢弃工作区的修改，回退到add或者commit最近的一个版本。

git reset HEAD <file>... 从暂存区撤销添加（unstage），与add -i中的revert命令效果一致。

三个撤销场景：

1. 改乱工作区文件内容，想直接丢弃，就用```git checkout -- file```。
2. 改乱而且添加到暂存区，分两步：先```git reset HEAD <file>```，再执行第一步。
3. 已经提交到本地版本库，就用```git reset --hard <HEAD~1> <commit>```,会丢弃所有本地更改，stage的也是。


git rm file:删除文件


##分支管理

git checkout -b <name>:新建分支<name>，并切换到该分支上。等同于
```
git branch <name>
git checkout <name>
```

git branch:列出所有分支。

git merge <name>:在<name>分支上commit之后，切到master上，将<name>合并到master。

git branch -d <name>:删除该分支。 -D，强行删除。

解决冲突，如果merge有冲突，则先将```<<<<<<<，=======，>>>>>>>``` 所标识出的地方修改，再add->commit

git log --graph:可以看到冲突解决问题。

git merge --no-ff -m 'merge with no-ff' dev: 禁用fast forward模式，可以在git log中看到分支合并信息。

git stash：把当前工作现场“储藏”起来，恢复git stash pop。使用场景，当出现紧急bug的时候，可以将工作区当前修改存起来。



git remote -v:查看远程库的信息

git push origin dev ：推送至远程分支

git branch -a:列出所有分支，包括远程库的

git checkout -b dev origin/dev:创建远程origin dev分支到本地，如果这个分支是别人后来push的，就要先pull一下。

多人合作修改同一分支时，如果git pull失败，报错如下

```
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
```

则需要根据提示，将本地dev与远程dev建立链接。
git branch --set-upstream-to=origin/dev dev

多人合作步骤：
1. 先尝试推送自己的修改```git push origin branch-name```
2. 若失败，则远程库比本地新，要用```git pull```尝试合并
3. 如果合并有冲突，则解决，并本地提交。
4. 再次```git push origin branch-name```


##标签管理

用来代替commit那一长串SHA1码。

git tag:显示所有tag
git tag v1.0:最后一次commit打上tag
git tag v0.1 commit:为某个特定的commit打上tag
git show v0.1:显示说明
git tag -a v0.1 -m "version 0.1 released" 3628164:添加签名
git tag -d v0.1:删除本地标签
git push origin :refs/tags/v0.1:删除远程标签
git push origin v1.0:推送某个标签至远程库
git push origin --tags:推送所有标签

```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
非常好用


##变基 rebase

rebase 命令，可以把在一个分支里提交的改变移到另一个分支里重放一遍，在另一个分支最新提交的版本之后。这样做会让后者的提交历史非常干净。

步骤
1. 在分支dev中commit，然后git rebase master
2. 如果冲突，解决冲突后，add，之后git rebase --continue
2. checkout到master，快速合并dev

将rebase作为清空提交历史的手段是最佳实践。千万不要把push到远程库的提交做rebase！！！！！！



##搭建git服务器
1. 安装git

```
sudo apt-get install git
```

2. 搭建ssh服务器

```
# 安装
sudo apt-get install ssh
man sshd # sshd — OpenSSH SSH daemon ...

# 检查是否运行
ps -e | grep sshd # 显示正在运行的sshd服务
sudo service sshd start # 如果没有sshd服务就启动

# 测试
ssh 192.168.240.129 # 服务器ip，以当前用户跟密码登陆,不出错就说明ssh服务器正常
exit # 退出登陆
```


3. 创建一个git用户，用来运行git服务

```
sudo adduser git
```

4. 创建证书登录

收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。

5. 初始化git仓库，假定仓库目录是/srv，也可以在git用户目录下创建仓库，这样克隆时候可以直接用相对路径。

```
sudo git init --bare sample.git
```

将owner改为git

```
sudo chown -R git:git sample.git
```


6. 禁用shell登录

```
sudo vim /etc/passwd
```

将形如：

```
git:x:1001:1001:,,,:/home/git:/bin/bash
```
改为

```
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```
这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。

7. 克隆远程仓库

```
git clone git@server:/srv/sample.git
Cloning into 'sample'...
warning: You appear to have cloned an empty repository.
```


