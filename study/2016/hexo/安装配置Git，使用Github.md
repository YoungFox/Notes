# 安装配置Git，使用Github

在开始之前，先在https://github.com/ 注册账号，注意，username稍微起的有意义点，别像我当年取了个“yang6233562”，简直low爆了。

## 安装配置Git
###1. [下载安装最新版的Git](http://git-scm.com/downloads)

###2. 打开终端，告诉本地Git你的名字，以便于后续提交能贴上正确的标签。在`~$`后输入以下代码：

```
git config --global user.name "YOUR NAME"
```

###3. 告诉Git你的邮箱，这个邮箱将和你每次提交相关联。

```
git config --global user.email "YOUR EMAIL ADDRESS"
```

###4. 通过Git来与GitHub进行认证（此处只讲SSH方式）


## 生成SSH keys
###1. 检查SSH keys

```
ls -al ~/.ssh
```

###2. 生成新的SSH key，可以一路回车

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```



###3. 将生成的SSH key添加到ssh-agent中

* 确认ssh-agent可用

```
eval "$(ssh-agent -s)"
```

* 添加

```
ssh-add ~/.ssh/id_rsa
```

###4. 将SSH key添加到你的github账号中

将~/.ssh/id_rsa.pub内容拷贝至github中Settings->SSH keys->Add SSH key

###5. 测试连接

* 打开终端输入：

```
ssh -T git@github.com
```

出现提示信息，输入“yes”

```
Hi YoungFox! You've successfully authenticated, but GitHub does not provide shell access.
```

出现此信息则表示成功。

