#1.线程概述
> 线程是程序执行的一条路径,一个进程可以包含多条线程
> 多线程并发执行,可以提高程序的效率,可以同时完成多项工作

#2.并发  并行
- 并行:同时执行
- 并发:轮流执行

#3.jvm是多线程的,除了main主线程.至少会还有一条垃圾回收的线程


#4.多线程的实现方法
- Thread
	- 继承Thread,重写父类的run()方法,将执行的代码写入run()方法中,创建子类对象
	
	
			MyThread mt = new MyThread();
			mt.start();		//调用start方法.jvm默认自动调用run()方法
			//mt.run();		//相当于一个普通方法

			class MyThread extends Thread {
			public void run() {
		
				
				}
			}	

- Runnable


#5.Sleep


#6.守护线程
- setDeamon(),设置一个线程为守护线程,该线程不会单独执行,当其他非守护线程都执行结束后自动退出.

#7.join() 线程
- 当前线程暂停,等待指定的线程执行结束(millis)后再执行.


#8.同步代码块synchronized(lock){}


1. 当多线程并发,有多个代码块同时执行,我们希望一个线程执行时不要cpu切换,执行完毕再执行别的代码. 就用同步.


#9.

- 非静态的同步方法的锁对象是this.
- 静态的同步方法的锁对象是该类的字节码对象.

#10.示例买票

		Ticket t1 = o;
		Ticket t2 = new Ticket();
		Ticket t3 = new Ticket();
		Ticket t4 = new Ticket();

		class Ticket extends Thread {
			private static int ticket = 100;
			 
			public  void run() {
				synchronized(Ticket.class) {
					while(true) {
						if(ticket <= 0)
							break;
						try{
							Thread.sleep(10);
						}catch(Exception e){}

						Syso(getName() + "...." + ticket--);
					}
				}
			}
		}


#11.单例设计模式(Singlet12on)
1. 私有构造方法

		***饿汉式***空间换时间
		class Singleton {
			private Singleton(){}
			
			//pulic static Singleton s = new Singleton();	//对外可能被修改
			private static Singleton s = new Singleton();
			
			public static Singleton getInstance() {
				return s;
		
			} 
		}

		***懒汉式***时间换空间,线程不安全,多线程访问时有可能创建多个对象
		private Singleton(){}
		private static Singleton s;
		public static Singleton getInstance() {
			if(s == null) {
				s = new Singleton();
			}
			return s;
		}

		******
		private Singleton(){}
		public  static final Singleton s = new Singleton();
	
		}

#12.TimerTask



#13.线程通信

##1.等待唤醒机制

	class P {
		private flag = 1;
		pubilc void print1() {
			synchronized(this) {
				if (flag != 1) {
					this.wait();
				}
				Syso("黑马程序猿");
				flag = 2;
				this.notify();		//随机唤醒单一线程
			}		
		}

		pubilc void print2() {
			synchronized(this) {
				if (flag != 2) {
					this.wait();
				}
				Syso("程序猿");
				flag = 1;
				this.notify();
			}		
		}
	}

##2.nodify()死锁,可以用notifyALL()优化.

- sleep()必须传入时间参数,不释放锁.
- wait()可以不传入参数,也可以传入参数,释放锁.

##3.互斥锁.jdk1.5新特性(ReentrantLock类)

    ReentrantLock r = new ReentrantLock();	//创建互斥锁
	Condition cd = r.newCondition();		//获取监视器

##4.ThreadGroup(线程组)


##5.线程的五种状态.
- new
- start()开启,就绪状态,有执行资格,没有执行权
- 有执行权,运行	
- sleep() wait() 堵塞状态
- 死亡状态,线程对象变成垃圾

##6.线程池(ExecutorService)
- 程序启动一个新线程的成本比较高,因为涉及到与操作系统的交互,使用线程池很好的提高了性能.


##7.Callable.有返回值,可以抛异常.


##8.简单工厂模式(静态工厂方法模式创建对象.)
- 客户端不需要负责对象的创建
- 如果有新的对象的增加,或者某些对象的创建方式不同,就需要不断的修改工厂类,不利于后期维护.

##9.工厂方法模式.

##10.适配器设计模式
- 是一个中间类,重写了借口中的所有抽象方法,重写方法体为空,并定义类为抽象
- 子类继承适配器类不用重写借口中的所有抽象方法,需要哪个方法就重写哪个方法.方便开发.