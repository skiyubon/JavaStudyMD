#1.File类概述
- File更应该叫路径,路径有绝对路径和相对路径.
- 绝对路径是一个固定的路径,从盘符开始.相对路径是当前项目
- 文件和目录路径的抽象表现形式

#2.File类构造方法

	****File(String pathname);根据一个路径得到File对象
	File file = new File("F:\\....\\xxx.txt")
	file.exists();
	
	File file2 = new File("xxx.txt");

	****Flie(String parent,String child):根据一个目录和一个子文件/目录得到File对象
	String parent = "F:\\...\\..";
	String child = "001.txt";
	File file = new File(parent, child);
	
	****File(File parent ,String child):根据一个父File对象和一个子文件/目录得到File对象
	File parent = new File("F:\\ ...\\..");
	String child = "001.txt";
	File file = new File(parent,child);

#2.File的常见方法

    File file = new File("xxx.txt");	//throws IOexception
	file.createNewFile();				//如果没有就创建,有就不创建
	******
	file.mkdir();						//创建单级文件夹
	******
	File file = new File("ccc\\ddd");
	file.mkdirs();						//创建多级文件夹

	****************重命名和删除*****************
	File file = new File("xxx.txt");
	File file2 = new File("ooo.txt");	
	file.renameTo(file2);		//路径名相同,就是改名;路径不同就是改名并剪切
	
	file.delete();				//不走回收站的删除文件或者文件夹,删除文件夹时文件夹内不能包含文件或者文件.

	public boolean isDirectory()
	public boolean isFile()
	public boolean exists()
	public boolean canRead()
	public boolean canWrite()
	public boolean isHidden()