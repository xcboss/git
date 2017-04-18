# git操作

1.安装git

2.打开git-bash

  创建本地ssh key:

  $ ssh-keygen -t rsa -C "your_email@youremail.com"

  (your_email@youremail.com改为你在github上注册的邮箱,之后会要求确认路径和输入密码，我们这使用默认的一路回车就行。成功的话会在~/下生成.ssh文件夹，进去，打开id_rsa.pub，复制里面的key。)

  回到github上，进入 Account Settings（账户配置），左边选择SSH Keys，Add SSH Key,title随便填，粘贴在你电脑上生成的key。


3.为了验证是否成功，在git bash下输入：

  $ ssh -T git@github.com


4.把本地仓库传到github上去，在此之前还需要设置username和email，因为github每次commit都会记录他们:

  $ git config --global user.name "your name"

  $ git config --global user.email "your_email@youremail.com"


5.仓库初始化：

  git init

  进入要上传的仓库，右键git bash，添加远程地址：

  $ git remote add origin git@github.com:yourName/yourRepo.git

  后面的yourName和yourRepo表示你再github的用户名和刚才新建的仓库，加完之后进入.git，打开config，这里会多出一个remote "origin"内容，这就是刚才添加的远程地址，也可以直接修改config来配置远程地址。


6.生成快照并存入项目索引：
  git add *  (*号即全部选择)
      ps:还有git rm,git mv等等操作…

7.项目索引提交：
  git commit -m"注释"

8.协作编程：

  将本地repo于远程的origin的repo合并，

  推送本地更新到远程：

  git push origin master

  更新远程更新到本地：

  git pull origin master

补充：

添加远端repo：

$ git remote add upstream git://github.com/pjhyett/github-services.git

重命名远端repo：

$ git://github.com/pjhyett/github-services.git为“upstream”


部分问题：

fatal: Not a git repository (or any of the parent directories): .git

没有.git这样一个目录，解决办法如下：

git init就可以了！

git reset 是指将当前head的内容重置，不会留log信息。

git reset HEAD filename  从暂存区中移除文件

git reset --hard HEAD~3  会将最新的3次提交全部重置，就像没有提交过一样。

git reset --hard [commit哈希值](38679ed709fd0a3767b79b93d0fba5bb8dd235f8)回退到 38679ed709fd0a3767b79b93d0fba5bb8dd235f8 版本

根据--soft --mixed --hard，会对working tree和index和HEAD进行重置:

git reset --mixed：此为默认方式，不带任何参数的git reset，它回退到某个版本，只保留源码，回退commit和index信息

git reset --soft：回退到某个版本，只回退了commit的信息，不会恢复到index file一级。如果还要提交，直接commit即可

git reset --hard：彻底回退到某个版本，本地的源码也会变为上一个版本的内容

例如：

我要彻底返回在上一次提交以前的版本。git reset --hrad HEAD~1

我要回到上一次提交的版本：git reset --hard