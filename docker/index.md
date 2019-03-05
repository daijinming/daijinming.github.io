- Ubuntu下安装Docker
>https://docs.docker.com/install/linux/docker-ce/ubuntu/

- Docker镜像加速
>
修改 /etc/docker/daemon.json 文件并添加上 registry-mirrors 键值。
~~~
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
~~~
修改保存后重启 Docker 以使配置生效.
`service docker restart`

