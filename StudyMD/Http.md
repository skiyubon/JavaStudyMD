#1.HTTP简介:
- web浏览器与webF服务器之间一问一答的交互的过程必须遵的规则,就是HTTP协议
- 超文本传输协议protocol,是tcp/ip的一个应用层的协议,用于定义web浏览器与web服务器之间的交互数据的过程及数据本身的格式
- 版本:HTTP/1.0,HTTP/1.1

#2.HTTP1.0的基本运行方式
- 客户端与服务器的信息交换过程分为四个过程,建立连接,发送请求信息,发送响应信息,关闭连接
- 浏览器与服务器的连接过程是短暂的,每次连接只能处理一个请求和响应.对每一个页面的访问,浏览器与服务器都要建立一次单独的连接
- 浏览器与服务器之间的所有通讯都是完全独立分开的请求与响应
- 无状态

#3.浏览器访问多图网页
- 在HTML网页中如果包含<img>标记的话,当浏览器解析到这些标记时,还会向服务器请求访问标记中指定的文件,即在此建立连接并发出HTTP请求
- 如果HTML页面中有一个超级链接:<a href="http://www.baidu.com">baidu</a>,当点击这个连接是,也会触发浏览器与WEB服务器开始一次新的HTTP通信


> HTTP1.1的特点

- 在一个TCP连接上,可以穿传送多个HTTP请求和响应
- 多个请求和响应可以重叠
- 增加了更多的请求头和响应头,比如:HOST,if-UNmodified-Since请求头等

#4.HTTP的请求消息
- 请求行:GET /books/java.html HTTP/1.1(get resource 协议)
- 多个消息头,描述客户端请求哪个主机,客户端的一些环境信息等
	- Accept:*/*				//能接受任意类型的数据
	- Accept-Language:en-us
	- Connection:keep-Alive
	- Host:Localhost			//主机
	- Referer:
	- User-Agent:Mozilla/4.0
	- Accept-Econding:gzip,deflate		//可以接受的文件问下

> 空格
- 消息体,正文内容



> ****************************************

- 状态行		HTTP/1.1 200 ok 	状态行用于描述服务器读请求的处理结果
- 多个消息头		//响应消息头描述服务器的基本信息,以及数据的描述,服务器通过这些数据的描述信息,可以通知客户端如何处理等一会儿它回送的数据
	- Server:Microsoft-IIS/5.0
	- Data:Thu, 13 Jul 2000 05:46:53 GMT
	- Content-Length:2291
	- Content-Type:text/html
	- Cache-control:private
	- 空行
- 正文内容,实体内容,代表服务器向服务端回送数据.
	- <HTML>
	- <BODY>
	- ....
	
#5.请求行
- 格式:请求方式 资源路径 HTTP版本号<CRLF>
- 请求方式:GET,POST,HEAD,OPTIONS,DELETE,TRACE,PUT
- 用户如果没有设置,默认情况下浏览器向服务器发送的都是get请求,例如:在浏览器直接输入地址访问,点超链接访问等都是get.用户如想把请求方式改为post,可通过更改表单的提交方式实现..
- 不管POST和GET,都用于向服务器请求某个web资源,这两种方式的区别主要表现在数据的传递上.
- 
> GET:
> 
- 如请求方式为GET方式,则可以在请求的URL地址后以?的形式带上交给服务器的数据,多个数据之间以&进行分隔,例如:
	- GET /mail/1.html?name=abc&password=xyz HTTP/1.1
	- GET方式的特点:在URL地址后附带的参数是有限制的,其数据容量通常不能超过1K.

> POST方式
> 
- 如请求方式为POST方式,则可以在请求正文内容中向服务器发送数据,POST方式的特点:传送的数据无限制.

#6.状态行
> 
- 格式:HTTP状态号 状态码 原因叙述<CRLF>
	- 举例:HTTP/1.1 200 OK
- 状态码:用于表示服务器对请求的各种不同处理结果和状态,它是一个三位的十进制数.响应状态码分为5类,使用最高位1-5来进行分类如下:
	- 100-199	-->表示成功接收请求,要求客户端提交下一次请求才能完成整个处理过程
	- 200-299	-->表示成功接收请求并已完成整个处理过程
	- 300-399	-->为完成请求,客户端需要进一步细化请求,例如:请求的资源已经移动一个新地址
	- 400-499	-->客户端的请求有错误
	- 500-599	-->服务器出现错误

> 常用的状态码:

- 200:表示一切正常,返回的是正常请求结果
- 302/207:(临时重定向)指出被请求的文档已被临时移动到别处,此文档的URL在Location响应头中给出.
- 304(未修改):表示客户机缓存的版本是最新的,客户机可以继续使用它,无需到服务器请求
- 404(找不到):服务器不存在客户机所请求的资源
- 500:服务器的程序发生错误

#7.HTTP请求头的细节
> 请求头字段用于客户端在请求消息中服务器传达附加信息,主要包括客户端可以接受的数据类型(MIME类型),压缩方法,语言,以及发出请求的超链接所属页面的URL地址等信息.


> 请求头的细节:

- Accept:浏览器可接受的MIME类型
- Accept-Charset:浏览器通过这个头告诉服务器,它支持的字符集
- Accept-Encoding:浏览器能够进行解码的数据编码方式,比如gzip
- Accept-Language:浏览器所希望的语言种类,当服务器能够提供一种以上的语言版本是要用到,可以在浏览器中设置
- HOST:初始URL中的主机和端口
- Referer:包含一个URL,用户从该URL代表的页面出发访问当前请求的页面
- Content-Type:内容类型
- If-Modified-Since:wed,02 Feb 2011 12:02:56GMT利用这个头与服务器的文件进行对比,如果一致,则从缓存中直接读取文件.
- User-Agent:浏览器类型
- Content-Length:表示请求消息正文的长度
- Connection:表示是否需要持久连接.如果服务器看到这里的值为"keep-Alive",或者看到请求使用得是HTTP1.1(HTTP1.1默认进行持久连接)
- Cookie:这是最重要的请求头之一
- Data:请求时间GMT 


-----
> 响应头的细节
> 响应头字段用于向客户端传递附加信息


- Location:http://www.it315.org/index.jsp指示新的资源的位置
- Server:apache tomcat指示服务器的类型
- Content-Encoding:gzip	服务器发送的数据采用的编码类型
- Content-Length:80 		告诉浏览器正文的长度
- Content-Language:zh-cn 服务器发送的文本的语言
- Content-Type:text/html;charset=GB2312服务器发送的内容的MIME类型
- Last-Modified:			文件最后修改的时间
- Refresh:1;URL=http://www.it315.org		指示客户端刷新频率.单位是秒
- Content-Disposition:attachment;filename=aaa.zip指示客户端下载文件
- Set-Cookies:SS=QQ=5Lb_nQ;path=/search		服务器发送的Cookie
- Expires:-1
- Cache-Control:no-cache(1.1)
- Pragma:no-cache(1.0)
- Connection:close/Keep-Alive
- Date:		响应时间

