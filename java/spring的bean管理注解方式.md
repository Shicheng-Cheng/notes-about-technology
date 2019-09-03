### Bean管理的注解方式
传统方式需要去xml中配置<bean id="" class=""></bean>
- @Component 描述Spring框架中Bean
- @Repository 用于对DAO实现类进行标注
- @Controller 用于对Controller实现类进行标注
- @Service 用于对Service实现类进行标注
#
而注解方式的话，只需要加上@Component("userservice")相当于xml配置中的id
#### 属性的注解方式
- 类的属性不设置get和set方法，可以在属性上添加注解@Value("xxx")
- 使用@Autowired进行自动注入 
- 1.默认按照类型进行注入：若存在两个相同bean类型相同，则按照名称注入
- 2.@Autowired注入时可以针对成员变量或者set方法：通过required属性，设置一定找到匹配的bean，并使用@Qualifier指定注入Bean的名称，此时该名称需要与所要引用的@Repository的名称保持一致。
- 3.@Resource(name="")可以代替@Autowired和@Qualifier一起使用的情况。
#### 其他注解

spring可以在创建和拆卸bean时调用bean的两个生命周期方法
<bean id="" class="" init_method="init" destroy-method="destroy"/>

- 当bean被载入容器时，调用init，注解方式：@PostConstruct 初始化

- 当bean从容器中删除，调用destroy，注解方式：@PreDestroy 销毁

  ------

开启注解扫描 

```xml
<context: componment-scan base-package="路径"/>
```

------

#### 注解和xml搭配使用

在xml文件中配置类的bean实体，然后利用注解对bean实体进行属性注入，不需要设置set方法。

- 在xml

  ```xml
  context: annotation-config/&gt;-
  ```

- 在bean实体中，在对应的类属性对象上添加注解@Resource(name="xml中bean的名字")