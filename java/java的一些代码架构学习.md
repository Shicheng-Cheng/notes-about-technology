编译器相关

table.java

	public class table {
    class vari {// 全局变量信息
        String name;// 变量名
        String tp;// 类型：int int[] function char string
        int ofad;// 偏移地址
        int other;//（如类型为函数，则指向函数表中的某一个。如类型为数组，则存放数组长度）
    }
    class func {// 函数信息
        String name;// 函数名
        List<String> xctp = new ArrayList<String>();// 形参类型
        List<String> xcname = new ArrayList<String>();// 形参名
        List<vari> vt = new ArrayList<vari>();// 函数中的临时变量
    }
  	List<vari> synbl = new ArrayList<vari>();// 全局变量总表
    List<func> pfinfl = new ArrayList<func>();// 函数表
    List<String> vall = new ArrayList<String>();// 活动记录，记录当前位置，是子函数还是主函数，来决定调用临时变量还是全局变量

使用内部类和集合中的ArrayList,其中集合的类型也可以是一个类，参照String,可以用来存储一些动态变化的表。外部属性用list存储，而其中的内部类属性也用list进行存储，打印属性时进行嵌套遍历。
类似对象数组，`table.vari tb=tb.synb1.get(XXX)`

----------

main.java
其中的analyzer类见下
	List<List<String>> anal = new analyzer().answer(path_in,path_out);

	String[] step, i, C, S, c, k, p;

	int n = 0;

	List<String[]> qtt;

	List<List<String[]>> qqtt=new ArrayList<List<String[]>>();
		

#这种list中嵌套其他类型的不是很理解
		i = (String[]) anal.get(0).toArray(new String[anal.get(0).size()]);
		if(step[0].substring(1, 2).equals("k")&&k[Integer.parseInt(step[0].substring(3, step[0].length() - 1))].equals("int")&&step[1].substring(1, 2).equals("k")&&k[Integer.parseInt(step[1].substring(3, step[1].length() - 1))].equals("main")){
			step=Arrays.copyOfRange(step,5,step.length-1);

		}
嵌套list的演示，比如一个都是学科下面有很多班级，一个班级又有很多学生。
#
	ArrayList<Person> first = new ArrayList<>(); //创建第一个班级
	first.add(new Person("杨幂", 30));
	first.add(new Person("李冰冰", 33));
	first.add(new Person("范冰冰", 20));
	
	ArrayList<Person> second = new ArrayList<>();
	second.add(new Person("黄晓明", 31));
	second.add(new Person("赵薇", 33));
	second.add(new Person("陈坤", 32));
	
	//将班级添加到学科集合中
	list.add(first);
	list.add(second);
	
	//遍历学科集合
	for(ArrayList<Person> a : list) {
		for(Person p : a) {
			System.out.println(p);
			}
		}
	}


----------
analyzer.java 
#
	public class analyzer {
	String[] k = { "main", "void", "if", "else", "while", "for", "int", "char", "string", "break", "continue","return","switch","case","default" };// 关键字放到数组里
	List<String> i = new ArrayList<String>();// 变量名
	List<String> C = new ArrayList<String>();// 字符
	List<String> S = new ArrayList<String>();// 字符串
	List<Double> c = new ArrayList<Double>();// 数字
	List<String> p = new ArrayList<String>();// 界符
	// 逻辑是，从头到尾读取String r也就是while(j<r.length)，switch(ascii码)
	// case0，是空格(32)，j++
	// case1，是字母（65-90，97-122），就接着往下读，如果一直没出现符号，就读到空格为止，是一个整体单词。
	// 对这个单词检查是否为关键字在k中，是则{k,n}(n的取值使k[n]==单词)，如果不是则认为它是变量名{i,n}
	// 为此要构建一个list i，每次出现变量名就看看list里有没有它，没有就加进去，使得i[n]==变量名
	// 作为一次结束也要j加到合适的值
	// case2，是数字（48-57），就接着往下读读到空格为止，构建list c，同上操作，{c,n},j++
	// case3，是"（34），往下读到"，构建list S，{S,n},j++
	// case4，是'（39），往下读到'，构建list C，{C,n},j++
	// case5，其他符号(33-47,58-64，91-96，123-126,非34，非39），如果下一个还是其他字符就读俩，否则就它本身一个字符
	// 构建list p，{p,n},j++
	// default，输出来我看看是啥异常情况？j++


----------
	public List<List<String>> answer(String path_in,String path_out) {
		List<List<String>> fr = new ArrayList<List<String>>();
		String result = "";
		try {
			File filename = new File(path_in);
			InputStreamReader reader = new InputStreamReader(new FileInputStream(filename)); // 建立一个输入流对象reader
			BufferedReader br = new BufferedReader(reader);// 建立一个对象，它把文件内容转成计算机能读懂的语言
			String r = "";
			String line = "";
			int j = 0;
			int t, status, jj;
			String word;
			line = br.readLine();
			while (line != null) {
				r = r + " " + line;
				line = br.readLine();	























******************************************************** 

操作系统相关

Config文件夹：设置一些final static属性的超参数

Model文件夹：声明一个基础类，然后在基础类上添加各种属性。
先创建若干个类,磁盘，用户，权限，盘符，设置私有属性，以及对象属性，集合属性，如果声明了集合属性，最好也声明它的get方法或者移除方法，在设置构造器时，尽量包含可能多的情况。
这里面的方法都是static修饰的方法。
service文件夹：

BlockService类，其中主要使用put和get方法，和DiskService类是级联关系
#
	public class BlockService {
	    //设置成static属性，则方法调用是安全的.
	    public static MappedByteBuffer disk= DiskService.disk;
	}
DiskService类，与SuperBlock进行关联
#	
	public class DiskService {
	    public static MappedByteBuffer disk;//磁盘
	    public static SuperBlock superBlock;//超级块
	    /**
	     * 初始化磁盘，如果没有disk.txt就创建，有则打开
	     * @throws IOException IO异常
	     */
	    public static void initDisk() throws IOException {
	        //创建或打开disk.txt文件，模拟磁盘
	        disk=new RandomAccessFile("disk.txt","rw").
	                getChannel().map(FileChannel.MapMode.READ_WRITE,0,DISKSIZE);
DataService类
#	
	public class DataService {
	    private static Stack<Integer> blockStack;





----------
坦克大战

对于一些公用的规则，可以将其划分固定的分类，将模式，方向，坦克以及墙块都设计成枚举类。
静态资源文件的路径均以静态字符串常量来进行声明，直接用"类.常量"来调用路径。
像基本的java代码架构需要熟悉，各种类之间的级联关系，枚举类的使用。先设计各种模型类，先设计可显示图像的抽象类，实现多种构造器。


- 碰撞检测的实现方法：利用Rectangle类创建一个对象，调用intersects()方法。
- 为了避免子弹击中墙块是同一墙块，重写equals()方法

#
	publit boolean equals(Object o1){
		if(o1 instanceof Wall){
			Wall wall=(Wall) o1;
			if(wall.x==x && wall.y==y){
				return 	true;
				}
			}
			return super.equals(o1);
		}


----------
涉及到数组的删除操作：即用后面的一个元素覆盖前一个元素，然后将数组的最后一位置为null。
统计不同种类的个数：即先判断对象是否属于某个类
注意this的运用