#### 准备环境

在pom.xml文件中开启：

```xml
<aop:aspectj-autoproxy />
<!--开启自动代理-->
```

#### execution

可以定义切点的方法切入

execution(<访问修饰符>,<返回类型><方法名>(<参数>)<参数>)

匹配save开头的方法：execution( * save*(..))

#### xml配置目标类和定义切面

```xml
<!--配置目标类-->
<bean id="bean的名称" class="类所在的路径"/>
<!--定义切面-->
<bean class="切面类所在路径"/>
```

#### 切面类

在声明类的上方添加**@Aspect**注释

在声明方法的上方添加**@Before(value="execution()")**注释

可以在方法中传入JoinPoint对象，用来获得切点信息。

#### 后置通知

通过returning属性，可以定义方法返回值，作为参数。

```java
@AfterReturning(value="execution(* com.demo.UserDao.update(..))",returning="returning)
public void afterReturning(Object returning){
    ...；
}
```

#### 环绕通知

around方法的返回值是目标代理方法的执行返回值。

若不调用**joinpoint**.**proceed**()，则目标方法被拦截。

```java
@Around(value="execution(* com.demo.UserDao.update(..))")
public void around(ProceedingJoinPoint joinpoint) throws Throwable{
    Object obj=joinpoint.proceed();
    return obj;
}
```

#### 异常抛出通知

可以设置**throwing**参数。

```java
@AfterThrowing(value="execution(* com.demo.UserDao.update(..))"，throwing="e")
public void AfterThrowing(Throwable e) {
   ...
}
```

#### @After最终通知

无论是否发生异常，最终通知总会被执行。

#### 切点命名

＠**Pointcut**定义切点，使用切点方法，

```java
private void（）{}；
```

即无参数方法，方法名为且点名。然后之前的value属性直接引用切点名即可。

#### aspectj的xml开发aop

```xml
<!--配置目标类-->
<bean id="bean的名称" class="类所在的路径"/>
<!--定义切面-->
<bean id="切面类的名称" class="切面类所在路径"/>
<!--aop的相关配置-->
<aop:config>
    <!--配置切入点-->
    <aop:pointcut id="pointcut" expression="execution(* com.demo.UserDao.update(..))/>
    <!--配置切面-->
    <aop:aspect ref="切面类的名称">
         <aop:before method="before" pointcut-ref="pointcut"/>
    </aop:aspect>
</aop:config>
```

