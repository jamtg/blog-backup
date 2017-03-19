---
title:  在Android手机上安装kali
date: 2016-12-29 15:28:30
tags: 
- android
- kali  
categories: android安装kali
---
# 前言
2016年陆续发行了kali 2.0和kali rolling 等最新的kali版本，那么手机怎样安装最新版的kali2.0和kalirolling呢？
#让我们开始吧
在Android上安装kali Linux系统只需要几步

1. root你的手机
2. 安装以下几个神奇的软件
点击下载安装
- [Linux deploy 2.0](http://www.coolapk.com/apk/ru.meefik.linuxdeploy)
- [JuiceSSH](http://www.coolapk.com/apk/com.sonelli.juicessh)
- [BusyBox](http://www.coolapk.com/apk/ru.meefik.busybox)

（在第3步之前需要先安装busybox，下载busybox这个软件，安装后打开，点击"install"即可安装busybox）

3.安装

(建议在晚上睡觉的时候安装，因为这种联网安装的方式要等一段时间)

- 你的手机连着网（而且网速不要太慢，不然你会等很长时间）
- 打开Linux deploy，点击左上角找到setting>languages，选择简体中文（如果你英语还可以，就不用设置了），然后退出，再打开，让设置生效。

![image](/images/home.png)

然后点击右下方的箭头，按下图配置

![image](/images/i1.png)
![image](/images/i2.png)
![image](/images/i3.png)

即  
Containerization method:"chroot"

　　发行版:"kali"

　　架构:armhf

　　发行版版本: rolling(也可以选sana)

　　源地址:http://202.141.160.110/kali

(这是中科大的源，比软件原来的要快很多)

　　安装类型:文件

　　安装路径:"安装类型"选择"文件"时，这个选项将定义系统安装在哪个镜像文件中，默认值为"外置存储/linux.img。你也可以像图中一样改成自己的想放镜像文件的路径，但文件的扩展名一定得是".img",比如xxx.img

　　镜像大小(MB):这个选项将定义系统所在镜像文件的大小。系统安装之前将在安装目录创建一个大小为设置的镜像大小的空文件用来存放系统文件和数据(相当于新Linux系统的总磁盘空间)。建议不要用默认值，填写2048m足够了。

　　文件系统:选择"自动"就好。

　　用户名:这个选项为登录系统时的用户名，默认为"android"，可以随意更改。

　　用户密码:这个选项为kali系统中用户的密码，可以根据自己的习惯填写。

　　Privileged Users:保持默认值"root"

　　DNS服务器:保持默认值

　　本地化:建议保持默认值POSIX，如果有其他需求，比如ssh返回结果中文化/VNC中文化时，选择"zh_CN.UTF8"

　　INIT/MOUNTS项:若有需求时可以设置，无需求可以忽略。

　　允许SSH服务器启动:打开此选项

　　SSH设置:保持默认

　　允许图形界面启动:若有需求可以设置(如果选择安装图形界面，还需要安装VNC(自行百度)这个软件)
　　设置完成后，按返回键返回到应用主界面，按下菜单键，选择"安装"开始Linux系统的安装，安装过程中需要一直保持网络连接(建议在WIFI下安装，大概需要几百兆流量)。

　　当看到终端输出">>>deploy"时，代表安装已开始:

![image](http://mlapp.b0.upaiyun.com/usr/uploads/2016/10/2948357969.png)

　　当看到终端输出"<<<deploy"时，代表安装已完成:

![image](http://mlapp.b0.upaiyun.com/usr/uploads/2016/10/4126387359.png)

（在这儿，我已经安装过了，所以盗了两张图，不要奇怪为什么和你手机显示的不一样，哈哈哈）

点击主界面下方的"启动"按钮可以启动新安装的系统，点击"停止"可以停止系统。
![image](http://mlapp.b0.upaiyun.com/usr/uploads/2016/10/3435956325.png)

至此，系统部署部分描述完毕。

　　部署完毕后，我们需要用到JuiceSSH这个SSH工具来登录系统。

　　成功启动系统后我们打开JuiceSSH，依次点击 "连接" - 右下角"+"按钮 进入新建连接界面:

　　昵称:可随意填写，我们以"Localhost - Android"为例

　　类型:SSH

　　地址:127.0.0.1

![image](http://mlapp.b0.upaiyun.com/usr/uploads/2016/10/4177744019.png)

　　认证:选择"新建"跳转到"新建认证"界面:

　　昵称:同样可以随意填写，我们同样以"Localhost - Android"为例

　　用户名:填写"配置文件设置"界面的"用户名"，默认为android

　　密码:填写"配置文件设置"界面的设置的"用户密码"
![image](http://mlapp.b0.upaiyun.com/usr/uploads/2016/10/2116566192.png)

　　点击右上角的"√"图标保存并返回到"新建连接"界面，再次点击"√"图标保存，在"连接列表"中点击刚刚新建的这个项目连接到我们刚刚部署好的系统。

　　因为我们是通过普通用户android登陆系统的，接下来我们需要设置超级用户(root)的密码并且以超级用户的身份登陆系统:

　　在终端中键入:

sudo passwd root

　　终端将会提示用户输入root用户的密码并且再次输入一次以确认(输入密码时密码将不可见，连*都不会显示)，设置完毕后，在终端键入命令su并输入刚刚设置好的root用户密码即可切换到root用户。
　　在Linux Deploy中启动部署好的系统，以普通用户方式登录到SSH并使用su命令切换到超级用户，在终端中执行:

apt-get install -y vim #安装vim编辑器

　　当然啦，使用系统自带的vi编辑器也是可以的，如果你对vi编辑器比较熟悉也可以使用vi编辑器编辑文件。vim编辑器安装完成后我们继续在终端执行:

vim /etc/ssh/sshd_config #使用vim编辑器打开/etc/ssh/sshd_config这个文件

　　打开文件后，键入i进入编辑模式，点击终端任意位置可以弹出特殊键键盘，使用上下光标滚动浏览文件，在文件的#Authentication部分找到PermitRootLogin这一项，将其改为yes，改动完成后点击特殊键键盘中的"ESC"键退出编辑模式，键盘键入:wq!保存并强制退出文件完成对文件的编辑操作。
　　当然，修改完sshd_config文件，停止并启动Linux系统后，你也可以直接以root用户连接到SSH了（如果想要快速连接，点击右上方的"闪电" 然后填root@127.0.0.1，连接的密码就是你自己设置的root密码）
　　如果你在前面安装了图形界面，那么你还需要下载VNC（百度一下）这个软件，然后点击主界面的"+"
填127.0.0.1:5900密码是一开始是设置的android的密码，如果出错的话，请在ssh连接后输入vncserver
```
root@localhost:/home/android# vncserver

New 'X' desktop is localhost:6

Starting applications specified in /root/.vnc/xstartup
Log file is /root/.vnc/localhost:6.log

root@localhost:/home/android#
```
记住New 'X' desktop is localhost:6的数字，我这里是6，然后再进入vnc里面把地址改为127.0.0.1:5906
590后面的数字根据你手机出现的数字改动一下，再次连接就可以进入图形界面了。
　　

然后，在Android上安装kali就完成了。

 ** ~~参考~~  ** 

[Linux Deploy:在Android上部署Linux](http://blog.mlapp.cn/134.html)
by 美丽应用
