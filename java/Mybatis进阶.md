### Mybatis进阶

#### 参数处理

- 单参数

  - Mybatis会直接取出参数值给Mapper文件赋值:**#{id}**

- 多参数

  - JavaBean传递参数      

    ```sql
    select * from person where username=#{param1} and gender=#{param2}
    ```

    Mybatis默认将多参数命名为param1,2,3...

  - Map接口

  - 注解@param

**封装成PoJo类**，传入构造方法。

- 集合类型参数处理

#### Mybatis动态SQL之foreach

#### ![20](C:\Users\Dell\Desktop\java笔记\引用图片\20.jpg)

![21](C:\Users\Dell\Desktop\java笔记\引用图片\21.jpg)

#### 批量插入

- 传统JDBC批量插入
  - For循环插入数据
  - 借助Statement对象的批处理方法addBatch
- Mybatis对批量插入的支持
  - 借助foreach标签  建议第一种
  - 借助数据库连接属性 allowMultiQueries=true
  - ![22](C:\Users\Dell\Desktop\java笔记\引用图片\22.jpg)
- 可借助Executor的batch批量添加，可与Spring框架整合

#### Mybatis核心对象

- ParameterHandler：处理SQL的参数对象
- ResultSetHandler: 处理SQL的返回结果集
- StatementHandler: 数据库的处理对象，执行SQL语句
- Executor: Mybatis的执行器，用于执行增删改查操作

#### Mybatis插件原理及接口

- 插件借助于责任链模式进行对拦截的处理
- 使用动态代理对目标对象进行包装，达到拦截目的
- 作用于Mybatis的作用域对象之上

![24](C:\Users\Dell\Desktop\java笔记\引用图片\24.jpg)

![25](C:\Users\Dell\Desktop\java笔记\引用图片\25.jpg)

#### 多插件开发过程

- 创建代理对象时，按照插件配置的顺序进行包装
- 执行目标方法后，按照代理的逆向进行执行

#### PageHelper拦截器进行分页

- 分页原理：开始记录索引的规律（当前页-1）*每页的条数
- 一共的页数：总记录%条数==0？总记录%条数：+1

