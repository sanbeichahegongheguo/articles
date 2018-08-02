## 一、vi介绍
## 二、vim介绍
通常情况下，国内使用的Ubuntu安装的vim是阉割版。
## 三、常用配置
```
syntax on
set number
set shiftwidth=4
set softtabstop=4
set tabstop=4
set expandtab
set expandtab
set showcmd
set cursorline
filetype indent on
```

## 四、插件

改变vim配色：安装colorscheme



主要有两种方式安装colorscheme：

1. 自行下载colorscheme安装，下载的文件扩展名通常为.vim。
2. 通过安装相关vim的插件获取。

### 1、自行下载colorscheme安装

在vim的配置文件`.vimrc`中配色方案的设置`colorscheme foo`为：

```
set t_Co=256 " required
colorscheme desert12
```

不过有时候我们对于自带的配色方案不太满意，那要怎么自己安装一些配色方案呢？主要分三步：

1. 在当前用户目录 `~/` 下的 `.vim` 目录(如果没有，`mkdir ~/.vim`进行新建该目录)。在 `~/.vim/` 下新建一个叫 `colors`的目录，我们下一步下载的配色方案.vim文件便放到该目录下。
2. 到一个配色网站上选择一个配色方案下载到 `~/.vim/colors` 目录下面。这里推荐一个非常好的网站: [A ColorScheme Editor for Vim](http://bytefluent.com/vivify/), 这个网站不仅有很多的配色方案可供选择，还能自行进行编辑(比如变亮或变暗)再下载。比如我们看好了一个叫molokai的配色方案，点击下载按钮后下载 molokai.vim 的文件到 `~/.vim/colors` 目录下面 
   ![vivify](./images/20160713204112504.png)
3. 修改 `.vimrc` 配置文件：`colorscheme molokai`，退出再打开vim就能看到效果了。

>注：网站上看到的配色方案效果仅供参考，不一定与实际使用的效果一样。

### 2、使用插件安装

vim插件：<https://github.com/flazz/vim-colorschemes>，使用插件管理器进行快速安装，安装完成后直接设置即可。

### 自己写一个 colorscheme

其实很简单，照葫芦画瓢即可，可以看我自己按照 spacemacs dark theme 修改的 [space-vim-dark](https://github.com/liuchengxu/space-vim-dark) colorscheme,

![space-vim](./images/space-vim-gui.png)

打开 colors 下面的 colorscheme, 其实很简单，完全可以自己写一个，主要内容差不多都是这样：

```
hi Function        ctermfg=134   guifg=#af5fd7 gui=bold            cterm=bold
hi Identifier      ctermfg=98    guifg=#875fd7 gui=bold           cterm=bold12
```

hi 就是 highlight，后面跟上一个类型，比如 Function, 就是指函数了，cterm 指的是 terminal 中的样式，比如加粗 bold，下划线 underline, gui 指的是 GUI vim中的样式，fg指的是 front ground前景色，bg 指的是 background 背景色, 基本就是如此了。

调教一番就能使用了。

reddit 上也有一个关于创建 Colorscheme 的讨论：[Creating Your Lovely Color Scheme](https://www.reddit.com/r/vim/comments/7auw18/creating_your_lovely_color_scheme_vimconf2017/)



Vim的颜色主题在
```bash
/usr/share/vim/vim74/colors
```
文件夹里。其中**vim74**文件夹名跟你所使用的vim版本号有关，如果是7.3版本，则是vim73。打开vim后在normal模式下输入“：colorscheme”查看当前的主题，修改主题使用命令“：colorscheme mycolor”，其中mycolor是你usr/share/vim/vim74/colors文件夹包含的文件名。也可以把这个命令写入~/.vimrc配置文件中，这样每次打开Vim都是你设定的主题。

![img](./images/20140322133716468.jfif)

上面是默认就会安装的colorscheme选项。
```
blue.vim      README.txt 
desert.vim    
koehler.vim  
peachpuff.vim  
slate.vim
darkblue.vim  
elflord.vim   
morning.vim      
torte.vim
default.vim   
evening.vim   
murphy.vim   
ron.vim        
zellner.vim
delek.vim     
industry.vim  
pablo.vim    
shine.vim
```

README.txt里的内容如下     

>   1 README.txt for color scheme files 
>
>   2 
>
>   3 These files are used for the ":colorscheme" command.  They appear in the
>
>   4 Edit/Color Scheme menu in the GUI.
>
>   5 
>
>   6 
>
>   7 Hints for writing a color scheme file:
>
>   8 
>
>   9 There are two basic ways to define a color scheme:
>
>   10 
>
>   11 1. Define a new Normal color and set the 'background' option accordingly.
>
>   12     set background={light or dark}
>
>   13     highlight clear
>
>   14     highlight Normal ...
>
>   15     ...
>
>   16 
>
>   17 2. Use the default Normal color and automatically adjust to the value of
>
>   18    'background'.
>
>   19     highlight clear Normal
>
>   20     set background&
>
>   21     highlight clear
>
>   22     if &background == "light"
>
>   23       highlight Error ...
>
>   24       ...
>
>   25     else
>
>   26       highlight Error ...
>
>   27       ...
>
>   28     endif
>
>   29 
>
>   30 You can use ":highlight clear" to reset everything to the defaults, and then
>
>   31 change the groups that you want differently.  This also will work for groups
>
>   32 that are added in later versions of Vim.
>
>   33 Note that ":highlight clear" uses the value of 'background', thus set it
>
>   34 before this command.
>
>   35 Some attributes (e.g., bold) might be set in the defaults that you want
>
>   36 removed in your color scheme.  Use something like "gui=NONE" to remove the
>
>   37 attributes.
>
>   38 
>
>   39 In case you want to set 'background' depending on the colorscheme selected,
>
>   40 this autocmd might be useful:
>
>   41      autocmd SourcePre */colors/blue_sky.vim set background=dark
>
>   42 Replace "blue_sky" with the name of the colorscheme.
>
>   43 
>
>   44 In case you want to tweak a colorscheme after it was loaded, check out that
>
>   45 ColorScheme autocmd event.
>
>   46 
>
>   47 To see which highlight group is used where, find the help for
>
>   48 "highlight-groups" and "group-name".
>
>   49 
>
>   50 You can use ":highlight" to find out the current colors.  Exception: the
>
>   51 ctermfg and ctermbg values are numbers, which are only valid for the current
>
>   52 terminal.  Use the color names instead.  See ":help cterm-colors".
>
>   53 
>
>   54 The default color settings can be found in the source file src/syntax.c.
>
>   55 Search for "highlight_init".
>
>   56 
>
>   57 If you think you have a color scheme that is good enough to be used by others,
>
>   58 please check the following items:
>
>   59 
>
>   60 - Does it work in a color terminal as well as in the GUI?
>
>   61 - Is "g:colors_name" set to a meaningful value?  In case of doubt you can do
>
>   62   it this way:
>
>   63     let g:colors_name = expand('<sfile>:t:r')
>
>   64 - Is 'background' either used or appropriately set to "light" or "dark"?
>
>   65 - Try setting 'hlsearch' and searching for a pattern, is the match easy to
>
>   66   spot?
>
>   67 - Split a window with ":split" and ":vsplit".  Are the status lines and
>
>   68   vertical separators clearly visible?
>
>   69 - In the GUI, is it easy to find the cursor, also in a file with lots of
>
>   70   syntax highlighting?
>
>   71 - Do not use hard coded escape sequences, these will not work in other
>
>   72   terminals.  Always use color names or #RRGGBB for the GUI.    


下面给出几个主题的实例，选择自己喜欢的，让你的Vim炫起来！

![img](./images/20140322133754562.png)

上图是evening主题

![img](./images/20140322134009671.png)

上图murphy主题

![img](./images/20140322134203859.png)

上图peachpuff主题

## 五、常用操作



