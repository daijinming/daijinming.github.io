简单说下composer update和composer install区别：这里说下 composer 的机制, 当 `composer.lock` 文件存在的时候, 执行 `composer install` 命令时, composer 会更新按照 `composer.lock` 里的 package 指定版本进行安装, 如果是执行 `composer update` 的话, 会更新 `package` 版本, 并更新 `composer.lock` 文件（没明白到底有啥区别，参考知乎）.

在composer 中国推荐的加速方法就是把默认的国外镜像换成国内的。
具体步骤：

`composer config repo.packagist composer https://packagist.phpcomposer.com`

该命令是修改config.json配置

然后在自己项目里面的composer.json文件里面添加如下：
```
     "repositories": {
            "packagist": {
                "type": "composer",
                "url": "https://packagist.phpcomposer.com"
            }
        }
```
