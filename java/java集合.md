#1.向collections接口的实现类的对象中添加数据obj时，要求obj所在类要重写equals()方法。
#2.集合转成数组：toArray()  数组转成集合：Arrays.aslist()
#3.在迭代集合元素时，推荐使用迭代器。此外，迭代器内部也定义了remove()，可以在遍历的时候删除集合中的元素。不同于集合直接调用的remove()方法。
	while(iterator.hasNext()){
		syso(iterator.next());
	}
#4.ArrayList:线程不安全，效率高，底层使用Object[] element存储  LinkedList:对于频繁的插入删除操作，效率较高，底层使用双向链表进行存储。
#5.ArrayList源码分析：
*	JDK1.7：在底层首先由两个构造器，this(10),public ArrayList(int capicity)，其中空参构造器this调用了另一个构造器，则在底层创建了一个长度为10的Object[]的数组，如果添加别的元素，需要进行比较，如果添加容量导致底层数组容量不够，则>>1+本身，相当于原有容量的1.5倍，同时需要将原有数组中的数据进行赋值，copyof()。建议在开发中使用带有参数的构造器。类似单例中的饿汉式实现。
*	JDK1.8:底层数组的初始化为{}，并没有创建长度，在第一次调用add方法时，底层才创建了长度为10的数组，并将数据添加到底层数组。类似单例模式中的懒汉式实现，延迟创建，节省内存。
#6.LinkedList源码分析：在定义Node时，使用了内部类，定义三种属性，Node类型的first和last,默认为null。
#7.vector源码分析：在底层首先由两个构造器，this(10),public Vector(int capicity)，其中空参构造器this调用了另一个构造器，则在底层创建了一个长度为10的Object[]的数组，如果添加别的元素，需要进行比较，如果添加容量导致底层数组容量不够，则扩充到原有容量的2倍。
#8.List中的remove方法：注意remove(int index)和remove(Object obj)的区别
#9.Set:存储无序的，不可重复的数据，以HashSet为例，存储的数据在底层数组中并非按照数组索引的顺序添加，而是根据数据的hashcode值。之所以元素不可重复，保证了添加的元素都经过了equals()方法来判断，不能返回True。
#10.泛型：定义泛型类时，一般类型名称使用T来表达，而容器内部元素使用E来表达。class 类名<T>,定义泛型类时也可以是数组类型。
#11.Hashmap:作为Map的主要实现类，线程不安全，效率高，可以存储null的key和value;Hashtable:作为古老的实现类，线程安全，效率低，不能存储null的key和value。
#12.LinkedHashmap：保证在遍历map元素时，可以按照添加的顺序实现遍历，在原有的底层结构上添加了一对指针，对于频繁的遍历操作，此类执行效率高。
#13.Map结构的理解：key无序，不可重复，Set存储key，key所在的类需要重写equals和hashcode方法，value是无序可以重复，value所在的类只需要重写equals方法，使用collection进行存储，一个键值对，key-value组成了一个Entry对象，使用Set存储。
#14.jdk8中不同的实现：new HashMap()：底层没有创建一个长度为16的数组，首次调用put方法时，会创建数组，当一个数组的某一个索引位置上的元素以链表形式存在的数据个数>8且当前数组的长度>64，数据改为红黑树存储。
#15.使用容器存储表格数据，每一行数据用Map去存储，整个表格再用list去存储，ORM：对象关系映射。也可以使用javabean对象存储每一行数据，多行用Map/list存储。完整的javabean对象，要有set/get方法，以及一个空参构造器。




