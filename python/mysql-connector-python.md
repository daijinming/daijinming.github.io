由于MySQL服务器以独立的进程运行，并通过网络对外服务，所以，需要支持Python的MySQL驱动来连接到MySQL服务器。

目前，有两个MySQL驱动：
- mysql-connector-python：是MySQL官方的纯Python驱动；
- MySQL-python：是封装了MySQL C驱动的Python驱动。

我们以mysql-connector-python为例，演示如何连接到MySQL服务器的test数据库：
~~~
## pipenv install mysql-connector-python

import mysql.connector


config = {
    'host': '127.0.0.1',
    'user': 'demo',
    'password': 'demo123',
    'port': 3306,
    'database': 'demodb',
    'charset': 'utf8'
}

## ** 这里被称为关键字参数
conn = mysql.connector.connect(**config)

cursor = conn.cursor()

# 创建user表:
cursor.execute('create table user (id varchar(20) primary key, name varchar(20))')
# 插入一行记录，注意MySQL的占位符是%s:
cursor.execute('insert into user (id, name) values (%s, %s)', ['1', 'Michael'])

print(cursor.rowcount)

# 提交事务:
conn.commit()
cursor.close()

# 运行查询:

cursor = conn.cursor()
cursor.execute('select * from user where id = %s', ('1',))
values = cursor.fetchall()
print(values)
# 关闭Cursor和Connection:
cursor.close()
conn.close()

~~~
由于Python的DB-API定义都是通用的，所以，操作MySQL的数据库代码和SQLite类似。

# 小结

- MySQL的SQL占位符是%s；

- 通常我们在连接MySQL时传入use_unicode=True，让MySQL的DB-API始终返回Unicode。

摘自：·[安装MySQL驱动](https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001391435131816c6a377e100ec4d43b3fc9145f3bb8056000)
