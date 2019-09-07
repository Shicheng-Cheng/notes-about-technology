#### 事务的定义

- 事务是正确执行一系列的操作（或动作），使得数据库从一种状态转换成另一种状态，且保证操作全部成功，或者全部失败。
- 事务原则：必须服从ACID原则。

#### Java事务机制

确保数据库操作的 ACID的特性。确保事务要么全部执行成功，要么撤销不执行。

#### 编程式事务实现方式

- 事务管理器方式
  - 类似应用**JTA UserTransaction API**方式，但异常处理更加简洁。
  - 核心类：spring事务管理的三个接口类以及**JdbcTemplate**类。

- 模板事务方式
  - 主要工具类为**JdbcTemplate**类。

#### 事务管理器案例

![5](C:\Users\Dell\Desktop\java笔记\引用图片\5.jpg)

![6](C:\Users\Dell\Desktop\java笔记\引用图片\6.jpg)

**步骤**：

- 获取事务管理器
- 创建事务属性对象
- 获取事务状态对象
- 创建JDBC对象
- 业务数据操作处理

**数据库操作工具类**

![7](C:\Users\Dell\Desktop\java笔记\引用图片\7.jpg)

![8](C:\Users\Dell\Desktop\java笔记\引用图片\8.jpg)

![9](C:\Users\Dell\Desktop\java笔记\引用图片\9.jpg)

#### 模板事务案例

**步骤**

- 获取模板对象
- 选择事务结果类型
- 业务数据操作处理

![10](C:\Users\Dell\Desktop\java笔记\引用图片\10.jpg)

![11](C:\Users\Dell\Desktop\java笔记\引用图片\11.jpg)

此时在**execute**函数中使用匿名内部类。

![12](C:\Users\Dell\Desktop\java笔记\引用图片\12.jpg)

#### 声明式事务实现原理

基于AOP模式机制，对方法前后进行拦截。

- tx拦截器
- 全注释

编程式事务侵入了 业务代码里面，但提供了更加详细的事务管理控制，而声明式事务基于AOP，将操作与事务进行解耦。