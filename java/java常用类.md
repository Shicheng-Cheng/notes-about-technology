# String
 - String是一个final类，实现了Serializable接口，表示字符串支持序列化，代表不可变的字符序列。其中不可变性体现在：当对字符串进行重新赋值时或对现有的字符串进行连接时或者使用replace()方法时，需要重写指定内存区域赋值，不能使用原有的value进行赋值。字符串是常量，用双引号表示，它们的值在创建之后不能更改，其中的字符内容是存储在一个字符数组final char[] value中。此外还实现了Comparable接口，表示String可以比较大小。
  - String通过字面量的方式(区别于new)给一个字符串赋值，此时的字符串值声明在字符串常量池中，而字符串常量池中不会存储相同内容的字符串。
## String的实例化方式：
*	通过字面量定义的方式
*	new+构造器方式   此时对象保存的地址值是数据在堆空间中开辟空间以后对应的地址值
String s=new String("abc")在内存中创建了两个对象，一个是堆空间的new结构，另一个是char[]对应的常量池中的数据。
- 常量与常量的拼接结果在常量池中，且各异。只要其中有一个结果是变量，则结果在堆中，若拼接结果调用intern()方法，则结果保存在常量池中。
- jdk 1.7:字符串常量池存储在堆空间  jdk 1.8：字符串常量池存储在方法区
## 字符串的常用方法：
*	int indexOf(String str)  返回指定字符串在字符串第一次出现的索引
*	boolean contains(Char s)  若包含指定的char值序列，返回true
*	判断字符串中是否全部有数字组成，即有1-n个数字组成  `boolean match=str.matches("\\d+");`
*	判断一个地区的电话号码是否符合规范`boolean match=str.matches("xxxx-\\d+{7,8}");\\7-8位数字`
## 数据类型转换
*	String->基本数据类型、包装类  调用parseXXX
*	基本数据类型、包装类->String   调用valueOf(xxx)，String.valueOf(int类型),也可以是Interger.valueOf("").
*	String->char[]    调用String的toCharArray()
*	char[]->String    调用String的构造器
*	String->byte[]    调用String的getBytes()  编码  字符串->字节   数据转换成二进制数据
*	byte[]->String    调用String的构造器
*	解码  字节->字符串    二进制数据转换成数据
## StringBuffer源码
事先在底层进行长度为16的char[]型数组，若要添加的数据底层数组盛不下，则需要扩容底层的数组，默认情况是扩容为原来容量*2+2,同时将原有数组的元素复制到新的数组。
## 方法链原理
返回当前对象，可以继续执行当前方法。
	public StringBuffer append(String str){
		super.append(str);
		return this;
	}
- 执行效率比较：StringBuidler>StringBuffer>String

# Date类  
使用new Date()构造器，调用toString()方法，来显示当前的年月日时分秒。调用getTime()方法，获取当前的Date对象对应的毫秒数。
- 将java.util.Date对象转换为java.sql.Date对象
	Date data=new Date();
	java.sql.Date data_new=new java.sql.Date(data.getTime());

- Calendar类：实例化，调用其静态方法getInstance()。
- JDK1.8的时间API：LocalDate,LocalTime,LocalDateTime
- SimpleDateFormat的使用
*	格式化：日期->字符串
#
	SimpleDateFormat simple=new SimpleDateFormat();
	Date data=new Date();
	String str=simple.format(data)
*	解析：字符串->日期
#
	String str="2019-08-12";
	Date date=simple.parse(str);

*	按照指定的方式进行格式化和解析：调用带参数的构造器
#
	SimpleDateFormat simple=new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
	String str=simple.format(date);



# 枚举类
- 枚举类的使用：类的对象有限个，确定的，或者当需要定义一组常量。若枚举类中只有一个对象，则可以作为单例模式的实现。
- 自定义枚举类：
*	声明枚举类的对象属性，用private final修饰
*	私有化类的构造器，给对象进行赋值
*	提供当前枚举类的多个对象，用public static final进行修饰
- enum修饰
*	提供当前枚举类的对象，用逗号隔开，末尾对象使用分号结尾
*	声明对象属性  (同上)
*	私有化类的构造器  (同上)
- 枚举类的常用方法：
*	values()方法：返回枚举类型的对象数组
*	重写toString()方法
*	valueOf()方法：将字符串转换为对应的枚举类对象
- 使用枚举类实现接口：可实现接口的抽象方法，也可以在枚举类对象中实现抽象方法。

# 注解
- 注解的使用实例
*	生成文档相关的注解
*	在编译时进行格式检查
*	跟踪代码依赖性，实现替代配置文件功能
- 自定义注解
使用@interface关键字，Annotation的成员变量在定义中以无参数方法的形式来声明，其方法名和返回值定义了该成员的名字和类型。称之为配置参数。类型只能是八种基本数据类型，String类型等，如果只有一个参数成员，建议使用参数名为value。若定义的注解中含有配置参数，则使用的时候必须指定参数值，即value=""。
注意：自定义注解需要配上注解的信息处理流程（使用反射）才有意义。
- 元注解：对现有注解进行解释说明
Retention：指定所修饰的Annotation的生命周期，SOURCE/CLASS/RUNTIME，只有声明为RUNTIME生命周期的注解，才能被反射所获取。
Target:用于指定被修饰的Annotation能用于修饰哪些元素(类，方法，构造器)
- 可重复注解：在所声明的注解上声明@Repeatable，成员值为MyAnnotation.class。
- 类型注解：ElementType.TYPE_PARAMETER 表示注解可以写在类型变量的声明语句中，比如泛型。TYPE_USE 表示注解可以写在使用类型的任何语句中。

# 比较类
- 比较类：重写CompareTo方法
	publi int CompareTo(Object o){
	if(o instanceof Good){
		Good good=(Good) o;
		if(this.price>good.price){
			return 1;}
		else if{
			return -1;
			}
		else{
			return this.name.compareTo(good.name);
		}
		}
	}

或者可以写成
	public Double.compare(this.price,good.price);
- comparator接口：当元素类型未实现comparable接口，又不方便修改代码，或者接口规则不合适，则考虑使用对象排序。
	Arrays.sort(arr,new Comparator(){
		public int compare(Object o1,Objecto2){
			if(o1 instanceof String && o2 instanceof String){
				String o1=(String) o1;
				String o2=(String) o2;
				return o1.compareTo(o2);
				}
			 new RuntimeException("输入类型不一致");
			}
		});
- Comparable接口的方式一旦确定，保证Comparable接口实现类的对象在任何位置都可以比较大小，而Comparator接口属于临时性的比较。
