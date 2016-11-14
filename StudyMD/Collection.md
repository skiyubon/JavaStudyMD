# 集合框架
##1.集合与数组的区别
###a:
> 数组既可以存储基本数据类型,基本数据类型存储的是值,又可以存储引用数据类型,引用数据类型存储的是地址值.但是太麻烦.

> 集合只能存储引用数据类型(对象),也可以存储基本数据类型,但是基本数据类型会自动装箱成对象.
###b:
> 数组长度是固定.

> 集合的长度是可变的,随元素的增加而增长.

##2.集合的继承体系
                            collection(单列集合的根借口)

                   List                    |           Set
            (有序,存取一致,有索引可重复)      |  (存取无序,无索引,不可重复)            
    ArrayList      LinkList      Vector    |  HashSet      TreeSet
    数组实现        链表实现       数组实现      哈希算法     二叉树(红黑树)算法   
  

##3.Collection
    Collection c = new ArrayList();//父类引用指向子类对象(爷爷类)
    c.add("abc");               //元素可以重复
    c.add(true);
    c.add(100);
    c.add(new Student());
    c.add("abc");               //任意类型add(E e);   
    syso(c);                    //重写了toString()方法 -->ArrayList--->...
    
    
    c.remove(100);              //删除指定元素
    c.clear();                  // 清空集合
    c.contains("abc");          // 判断是否包含
    c.isEmpty();                // 判断是否为空
    c.size();                   // 获取元素的个数  

##4.遍历集合
> A:转数组遍历--->toArray()  返回Object[].

    Collection c = new ArrayList();
    c.add(new Studnt("张三",23));
    c.add(new Studnt(...));
    c.add(new Studnt(...));
    c.add(new Studnt(...));

    Object[] arr = c.toArray();             //集合转数组,向上转型
    for (int i = 0 ,i < arr.length; i ++)
    {
        syso(arr[i]);
        //Student s = (Student)arr[i];//强制向下转型,然后可以可以使用子类的特有功能
        //syso(s.getName());           
    }        
    
    `*`addAll(Collenction<? extends e> c)
    Collectin c1 = new ArrayList();
    c1.add("a");
    c.addAll(c1);           //添加整个集合的每一个元素
    c.add(c1);              //把参数集合当做一个对象添加
    
    `*`removeAll(Collectin c)
    c.removeAll(c1);        //删除的是交集.
    
    `*`containsAll(Collection c)  //判断是否包含传入的集合
    `*`retainAll(Collection c)    //取交集,如果调用的集合改变就返回true,没改变就false
    
##5.集合之迭代器遍历

    Iterator[接口]
    Collection c = new ArrayList();
    c.add("a");
    c.add("b");
    c.add("c");
    Iterator it = c.iterator();     //获取迭代器
    boolean b = it.hasNext();       //判断集合中是否有元素
    Object obj1 = it.next();        //获取元素,自动类型提升
    Object obj2 = it.next();
    while(it.hasNext()) {
        syso(it.next());
        //Student s = (Student)it.next();
        //syso(s.getName());

    }
> 迭代器之原理:

> 每一个集合的存取是不一样的,就需要在每一个集合中定义自己的hasNext()和next()方法

> 可以抽像抽取出迭代器接口并抽象hasNext()和next(),具体实现由不同存取结构的每个集合定义实现.

##6.List集合,Collection的子接口.
    List list = new ArrayList();
    list.add("a");
    list.add("b");
    list.add(1,"c");   //add(int index,E element),IndexOutOfException
                       //index <= size | index >= 0
    remove(int index); //通过index删除元素,并返回删除的元素,index不会自动装箱而误删掉int的元素对象.
    remove(Object obj);//删除元素对象    
    
    get(int index);    //根据索引返回元素对象.可以用来遍历
    set(int index, E element);    //将指定位置的元素修改.
    
##7.并发修改异常的发生及解决方案
> 需求:判断集合里是否有"word"元素,有就填加"javaee"这个元素.

    List list  = new ArrayList();
    list.add("word");
    Iterator it = list.iterator();
    while(it.hasNext()) {
        String str = (String)it.next();
        if("word"equals(str))
            lits.add("javaee");  //ConcurrentModifficationException
    }                            //遍历的同时,并发修改.

    ****************************************************
    解决方案:listIterator(列表迭代器)
    ****************************************************
    ListIterator lit = list.listIterator();  
    while(*lit*.hasNext()) {
        String str = (String)lit.next();
        if("word"equals(str))
            //lits.add("javaee");  //ConcurrentModifficationException
            lit.add("javaee");
    }  
    ListIterator:
    ListIterator lit = list.listIterator();
    while(lit.hasNext()) {
        syso(lit.next());           //获取元素并将指针向后移动
    }

    while(lit.hasPrevious()) {
        syso(lit.previous());       //获取元素并将指针向前移动
    }

##8.Vector
    Vector v = new Vector(0;
    v.addElement("a");
    v.addElement("b");
    v.addElement("c");
    
    Enumeration en = v.elements();      //获取枚举
    while(en.hasMoreElements()) {
        syso(en.nextElement())
    }

##9.Arraylist和Linkedlist的区别
###A:Array

> 查询修改快,增删慢.
###B:Linkedlist

> 查询修改慢,增删快.


##10.List的三个子类的特点.  
    Arraylist:
        查询修改快,增删慢.线程不安全.相对Vector效率高.底层是Array实现.
    ******************************
    Linkedlist:
        查询修改慢,增删快,线程不安全.
    ******************************
    Vector:
        查询修改快,增删慢,线程安全. 相对Arraylist效率低.底层是Array实现.  

##11.LinkedList的特点.
    addFirsr(E e),addLast(E e);
    getFirst(),getLast();
    removeFirst(), removeLast();
    get(index)                  //根据索引查找元素,从头/尾找

    LinkedList list  = new LinkedList();
    list.addFirst("a");
    list.addFirst("b");
    list.addFirst("c");
    list.addFirst("d");         //dcbae
    list.addLast("e");  
    list.get(1);                //c    


##12.栈内存LinkedList模拟实例.
    现进后出     *       *
                *       *
                *       *
                *       *
                *       *
                *       *
                *       *
                *       *
                *********
    LinkedList list = new LinkedList();
    list.addLast("a");
    list.addLast("b");
    list.addLast("c");
    list.addLast("d");
    list.removeLast();
    
    whilie(!list.isEmpty()){
        syso(list.removeLast());
    }
    
    <封装LinkedList成栈类>
    public class Stack {
        private LinkedList list = new LinkedList();
        
        public void in(Object obj) {            //进栈
               list.addLast(obj);
        }
        
        public Object out() {                   //出栈
                return list.removeLast();
         }
        
        public boolean isEmpty() {              //判断栈是否为空
                return list.isEmpty();
        }
    }   


    Stack s = new Stack();
    s.in("a");
    s.in("b");
    s.in("c");
    s.in("d");
    s.out();
    s.isEmpty();    


##13.泛型<> Collection< E >
> A:提高安全性,将运行时的错误转换到编译器.


- 调用时省去强转的麻烦.
    
> B:<>中必须是引用数据类型

> C:使用注意事项:前后的泛型必须一致,或者后面的泛型可以省略不写.


    泛型
    ArrayList<String> list = new　ArrayList<>();
    泛型的迭代器
    Iterator<String> it = list.iterator();


###1.泛型类和方法
    class Tool<Q>{
        private Q q;
        public Q getObj() {}
    



        public void show(T t) {     //方法泛型需要与类的泛型一致,不能是T
            syso(t)
    }
        
    public <T> void show(T t) {     //如果不与类的泛型不一致,方法上加泛型.
            syso(t)
    }

    public static void print(Q q){} //静态方法必须声明自己的泛型,此处报错和类的泛型一致了.
    public static <Q> void print(Q q){} //静态方法必须声明自己的泛型,正确

###2.接口泛型
    interface Inter<T> {
        public void show(T t);
    }
    ********************************
    class Demo implements Inter<String> {
        @Override        
        public void show(String str) {}
    }
    *******************************
    class Demo1 <Q> implements Inter<Q> {
        public void show(Q q){

        }
    }

##14.集合三种迭代的删除特点
1. for循环可以删除,但是每次删除后必须把索引--,向上修正.不然会有漏删的情况.
2. Iterator删除,next()方法底层会修正指针.
3. foreach不能删除,因为它的底层遍历就是依赖的Iterator,并发修改异常    


##15.可变参数   
	int[] arr = {11,22,33,44,55};
	print(arr);

	print(11,22,33,44,55);
	print();

	public static void print(int[] arr){
		for() {}   
	}
										//不可重载,可变参数其实就是数组
	public static void print(int ... arr) {	//可变参数列表,代表一个数组
		for() {}							//可变范围0 - +∞
	} 
	public static void print(int x, int ... arr){
	}						//如果参数有多个参数,可变参数一定是最后一个.


##16.数组转集合:asList()
	String[] arr = {"a","b", "c"};
	List<String> list = Arrays.asList(arr);
	list.add("d");		//UnsupportedOperationException不支持操作异常
						//虽然不能增删元素,但是可以用集合的思想操作数组 

	int[] arr = {11,22,33,44,55};
	List list = Arrays.asList(arr);
	syso(list);			//打印一个地址值,会将整个数组当做一个对象转换

	Integer[] arr = {11,22,33,44,55};
	List<Integer> list = Arrays.asList(arr); 
	syso(list);			//将数组转集合,必须按钮将基本数据包装

##17.集合转数组:Object toArray()和< T > T[] toArray(T[] a)加泛型有参数的.
	ArrayList<String> list = new ArrayList<>();
	list.addf("a");
	list.addf("b");
	list.addf("c");
	list.addf("d");

	String[] arr = list.toArray(new String[0]};
	
	for() {} 		//abcd,
 

> 当集合转换数组成,如果数组<=集合的size,转后的数组长度=集合的size;

> 如果转后的数组长度>集合的size,转后的数组长度就=数组的长度


##18.集合嵌套集合
	ArrayList<ArrayList<Person>> list = new ArrayList<>();
		
	ArrayList<Person> first = new ArrayList<>();
	first.add(new Person("杨幂", 30)); 
	first.add(new Person("李冰冰", 30));
	first.add(new Person("范冰冰", 30));
	
	ArrayList<Person> second = new ArrayList<>();
	second.add(new Person("黄晓明", 30)); 
	second.add(new Person("赵薇", 30));
	second.add(new Person("陈坤", 30));

	list.add(frist);
	list.add(second);
		
	for(ArrayList<Person> a : list){
		for(Person p : a) {
			syso(p);
		}
	}  

##19.Collections工具类.


- 构造方法私有



- 常见方法
- 
		public static <T> void sort(List<T> list)  			//排序
		public static <T> int binarySearch(List<T> list,T)  //二分查找
		public static <T> T max(List<T> list>				//取最大值
		public static void revers(List<?> list)				//翻转
		public static void shufflie(List<?> list)			//随机置换

		Collection.synchronizedList(List<T> list)			//线程转安        