#IO流
> IO流是用来处理设备间的数据传输
##1.分类
- 输入流 -->程序使用输入流读取文件
- 输出流 --->程序使用输出流写出文件
> 
1. 字节流,操作任何数据,因为计算机中任何数据都是以字节流的形式存储的
2. 字符流,只能操作纯字符数据,比较方便


##2.结构
1. 字节流的抽象父类 
	1. InputStream
	2. OutputStream
2. 字符流的抽象父类
	1. Reader
	2. Writer
	
##3.IO程序的书写
- 使用前导入IO包中的类
- 使用中要进行异常处理
- 使用后要关闭流
 
#4.InputStream & OutputStream
	FileIntputStream
> 
	FileIntputStream fis = new FileInputStream("xxx.txt");				//throws Exception
	int b = fis.read();			//文件不可读Exception
	Syso(b);
	int b1 = fis.read();
	Syso(b1);
	fis.close();
> read()返回的是Int,而不是byte.

> 字节输入流可以操作任意类型的文件,以二进制存储,如果返回byte,有可能在读的时候返回11111111(-1的补码),返回的是-1,文件读取会中断;

> 返回的是Int,会在每次读的byte前补0,返回的都是正数,因此不会提前中断读取.

	FileOutputStream
	
> 
	FileOutputStream fos = new FileOutputStream("xxx.txt");	//没有就自动创建文件,有的话,就会先将文件先清空.
	fos.write(97);		//虽然写出的是四位的int数,但是写到文件上的是一个字节
	fos.write(98);
	fos.close();

	FileOutputStream(File,true);	//设置true.在此文件设置续写模式

#5.IO读取写入实例
	FileInputStream fis = new FileInputStream("xxx.txt");
	FileOutputStream fos = new FileOutputStream("copy.txt");
	int b;
	while((b = fis.read()) != -1){
		fos.write(b);
	}

	fis.close();
	fos.close();

#6.IO读写字节数组
	FileInputStream fis = new FileInputStream("xxx.txt");
	FileOutputStream fos = new FileOutputStream("copy.txt");
	byte[] b = new byte[fis.available()];	//一次性读取完毕,但是得创建长										//度最大的数组,有可能内存溢出.
	fis.read(b)
	fos.write(b);
	
	fis.close();
	fos.close();

#7.IO读写之小数组读写
	FileInputStream fis = new FileInputStream("xxx.txt");
	FileOutputStream fos = new FileOntputStream("copy.txt");
	byte[] b = new byte[1024 * 8];
	int len;
	while((len = fis.read(b)) != -1) {
		fos.write(b,0,len);
	}
	fis.close();
	fos.close();

#8.BufferedInputStream & BufferedOutputStream(装饰设计模式)
	FileInputStream fis = new FileInputStream("xxx.txt");
	FileOutputStream fos = new FileOutputStream("copy.txt");
	BufferedInputStream bis = new BufferedInputStream(fis);
	BufferedOutputStream bos = new BufferedOutputStream(fos);
	
	int b ;
	while((b = bis.read()) != -1) {				//内置缓冲区数组大小8192
		bos.write(b);
	}
	bis.close();
	bos.close();

- Buffered$InputOutputStream和8192的小数组谁快?
	- 小数组稍快.
	 
#9.flush和close的区别
- close 方法具备刷新的功能,在关闭流之前,就会刷新一次缓冲区数据到文件上.
- flush 方法也就是刷新方法,刷完后还可以再写.而close方法刷完之后关闭流,不能再写
- flush可以实时刷新


#10.jdk1.7IO流的标准写法
	try(			//自动调用实现了AutoCloseable的类的对象的close();
    FileInputStream fis = new FileInputStream();
	FileOutputStream fos = new FileOutputStream();
	){
		int b;
		while((b = fis.read()) != -1) {
			fos.write(b);
		}	
	}

##11.FileReader & FileWrite
	
	FileReader fr = new FileReader("xxx.txt");
	int c;
	while((c = fr.read())!=-1){
	
	}

##12.只读或者只写纯文件的时候使用
> 字符类拷贝的时候,中途有一个转换的过程.
> 字符流不可以拷贝纯文本文件,在转换的过程中,可能找不到对应的字符就用?替代

##13.字符流自定义小数组
	FileReader fr = new FileReader("xxx.txt");
	FileWriter fw = new FileWriter("yyy.txt");
	char[] arr = new char[1024];
	int len;
	while(){}
	fr.close();
	fw.close();

##14.BufferedReader  &  BufferedWriter
	BufferedReader br = new BufferedReader(new FileReader("xxx.txt"));
	BufferedWriter bw = new BufferedWriter(new FileWriter("yyy.txt"));
	int c;
	while((c = br.read())!=-1) {
		bw.writer(c);
	}
	br.close();
	bw.close();

	***********************
	bw.readLine() 读取一个文本行,通过\n\r即可认为某行已终止,到达流末尾则返回空
	bw.newLine()	写出\r\n,是跨平台的换行
	bw.write("\r\n");	只是windows系统
	

##15.指定编码表读取(转换流)
	InputStreamReader isr = new InputStreamReader(new FileInputStream("aaa.txt"),"utf-8");
	OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream(bbb),"gbk");	//默认用平台的gbk码表

##16.递归调用
- 好处:不用知道循环的次数
- 弊端:有可能内存溢出
- 构造方法不能用递归
- 返回值:可以有,也可以没有.

##17.递归遍历文件夹
1. 获取该文件夹路径下的所有的文件和文件夹,存储在File数组中
2. 遍历数组,对每一个文件或文件夹做判断
3. 如果是文件,并且后缀是.java的,就打印
4. 如果是文件夹,就递归调用

   		 public static File getDir() {
		Scanner sc = new Scanner(System.in);
		Syso("请输入一个文件夹路径")
		while(){
			String line = sc.nextLine();
			File dir = new File(line);
			if(!dir.exists()){
				Syso("您输入的文件夹路径不存在,请重新输入");
			}else if(die.exists()){
				syso("您输入的是文件路径,请重新输入")
			}else{
				return dir;
				}
			}
		}

		public static void printJavaFile(File dir){
		File[] subFiles = die.listFiles();
		for(File subFile : subFiles) {
			if (subFile.isFile() && subFile.getName().endswith(".java")){
				Syso();	
			}else if(subFile.isDirectory() && subFile.listFiles() != null){				/如果系统文件夹不具备访问权限listFiles()返回null
				printJavaFile(subFile);
			}
		}
	}

##18.系列流(SequenceInputStream)
- 把多个字节输入流整合成一个,从序列流中读取数据时,将从被整合的第一个流开始读,读完一个读下一个.依次类推,直到达到最后一个流的文件末尾.

    	SequenceInputStream sis = new SequenceInputStream(new FileInputStream("a.txt"),new FileInputStream("b.txt"));
		FileOutputStream fos = new FileOutputStream("c.txt");
		int b;
		while((b = sis.read()) != -1){
		fos.writer(b);
		}

		sis.close();		//sis关闭的时候,会将构造方法中的流对象也关闭
	fos.close();

##19.序列流整合多个
- SequenceInputStream(Enumeration<? extends InputStream> e) 

    	Vector<FileInputStream> v = new Vector<>();
		v.add(fis1);
		v.add(fis2);
		v.add(fis3);
		v.add(fis4);
		v.add(fis5);
	
		Enumeration<FileInputStream	> en = v.elements();
		SequenceInputStream sis = new SequenceInputStream(en);

##20.内存输出流ByteArrayOutputStream
> ByteArrayInputStream 包含一个内部缓冲区，该缓冲区包含从流中读取的字节。内部计数器跟踪 read 方法要提供的下一个字节。
> ByteArrayOutputStream 此类实现了一个输出流，其中的数据被写入一个 byte 数组。缓冲区会随着数据的不断写入而自动增长。可使用 toByteArray() 和 toString() 获取数据。 相当于在内存中创建了可以增长的内存数组.

> FileInputStream读取中文的时候出现了乱码
- 字符流读取
- ByteArrayOutputStream

	FileInputStream fis = new FileInputStream("a.txt");
	ByteArrayOutputStream baos = new ByteArrayOutputStream();
	int b;
	while((b = fis.read()) != -1){
		baos.write(b);
	}
		
	//Syso(baos);			//将缓冲区的内容转换成字符串toString()
	byte[] arr = baos.toByteArray();
	syso(new String(arr));
	fis.close();

##21.随机访问流


- RandomAccessFile,不是一个流,是Object的直接子类,但是可以读写.

	RandomAccessFile raf = new RandomAccessFile("g.txt");
	raf.write(97);
	int x =raf.read();
	raf.seek(10);		//设定指针位置
	raf.write(98);		//当前指针位置写入


##22.对象操作流,ObjectOutputStream
> 该流可以将一个对象写出,或者读取一个对象到程序中,也就是执行了序列化和反序列化的操作.
	Person implements Serializable
	Person p1 = new Person("张三",23);
	Person p2 = new Person("李四",24);
	
	ObjectOutputStream oos = new ObjectOutputStram(new FileOutputStream("a.txt"));

	oos.writeObject(p1);
	oos.writeObject(p2);
	ooos.close();	

	OjectInputStream ois = new OjdectInputStream(new FileInputStream("a.txt"));
	person p1 = (Person)ois.readObject();
	person p2 = (Person)ois.readObject();
	//Person p2 = (Person)ois.readObject();	EOFException,文件末尾异常
	syso(p1);
	syso(p2);
	ois.close();

	******************优化*********************
	ArrayList<Person> list = new ArrayList<>();
	list.add(p1);
	list.add(p2);
	oss.writeObject(list);
	ArrayList<Person> l = (ArrayList<Person>)ois.readObject();
	fore(Person p : l)

##23.Serializeable的ID
> Oject序列化瞬时信息


##24.数据输入输出流
- DataInputStream,DataOutputStream可以按照基本数据类型大小读写数据


##25.打印流PrintStream字节流  PrintWriter字符流
- 只操作数据目的.
> 可以方便的将对象的toString()结果输出,并且自动加上换行,而且可以自动

    PrintStream ps = System.out;
	ps.println(97);				//97,底层调用toString转换成字符串打印
	ps.write(97);				//a,查找码表

	Person p1 = new Person("张三",23);
	ps.println(p1);				//打印引用数据类型,如果是null就打印null,不是null就是打印toString()结果.
	**********************************************
	PrintWriter pw = new PrintWriter("f.txt");
	pw.println(97);			//97
	pw.write(97);			//a
	pw.close();

##26.标准输入输出流 system.in system.out
	
	InputStream is = System.in;
	int x = is.read();
	Syso(x);

	****************改变标准输入输出流***************
	System.setIn(new FileInputStream("a.txt"));	//改变输入流
	System.setOut(new PrintStream("b.txt"));	//改变输出流

	InputStream is = System.in;			//获取标准输入流.默认指向键盘,改变后指向了a.txt
	PrintStream ps = System.out;		//获取标准输出流.默认指向控制台,改变后指向了b.txt

	int b ;
	while((b = is.read()) != -1) {
		ps.write(b);
	}
	is.close();
	ps.close();

##27.键盘输入的两种方法
	
	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	String line = br.readLine();
	System.out.println(line);
	br.close();

	
	Scanner sc = new Scanner(System.in);
	String line = sc.nextLine();

##28.Properties(配置文件),Hashtable的子类
> Properties 类表示了一个持久的属性集。Properties 可保存在流中或从流中加载。属性列表中每个键及其对应值都是一个字符串。用的时候全存字符串儿就可以了.


	Properties prop = new Properties();
	prop.put("abc",123);
	
	**************Properties的特殊功能***************
	prop.setProperty("name","张三");
	prop.setProperty("tel","12346798"); 
	Enumeration<String> en = (Enumeration<String>)prop.propertyName();
	while(en.hasMoreElements()) {
		String key = en.nextElements();
		String value = prop.getProperty(key);
		Syso(key + "=" value);
	}

	*******************
	prop.load(new FileInputStream("config.properties"));//将文件上的键值对读取到集合中.
	prop.setProperty("tel","15514894165");//只是在内存中更改,没有写到文件中
	prop.store(new FileOutputStream("config.properties"),"xxx");第二参数是对属性列表的描述.