# 'pip' 不是内部或外部命令，也不是可运行的程序或批处理文件。

**解决办法**：增加环境变量。

E:\dev_install_root\Python27\Scripts

到PATH中去。

![img](./images/add scripts into path.png)

因为E:\dev_install_root\Python27\Scripts中包含了对应的pip。



# pip安装第三方库时提示:You are using pip version 8.1.1, however version 9.1.0 is available.

用pip安装第三方库时提示：

```bash
You are using pip version 8.0.2, however version 8.1.0 is available.
```

然而使用

```bash
pip install --upgrade pip 
```

无效，用

```bash
python -m pip install --upgrade pip
```

