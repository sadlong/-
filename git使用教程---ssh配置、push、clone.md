#  git使用教程---ssh配置、push、clone

由于你的本地 Git 仓库和 GitHub 仓库之间的传输是通过SSH加密的，所以我们需要配置验证信息：

使用以下命令生成 SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

后面的 **your_email@youremail.com** 改为你在 Github 上注册的邮箱，之后会要求确认路径和输入密码，我们这使用默认的一路回车就行。

成功的话会在 **~/** 下生成 **.ssh** 文件夹，进去，打开 **id_rsa.pub**，复制里面的 **key**。

```
$ ssh-keygen -t rsa -C "429240967@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/tianqixin/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):    # 直接回车
Enter same passphrase again:                   # 直接回车
Your identification has been saved in /Users/tianqixin/.ssh/id_rsa.
Your public key has been saved in /Users/tianqixin/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:MDKVidPTDXIQoJwoqUmI4LBAsg5XByBlrOEzkxrwARI 429240967@qq.com
The key's randomart image is:
+---[RSA 3072]----+
|E*+.+=**oo       |
|%Oo+oo=o. .      |
|%**.o.o.         |
|OO.  o o         |
|+o+     S        |
|.                |
|                 |
|                 |
|                 |
+----[SHA256]-----+
```

回到github上进入account--->settings---> SSH and GPG keys---> New SSH key，title可以随便，然后粘贴下来刚刚复制下来的key。

这里我出现了`Key is invalid. You must supply a key in OpenSSH public key format`的问题，解决方法是在git命令行窗口中输入` clip < ~/.ssh/id_rsa.pub `，这时你的粘贴板上就有密钥内容了，然后再次回到github界面直接粘贴就行了。

下面是获取成功的界面

![1703147964561](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1703147964561.png)

也可以输入以下命令查看是否成功

```git
$ ssh -T git@github.com
The authenticity of host 'github.com (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ECDSA) to the list of known hosts.
Hi sadlong! You've successfully authenticated, but GitHub does not provide shell access.//说明成功了

```



创建仓库的界面是这样的

![1703149690105](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1703149690105.png)



以下是第一次创建仓库之后会进行的操作，在仓库里创建一个README.md文件

```git
$ echo "# 菜鸟教程 Git 测试" >> README.md     # 创建 README.md 文件并写入内容 写入的内容为：菜鸟教程 Git 测试
$ ls                                        # 查看目录下的文件
README
$ git init                                  # 初始化
$ git add README.md                         # 添加文件
$ git commit -m "添加 README.md 文件"        # 提交并备注信息
[master (root-commit) 0205aab] 添加 README.md 文件
 1 file changed, 1 insertion(+)
 create mode 100644 README.md

# 提交到 Github
$ git remote add origin xxx #xxx为SSH那栏的信息，粘贴过来就行
$ git push -u origin master

```



**查看当前远程库**

```git
$ git remote origin
$ git remote -v origin    
git@github.com:tianqixin/runoob-git-test.git (fetch)
git@github.com:tianqixin/runoob-git-test.git (push)
```

 执行时加上 -v 参数，你还可以看到每个别名的实际链接地址。 



**上传文件操作**

```git
$ git add 文件名
$ git commit -m "备注修改了什么"
$ git remote -v #查看以下连接的仓库SSH信息然后复制下来
$ git remote add origin SSH信息
$ git push -u origin main #这里只能用main不知道为什么不能用master
$ git log #查看日志
```





**clone仓库代码到本地**

```bash
先在你要存放的文件中右键并点击git bash here执行以下命令
git clone url
这里的url是指仓库的地址，在哪里找呢？---找到你要clone的仓库点击绿色按钮code，复制https的一串就是url
```





##  在新的文件夹中push代码步骤

将文件夹TCP客户端提交到git@github.com:sadlong/Qt-program-list.git中的main分支

```cpp
$ git init
$ git remote add origin git@github.com:sadlong/Qt-program-list.git
$ git pull origin main
$ git checkout -b main
$ git add TCP客户端
$ git commit -m '网络编程入门'
$ git push -u origin main
```

主要是要有git pull ...的步骤来更新之前提交过的状态