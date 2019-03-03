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


