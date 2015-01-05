---
layout: post
title: 使用gitblit搭建git服务器(win7)
category : tech
guid: b9c11b45-ee33-4c55-b1fc-824f4eb54860
tags : [dream, git]
---
{% include JB/setup %}

局域网内为了方便对项目开发代码进行版本控制，经常需要搭建一个版本控制服务器. 出于简单实用的考虑, gitblit是一个很不错的选择， 以下就个人的实践经验总结一下如何使用gitblit搭建git服务器. 

1. 安装git for windows--<http://msysgit.github.io/>, 这个没什么好说的了，一路'next'

2. 安装gitblit--<http://www.gitblit.com/>,  解压到想安装的目录即可

3. 配置gitblit, 主要是配置服务器端代码仓库存放位置， 访问端口号， 访问ip(目前还未测试ipv6), 配置文件在gitblit安装目录的`data`目录下，名为`gitblit.properties`. 以下是一个配置样例(参考链接1)：

	> git.repositoriesFolder = D:/GitRep     # 服务器端代码仓库存放在服务器D:/GitRep文件夹中
	> 
	> server.httpPort = 8585                     # 访问端口号，https有个安全问题，需要安全认证
	> server.httpsPort = 8443
	> 
	> server.httpBindInterface =                # 访问ip, 默认为localhost
	> server.httpsBindInterface =

4. 启动gitblit, 打开gitblit安装目录下gitblit.cmd即可

5. 在浏览器中输入http://localhost:8585, 登录gitblit后台管理界面

6. 添加用户  ![gitblit-add-user](/assets/images/git/gitblit-add-user.jpg)

7. 创建版本库   ![gitblit-create_repos](/assets/images/git/gitblit-create-repos.jpg)

8. 在客户端从`git bash`中`clone`仓库, 修改之后提交.

		8.1 clone仓库. 使用用户admin进行clone, 在git bash中输入
    >    git clone ssh://admin@localhost:29418/test/ws.git
    由于在本机搭建，@后的ip地址为localhost, 输入密码后clone成功，gitblit有一个默认账户admin, 密码也是admin

    <font color="red">注意使用http协议clone, 后面无法提交，参考链接3. 因此需要使用ssh协议</font> ![gitblit-ssh](/assets/images/git/gitblit-ssh.jpg)

		8.2  修改之后提交， `git bash` 中输入

> git add -A   
> git commit -m 'add something'  



	8.3  推送到服务器`git push -u origin master`, 输入admin密码完成向远程仓库推送


全篇参考[setting-up-github-like-server-locally-using-gitblit](https://amitgharat.wordpress.com/2013/07/16/setting-up-github-like-server-locally-using-gitblit).



一些问题：

1. 如何设置ssh以避免每次推拉都需要输入密码
2. 如何在一台机子上设置多用户ssh
3. 在一台机子上如可为不同的项目不同用户设置ssh



主要参考链接:   
1. [Gitblit的安装配置及访问](http://blog.csdn.net/ryanzll/article/details/8823082)        
2. [setting-up-github-like-server-locally-using-gitblit](https://amitgharat.wordpress.com/2013/07/16/setting-up-github-like-server-locally-using-gitblit), 需要[代理访问](https://51fanqiang.net/)    
3. [bitbucket-windows-and-fatal-could-not-read-password-for](http://stackoverflow.com/questions/20923193/bitbucket-windows-and-fatal-could-not-read-password-for)   
4. [git/ssh捋不清的几个问题](http://www.cnblogs.com/hustskyking/p/problems-in-git-when-ssh.html)
