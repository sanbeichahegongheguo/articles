Liunx安装pycharm

  Linux Installation Instructions
  ------------------------------------------------------------------------------
1. Unpack the PyCharm distribution archive that you downloaded to
     where you wish to install the program. We will refer to this destination
     location as your {installation home} below.

2. Open a console and cd into "{installation home}/bin" and type:
```bash
       ./pycharm.sh
```
to start the application. As a side effect, this will initialize various configuration files in the 
```bash
     ~/.PyCharmCE2017.3 directory.
```
3. [OPTIONAL] Add "{installation home}/bin" to your PATH environment
     variable so that you may start PyCharm from any directory.
    
4. [OPTIONAL] To adjust the value of the JVM heap size, create
      ~/.PyCharmCE2017.3/pycharm.vmoptions (or pycharm64.vmoptions
      if using a 64-bit JDK), and set the -Xms and -Xmx parameters. To see how
      to do this, you can reference the vmoptions file under
      "{installation home}/bin" as a model.



Plugins插件推荐