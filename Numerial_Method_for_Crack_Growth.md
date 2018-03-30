# git基本命令

首先到官网(https://git-scm.com/)上下载git，并安装。

```shell
#查看git版本
$ git --version

#查看ssh版本
$ ssh -v
```



#### 1.创建ssh key

```shell
$ cd ~
#看看有没有.ssh文件夹
$ cd .ssh
#运行命令创建ssh key
$ ssh-keygen -t rsa -C "yout email adress"(github sign in name)

#接下来都回车就可以了，之后进入.ssh文件
$ cd .ssh
$ ls

#就会发现有id_rsa , id_rsa.pub, 打开后一个文件
$ sublime id_rsa.pub
```





#### 2.在github设置ssh key

登录github中，在settings- ssh key- add ssh key中粘贴id_rsa.pub中的内容，title可以随便填写。



#### 3.测试本地是否和github连上

```shell
$ ssh -T git@github.com
```



#### 4.使用git在本地建立项目更新到github

```shell
#进入我创建好的github仓库
$ cd ~
$ mkdir Github_Repo
$ cd Github_Repo

#查看该目录下的文件
$ ls -ah

#创建并进入我的笔记文件夹
$ mkdir Daily_Note
$ cd Daily_Note

#生成新的文件
$ touch filename.md
$ sublime filename.md

#输入内容之后保存

$ git add Numerial_Method_for_Crack_Growth.md
$ git commit -m 'first commit'
#因为之前没有配置username。所以首次commit会有提示。自己主动建立
设置方式

$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

然后在github上建立一个同名的repository，我这里应该是Daily_Note。

```shell
#远程项目和本地关联上
$ git remote add origin git@github.com:duigi/Daily_note.git
#将本地项目推送到github上
$ git push -u origin master
```



