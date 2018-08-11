Debian/Ubuntu Linux都使用apt,升级时都是: 
```bash
apt-get update 
apt-get upgrade 
apt-get dist-upgrade
```


安装或升级系统分下面几个步骤。

第一步，获得最近的软件包的列表；列表中包含一些包的信息，比如这个包是否更新过。

第二步，如果这个包没有发布更新，就不管它；

​            如果发布了更新，就把包下载到电脑上，并安装。

 

apt-get update对应的就是第一步；

apt-get upgrade 与apt-get dist-upgrade对应的是第二步。

 

由于包与包之间存在各种依赖关系。upgrade只是简单的更新包，不管这些依赖，它不和添加包，或是删除包。而dist-upgrade可以根据依赖关系的变化，添加包，删除包。

 

一般在运行upgrade或dist-upgrade之间，要运行update.

但是常常有人会问, 
upgrade和dist-upgrade有何不同。

仔细查查,似乎大家对upgrade和dist-upgrade的解释都有点不同,在此也纪录自己的看法。

我认为apt-get 的 upgrade和dist-upgrade的差别：
upgrade：系统将现有的Package升级,如果有相依性的问题,而此相依性需要安装其它新的Package或影响到其它Package的相依性时,此Package就不会被升级,会保留下来。
dist-upgrade：可以聪明的解决相依性的问题,如果有相依性问题,需要安装/移除新的Package,就会试着去安装/移除它。 
(所以通常这个会被认为是有点风险的升级) 

apt-get upgrade 和 apt-get dist-upgrade 本质上是没有什么不同的。

只不过，dist-upgrade 会识别出当依赖关系改变的情形并作出处理，而upgrade对此情形不处理。
例如软件包 a 原先依赖 b c d，但是在源里面可能已经升级了，现在是 a 依赖 b c e。这种情况下，dist-upgrade 会删除 d 安装 e，并把 a 软件包升级，而 upgrade 会认为依赖关系改变而拒绝升级 a 软件包。

man apt-get的解释: 

upgrade: upgrade is used to install the newest versions of all packages currently installed on the system from the sources enumerated in /etc/apt/sources.list. Packages currently installed with new versions available are retrieved and upgraded; under no circumstances are currently installed packages removed, or packages not already installed retrieved and installed. New versions of currently installed packages that cannot be upgraded without changing the install status of another package will be left at their current version. An update must be performed first so that apt-get knows that new versions of packages are available. 

dist-upgrade: dist-upgrade in addition to performing the function of upgrade, also intelligently handles changing dependencies with new versions of packages; apt-get has a "smart" conflict resolution system, and it will attempt to upgrade the most important packages at the expense of less.