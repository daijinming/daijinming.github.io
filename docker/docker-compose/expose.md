`ports`暴露容器端口到主机的任意端口或指定端口，用法：
~~~
ports:
  - "80:80"         # 绑定容器的80端口到主机的80端口
  - "9000:8080"     # 绑定容器的8080端口到主机的9000端口
  - "443"           # 绑定容器的443端口到主机的任意端口，容器启动时随机分配绑定的主机端口号
~~~
不管是否指定主机端口，使用ports都会将端口暴露给主机。

`expose`暴露容器给link到当前容器的容器，用法：
~~~
expose:
  - "3000"
  - "8000"
~~~
以上指令将当前容器的端口3000和8000暴露给link到本容器的容器。

和ports的区别是，expose不会将端口暴露给主机。