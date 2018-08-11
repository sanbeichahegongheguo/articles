## 一、Liunx下安装R和Rstudio



## Prerequisites

RStudio Server v1.1 requires Debian version 8 (or higher) or Ubuntu version 12.04 (or higher).

**Installing R**
RStudio requires a previous installation of R version 3.0.1 or higher. To install the latest version of R you should first add the CRAN repository to your system as described here:

- [Debian Packages for R](https://cran.rstudio.com/bin/linux/debian/)
- [Ubuntu Packages for R.](http://cran.rstudio.com/bin/linux/ubuntu/README.html)

You can then install R using the following command:

```bash
sudo apt-get install r-base
```

***NOTE***: if you do not add the CRAN Debian or Ubuntu repository as described above this command will install the version of R corresponding to your current system version. Since this version of R may be a year or two old it is strongly recommended that you add the CRAN repositories so you can run the most up to date version of R.

## Debian 8 / Ubuntu

To download and install RStudio Server open a terminal window and execute the following commands (corresponding to the 32 or 64-bit version as appropriate). Note that the gdebi-core package is installed first so that gdebi can be used to install RStudio and all of its dependencies.

**64bit** 

Size:  60.6 MB MD5: ea77929e40eac30baee9e336e26a1dd5 Version:  1.1.456 Released:  2018-07-19
```bash
sudo apt-get install gdebi-core`
wget https://download2.rstudio.org/rstudio-server-1.1.456-amd64.deb`
sudo gdebi rstudio-server-1.1.456-amd64.deb`
```
**32bit** 

Size:  51.8 MB MD5: f3e2e67cdb0ec84fd62076f5d0f7539c Version:  1.1.456 Released:  2018-07-19
```bash
sudo apt-get install gdebi-core`
wget https://download2.rstudio.org/rstudio-server-1.1.456-i386.deb`
sudo gdebi rstudio-server-1.1.456-i386.deb`
```
## Debian 9+

To download and install RStudio Server open a terminal window and execute the following commands.

**64bit** 

Size:  38.8 MB MD5: 5ce46eeafd40bd4e2db65841f3ab5759 Version:  1.1.456 Released:  2018-07-19
```bash
sudo apt-get install gdebi-core`
wget https://download2.rstudio.org/rstudio-server-stretch-1.1.456-amd64.deb`
sudo gdebi rstudio-server-stretch-1.1.456-amd64.deb`
```
You may choose to [verify the build’s GPG signature](https://www.rstudio.com/code-signing/) prior to installing it.

## Next Steps

See the [Getting Started document](http://www.rstudio.com/ide/docs/server/getting_started) for information on configuring and managing the server.

Read the [RStudio Server Professional Admin Guide](http://docs.rstudio.com/ide/server-pro/) for more detailed instructions.





```bash
sudo ipconfig   查看机器的ip地址，其中inet：后面的为ip
```

打开浏览器，输入“ip：8787”，即可打开rstudio，用户和密码为登录系统的用户和密码。

 因为服务是在本地，所以写127.0.0.1:8787就可以开始了。

（8787 为Rstudio Server 默认的兼听端口，可以自己配置）。

 

至此安装完毕，查看网上还有后续的安装ggplot2，直接在rstudio中install.package("")即可。