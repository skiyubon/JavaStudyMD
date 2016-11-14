#Map,双列集合,映射.

##1.Map<K k, V v)


- 双列集合的键是唯一的,不可以重复.
- 每一个键最多只能对应一个值,值是可以重复.

##2.Map的结构体系.
- HashMap,存取无序,键不重复
- LinkedHashMap,存取有序,怎么存就怎么取.
- TreeMap,排序存储

##3.HashMap如何保证键的唯一性
- 必须重写自定义类的hashCode()和equals()方法.

	HashMap<Student,Integer) hm = new HashMao<>();

##4.Map的迭代,没有获取迭代器Map.iterator()方法.
1. 第一种方式:通过get(K k)方法获取值的方式.
 	
	    HashMap<Student,Integer> hm = new HashMap<>();
    	Set<Student> keySet = hm.keySet();
    	Iterator<Student> it = keySet.iterator();
    	while(it.hasNext()) {
    		Student key = it.next();
    		Integer value = hm.get(key);
    		Syso(key + "=" + value);
    	}
	**************************************************
	    for(Shtudent key : hm.keySet()) {
    		Integer value = hm.get(key);
    		Syso(key + "=" + value)
    	}
	
2. 第二种方式:通过Map.Entry<k,v>键值对对象来遍历.
		
		Set<Map.Entry<Student,Integer>> entrySet = hm.entrySet();
		for(Map.Enrty<Student,Integer> entry : entrySet){
			Student key = entry.getKey(k);
			Integer value = entry.getValue();
			Syso(key + "=" + value);
		}
		

##5.TreeMap
	TreeMap<Student,String> tm = new TreeMap<>(new Comparator<Student> {
		@override
		pblic int compare(Student s1,Student s2) {
			int num = s1.getName().compareTo(s2.getName());
			ruturn num == 0 ? 1 : num;
		}
	});

	tm.put(new Student("张三",23),"北京");
	tm.put(new Student("李四",24),"上海");
	tm.put(new Student("王五",25),"广州");
	tm.put(new Student("周六",26),"深圳");
	
- TreeMap的实例
- 统计字符串儿中每个字符出现的字数
- "aaaaabbbbccccdddd"

> 
	`String s = "aaaaabbbbccccdddd"; `
	char[] arr = s.toCharArray();
	HashMap<Charactor, Integer> hm = new HashMap<>();
	for(char c : arr) {
		if(!hm.contains(c) {
			hm.put(c,1);	
		}else {
			hm.put(c,hm.get(c)+1);
		}
		// hm.put(c,!hm.containsKey(c) ? 1 : hm.get(c) + 1);
	}

##6.Map的嵌套
	//定义88期
	HashMap<Student,String> hm88 = new HashMap<>();
	hm.put(new Student("张三", 23) , "北京");
	hm.put(new Student("李四", 24) , "北京");
	hm.put(new Student("王五", 25) , "北京");
	hm.put(new Student("赵六", 26) , "北京");
	//定义99期
	HashMap<Student,String> hm99 = new HashMap<>();
	hm.put(new Student("唐僧",  2300)  , "北京");
	hm.put(new Student("孙悟空", 1024) , "北京");
	hm.put(new Student("猪八戒", 1025) , "北京");
	hm.put(new Student("沙和尚", 1026) , "北京");
	
	大集合
	HashMap<HashMap<Student, String>, String> hm = new	HashMap<>();
	hm.put<hm88,"第88期基础班");
	hm.put<hm99,"第99期基本班");

	for(HashMap<Student, String> h : hm.keySet()) {
		String value = hm.get(h);
		for(Student key : h.keySet()) {
			String value2 = h.get(key);
			Syso(key + "=" + value2 + "..." + value);
		}
	}

##7.Hashtable,和HashMap的区别
1. 相同点:都是哈希算法,都是双列集合.
2. 区别:
	-  A:
	- HashMap是线程不安全,效率高,JDK1.2版本的.
	- Hashtale是线程安全的,效率低,JDK1.0版本的.
	-  B:
	- HashMap可以存储null键和null值.
	- Hashtable不可以存储null键和null值.
