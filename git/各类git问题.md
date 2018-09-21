# The file will have its original line endings in your working directory

出现这个问题主要原因是：我们从别人github地址上通过git clone下载下来，而又想git push到我们自己的github上，那么就会出现上面提示的错误信息

此时需要执行如下代码：
```bash
git rm -r --cached .
git config core.autocrlf false
git add .
```
. 代表当前目录


