File类，是一个静态类，主要是来提供一些函数库用的。静态实用类，提供了很多静态的方法，支持对文件的基本操作，包括创建，拷贝，移动，删除和 打开一个文件。

File类方法的参量很多时候都是路径path。File的一些方法可以返回FileStream和StreamWriter的对象。可以 和他们配套使用。System.IO.File类和System.IO.FileInfo类

主要提供有关文件的各种操作，在使用时需要引用System.IO命名空间。

一、File类常用的操作方法

1、创建文件方法

//参数1：要创建的文件路径

File.Create（@"D:\Test\Debug1\测试.txt"）

2、打开文件方法

 //参数1：要打开的文件路径，参数2：打开的文件方式

File.Open(@"D:\Test\Debug1\测试.txt",FileMode.Append)

3、追加文件方法

 //参数1：要追加的文件路径，参数2：追加的内容

File.AppendAllText(@"D:\Test\Debug1\测试.txt","哈哈");

4、复制文件方法

 //参数1：要复制的源文件路径，参数2：复制后的目标文件路径，参数3：是否覆盖相同文件名
 File.Copy(@"D:\Test\Debug1\测试.txt", @"D:\Test\Debug2\测试1.txt", true);

5、移动文件方法

 //参数1：要移动的源文件路径，参数2：移动后的目标文件路径
File.Move(@"D:\Test\Debug1\测试.txt", @"D:\Test\Debug3\测试2.txt");

6、删除文件方法

 //参数1：要删除的文件路径
 File.Delete(@"D:\Test\Debug1\测试.txt");

7、设置文件属性方法

//参数1：要设置属性的文件路径，参数2：设置的属性类型（只读、隐藏等）
File.SetAttributes(@"D:\Test\Debug1\测试.txt", FileAttributes.Hidden);
