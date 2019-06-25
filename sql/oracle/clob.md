# oracle数据中，插入clob类型字段遇到的问题

varchar2 支持的最大长度为4000，当超过4000报错，查阅相关文章，提到clob类型可以存储4G大小。于是将对应表的字段设置成clob类型，clob可以直接像varchar类型一样直接插入，和读取。但是如果直接插入，默认当成varchar类型，限制长度为4000。

       已有解决上述问题，使用的方法是：
```
        declare

            v_clob clob;

        begin 

            v_clob = '需要插入的内容';

            insert into t_table ('插入clob对应的字段') values(clob);

        end ;
```

但是！但是！但是！重要事情说三遍， 还是遇到问题了，发现当xml文件大小>32k,会报PLS-00172，string literal too long，通过网上搜索，发现，PL SQL 支持最大长度为32k。找了n久，发现一种行之有效的方法，就是采用拼接方法（“||”），一个clob变量放置不超过32k大小内容。我的做法就是将xml文件内容分成多个clob，采用拼接"||",
```
        declare

            v_clob clob;

            v_clob1 clob;

            v_clob2 clob;

            ... ...

       begin 

            v_clob = '< 32k 内容';

            v_clob1 = '< 32k 内容';

            v_clob2 = '< 32k 内容';

            ... ... 

            insert into t_table ('插入clob对应的字段') values(clob||clob1||clob2....);

        end ;
```
       对clob变量申明可以多个，赋值的时候也可由多个，在插入字段时候，使用 “||” 将上述变量拼接。
       
       
       
摘自：https://my.oschina.net/u/555206/blog/877241

       
