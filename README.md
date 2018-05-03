git 基础用法

在本地创建版本库galaxy
$ git init galaxy

进入galaxy文件夹
$ cd galaxy

在github建立远程仓库库建立本地版本库与远程仓库的链接
$ git remote add origin git@github.com:Dana0915/galaxy-test.git
git@github.com:Dana0915/galaxy-test.git这是我自己帐户的SSH密钥和密码短语。

创建README.md文件
$ touch README.md

在本地编辑README.md文件
例如：this is simple test

抓取到README.md文件
$ cat README.md
this is simple test

查看README.md文件状态
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

用命令git add告诉Git，把文件添加到仓库
$ git add .

用命令git commit告诉Git，把文件提交到仓库：

$ git commit -m "this is simple test"

就可以把本地库的所有内容推送到远程库上
git push -u origin master
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

遇到的问题:

下面是我在使用git和heroku时曾遇到的问题
Permission denied (publickey).
fatal: The remote end hung up unexpectedly.
Permission denied (publickey).
fatal: Could not read from remote repository.

解决办法：请确保以下2步均做到

1、远程服务器已经有了对应于本地主机上公钥

2、本地主机ssh服务开启(windows上是ssh-agent.exe运行)，并且本地主机私钥要包含在ssh服务列表中

具体操作细节：

为远程服务器（heroku）添加公钥的方法：可以到~/.ssh 下查看是否存在密钥对，如id_rsa和id_rsa.pub，可以直接运行  
$ heroku keys:add  

如果不存在的话，打命令生成一对
$ ssh-keygen -t rsa 

然后在执行
$ heroku keys:add

检查本地私钥是否存在于ssh服务中
$ eval `ssh-agent -s`  

如果运行这句出现Could not open a connection to your authentication agent，那么就先运行
$ ssh-agent bash  

再运行
$ ssh-add -l  

如果不存在，需要添加进去
ssh-add ~/.ssh/id_rsa 

如果是push到git的话，给git添加公钥的话，可以手动把~/.ssh/id_rsa.pub的内容复制好，然后如下
https://github.com/settings/keys

点击New SSH key 按钮把复制的公钥粘贴进来

点击add key 按钮保存成功