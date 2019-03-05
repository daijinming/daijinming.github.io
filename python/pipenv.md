在使用pipenv之前，必须彻底的忘记pip这个东西
新建一个准备当环境的文件夹pipenvtest，并cd进入该文件夹：
`pipenv --three`   会使用当前系统的Python3创建环境

`pipenv --python 3.6` 指定某一Python版本创建环境

`pipenv shell` 激活虚拟环境

`pipenv --where`  显示目录信息

`/home/jiahuan/pipenvtest`

`pipenv --venv`  显示虚拟环境信息

`/home/jiahuan/.local/share/virtualenvs/pipenvtest-9KKRH3OW`

`pipenv --py`  显示Python解释器信息

`/home/jiahuan/.local/share/virtualenvs/pipenvtest-9KKRH3OW/bin/python`

`pipenv install requests` 安装相关模块并加入到Pipfile

`pipenv install django==1.11` 安装固定版本模块并加入到Pipfile

`pipenv graph` 查看目前安装的库及其依赖

`pipenv check`检查安全漏洞

`pipenv uninstall --all` 卸载全部包并从Pipfile中移除
