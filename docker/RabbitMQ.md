RabbitMQ作为一款消息队列中间件，目前比较流行，比较稳定，性能良好，那么如何通过docker来安装RabbitMQ,下面我们来看一看如何操作

这里注意获取镜像的时候要获取management版本的，不要获取last版本的，management版本的才带有管理界面。
# 获查询镜像
~~~
 docker search rabbitmq:management
~~~

# 获取镜像
~~~
docker pull rabbitmq:management
~~~

# 运行镜像
~~~
docker run -d -p 5672:5672 -p 15672:15672 --name rabbitmq rabbitmq:management
~~~

#访问管理界面

访问管理界面的地址就是 http://[宿主机IP]:15672，可以使用默认的账户登录，用户名和密码都guest
