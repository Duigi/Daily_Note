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

#创建文件之后一定要将其add
$ git add filename.md
$ git commit -m 'first commit'


#用户名邮箱作用:我们需要设置一个用户名和邮箱, 这是用来上传本地仓库到GitHub中, 在GitHub中显示代码上传者.
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

为了把本地库推到远程服务器，首先需要在Github上面也建一个同名的repository，我这里应该是Daily_Note。

```shell
#远程项目和本地关联上
$ git remote add origin git@github.com:duigi/Daily_note.git
#将本地项目推送到github上
$ git push -u origin master

#可能会报以下错误
To github.com:yun591855479/hellogithub.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:yun591855479/hellogithub.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

#这是本地没有README文件造成的,现在去将该文件pull下来
$ git pull --rebase origin master
#更新github代码仓库到本地。使用下面的命令即可更新代码
$ git pull origin master
$ls -ah
#此时再将本地项目推送到github上
$ git push -u origin master

#<tips:想要与他人分享你牛鼻的提交，你需要将改动推送到远端仓库。 执行 git push [alias] [branch]，就会将你的 [branch] 分支推送成为 [alias] 远端上的 [branch] 分支。>
```

“origin”经常被用作远端仓库别名，就因为git clone默认用它作为克隆的链接的别名。

“git remote add xxx 远程服务器仓库地址aaa”：该方法是关联本地与服务器的仓库，为服务器的仓库取个别名叫xxx，一般情况下该别名就叫origin，此时他关联的就是远程服务器地址aaa这个仓库。

而删除某个别名用：“git remote rm tt” 删除现存的某个别名tt，也就是断开别名tt所对应的远程仓库的连接，不再需要它了、项目已经没了，等等。例如：git remote rm origin



#### 遇到的问题

```shell
#当我再次关联时会报错
$ git remote add origin git@github.com:duigi/Daily_note.git
fatal: remote origin already exists.

#我们需要移除
$ git remote rm origin

#再执行
$ git remote add origin git@github.com:duigi/Daily_note.git
```



#### 直接将github上的仓库clone下来

直接在gitHub上创建仓库，本地不创建。在终端输入’git clone’命令就能下载github的代码了：例如：我们在github上创建了一个仓库test2

```shell
#命令行执行：
$ git git clone https://github.com/duigi/Python-note.git
Cloning into 'Python-note'...
warning: You appear to have cloned an empty repository.

#查看文件
[github_repo Smiley$ ls
Daily_Note	Python-note
```

##### 补充

在下载下来的下面做一些修改并提交。
$ 进入刚下载的代码仓库：cd example/
$ 修改”README.md”文件：echo "hello github" > README.md
$ 添加修改的代码：git add README.md
$ 查看修改的状态：git status
$ 填写提交信息：git commit -m "add test message"
$ 正式提交代码：git push origin master