## JDBC Template

### 创建项目配置

- #### Maven

  - Mysql驱动
  - spring(core,beans,context,aop)
  - JDBC Template(jdbc,tx)

- #### Spring配置

  ```xml
  <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
      <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
      <property name="url" value="jdbc:mysql//localhost:3306/selection_course?useUnicode=true&amp;characterEncoding=utf-8"/>
      <property name="username" value="root"/>
      <property name="password" value="admin"/>
  </bean>
  <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
      <property name="dataSource" ref="dataSource"/>
  </bean>
  <context:component-scan base-package="要扫描注解的包名"/>
  ```

  ### 基本方法调用

  #### update方法

  ```java
  int update(String sql,Object[] args)
  int update(String sql,Object... args)
  ```

  #### batchupdate方法

  ```java
  int[] batchupdate(String[] sql)
  int[] batchupdate(String sql,List<Object[]> args)
  ```

  #### query相关方法

  ```java
  int count=jdbcTemplate.queryForObject(sql,Integer.class);
  List<String> names=jdbcTemplate.queryForList(sql,String.class,"接收一个字符串");
  ```

  #### 查询复杂对象方法

  ```java
  String sql1="select * from student where id=？"；
  Map<String,Object> stu=jdbcTemplate.queryForMap(sql,100);
  String sql2="select * from student"；
  List<Map<String,Object>> stu=jdbcTemplate.queryForList(sql);
  ```

  #### 查询实体对象

  ```java
  private class StudentRowMapper implements RowMapper<Student>{
      public Student mapRow(ResultSet resultset,int i) throws SQLException{
          Student stu=new Student();
          stu.setId(resultset.getInt("id"));
          stu.setName(resultset.getString("name"));
          stu.setBorn(resultset.getDate("born"));
          return stu;
      }
  }
  String sql="select * from student"；
  List<Student> stus=jdbcTemplate.query(sql,new StudentRowMapper());
  ```

  ### 持久层实现

  #### 编写实体类

  #### DAO

  - 使用**@Autowired**注入**JDBCTemplate**
  - 声明**RowMapper**

  ![Screenshot_20190906-110631](C:\Users\Dell\Desktop\java笔记\引用图片\1.jpg)

  ![2](C:\Users\Dell\Desktop\java笔记\引用图片\2.jpg)

  