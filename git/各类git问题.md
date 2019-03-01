# 1、The file will have its original line endings in your working directory

出现这个问题主要原因是：我们从别人github地址上通过git clone下载下来，而又想git push到我们自己的github上，那么就会出现上面提示的错误信息

此时需要执行如下代码：
```bash
git rm -r --cached .
git config core.autocrlf false
git add .
```
. 代表当前目录

# 2、Git 的 config 有三级

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