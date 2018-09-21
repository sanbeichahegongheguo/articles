使用Mac的一些体会

## 一、一定要回使用命令行
### ①必装软件或包
#### 1、brew

brew是一个第三方基于Ruby开发的Mac OS X操作系统软件包管理工具，类似于centos下的yum或者ubuntu下的apt-get，非常方便，免去了自己手动编译安装的不便。
```bash
brew 安装目录  /usr/local/Cellar
brew 配置目录  /usr/local/etc
brew 命令目录  /usr/local/bin
```
　　注：homebrew在安装完成后自动在/usr/local/bin加个软连接，所以平常都是用这个路径。

\# 安装方法（在终端根目录下输入）：

>官方安装地址的安装方式：
>```bash
>/usr/bin/ruby <(curl -fsSkL raw.github.com/mxcl/homebrew/go)
>```
>但很不稳定，推荐命令：
>```bash
>/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
>```

输入几次密码和回车后就安装成功了。

\# 常用命令
```bash
brew list                   # 显示目前已经安装的软件包，建议安装完毕就先使用一次。看看是否已经安装了git，如果没有git包（一般默认都会安装了），请先输入 brew install git 安装git，因为后面的更新都是通过Git命令更新。我的版本默认安装有 gmp, isl, libmpc, mpfr
brew install [包的名称]      # 就可以直接安装所需要的包
brew update                 # 更新brew可安装的更新包
brew search 包的名称         # 搜索包含包名称的程序
brew tap                    # 查看安装的扩展列表
brew home 包的名称           # 用浏览器打开包的介绍页面
brew info 包的名称           # 显示包的信息
brew deps 包的名称           # 显示包的依赖
brew -h                     # brew的帮助文档
```
———————————————————————————————————————
```bash
brew search php55         # 搜索php5.5
brew install php55        # 安装php5.5
brew remove  php55        # 卸载php5.5
brew upgrade php55        # 升级php5.5
brew options php55        # 查看php5.5安装选项
brew info php55           # 查看php5.5相关信息
brew home php55           # 访问php5.5官方网站
brew services list        # 查看系统通过 brew 安装的服务
brew services cleanup     # 清除已卸载无用的启动配置文件
brew services restart php55 # 重启php-fpm
```
#### 2、替换homebrew镜像源

由于homebrew上面的东西，很多要么被墙，要么速度很慢，建议更换brew源(操作分为两部分，这步也完全可以跳过，等一会觉得速度确实慢的时候再修改，因为我觉得没修改的是速度也没有特别慢，可能是以前网络确实慢)：

\# 替换homebrew默认源

~目录下输入：
```bash
cd "$(brew --repo)"  # 这个命令会进入到相应目录，可以用pwd命令查看
```
```bash
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git\ # 这个命令就是修改镜像源为清华镜像源。清华镜像源详细介绍见：[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)# Homebrew Bottles源(二进制代码包)
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```
然后输入命令更新：
```bash
brew update
```
#### 3、cask

先看一下介绍：

>####brew
>
>Homebrew is the easiest and most flexible way to install the UNIX tools Apple didn’t include with macOS.
>
>####brew cask
>
>Homebrew-Cask extends Homebrew and brings its elegance, simplicity, and speed to macOS applications and large binaries alike。
>
>简单来说，就是因为Mac是基于Unix的，为了便于安装了使用Apple没有提供的GNU下的多种Unix工具，开发者开发了brew工具。而brew cask是对于brew的扩展，可以采用brew的方式安装图形界面的软件。brew cask search | wc -l 可以得到cask的数量是3754个。例如常用的包括java, mactex, rstudio等。
>
>作者：leether
>
>链接：https://www.zhihu.com/question/22624898/answer/238123831
>
>来源：知乎
>
>著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
>

---

> brew主要用来下载一些不带界面的命令行下的工具和第三方库来进行二次开发。
>
> brew cask主要用来下载一些带界面的应用软件，下载好后会自动安装，并能在mac中直接运行使用。
>
> 举个例子，
>
> brew install curl可以安装curl第三方库，这样你在开发时就可以使用它的库来进行开发；
>
> brew cask install chrome可以安装谷歌浏览器应用程序，可直接运行brew偏管理第三方库和命令行工具方面。brew cask可以看作是苹果官方app store的补充，是一个众多贡献者们维护的非苹果官方软件商店，你也可以在这里下mac软件。
>
> 有一些免费好用的mac软件没有在苹果官方app store商店上架，我们就可以在brew cask中下载。如果我要下载10个免费小软件，而这些软件没有在苹果商店上架，我们不需要一个一个去谷歌它们的官方网站，再去这些软件的官网去下载，我们统一在brew cask中下载。使用brew cask来进行包管理还有一个好处，这10个免费软件如果自身不带升级功能，但现在它们有更新，直接在brew cask里就可以统一升级。这也是你问的那句”为何网路上跟推荐用brew cask呢？”的原因。
>
> 如果安装mac图形界面软件，推荐先在苹果官方商店里搜索下载，没有的话去brew cask试试，如果还没有，只能去这个软件的官方网站去下载了。
>
> 作者：Cloud Strife
>
> 链接：https://www.zhihu.com/questin/22624898/answer/105234217
>
> 来源：知乎
>
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

\# 安装方法：

在根目录下输入：
```bash
brew install cask
```
#### 4、iterm2

iterm2 是一款远比系统自带的终端更好看的终端界面。在已经安装了cask之后就可以用命令行来安装了。

\# 安装方法：

在根目录下输入：
```bash
brew cask iterm2
```
安装完成后，在Preference>Profiles>Colors 右下角选择主题。iterm2早期版本不带什么主题，所以搜索iterm2的话会出来一些建议下载主题的帖子，那都是老帖子了，后来的新版本自带了，推荐使用Solarized Dark。

#### 5、tree

最后在讲配置终端界面前，再建议装一个包tree，懂的人自然懂。

在根目录下输入：
```bash
brew install tree
```
即可。

# 一些好玩的包的推荐介绍

### ②、终端界面的设置

#### 1、弃用bash，选用zsh

zsh和bash都是shell，只是zsh的可扩展性远远强于bash，所以建议由极客精神的朋友使用zsh，在以后的工作中慢慢学着来配置专属于自己的shell。

> Shell是Linux/Unix的一个外壳，你理解成衣服也行。它负责外界与Linux内核的交互，接收用户或其他应用程序的命令，然后把这些命令转化成内核能理解的语言，传给内核，内核是真正干活的，干完之后再把结果返回用户或应用程序。
>
> Linux/Unix提供了很多种Shell，为毛要这么多Shell？难道用来炒着吃么？那我问你，你同类型的衣服怎么有那么多件？花色，质地还不一样。写程序比买衣服复杂多了，而且程序员往往负责把复杂的事情搞简单，简单的事情搞复杂。牛程序员看到不爽的Shell，就会自己重新写一套，慢慢形成了一些标准，常用的Shell有这么几种，sh、bash、csh等，想知道你的系统有几种shell，可以通过以下命令查看：
>```bash
>cat /ect/shells
>```
> 显示如下：
>```bash
>/bin/bash
>/bin/csh
>/bin/ksh
>/bin/sh
>/bin/tcsh
>/bin/zsh
>```
> 在 Linux 里执行这个命令和 Mac 略有不同，你会发现 Mac 多了一个 zsh，也就是说 OS X 系统预装了个 zsh，这是个神马 Shell 呢？
>
> 目前常用的 Linux 系统和 OS X 系统的默认 Shell 都是 bash，但是真正强大的 Shell 是深藏不露的 zsh， 这货绝对是马车中的跑车，跑车中的飞行车，史称『终极 Shell』，但是由于配置过于复杂，所以初期无人问津，很多人跑过来看看 zsh 的配置指南，什么都不说转身就走了。直到有一天，国外有个穷极无聊的程序员开发出了一个能够让你快速上手的zsh项目，叫做「oh my zsh」，Github 网址是：https://github.com/robbyrussell/oh-my-zsh。这玩意就像「X天叫你学会 C++」系列，可以让你神功速成，而且是真的。
>
> 好，下面我们看看如何安装、配置和使用 zsh。
>
> ——池建强

改用zsh方法：

根目录下输入
```bash
chsh -s /bin/zsh
```
输入用户密码即可。

#### 2、安装oh-my-zsh

上面池老师也说了，oh-my-zsh 是国外一个大神给针对zsh已经配置好的一个工具，安装之后针对自己的喜好进行修改就可以高效使用了。

\# 自动安装方法：

根目录下输入1行命令
```bash
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```
> 或者
```
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"****
```
在这之前如果你没有安装wget，那么请先输入
```bash
brew install wget
```
**wget**是一个从网络上自动下载文件的自由工具，支持通过HTTP、HTTPS、FTP三个最常见的TCP/IP协议下载，并可以使用HTTP代理。*wget*名称的由来是“World Wide Web”与“get”的结合。

\# 手动安装方法：

根目录下输入2行命令
```bash
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
![img](https://img-blog.csdn.net/20170317093135310?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzMxMDA3NQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

出现这个图就是安装成功。

#### 3、配置oh-my-zsh

安装了oh-my-zsh之后，~目录下就会有一个.zshrc（注意开头有点，可以先 ls -a 命令看一下）。

输入命令：
```bash
open ~/.zshrc
```
就可以看到oh-my-zsh已经给你提议的配置。

注意开头有 \# 的都只是注释状态，未有生效。只有有的命令去掉 \# 之后才能生效。

下面先一一解释一下。

1、头五行是讲你需要配置自己的shell路径，并使用zsh作为你的shell，并告诉你的oh-my-zsh的安装路径。（忽略）

**2、中间就是告诉你可以设置zsh的主题，默认是robbyrussell，池建强老师用的就是这个默认主题，但是我的用的是ys。修改就是在ZSH_THEME= 的后面输入你想要的主题名称即可，一定要注意的是，去掉那个引号才能生效。看文档的说明，也可以用“randon”，这样每次打开shell都会随机用一个主题。**

\#修改想了解大部分的zsh主题可以点击这里

池建强老师说自己虽然用的是robbyrussell，不过他又跑到robbyrussell的主题文档里对里面一个配置做了修改：

> ```
> PROMPT='%{$fg_bold[red]%}➜ %{$fg_bold[green]%}%p%{$fg[cyan]%}%d %{$fg_bold[blue]%}$(git_prompt_info)%{$fg_bold[blue]%}% %{$reset_color%}>'
> #PROMPT='%{$fg_bold[red]%}➜ %{$fg_bold[green]%}%p %{$fg[cyan]%}%c %{$fg_bold[blue]%}$(git_prompt_info)%{$fg_bold[blue]%} % %{$reset_color%}'
> ```

对照原来的版本，他把cyan后面的 c 改为 d。因为c 表示当前目录，d 表示绝对路径，另外在末尾增加了一个「 > 」.

也就是说池老师也是喜欢显示绝对路径。而这个功能ys就已经配置好了。

3、接着文档就是告诉你看oh-my-zsh已经下载的主题，是在  ~/.oh-my-zsh/themes/   下查看。具体内容我们上一个超链接里都有讲。

4、接下来是

>\# Uncomment the following line to use case-sensitive completion.
>
>\# CASE_SENSITIVE=”true“

case-sensitive 就是大小写敏感的意思。如果把那个 \# 去掉，就会生效，不去掉就不开启。

5、接来下是

> \# HYPHEN_INSITIVE="true"

这是连字符不敏感。文档也不建议打开，因为会导致  _  和  -  无法区分。

6、接下来是

> \# DISABEL_AUTO_UPDATE="true"

很明显是不允许自动更新的。当然也不建议了。

7、接下来是

> \# ENABLE_CORRECTION="true"

校正功能。这个打开了会很麻烦，特别是系统总是容易自以为是帮你修正。没必要，我们有相应功能更强大的插件就好。后面会给大家介绍。

8、接下来是

>\# COMPLETION_WAITING_DOTS="true"

按tab键补全命令的时候，如果没什么可补全的就会出现三个红点，更人性化显示。这里我们启用，所以删去 \#。

9、接下来是

> \# DISABLE_UNTRACKED_FILES_DIRTY="true"

这是对文件储存做记录的，用不到，忽略。

10、接下来是

> \# The optional three formats: "mm/dd/yyyy" | "dd.mm.yyyy" | "yyyy-mm-dd"
>
> \# HIST_STAMPS="mm/dd/yyyy"

这是历史命令日期显示格式的设置。有三种方式： "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"。我个人喜好第三个，所以删去 \#， 然后设置为：

> HIST_STAMPS="yyyy-mm-dd"

11、接下来是

> \# Would you like to use another custom folder than $ZSH/custom?
>
> \# ZSH_CUSTOM=/path/to/new-custom-folder

设置一个新的zsh环境。忽略。

12、重点来了，选择 oh-my-zsh 插件的。

> \# Which plugins would you like to load? (plugins can be found in ~/.oh-my-zsh/plugins/*)
>
> \# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/\
>
> \# Example format: plugins=(rails git textmate ruby lighthouse)
>
> \# 插件设置，如果添加太多启动速度会比较慢
>
> plugins=(git autojump)

不要添加太多，添加太多会变慢。

在目录   ~/.oh-my-zsh/plugins   下可以看到所有已经安装的插件（共213个）：

>|oh-my-zsh插件       |
>| :----------       |
>|adb                |
>|ant                |
>|apache2-macports   |
>| archlinux         |
>| asdf               |
>| autoenv                                                      |
>| autojump                                                     |
>| autopep8                                                     |
>| aws                                                          |
>| battery                                                      |
>| bbedit                                                       |
>| bgnotify                                                     |
>| boot2docker                                                  |
>| bower                                                        |
>| branch                                                       |
>| brew                                                         |
>| brew-cask                                                    |
>| bundler                                                      |
>| bwana                                                        |
>| cabal                                                        |
>| cake                                                         |
>| cakephp3                                                     |
>| capistrano                                                   |
>| cask                                                         |
>| catimg                                                       |
>| celery                                                       |
>| chruby                                                       |
>| chucknorris                                                  |
>| cloudapp                                                     |
>| codeclimate                                                  |
>| coffee                                                       |
>| colemak                                                      |
>| colored-man-pages                                            |
>| colorize                                                     |
>| command-not-found                                            |
>| common-aliases                                               |
>| compleat                                                     |
>| composer                                                     |
>| copydir                                                      |
>| copyfile                                                     |
>| cp                                                           |
>| cpanm                                                        |
>| debian                                                       |
>| dircycle                                                     |
>| dirhistory                                                   |
>| dirpersist                                                   |
>| django                                                       |
>| dnf                                                          |
>| docker                                                       |
>| docker-compose                                               |
>| emacs                                                        |
>| ember-cli                                                    |
>| emoji                                                        |
>| emoji-clock                                                  |
>| emotty                                                       |
>| encode64                                                     |
>| extract     功能强大的解压插件，所有类型的文件解压一个命令  x   全部搞定，不用再要去记忆  tar   后面的参数了。不过不是经常使用压缩文件的不是特别建议开启，有需要的时候开启，用完后在配置里删去。![img](https://upload-images.jianshu.io/upload_images/44137-8ae00edef5e5c8dc.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/700) |
>| fabric                                                       |
>| fancy-ctrl-z                                                 |
>| fasd                                                         |
>| fastfile                                                     |
>| fbterm                                                       |
>| fedora                                                       |
>| forklift                                                     |
>| frontend-search                                              |
>| gas                                                          |
>| geeknote                                                     |
>| gem                                                          |
>| git         此插件为默认开启的插件，提供了大量git的alias（即别名/缩写命令）。 ![img](https://upload-images.jianshu.io/upload_images/44137-b6e9ba5d15e88b81.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/622) |
>| git-extras                                                   |
>| gitfast                                                      |
>| git-flow                                                     |
>| git-flow-avh                                                 |
>| github                                                       |
>| git-hubflow                                                  |
>| gitignore                                                    |
>| git-prompt                                                   |
>| git-remote-branch                                            |
>| glassfish                                                    |
>| gnu-utils                                                    |
>| go                                                           |
>| golang                                                       |
>| gpg-agent                                                    |
>| gradle                                                       |
>| grails                                                       |
>| grunt                                                        |
>| gulp                                                         |
>| heroku                                                       |
>| history                                                      |
>| history-substring-search                                     |
>| httpie                                                       |
>| iwhois                                                       |
>| jake-node                                                    |
>| jhbuild                                                      |
>| jira                                                         |
>| jruby                                                        |
>| jsontools                                                    |
>| jump                                                         |
>| kate                                                         |
>| kitchen                                                      |
>| knife                                                        |
>| knife_ssh                                                    |
>| laravel                                                      |
>| laravel4                                                     |
>| laravel5                                                     |
>| last-working-dir                                             |
>| lein                                                         |
>| lighthouse                                                   |
>| lol                                                          |
>| macports                                                     |
>| man                                                          |
>| marked2                                                      |
>| mercurial                                                    |
>| meteor                                                       |
>| mix                                                          |
>| mix-fast                                                     |
>| mosh                                                         |
>| mvn                                                          |
>| mysql-macports                                               |
>| n98-magerun                                                  |
>| nanoc                                                        |
>| nmap                                                         |
>| node                                                         |
>| npm                                                          |
>| nvm                                                          |
>| nyan                                                         |
>| osx                                                          |
>| pass                                                         |
>| paver                                                        |
>| pep8                                                         |
>| per-directory-history                                        |
>| perl                                                         |
>| phing                                                        |
>| pip                                                          |
>| pj                                                           |
>| pod                                                          |
>| postgres                                                     |
>| pow                                                          |
>| powder                                                       |
>| powify                                                       |
>| profiles                                                     |
>| pyenv                                                        |
>| pylint                                                       |
>| python                                                       |
>| rails                                                        |
>| rake                                                         |
>| rake-fast                                                    |
>| rand-quote                                                   |
>| rbenv                                                        |
>| rbfu                                                         |
>| rebar                                                        |
>| redis-cli                                                    |
>| repo                                                         |
>| rsync                                                        |
>| ruby                                                         |
>| rvm                                                          |
>| safe-paste                                                   |
>| sbt                                                          |
>| scala                                                        |
>| scd                                                          |
>| screen                                                       |
>| scw                                                          |
>| sfffe                                                        |
>| singlechar                                                   |
>| spring                                                       |
>| sprunge                                                      |
>| ssh-agent                                                    |
>| stack                                                        |
>| sublime  如果sublime用得多，该插件可以用命令行打开sublime。我不是很常用，没开启。常用命令如下： ![img](C:\Users\liumian\AppData\Local\Temp\企业微信截图_15243741176118.png) |
>| sudo                                                         |
>| supervisor                                                   |
>| suse                                                         |
>| svn                                                          |
>| svn-fast-info                                                |
>| symfony                                                      |
>| symfony2                                                     |
>| systemadmin                                                  |
>| systemd                                                      |
>| taskwarrior                                                  |
>| terminalapp                                                  |
>| terminitor                                                   |
>| terraform                                                    |
>| textastic                                                    |
>| textmate                                                     |
>| thefuck                                                      |
>| themes                                                       |
>| thor                                                         |
>| tmux                                                         |
>| tmux-cssh                                                    |
>| tmuxinator                                                   |
>| torrent                                                      |
>| tugboat                                                      |
>| ubuntu                                                       |
>| urltools                                                     |
>| vagrant                                                      |
>| vault                                                        |
>| vim-interaction                                              |
>| vi-mode                                                      |
>| virtualenv                                                   |
>| virtualenvwrapper                                            |
>| vundle                                                       |
>| wakeonlan                                                    |
>| wd                                                           |
>| web-search                                                   |
>| wp-cli                                                       |
>| xcode                                                        |
>| yii                                                          |
>| yii2                                                         |
>| yum                                                          |
>| z   强大的目录自动跳转命令，会记忆你曾经进入过的目录，用模糊匹配快速进入你想要的目录。 建议开启。![img](https://upload-images.jianshu.io/upload_images/44137-19c4861379da0110.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/700) |
>| zeus                                                         |
>| zsh-navigation-tools                                         |
>| zsh_reload                                                   |

除了上面默认自带的一百多个插件，我这里再推荐两个插件：



13、
