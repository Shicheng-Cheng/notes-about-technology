调研：
#基本功能
###基于NIO实现，支持http/1.1协议，支持连接复用，静态资源缓存。能在上面部署项目。

一个Tomcat中只有一个Server，一个Server可以包含多个Service，一个Service只有一个Container，但是可以有多个Connectors，这是因为一个服务可以有多个连接，如同时提供Http和Https链接，也可以提供向相同协议不同端口的连接。多个Connector和一个Container就形成了一个Service，有了Service就可以对外提供服务了，但是Service还要一个生存的环境，必须要有人能够给她生命、掌握其生死大权，那就非Server莫属了！所以整个Tomcat的生命周期由Server控制。

一个请求发送到Tomcat之后，首先经过Service然后会交给我们的Connector，Connector用于接收请求并将接收的请求封装为Request和Response来具体处理，Request和Response封装完之后再交由Container进行处理，Container处理完请求之后再返回给Connector，最后在由Connector通过Socket将处理的结果返回给客户端，这样整个请求的就处理完了！
Connector最底层使用的是Socket来进行连接的，Request和Response是按照HTTP协议来封装的，所以Connector同时需要实现TCP/IP协议和HTTP协议！

Connector就是使用ProtocolHandler来处理请求的，不同的ProtocolHandler代表不同的连接类型，比如：Http11Protocol使用的是普通Socket来连接的，Http11NioProtocol使用的是NioSocket来连接的。
其中ProtocolHandler由包含了三个部件：Endpoint、Processor、Adapter。
（1）Endpoint用来处理底层Socket的网络连接，Processor用于将Endpoint接收到的Socket封装成Request，Adapter用于将Request交给Container进行具体的处理。
（2）Endpoint由于是处理底层的Socket网络连接，因此Endpoint是用来实现TCP/IP协议的，而Processor用来实现HTTP协议的，Adapter将请求适配到Servlet容器进行具体的处理。
（3）Endpoint的抽象实现AbstractEndpoint里面定义的Acceptor和AsyncTimeout两个内部类和一个Handler接口。Acceptor用于监听请求，AsyncTimeout用于检查异步Request的超时，Handler用于处理接收到的Socket，在内部调用Processor进行处理。
#
*	最简易版本：创建一个server类，accept()方法调用handler中重写的run方法。
*	v1.1  
*	Server类  初始化服务器
*	调用static修饰的代码块，调取配置文件中的参数。比如在最简易版本中，监听的版本号可以通过配置文件进行读取，ServerSocket(port)。并在当前线程内创建一个Client服务。
*	Request类  进行输入流的解析，先读取Socket的对象，进行相关url逻辑的编写。
*	Response类
*	分情况处理：URL为空，返回默认资源，若存在，加载该资源，若不存在，返回错误信息。
tcp/ip 传输层  http:应用层

*	客户端三次握手与服务器建立tcp连接
*	调用socket的accept方法对http报文进行读取
*	解析报文创建request对象
*	容器返回一个response对象
*	将response对象再生成一份响应报文
*	tcp把报文发给客户端
*	如果无连接复用，就四次挥手断开连接

日志记录器：错误，警告，消息