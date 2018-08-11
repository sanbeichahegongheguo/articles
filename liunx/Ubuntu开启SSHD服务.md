# Ubuntu开启SSHD服务

ubuntu安装ssh服务

一、openssh-client

SSH分客户端openssh-client和openssh-server.

如果你只是想从Ubuntu登陆别的机器的SSH，只需要安装openssh-client。

Ubuntu通常默认是有安装的。如果没有则输入

```bash
sudo apt-get install openssh-client
```

检测。

二、openssh-server

Ubuntu默认并没有安装ssh服务，如果要使本机开放SSH服务允许别的机器远程登录，就需要安装openssh-server。

判断是否安装ssh服务，可以通过如下命令进行：

```bash
ssh localhost
```

如果输出：

```bash
ssh: connect to host localhost port 22: Connection refused
```

表示没有还没有安装，可以通过apt安装：

```bash
sudo apt-get install openssh-server
```



通常安装好后就会自动启动，可以输入指令确认sshserver是否启动了：

```bash
ps -e |grep ssh
```

如果看到如下的sshd那说明ssh-server已经启动了：

```bash
2152 ?        00:00:00 ssh-agent
3582 ?        00:00:00 sshd
```

如果没有则可以这样启动：

```bash
sudo /etc/init.d/ssh start
```

ssh-server配置文件位于/ etc/ssh/sshd_config，在这里可以定义SSH的服务端口，默认端口是22，你可以自己定义成其他端口号，如222。

先停止ssh服务，更改端口号后重启SSH服务：

```bash
sudo /etc/init.d/ssh stop
sudo /etc/init.d/ssh start
```

然后使用以下方式登陆SSH：

```bash
ssh tuns@192.168.0.100 
```

tuns为192.168.0.100机器上的用户名，需要输入密码。

断开连接：

```bash
exit
```



二、

ubuntu默认并没有安装ssh服务，如果通过ssh链接ubuntu，需要自己手动安装ssh-server。判断是否安装ssh服务，可以通过如下命令进行：

ssh localhost

ssh: connect to host localhost port 22: Connection refused

如上所示，表示没有还没有安装，可以通过apt安装，命令如下：

sudo apt-get install openssh-server

 

（若找不到安装包，先运行apt-get update，运行命令若出现E: 无法获得锁 /var/lib/apt/lists/lock - open (11: 资源暂时不可用)E: 无法对目录 /var/lib/apt/lists/ 加锁的问题，执行命令sudo rm /var/lib/apt/lists/lock即可。这是一种极端的情况，也就是在上次更新没有正常关闭的情况下使用。在大部分情况下，出现问题的原因在于其它的程序如系统的自动更新等正在使用apt-get进程，所以解决方法也就是将这一进程关闭。）

 

系统将自动进行安装，安装完成以后，先启动服务：

 service ssh start

ssh start/running, process 3582

sudo /etc/init.d/ssh start

 

启动后，可以通过如下命令查看服务是否正确启动

 ps -e | grep ssh

 2152 ?        00:00:00 ssh-agent

 3582 ?        00:00:00 sshd

 

如上表示启动ok。注意，ssh默认的端口是22，可以更改端口，更改后先stop，

然后start就可以了。改配置在/etc/ssh/sshd_config下