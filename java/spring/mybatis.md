- 官方教程
http://www.mybatis.org/mybatis-3/zh/index.html

- 关于分页
```
实现：通过sql语句实现分页也是非常简单的，只是需要改变我们查询的语句就能实现了，即在sql语句后面添加limit分页语句。

首先还是在StudentMapper接口中添加sql语句查询的方法，如下：

List<Student> queryStudentsBySql(Map<String,Object> data);
然后在StudentMapper.xml文件中编写sql语句通过limiy关键字进行分页：

 <select id="queryStudentsBySql" parameterType="map" resultMap="studentmapper">
        select * from student limit #{currIndex} , #{pageSize}
</select>
接下来还是在IStuService接口中定义方法，并且在StuServiceIml中对sql分页实现。

List<Student> queryStudentsBySql(int currPage, int pageSize);
 @Override
    public List<Student> queryStudentsBySql(int currPage, int pageSize) {
        Map<String, Object> data = new HashedMap();
        data.put("currIndex", (currPage-1)*pageSize);
        data.put("pageSize", pageSize);
        return studentMapper.queryStudentsBySql(data);
    }
sql分页语句如下：select * from table limit index, pageSize;
```
