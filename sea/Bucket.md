~~~
<?php
//新浪云 Storage PHP use
use sinacloud\sae\Storage as Storage;

// 方法一：在新浪云运行环境中时可以不传认证信息，默认会从应用的环境变量中取
$s = new Storage();

//**Bucket 操作**
// 创建一个 Bucket test
$s->putBucket("test");

// 获取 Bucket 列表
print_r($s->listBuckets());

// 获取 Bucket 列表及 Bucket 中 Object 数量和 Bucket 的大小
print_r($s->listBuckets(true));

// 获取 test 这个 Bucket 中的 Object 对象列表，默认返回前 1000 个，如果需要返回大于 1000 个 Object 的列表，可以通过 limit 参数来指定。
print_r($s->getBucket("test"));

// 获取 test 这个 Bucket 中所有以 a/ 为前缀的 Objects 列表
print_r($s->getBucket("test", 'a/'));

// 获取 test 这个 Bucket 中所有以 a/ 为前缀的 Objects 列表，只显示 a/N 这个 Object 之后的列表（不包含 a/N 这个 Object）。
$s->getBucket("test", 'a/', 'a/N');

// Storage 也可以当成一个伪文件系统来使用，比如获取 a/ 目录下的 Object（不显示其下的子目录的具体 Object 名称，只显示目录名）
$s->getBucket("test", 'a/', null, 10000, '/');

// 删除一个空的 Bucket test
$s->deleteBucket("test");

// 获取 Bucket 列表
print_r($s->listBuckets());


/**Object 上传操作**/

// 把 $_FILES 全局变量中的缓存文件上传到 test 这个 Bucket，设置此 Object 名为 1.txt
$s->putObjectFile($_FILES['uploaded']['tmp_name'], "test", "1.txt");

// 把 $_FILES 全局变量中的缓存文件上传到 test 这个 Bucket，设置此 Object 名为 sae/1.txt
$s->putObjectFile($_FILES['uploaded']['tmp_name'], "test", "sae/1.txt");

// 上传一个字符串到 test 这个 Bucket 中，设置此 Object 名为 string.txt，并且设置其 Content-type
$s->putObject("This is string.", "test", "string.txt", array(), array('Content-Type' => 'text/plain'));

 // 上传一个文件句柄（必须是 buffer 或者一个文件，文件会被自动 fclose 掉）到 test 这个 Bucket 中，设置此 Object 名为 file.txt
 $s->putObject(Storage::inputResource(fopen($_FILES['uploaded']['tmp_name'], 'rb'), filesize($_FILES['uploaded']['tmp_name']), "test", "file.txt", Storage::ACL_PUBLIC_READ);
 

/**Object 下载操作**/

// 从 test 这个 Bucket 读取 Object 1.txt，输出为此次请求的详细信息，包括状态码和 1.txt 的内容等
var_dump($s->getObject("test", "1.txt"));

// 从 test 这个 Bucket 读取 Object 1.txt，把 1.txt 的内容保存在 SAE_TMP_PATH 变量指定的 TmpFS 中，savefile.txt 为保存的文件名；
//SAE_TMP_PATH 路径具有写权限，用户可以往这个目录下写文件，
//但文件的生存周期等同于 PHP 请求，也就是当该 PHP 请求完成执行时，所有写入 SAE_TMP_PATH 的文件都会被销毁
$s->getObject("test", "1.txt", SAE_TMP_PATH ."savefile.txt");

// 从 test 这个 Bucket 读取 Object 1.txt，把 1.txt 的内容保存在打开的文件句柄中/$s->getObject("test", "1.txt", fopen(SAE_TMP_PATH."savefile.txt", 'wb'));


/**Object 删除操作**/

// 从 test 这个 Bucket 删除 Object 1.txt
$s->deleteObject("test", "1.txt");


/**Object 复制操作**/

// 把 test 这个 Bucket 的 Object 1.txt 内容复制到 newtest 这个 Bucket 的 Object 1.txt
$s->copyObject("test", "1.txt", "newtest", "1.txt");

// 把 test 这个 Bucket 的 Object 1.txt 内容复制到 newtest 这个 Bucket 的 Object 1.txt，并设置 Object 的浏览器缓存过期时间为 10s 和 Content-Type 为 text/plain
$s->copyObject("test", "1.txt", "newtest", "1.txt", array('expires' => '10s'), array('Content-Type' => 'text/plain'));


/**生成一个外网能够访问的 url**/

// 为私有 Bucket test 中的 Object 1.txt 生成一个能够在外网用 GET 方法临时访问的 URL，次 URL 过期时间为 600s
$s->getTempUrl("test", "1.txt", "GET", 600);

// 为 test 这个 Bucket 中的 Object 1.txt 生成一个能用 CDN 访问的 URL
$s->getCdnUrl("test", "1.txt");


/**调试模式**/

// 开启调试模式，出问题的时候方便定位问题，设置为 true 后遇到错误的时候会抛出异常而不是写一条 warning 信息到日志。
$s->setExceptions(true);

?>
~~~

use sinacloud\sae\Storage as Storage
Storage类文档地址： http://apidoc.sinaapp.com/source-class-sinacloud.sae.Storage.html#110-950


