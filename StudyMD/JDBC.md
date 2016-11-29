#1.JDBC(java Data Base Connectivity ,java数据库连接)面向接口

> 是一个用于执行SQL语句的javaAPI,可以为多种关系型数据库提供统一访问,由java语言编写的类和接口组成.是java访问数据库的标准规范.
> 
> 提供了一种基准,可以构建更高级的工具和接口,使数据库开发人员能够编写数据库应用程序.
> 
> JDBC需要连接驱动,驱动是俩个设备进行通信,满足一定通信数据格式,数据格式由设备提供商规定,设备提供商为设备提供驱动软件,通过该软件可以设备进行通信.

    MySQL驱动,也是类库,实现了Sun规定的接口.
	Oracle驱动,也是类库,实现Sun规定的接口.
	...    

#2.JDBC开发步骤:
- 1.注册驱动
- 2.获取连接
- 3.获取语句执行平台
- 4.执行SQL语句
- 5.处理结果
- 6.释放资源


#3.示例

    public static void main(String[] args) throws ClassNotFoundException, Exception {
		Class.forName("com.mysql.jdbc.Driver");
		String url = "jdbc:mysql://localhost:3306/mybase";
		String username = "root";
		String password = "123";
		Connection con = DriverManager.getConnection(url, username, password);
		Statement stat = con.createStatement();
		String sql = "select * from sort";
		ResultSet rs = stat.executeQuery(sql);
		//处理结果集
		//System.out.println(rs);
		while (rs.next()) {
			//获取每列数据,使用resultset的getXXX方法
			System.out.println(rs.getInt("sid") + "  " + rs.getString("sname") + 
			"  " + rs.getDouble("sprice") + "  " + rs.getString("sdesc"));
			//弊端:getInt(colum),列编号因为查询的列数不同而不同
			//getInt(String 列名), 列名则不会
			//或者getObject();也可以
		}
		rs.close();
		stat.close();
		con.close();
	}

#4.SQL的注入攻击,登陆案例
> 

    Class.forName("com.mysql.jdbc.Driver");
		String url = "jdbc:mysql://localhost:3306/mybase";
		String username = "root";
		String password = "123";
		Connection con = DriverManager.getConnection(url, username, password);
		Statement stat = con.createStatement();
		
		Scanner sc = new Scanner(System.in);
		String user = sc.nextLine();
		String pass = sc.nextLine();
		
		//执行SQL语句查询,查询存在,登陆成功,否则失败
		
		String sql1 = "SELECT * FROM users1  WHERE username=? AND PASSWORD=?";
		PreparedStatement pst = con.prepareStatement(sql1);
		//pst.set方法.设置问号占位符上的参数
		pst.setObject(1, user);
		pst.setObject(2, pass);
		
		
		
		
		/*String sql = "SELECT * FROM users1 "
				+ "WHERE username='" +user +"' AND PASSWORD='" +pass+ "'";
		
				//+ "OR 1=1";	注入攻击
		System.out.println(sql);
		ResultSet rs = stat.executeQuery(sql);
		//System.out.println(rs.next());
		
		*/
		ResultSet rs = pst.executeQuery();
		while (rs.next()) {
			System.out.println(rs.getString("username") + rs.getString("password"));
			
		}
		
		rs.close();
		pst.close();
		con.close();

#5.JDBC.update示例

    	Class.forName("com.mysql.jdbc.Driver");
		String url = "jdbc:mysql://localhost:3306/mybase";
		String username = "root";
		String password = "123";
		Connection con = DriverManager.getConnection(url, username, password);
		
		//参数?占位符
		String sql = "update sort set sname=?,sprice=? where sid=?";
		//
		PreparedStatement pst = con.prepareStatement(sql);
		//设置
		pst.setObject(1, "汽车美容");
		pst.setObject(2,4500 );
		pst.setObject(3,7);
		
		pst.executeUpdate();
		
		pst.close();
		con.close();

#6.JDBC查询并获取结果集

    Class.forName("com.mysql.jdbc.Driver");
		String url = "jdbc:mysql://localhost:3306/mybase";
		String username = "root";
		String password = "123";
		Connection con = DriverManager.getConnection(url, username, password);
		
		String sql = "Select * from sort";
		
		CallableStatement pst = con.prepareCall(sql);
		
		ResultSet rs = pst.executeQuery();
		while (rs.next()) {
			System.out.println(rs.getString("sid") + "   "+rs.getString("sname") + "   "+rs.getDouble("sprice") + "   ");
			
		}
		
		pst.close();
		con.close();

#7.JDBC工具类的定义示例

    /*
	 * 实现JDBC的工具类
 	 * 定义方法,直接返回数据库的接连对象
 	*/

	public class JDBCUtils {
	private JDBCUtils(){};
	private static Connection con;
	
	static{
		try {
			Class.forName("com.mysql.jdbc.Driver");
			String url = "jdbc:mysql://localhost:3306/mybase";
			String username = "root";
			String password = "123";
			con = DriverManager.getConnection(url, username, password);
		} catch (Exception ex) {
			throw new RuntimeException(ex+"数据库连接失败!");
		}
		
	}
	/*
	 * 定义静态方法,返回数据库的连接对象
	 * 
	 */
	
	public static Connection getConnection(){
		return con;
	} 
	
	/*
	 * 关闭方法
	 */
	
	public static void close(Connection con,Statement stat,ResultSet rs){
		
		if (rs!=null) {
			try {
				rs.close();
			} catch (SQLException e) {
				// TODO: handle exception
			}
		}
		if (stat!=null) {
			try {
				stat.close();
			} catch (SQLException e) {
				// TODO: handle exception
			}
		}
		if (con!=null) {
			try {
				rs.close();
			} catch (SQLException e) {
				// TODO: handle exception
			}
		}
	}
	}

#8.JDBC获取每行数据并封装到java类对象中

    Connection con = JDBCUtils.getConnection();
		
		PreparedStatement pst = con.prepareStatement("Select * from sort");
		
		ResultSet rs = pst.executeQuery();
		
		List<Sort> list = new ArrayList<>();
		
		while (rs.next()) {
			Sort s = new Sort(rs.getInt("sid") , rs.getString("sname") , rs.getDouble("sprice") , rs.getString("sdesc"));
			list.add(s);
		}
		JDBCUtils.close(con, pst, rs);
		for (Sort s : list) {
			System.out.println(s);
		}


#9.使用property配置文件



- 在开发中获得连接的4个参数通都存在配置文件,方便后期维护,程序如需修改就修改配置文件.

	    /*
		 * 编写JDBC工具类,获取数据库连接
		 * 采用读取配置文件的文件,获取连接对象
		 * 读取配置文件,获取连接,执行一次,static{}
		 */
		public class JDBCUtilsConfig {
		private static Connection con;
		private static String driverClass;
		private static String url;
		private static String username;
		private static String password;
		static{
			try {
				readConfig();
				
				Class.forName(driverClass);
				 con = DriverManager.getConnection(url, username, password);
				
			} catch (Exception e) {
				throw new RuntimeException("连接失败!");
			}
		}
	
		private static void readConfig() throws IOException {
			InputStream in = JDBCUtilsConfig.class.getClassLoader().getResourceAsStream("database.properties");
			Properties pro = new Properties();
			pro.load(in);
			driverClass = pro.getProperty("driverClass");
			url = pro.getProperty("url");
			username = pro.getProperty("username");
			password = pro.getProperty("password");
		}
		
		public static Connection getConnection() {
			return con;
		}
		}

#10.DBUtils
- JDBC进行开发,不免重复代码过多,为了简化JDBC开发,用Apache Commons组件的一个成员:DBUtils
- DBUtils就是JDBC的简化开发工具包.

#11.DBUtils
> 是java编程中的数据库操作实用工具,小巧简单实用
> DBUtils封装了对JDBC的操作,简化了ＪＤＢＣ操作,可以少些代码
> DBUtils三个核心功能介绍
> 
- QueryRunner中提供对SQL语句操作的API
- ResultSetHandler接口.用于定义select操作后,怎样封装结果集
- DBUtils类,是一个工具类,定义了关闭资源与事务处理的方法

#12.事务处理
> 包装某些操作成一个事务
>
- 执行事务成功,commit事务
- 执行事务失败,rollbacks事务


#13.JavaBean
> 就是一个类,在开发中常用来封装数据
> 
- 需要实现接口:java.io.Serializable,省略了不影响程序
- 提供私有字段
- 提供getset方法
- 提供无参构造

#14.数据库连接池
- 连接过多,获取和释放,非常消耗系统资源
- 使用连接池,提高性能
- 可以重复使用Connection.close()并不是销毁连接,而是归还连接
- java为数据库连接池提供了公共的接口:javax.sql.DataSource(规范)
- DBCP,C3P0

