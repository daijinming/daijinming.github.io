Ubuntu16.04 下安装 Notepad++ 记录  

要安装Snap，请运行以下命令    
`sudo apt-get install snapd snapd-xdg-open`  
第2步：安装 Notepad ++    
`sudo snap install notepad-plus-plus`  
第三步：安装一些插件  
~~~
sudo snap connect notepad-plus-plus:process-control

sudo snap connect notepad-plus-plus:removable-media

sudo snap connect notepad-plus-plus:hardware-observe

sudo snap connect notepad-plus-plus:cups-control

~~~

  
https://www.jianshu.com/p/b16fe3649d8e


