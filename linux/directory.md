- Linux 软件安装到 /usr，/usr/local/ 还是 /opt 目录区别

~~~
/usr：系统级的目录，可以理解为C:/Windows/，

/usr/lib理解为C:/Windows/System32。
/usr/local：用户级的程序目录，可以理解为C:/Progrem Files/。用户自己编译的软件默认会安装到这个目录下。
/opt：用户级的程序目录，可以理解为D:/Software，opt有可选的意思，这里可以用于放置第三方大型软件（或游戏），

当你不需要时，直接rm -rf掉即可。在硬盘容量不够时，也可将/opt单独挂载到其他磁盘上使用。

源码放哪里？
/usr/src：系统级的源码目录。
/usr/local/src：用户级的源码目录。
~~~
