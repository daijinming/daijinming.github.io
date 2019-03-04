- git clone 的另外一种方式

~~~
#创建目录，初始化本地仓库
$ mkdir search && cd search
$ git init 
$ git remote add github git@github.com:yyy/search.git
# 实际上，pull 就是 fetch + merge
$ git pull github --all --tags
~~~

- 把工作目录迁移到Github上去

~~~
$ git remote add github git@github.com:yyfrankyy/search.git
$ git push github --all --tags
~~~

- 显示所有的远程仓库
`git remote -v`


- 查看项目仓库中包含的标签

示例根据章节设置了对应的标签，每个标签都对应一个程序版本。可以使用 git tag -n 命令查看项目中包含的标签

`git tag -n`

使用 git checkout 签出对应标签版本的代码，添加添加标签名作为参数。

`git checkout foo`

撤销改动

`git reset --hard`

比较两个版本的变化

`git diff foo bar`

直观的方法查看版本变化,打开 git浏览客户端

`gitk`

定期使用 git fetch更新本地库

~~~
git fetch --all
git fetch --tags
git reset --hard origin/master	
~~~


