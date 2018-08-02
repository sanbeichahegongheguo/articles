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
## 四、pip和conda有什么不一样？
既然都是关于python的包管理工具为什么有了pip 我们还需要conda？在stackoverflow上的英文回答：
>
> Having been involved in the python world for so long, we are all aware of pip, easy_install, and virtualenv, but these tools did not meet all of our specific requirements. The main problem is that they are focused around Python, neglecting non-Python library dependencies, such as HDF5, MKL, LLVM, etc., which do not have a setup.py in their source code and also do not install files into Python’s site-packages directory.
> So Conda is a packaging tool and installer that aims to do more than what pip does; handle library dependencies outside of the Python packages as well as the Python packages themselves. Conda also creates a virtual environment, like virtualenv does.
>
> As such, Conda should be compared to Buildout perhaps, another tool that lets you handle both Python and non-Python installation tasks.
>
> Because Conda introduces a new packaging format, you cannot use pip and Conda interchangeably;  pip cannot install the Conda package format. You can use the two tools side by side but they do not interoperate either.
>

> 在python的世界里也浸淫多年了，我们早已习惯有 pip ,easy_install 和virtualenv的世界，但是这些🔧没有解决我们所有的需求哦。这其中主要的问题是他们全部都集中解决关于python相关问题而忽略了非python库的依赖关系。(这句我没他看明白),就像 HDF5, MKL LLVM,etc等，在他们的源码中并没有setup.py这种东西而且也没有安装文件在python的site-packages 目录中。
>
> 所有conda就是一个包管理工具和安装工具，它就是要做比pip更多的事情；在python-site-packages之外管理python 库依赖关系。 而且conda同样也像virtualenv一样创建一个虚拟环境。
>
> conda可以让你同时管理安装处理你有关python的任务和跟python无关的任务
>
> conda使用了一个新的包格式，你不能交替使用pip 和conda。因为pip不能安装和解析conda的包格式。你可以使用两个工具 但是他们是不能交互的。
>

conda环境的常用启动命令
```bash
# 启动
source activate xxx

# 关闭
source deactivate

# 更新
conda env update -f environment.yml 更新配置文件
```