## 一、anaconda介绍
## 二、anaconda版本
## 三、同时安装anaconda2\3

#### 更改pip源
### windows
在 c:\user\username\pip\pip.ini中加入
```
[global]
index-url=https://pypi.tuna.tsinghua.edu.cn/simple 
[install]  
trusted-host=pypi.tuna.tsinghua.edu.cn
disable-pip-version-check = true  
timeout = 6000 
```

>注意：首先需要创建pip文件夹与pip.ini文件。

#### linux（ubuntu）

同样首先建pip的配置文件

```bash
cd $HOME  
mkdir .pip  
cd .pip
sudo vim pip.conf  
```
在里面添加
```
[global]  
index-url=https://pypi.tuna.tsinghua.edu.cn/simple
[install]  
trusted-host=pypi.tuna.tsinghua.edu.cn 
disable-pip-version-check = true  
timeout = 6000 
```


#### 更改anaconda源
```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ # 不要有引号，网上有的帖子会在链接两端加引号，需要去掉。
conda config --set show_channel_urls yes
```
好了，这下可以开心的下载东西了

<br>

#### 如何删除添加的源呢？
```bash
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
```
#### 看看当前的 cofig 是什么样的
```bash
conda config --show
```