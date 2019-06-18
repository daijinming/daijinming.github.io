创建组件:

       我是在Node.js的命令行环境下创建的组件，先cd到angular项目的目录下

创建组件的命令:
```
        ng generate component component-name

        (ng g component component-name)

 ```

创建组件成功后会包含四个文件:
```
       component-name.component.css           // component-name组件的外部样式表

       component-name.component.html        // component-name组件的html页面

       component-name.component.ts             // component-name组件的逻辑文件

       component-name.component.spec.ts    // component-name组件的测试文件(一般不需要,可以删除)
```
component-name.conponent.css文件内容初始为空，写css

component-name.conponent.html 文件内容一般是<p>component-name works!</p>，用来写html内容

component-name.conponent.ts中:

       import {Component} from ‘@angular/core’;   //声明组件是来自于@angular/core中的方法

       @Component({

              selector:‘app-component-name’                                 //组件在html用使用的标签名

              templateUrl:‘component-name组件html文件的路径’  //也可以直接写html语言

              styleUrls:[‘component-name组件style文件的路径’]    //找到样式文件用来渲染html

})

       剩下的部分用来写component组件的逻辑部分

 

组件创建成功后，还应该在app.module.ts中

import                //导入此组件

declarations      //声明此组件
