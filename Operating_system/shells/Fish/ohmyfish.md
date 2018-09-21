<!-- TOC -->

- [1. 前言](#1-前言)
- [2. 正文](#2-正文)
    - [2.1. 安装 Oh My Fish](#21-安装-oh-my-fish)
        - [2.1.1. 安装一个新主题](#211-安装一个新主题)
        - [2.1.2. 改变主题](#212-改变主题)
        - [2.1.3. 安装插件](#213-安装插件)
        - [2.1.4. 更新包](#214-更新包)
            - [2.1.4.1. 仅更新核心功能（omf 本身），运行：](#2141-仅更新核心功能omf-本身运行)
            - [2.1.4.2. 更新所有包：](#2142-更新所有包)
            - [2.1.4.3. 显示关于包的信息](#2143-显示关于包的信息)
        - [2.1.5. 移除包](#215-移除包)
        - [2.1.6. 管理仓库](#216-管理仓库)
            - [2.1.6.1. 要管理用户安装的仓库包，使用这条命令：](#2161-要管理用户安装的仓库包使用这条命令)
            - [2.1.6.2. 列出所有安装的仓库，运行：](#2162-列出所有安装的仓库运行)
            - [2.1.6.3. 添加一个仓库：](#2163-添加一个仓库)
            - [2.1.6.4. 移除一个仓库：](#2164-移除一个仓库)
    - [2.2. Oh My Fish 排错](#22-oh-my-fish-排错)
    - [2.3. 获取帮助](#23-获取帮助)
    - [2.4. 卸载 Oh My Fish](#24-卸载-oh-my-fish)

<!-- /TOC -->
# 1. 前言
几天前，我们讨论了如何安装 Fish shell，这是一个健壮的、完全可用的 shell，带有许多很酷的功能，如自动建议、内置搜索功能、语法高亮显示、基于 web 配置等等。今天，我们将讨论如何使用 Oh My Fish (简称 omf ) ，让我们的 Fish shell 变得漂亮且优雅。它是一个 Fishshell 框架，允许你安装扩展或更改你的 shell 外观的软件包。它简单易用，快速可扩展。使用 omf，你可以根据你的想法，很容易地安装主题，丰富你的外观和安装插件来调整你的 Fish shell。

# 2. 正文
## 2.1. 安装 Oh My Fish
安装 omf 很简单。你要做的只是在你的 Fish shell 中运行下面的命令。
```bash
curl -L https://get.oh-my.fish | fish
```

一旦安装完成，你将看到提示符已经自动更改，如上图所所示。另外，你会注意到当前时间在 shell 窗口的右边。

就是这样。让我们继续并调整我们的 fish shell。

现在，让我们将 Fish Shell 变漂亮
列出所有的安装包，运行：

```fish
omf list
```
这条命令将显示已安装的主题和插件。请注意，包可以是主题或插件。安装包意味着安装主题和插件。

所有官方和社区支持的包（包括插件和主题）都托管在 Omf 主仓库 中。在这个主仓库中，你可以看到大量的仓库，其中包含大量的插件和主题。

现在让我们看一下可用的和已安装的主题列表。为此，运行：
```fish
omf theme
```

如你所见，我们只有一个已安装的主题，这是默认的，但是还有大量可用的主题。在安装之前，你在这里可以预览所有可用的主题。这个页面包含了所有的主题细节，特性，每个主题的截图示例，以及哪个主题适合谁。

### 2.1.1. 安装一个新主题
请允许我安装一个主题，例如 clearance 主题，这是一个极简的 fish shell 主题，供那些经常使用 git 的人使用。为此，运行：
```fish
omf install clearance
```

如上图所示，在安装新主题后，Fish shell 的提示立即发生了变化。

让我浏览一下系统文件，看看它如何显示。



看起来不错！这是一个非常简单的主题。它将当前工作目录，文件夹和文件以不同的颜色区分开来。你可能会注意到，它还会在提示符的顶部显示当前工作目录。

### 2.1.2. 改变主题
就像我之前说的一样，这个主题在安装后被立即应用。如果你有多个主题，你可以使用以下命令切换到另一个不同的主题：
```fish
omf theme <theme-name>
```
例如：
```fish
omf theme agnoster
```
现在我正在使用 agnoster 主题。 agnoster 就是这样改变了我 shell 的外观。



### 2.1.3. 安装插件
例如，我想安装一个天气插件。为此，只要运行：
```fish
omf install weather
```
天气插件依赖于 jq（LCTT 译注：jq 是一个轻量级且灵活的命令行JSON处理器）。所以，你可能也需要安装 jq。它通常在 Linux 发行版的默认仓库中存在。因此，你可以使用默认的包管理器来安装它。例如，以下命令将在 Arch Linux 及其衍生版中安装 jq。
```fish
sudo pacman -S jq
```
现在，在 Fish shell 中使用以下命令查看天气：
```fish
weather
```

寻找包
要搜索主题或插件，请执行以下操作：
```fish
omf search <search_string>
```
例如：
```fish
omf search nvm
```
为了限制搜索的主题范围，使用 -t 选项。
```fish
omf search -t chain
```
这条命令只会搜索主题名字中包含 “chain” 的主题。

为了限制搜索的插件范围，使用 -p 选项。
```fish
omf search -p emacs
```
### 2.1.4. 更新包
#### 2.1.4.1. 仅更新核心功能（omf 本身），运行：
```fish
omf update omf
```
如果是最新的，你会看到以下输出：
```
Oh My Fish is up to date.
You are now using Oh My Fish version 6.
Updating https://github.com/oh-my-fish/packages-main master... Done!
```
#### 2.1.4.2. 更新所有包：
```fish
omf update
```
要有选择地更新软件包，只需包含如下所示的包名称：
```fish
omf update clearance agnoster
```
#### 2.1.4.3. 显示关于包的信息
当你想知道关于一个主题或插件的信息时，使用以下命令：
```fish
omf describe clearance
```
这条命令将显示关于包的信息。
```
Package: clearance
Description: A minimalist fish shell theme for people who use git
Repository: https://github.com/oh-my-fish/theme-clearance
Maintainer:
```
### 2.1.5. 移除包
移除一个包，例如 emacs，运行：
```fish
omf remove emacs
```
### 2.1.6. 管理仓库
默认情况下，当你安装了 Oh My Fish 时，会自动添加官方仓库。这个仓库包含了开发人员构建的所有包。

#### 2.1.6.1. 要管理用户安装的仓库包，使用这条命令：
```fish
omf repositories [list|add|remove]
```
#### 2.1.6.2. 列出所有安装的仓库，运行：
```fish
omf repositories list
```
#### 2.1.6.3. 添加一个仓库：
```fish
omf repositories add <URL>
```
例如：
```fish
omf repositories add https://github.com/ostechnix/theme-sk
```
#### 2.1.6.4. 移除一个仓库：
```fish
omf repositories remove <repository-name>
```
## 2.2. Oh My Fish 排错
如果出现了错误，omf 足够聪明来帮助你，它可以列出解决问题的方法。例如，我安装了 clearance 包，得到了文件冲突的错误。幸运的是，在继续之前，Oh My Fish 会指示我该怎么做。因此，我只是简单地运行了以下代码来了解如何修正错误。
```fish
omf doctor
```
通过运行以下命令来解决错误：
```fish
rm ~/.config/fish/functions/fish_prompt.fish
```

无论你何时遇到问题，只要运行 omf doctor 命令，并尝试所有的建议方法。

## 2.3. 获取帮助
显示帮助部分，运行：
```fish
omf -h
```
或者
```fish
omf --help
```
## 2.4. 卸载 Oh My Fish
卸载 Oh My Fish，运行以下命令：
```fish
omf destroy
```
继续前进，开始自定义你的 fish shell。获取更多细节，请参考项目的 GitHub 页面。

这就是全部了。我很快将会在这里开始另一个有趣的指导。在此之前，请继续关注我们！

干杯！

<完>