>##浏览器发给服务端是一个http格式的请求，当服务器收到这个请求时，需要调用服务端程序，即所写的java类。Servlet接口与Servlet容器达到了http服务器与业务类解耦的目的。如果想要实现新的功能，只需要实现一个servlet即可，并将其注册到Tomcat中。Servlet容器在加载Servlet类的时候会直接调用init方法，在卸载的时候调用destroy方法。
>web应用程序的开发：
>#
*	设计并实现类，定义类与类之间的关系，实现类的方法，在方法内部实现具体的业务逻辑
*	在类设计好之后，需要创建对应的实例，并根据类与类的关系组装一起。
#
>Spring的IOC容器：负责创建组装Bean，通过配置文件或者注解，容器除了创建组装Bean，还需要解析配置文件或者注解。
>Spring MVC是Servlet的实现，是Bean容器，不负责加载和实例化Servlet。Spring的API可以创建一个容器，而程序注册一个Servelt到容器中。用web容器的Session方案，需要特定的web容器，而用Spring Session可能比较简单，不需要和特定的Servlet容器打交道。
>Tomcat和Jetty本身具有HTTP服务器和Servlet容器的两种功能，Spring boot在调用嵌入式Tomcat时不需要额外的http服务器。
>HTTP是无状态的协议，为了识别特定用户，所以出现了cookie和session,cookie本质上是一份存储在本地的文件，里面包含了每次请求中需要传递的信息，而session是服务器端开辟了一块存储空间来保存状态信息，Tomcat负责创建管理Session，并提供多种持久化方式，并且定期进行后台线程定期轮询，清除过期的Session。所谓无状态，指的是不同请求间数据不存在依赖，而服务器为用户保存的状态属于应用层，与协议无关，keep-alive表示tcp的连接可以复用，利用已有的传输通道进行http协议内容的传输，不需要再次创建/关闭连接。