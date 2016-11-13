#1.HashSet

> 存取无序,元素不重复.
	@override hashCode()&equals()

	public int hashcode() {
		int prime = 31;
		int result = 1;
		result = result * prime + age;
		result = result * prime +(name==null)? 0:name.hashCode();
		return result;
	}

	public boolean equals(Object obj) {
	if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Student other = (Student) obj;
		if (age != other.age)
			return false;
		if (name == null) {
			if (other.name != null)
				return false;
		} else if (!name.equals(other.name))
			return false;
		return true;
	}

#2.LinkedHashSet
>存取有序的Set

#3.TreeSet,自然排序
> 用来给集合中的元素排序的.同样也可以保证元素的唯一.

	TreeSet<Person> ts = new TreeSet<>();
	ts.add(new Person("张三",23));
	ts.add(new Person("张三",23));
	ts.add(new Person("李四",24));
	ts.add(new Person("李四",24));
	ts.add(new Person("张三",23)); 	//Person is not cast of Compareble


1. 当compareTo()返回0,集合中只有一个元素
2. 当compareTo()返回+,集合怎么存就怎么取
3. 当compareTo()返回-,集合将存储的元素倒序
 
> 二叉树存储:

- TreeSet.add方法,会调用compareTo()
- 小的存储在左边(-),大的存储在右边右边(+),相等就不存(0).
- compareTo方法.在TreeSet集合中如何存取取决于compareTo()的返回值.
	
		@compareTo()
		public int compareTo(Person other) {
		int NUM = this.age - other.age;			//以年龄为主要条件
		return NUM == 0 ? this.name.compareTo(other.name) : NUM;
	}

##TreeSet之比较器comparator
	TreeSet<Person> ts = new TreeSet<>(new compareByLen());
	//TreeSet<Person> ts = new TreeSet<>(new comparator<String>(){});
	匿名内部类并重写里面的方法
		ts.add("aaaa");				//指定了比较器,则优先使用比较器
		ts.add("z");				
		ts.add("adc");
		ts.add("cba");
		ts.add("q");

	class compareByLen implements Comparator<String> {	
		
		@override
		public int compare(String s1, String s2) {
			int num = s1.length() - s2.length();		//长度为主要条件
			return num == 0 ? s1.compareTo(s2) : num;//内容为次要条件
		}
	}

1. 自然排序,compareble,TreeSet的add()会把存入的对象提升为compareble类型
	重写compareble的compareTo()方法.	
	调用对象的compareTo()方法和集合中的对象比较
	
2. 比较器顺序,comparator,add()自动调用comparator的子类对象,重写compare()
	调用接口中的compare().调用的对象是第一个参数,集合中的对象是第二个参数.
	
##TreeSet的实例1
> 定义一个无序重复的字符串的集合,对其排序但要保留重复的字符串.

	ArrayList<String> list = new ArrayList<>();
	list.add("aaa");
	list.add("aaa");
	list.add("bbb");
	list.add("bbb");
	list.add("casa");
	list.add("adwq");
	list.add("eee");
	list.add("fff");
	
	sort(list);

	syso(list);
												
	public static void sort(ArrayList<String> list) {
		TreeSet<String> ts = new TreeSet<String>(new Comparator<String>(){
			public int compare(String s1, String s2){
				int num = s1.compareTo(s2);
				return num == 0 ? 1 : num;
			}				//用自己的比较器实现去重但保留重复的元素
		});
		
		ts.addAll(list);
		list.clear();
		list.addAll(ts);
	}

##TreeSet的实例2
	**helloitcast -----> acehillostt**	
	character 有自己的自然排序compareble的compareTo()方法.相同就返回0,不存
	
	Scanner sc = new Scanner(System.in);
	Syso("请输入一个字符串儿:"	);
	String line = sc.nextLine();	
	char[] arr = line.toCharArray();		//new一个比较器,相同就返回1
	TreeSet<Character> ts = new TreeSet<>(new Comparator<Character>{
			public int compare(Character c1, Character c2) {
				//int num = c1 - c2;			//自动拆箱
				int num = c1.compareTo(c2);
				return num == 0 ? 1 : num;
			}

		});
	
	for(Char c : arr) {
		ts.add(c);			//自动装箱
	}

	for(Character c : ts) {
		Syso(c);
	}
	
	
	