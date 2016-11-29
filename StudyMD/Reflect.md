#1.反射获取字节码对象的三种方法
> 


- Class.forName("全类名");
- 对象名.getClass();
- 类名.class();

#2.获取构造方法并创建对象

> 1.通过Class对象的newInstance方法能创建有空参构造的被反射的类实

> 2.获去被反射类的构造方法对象,用该对象的newInstance()可以创建目标实例

		


#3.获取成员(暴力反射)


> 1.字段

		getField();
		getDeclaredField(String Fieldname);		//获取私有字段的字段对象,然后通过该对象的执行 get 或 set 访问操作期间进行扩展转换
	
> 2.方法

		getMethod(String Methodname,Class<?>... parameterTypes);		  //获取被反射类的方法的方法对象,可变参数列表:Int.class


#4.通过反射越过泛型检查.掘金
> 泛型只在编译期有效,在运行期会被擦除掉.

	ArrayLise<Integer> list = new Arraylist<> ();

	Class clazz = Class.forName("java.util.ArrayList");
	Method m = clazz.getMethod("add",Object.class);
	m.invoke(list,"String");

#5.设置属性值方法示例.

	public void setProperty(Object obj, String propertyName,value){
	Class clazz = obj.getClass();
	Field field = clazz.getDeclaredField(propertyName)
	field.setAccessble(true);
	field.set(obj,value);
	}

#6.配置文件读取
	BufferedReader bfr = new BufferedReader(new FileReader("1.properties"));		
	Class clazz = Clazz.forName(bfr.readLine());
	

#7.动态代理



#8.模板设计模式
- 定义一个方法的骨架,剩下的部分可以抽象并让子类去灵活实现.
- 算法骨架要修改的话,就得修改骨架原码.


#9.枚举.(限定数量的多例设计)
- 自定义枚举类

		(abstract) class Week {
			public static final Week Mon = new Week();
			public static final Week Tue = new Week("星期二");
	
			public static final Week Wed = new Week("星期三"){
				public void show() {};
			};
		
			private String name;
			private Week() {};
			private Week(String name) {
				this.name = name;
			}
			
			public abstract void show();		
		}

- Enum
 
		public enum Week {
		 	MON,TUE,WED;
			MON("星期一"),TUE("星期二"),WED("星期三");
			
			MON("星期一"){
				public void show() {};
			}

			private String name;
			private Week() {};
			private Week(String name) {
				this.name = name;
			}	

			public abstract void show();		
		 }



* 枚举项必须在第一行.
* 可以构造方法,必须是私有的,默认也是私有.
* 可以有抽象方法,但是枚举项中必须重写抽象方法.
* 可以在switch()中可用枚举.

	ordinal();     返回枚举项的编号序列
	compareTo();   比较枚举项的编号
	valueOf(Class<T> enumType,String name);通过字节码对象获取指定枚举项
	values();		


#10.jdk1.7新特性
* 二进制字面值常量
* 数字字面量可以出现下划线
* switch语句可以用字符串
* 泛型简化,<>
* 异常的多个catch合并,每个异常用|或
* try-with-resource语句,(){}自动关流.

#11.jdk1.8新特性
* 接口中可以定义有方法体的非静态一般方法,用default修饰
* 接口中可以定义静态方法,不用default.
* 局部-内部类使用局部方法,必须用final修饰,延长生命周期,8可以省略.
* hashSet,可以保证存取有序.
	