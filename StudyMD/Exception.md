#错误和异常
#1.体系结构


> *Throwable

		*Error
		*Exception
			*RuntimeException
			*!RuntimeException
 
#2.Java处理Exception的方式


- main函数接受到这个问题时,有两种处理方式
	- 自己将问题处理,然后继续运行
	- 自己没有针对的处理方法,将问题交给main的调用者jvm处理	
	- jvm有默认的处理机制,将Exception详细信息输出到控制台
	
#3.处理Exception的方法之try-catch
1.try(检测Exception) {...} catch(捕获Exception){...}finally{...}

- try catch

- try catch finally

- try finally

- try-catch处理Exception之后,程序可以继续往后执行
	
2.多种异常处理的格式与用法 

	try {
	}catch(){
	}catch(){
	}

3.

- 客户端开发,一般处理异常是try-catch处理.


- 服务端开发,一般是底层开发,一把把异常向上抛

#4.jdk7处理Exception的新写法
	catch(ArithmeticException | ArrayIndexOutOfBoundsException){}

#5.RuntimeException 与 编译期异常的区别
- 编译时异常,也可以理解(冯佳)为未雨绸缪异常,编译期发现会有可能发生异常,要提供处理备案,不然编译通不过.
- 运行时异常就是程序猿的错误,必须回去处理代码.

#6.Throwable借口的方法

	try {
		System.out.println(1/0);
	}catcah(Exception e) {

		System.out.println(e.getMessage());			//获取异常信息
		System.out.println(e.toString());//获取异常类名和信息,返回字符串
		e.printStackTrace();				//jvm默认就用这种方法处理异常
	}
	
#7. 第二种:throws - throw	处理Exception的方法

	- 编译时异常的抛出,必须对其进行处理,处理不了就throws给调用者,由调用者处理.
	- 运行时异常的抛出,不用对其进行处理
- throws
	- 用在方法声明后,跟的是异常对象的抛出
	- 可以跟多个类名,用逗号隔开
	- 表示抛出异常,由方法调用者处理
- throw 
	- 在方法体内,跟的是一个/不能多个异常对象
	- 表示抛出异常,由方法体语句处理

#8.finally的特点
- 被finally控制的语句体一定会执行
- 特殊情况:在执行到finally之前jvm退出了.
- 一般用于关闭流释放资源

#9.final,finally,finalize的区别
- final:
	- 修饰类,不能被继承
	- 修饰方法,不能被重写
	- 修饰的变量,只能赋值一次
- finally:
	- 是try语句中的一个语句体,不能单独使用

- finalize:
	- 是垃圾回收器回收垃圾的一个方法
- 如果catch里面有return语句,finally的代码还会执行吗?(会,在return前.)

		int x = 0;
		try {
			x = 20;
			syso(1/0);
			return x;
    	}catch(Exception e) {
    		x = 30;
    		return x;
    	}finally{
    		x = 40;
			//return //千万不要在finally里写ruturn,会覆盖try.catch的结果.
    	}

#10.自定义异常
- 针对不同的异常,定义出各自的异常类名,方便寻找错误
- 可以继承Exception或者继承RuntimeException

#11.异常的注意事项和使用方法
> A:子类重写父类方法时,子类的方法必须抛出相同的异常或父类异常的子类
> 
> B:父类抛出了多个异常,子类只能抛出相同的异常或者他的子集.子类不能抛父类没有的异常
> 
> C:重写的方法没有异常抛出,那么子类的方法绝不可以抛出异常,如果子类方法内有异常,子类只能try,不能throw
> 
- 后续程序需要继续运行就try
- 后续程序不需要继续运行就throw.
	