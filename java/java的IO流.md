#1.InputStream类是字节输入流的抽象类，是所有字节输入流的父类，用来处理单字节。而Reader类负责处理字符。
#2.OutputStream类是字节流的抽象类，是所有字节输出流的父类。字符输出流是Writer类。
#3.写入文件过程：
*	先创建一个File file对象，如果是写文件，则将file对象传入OutputStream的参数中，然后获得byte类型数组，传入write。
#读取文件过程
*	同样将file对象传入InputStream中
#
	byte[] byt=new byte[1024];
	int len=-1;
	while((len=in.read(byt)!=-1){
		syso(new String(byt,0,len);
	}
#4.BufferedInputStream类是对所有的InputStream的子类进行带有缓冲区的包装。
#5.路径分隔符：windows("\\")  unix("/")
#6.File类的对象常会作为参数传递到流的构造器，指明读取或写入的终点。
#7.流的体系结构：抽象基类->节点流->缓冲流
#8.字符输入流 read():返回读入的一个字符，如果达到文件末尾，返回-1.
	FileReader fr=new FileReader(file);
	int data;
	while((data=fr.read())!=-1)
#9.字符输出流：
	char[] str=new char[5];
	int len;//记录每次读入到str数组中的字符个数
	//每次写入len个字符
	while((len=fr.read(str))!=-1){
		fr.write(str,0,len);
	}