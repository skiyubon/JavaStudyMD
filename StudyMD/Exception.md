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
	
#3.处理Exception的方法
1. try(检测Exception) {...} catch(捕获Exception){...}finally{...}
	1. try catch
	2. try catch finally
	3. try finally
	4. try-catch处理Exception之后,程序可以继续往后执行
2. 

