# Git问题总结

## 1、The file will have its original line endings in your working directory

出现这个问题主要原因是：我们从别人github地址上通过git clone下载下来，而又想git push到我们自己的github上，那么就会出现上面提示的错误信息

此时需要执行如下代码：
```bash
git rm -r --cached .
git config core.autocrlf false
git add .
```
. 代表当前目录

## 2、Git 的 config 有三级

### 2.1 最高级：`git config --system`

信息保存在 /etc/gitconfig

为系统设置配置。

### 2.2 第二级：`git config --global`

信息保存在 ~/.gitconfig 或 ~/.config/git/config

只针对当前用户。

### 2.3 第三级：`git congfig --local`

信息保存在当前仓库的Git目录中的 `.git/config`

只针对该仓库。

每一个级别覆盖上一级别的配置。

## 3、Git传输协议 和 HTTPS 传输协议

## 4、让git status 显示中文，解决中文乱码

### 4.1 问题描述

status查看有改动但未提交的文件时总只显示一串数字串，显示不出中文文件名，非常不方便。如下图： 

![](./pic/status-dig.jpg)

### 4.2 原因

  在默认设置下，中文在工作区状态输出时，不能正确显示，而是显示为八进制的字符编码。

### 4.3 解决办法一

将 git 配置文件 `core.quotepath`项设置为 false。 

quotepath 表示引用路径；加上`--global`表示全局配置。

可以直接在 git bash 终端输入命令：

```bash
git config --global core.quotepath false
```

但是注意，这样设置后，你的git bash终端也要设置成中文和utf-8编码，才能正确显示中文，不然还是乱码。

效果对比如下：

![](./pic/git-utf8.jpg)

git bash 终端设置办法：

- 在git bash的界面中右击空白处，弹出菜单，选择 `选项->文本->本地Locale` ，设置为 `zh_CN` ，而旁边的字符集选框选为 `UTF-8` 。
- 如果是英文界面则是： 
  `Options->Text->Locale` 改为 `zh_CN，Character set改为UTF-8`

如图：

![](./pic/git-zh-utf8.jpg)

### 4.4 解决办法二

如果你的git bash终端没有菜单选项显示，还可以通过直接修改配置文件的方式来解决中文乱码问题。

进入git的安装目录：

1. 编辑 `etc\gitconfig` Git系统文件，也有些windows系统是存放在`C:\Users\Administrator\.gitconfig`路径或`安装盘符:\Git\mingw64\etc\gitconfig`，在文件末尾增加以下内容：

```bash
[gui]  
    encoding = utf-8  
    # 代码库统一使用utf-8  
[i18n]  
    commitencoding = utf-8  
    # log编码  
[svn]  
    pathnameencoding = utf-8  
    # 支持中文路径  
[core]
    quotepath = false 
    # status引用路径不再是八进制（反过来说就是允许显示中文了）
```

2. 编辑 `etc\git-completion.bash` 文件,在文件末尾增加以下内容：

```bash
# 让ls命令能够正常显示中文
alias ls='ls --show-control-chars --color=auto' 
```

3. 编辑 `etc\inputrc` 文件，修改 output-meta 和 convert-meta 属性值：

```bash
set output-meta on  # bash可以正常输入中文  
set convert-meta off  
```

4. 最后编辑profile文件，在文件末尾添加如下内容：

```bash
export LESSHARESET=utf-8
```

   ## 5、详解git fetch与git pull的区别

git fetch和git pull都可以将远端仓库更新至本地那么他们之间有何区别?想要弄清楚这个问题有有几个概念不得不提。

- FETCH_HEAD： 是一个版本链接，记录在本地的一个文件中，指向着目前已经从远程仓库取下来的分支的末端版本。
- commit-id：在每次本地工作完成后，都会做一个git commit 操作来保存当前工作到本地的repo， 此时会产生一个commit-id，这是一个能唯一标识一个版本的序列号。 在使用git push后，这个序列号还会同步到远程仓库。

### 5.1 有了以上的概念再来说说git fetch。

- git fetch：这将更新git remote 中所有的远程仓库所包含分支的最新commit-id, 将其记录到.git/FETCH_HEAD文件中。

git fetch更新远程仓库的方式如下：

```bash
git fetch origin master:tmp 
//在本地新建一个temp分支，并将远程origin仓库的master分支代码下载到本地temp分支
git diff tmp 
//来比较本地代码与刚刚从远程下载下来的代码的区别
git merge tmp
//合并temp分支到本地的master分支
git branch -d temp
//如果不想保留temp分支 可以用这步删除
```

- 如果直接使用git fetch，则步骤如下：

- 创建并更新本地远程分支。即创建并更新origin/xxx 分支，拉取代码到origin/xxx分支上。
- 在FETCH_HEAD中设定当前分支-origin/当前分支对应，如直接到时候git merge就可以将origin/abc合并到abc分支上。

```bash
git fetch origin
//只是手动指定了要fetch的remote。在不指定分支时通常默认为master.
```

```bash
git fetch origin dev
//指定远程remote和FETCH_HEAD，并且只拉取该分支的提交。
```

### 5.2 git pull

首先，基于本地的FETCH_HEAD记录，比对本地的FETCH_HEAD记录与远程仓库的版本号，然后git fetch 获得当前指向的远程分支的后续版本的数据，然后再利用git merge将其与本地的当前分支合并。所以可以认为git pull是git fetch和git merge两个步骤的结合。 
git pull的用法如下：

```bash
git pull <远程主机名> <远程分支名>:<本地分支名>

//取回远程主机某个分支的更新，再与本地的指定分支合并。
```

因此，与git pull相比git fetch相当于是从远程获取最新版本到本地，但不会自动merge。

如果需要有选择的合并git fetch是更好的选择。效果相同时git pull将更为快捷。



本文来自 R-H-R 的CSDN 博客 ，全文地址请点击：https://blog.csdn.net/riddle1981/article/details/74938111?utm_source=copy 

## 6、Git 里删除文件

## 7、git log 格式化输出

git log命令可一接受一个--pretty选项，来确定输出的格式。

如果我们只想输出hash，可以输入：

```bash
git log --pretty=format:"%h" 
```

git用各种placeholder来决定各种显示内容： 下面内容来自[这里](http://linux.die.net/man/1/git-show)

```bash
%H: commit hash
%h: 缩短的commit hash
%T: tree hash
%t: 缩短的 tree hash
%P: parent hashes
%p: 缩短的 parent hashes
%an: 作者名字
%aN: mailmap的作者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
%ae: 作者邮箱
%aE: 作者邮箱 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
%ad: 日期 (--date= 制定的格式)
%aD: 日期, RFC2822格式
%ar: 日期, 相对格式(1 day ago)
%at: 日期, UNIX timestamp
%ai: 日期, ISO 8601 格式
%cn: 提交者名字
%cN: 提交者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
%ce: 提交者 email
%cE: 提交者 email (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
%cd: 提交日期 (--date= 制定的格式)
%cD: 提交日期, RFC2822格式
%cr: 提交日期, 相对格式(1 day ago)
%ct: 提交日期, UNIX timestamp
%ci: 提交日期, ISO 8601 格式
%d: ref名称
%e: encoding
%s: commit信息标题
%f: sanitized subject line, suitable for a filename
%b: commit信息内容
%N: commit notes
%gD: reflog selector, e.g., refs/stash@{1}
%gd: shortened reflog selector, e.g., stash@{1}
%gs: reflog subject
%Cred: 切换到红色
%Cgreen: 切换到绿色
%Cblue: 切换到蓝色
%Creset: 重设颜色
%C(...): 制定颜色, as described in color.branch.* config option
%m: left, right or boundary mark
%n: 换行
%%: a raw %
%x00: print a byte from a hex code
%w([[,[,]]]): switch line wrapping, like the -w option of git-shortlog(1).
```



除此之外， 使用 `--graph` 选项可以显示 branch 的 ascii 图例。

如果你自己定制了一个喜欢的输出方案，可以保存到 git config，或者设置 alias 以便日后使用。
`~/.gitconfig` 中加入:

```bash
[alias]
    lg = log --graph
```

或者运行：

```bash
git config --global alias.lg "log --graph"
```

最后来一个[别人分享](http://www.jukie.net/bart/blog/pimping-out-git-log)的例子，稍微有些慢，但是可以看下`git log`定制效果，效果很酷。。

```bash
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%Creset %Cblue%cn%Creset' --abbrev-commit --date=relative
```

