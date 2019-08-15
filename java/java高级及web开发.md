##1.Junit单元测试 
*	黑盒测试，白盒测试（关注具体逻辑）
*	定义一个测试用例（测试用例） 
*	建议：测试类名+Test 
*	包名 xx.xx.test  可以独立运行 
*   返回值：void 
*	参数列表（空参）
*	给方法加@test，导入junit
*	绿色代表成功，一般用断言操作来处理结果，`Assert.assertEquals(期望结果，运算结果）`
*	@Before:初始化资源 @After:释放资源
##2.反射：框架设计的灵魂
*	框架：半成品软件 
*	反射：将类的各个组成部分封装为其他对象
*	好处：可以在程序运行过程中操作这些对象，也可以解耦，提高程序的可扩展性。
#
	cls=Class.forName("包名.类名");
	Iphone phone=(Iphone) cls.Constructor().new Instance();


----------
xml:可扩展标记语言  作为数据的一种存储格式或用于存储软件的参数，程序解析此配置文件，可以达到不修改代码便可以修改程序的目的。	
##3.B/S与c/s模式:浏览器/服务器模式，客户端/浏览器模式。其中web服务器是运行及发布web应用的容器，只有将web应用放置在容器中，才能使用户通过浏览器进行访问。
##4.在一次完整的http通信过程中，web浏览器与web浏览器之间完成7个步骤:
*	建立tcp连接 
*	浏览器向web服务器发送请求指令
*	浏览器发送请求头信息
*	web服务器进行应答，应答的第一部分是协议的版本号和应答状态码
*	web服务器发送应答头信息
*	web服务器向浏览器发送数据
*	关闭tcp连接
##5.生命周期方法：
按照以下顺序进行调用，构造servlet。使用init方法将其初始化，然后处理来自客户端的对servlet方法的全部调用，最后从服务中取出servlet，然后使用destroy方法进行销毁，最后进行垃圾回收并终止。在第一次访问时，服务器会创建servlet对象，并调用init方法，在调用service方法，第二次访问时，servlet对象已经存在，不需再创建，服务器停止，会释放servlet，调用destroy方法。
*	第一种方法，实现httpservlet
###  ###
	@WebServlet("/Myservlet1")
	public class Myservlet1 extends HttpServlet {
		private static final long serialVersionUID = 1L;

    public Myservlet1() {
        super();
    }
	/**
	 * 接受get请求，request为请求对象，response为响应对象
	 * 其中请求对象封装请求数据，响应对象封装动态网页
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doGet(request, response);
	}

}
*	第二种方法，实现servlet接口
#
	public class Myservlet2 implements Servlet{
	@Override
	public ServletConfig getServletConfig() {
		return null;
	}

	//获取基本信息，版权作者
	@Override
	public String getServletInfo() {
		return null;
	}
	//初始化方法
	@Override
	public void init(ServletConfig config) throws ServletException {
		
	}
	@Override
	public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
		
	}
	@Override
	public void destroy() {
		
	}
}
##6.servlet的两种配置方式
*	注解式配置 @webServlet("/hello"),类似flask中的装饰器作用
*	web.xml进行配置
添加servlet节点和servlet-mapping节点,load-on-startup为启动的优先级，数字越小越先起作用。
#
	<servlet>
		<servlet-name>name</servlet-name>
		<servlet-class>全名称</servlet-class>
		<load-on-startup>1</servlet-mapping>
	</servlet>
	<servlet-mapping>
		<servlet-name>name</servlet-name>
		<url-pattern>路径</url-pattern>
	</servlet-mapping>
其中路径还存在后缀匹配（*.)和通配符匹配(/+星号)
##7.GET请求：get提交的数据会放在URL之后，以？分割url和传输数据，参数之间用&相连，对应servlet的是doget方法。POST请求：将提交的数据放到http包中的body中，对应servlet的是dopost方法.
##8.servlet进程安全问题：因为每次请求都会创建一个线程，若多人请求，多个线程就会操作同一个对象，会导致成员变量的值发生变化。
如何保证线程安全：
*	synchornized  将存在线程安全问题的代码放到同步代码块中。
*	尽可能使用局部变量。
##9.注解是JAVA提供的一种将元程序中元素关联信息和元数据的方法，它是一个接口，程序可以通过反射来获取指定程序中元素的注解对象，进而获取注解中的元数据信息。