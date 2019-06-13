日志分两类，一类是 Docker 引擎日志；另一类是 容器日志。

Docker 引擎日志 
Docker 引擎日志 一般是交给了 Upstart(Ubuntu 14.04) 或者 systemd (CentOS 7, Ubuntu 16.04)。前者一般位于 /var/log/upstart/docker.log 下，后者一般通过 jounarlctl -u docker 来读取。


容器日志 
容器的日志 则可以通过 docker logs 命令来访问，而且可以像 tail -f 一样，使用 docker logs -f 来实时查看。如果使用 Docker Compose，则可以通过 docker-compose logs <服务名> 来查看。



[日志都在哪里？怎么收集？](https://www.cnblogs.com/YatHo/p/7866029.html)
