#  创建phpMyAdmin镜像
~~~
docker run -d \ 
--name myadmin \ 
-e PMA_HOST=114.1.96.* \ 
-e PMA_PORT=6000 \ 
-p 5060:80 \ 
phpmyadmin/phpmyadmin


docker run -d --name myadmin -e PMA_HOST=114.1.96.* -e PMA_PORT=6000 -p 5060:80 phpmyadmin/phpmyadmin
~~~

更多参考：https://blog.csdn.net/weixin_36296538/article/details/84189706

