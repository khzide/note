# NodeJS学习笔记

##  安装

### 查看版本号

```cmd
D:\>npm -v
8.15.0

D:\>node -v
v16.17.0

```



### 配置环境变量

配置package的环境变量，如果不配置全局

安装包路径默认  'C:\Users\<用户>\AppData\Roaming\npm'，

nodejs的缓存位置默认：'C:\Users\<用户>\AppData\Roaming\npm-cache'，

由于npm安装工具默认会跑到C盘[因为npmrc文件中默认的设置为：prefix=${APPDATA}\npm]，这样有时可能会因为系统权限的问题，导致不能正常成功的安装某些工具，那么我们可以先将npm安装的全局路径自定设置一下，

* 方式一：

  我们可以在nodejs的目录下[即你的node.js安装后的根目录]新建两个目录：node_global，node_cache，然后找到nodejs目录下的node_modules/npm目录下名为npmrc 或者 .npmrc文件，[为安全，我们可以先将该文件copy一个副本出来进行备份]使用文本编辑器打开，修改并新增如下：prefix 和 cache 分别对应之前新建的目录node_global 和 node_cahce 

![img](node.assets\20170223105352444.jpg)

* 方式2：

```cmd
D:\>npm config set cache "d:\nodejs\node_cache"
D:\>npm config set prefix "d:\nodejs\node_global"
```

注意：设置成功后，之后用命令npm install XXX -g（全局安装），安装以后模块就在d:\NodeJs\node_global里
