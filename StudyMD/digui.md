##1.从键盘接受一个文件夹路径,统计该文件夹的大小

	Scanner sc = new Scanner(System.in);
	File dir = null;
	while(true) {
		Syso("请输入一个文件夹路径");
		String str = sc.nextLint()
		File file = new File(str);
		if(file.exists() && file.isDirectory) {
			dir = file;
			break;
		}else{
			Sys("你输入的路径有误");
		}		
	}
	Syso(getFilelen(dir));
	
	public static void getFileLen(File dir){
		long len = 0;
		File[] subFiles = dir.listFiles();
		for(File file : subFiles){
			if(file.isFile){
				len = len + file.Length();
			}else{
				len = len + getFileLen(file);
			}
		}
		return len;
	}

##2.删除文件夹大小
	
    Scanner sc = new Scanner(System.in);
	File dir = null;
	while(true) {
		Syso("请输入一个文件夹路径");
		String str = sc.nextLint()
		File file = new File(str);
		if(file.exists() && file.isDirectory) {
			dir = file;
			break;
		}else{
			Sys("你输入的路径有误");
		}		
	}
	deleteFile(dir);
	//1.获取该文件夹下的所有文件和文件夹
	//2.是文件就删除
	//3.是文件夹就就递归
	public static void deleteFile(File dir){
		File[] subFiles = dir.listFiles();
		for(File file : subFiles) {
			if(file.isFile()){
				file.delete();
			}else {
				deleteFile(file);
			}
		}
		dir.delete();	//删除空文件夹
	}

##3.从键盘接受两个文件夹路径,把其中一个文件夹中拷贝到另一个文件夹中
	
	public static void main(String[] args) throws IOException {
		Scanner sc = new Scanner(System.in);
		System.out.println("源文件路径");
		File src = new File(sc.nextLine());
		System.out.println("目标文件路径");
		File dest = new File(sc.nextLine());
		sc.close();
		copy(dest, src);
		
	}

	private static void copy(File dest,File src) throws IOException {
		File dir = new File(dest,src.getName());
		dir.mkdirs();
		File[] subFiles = src.listFiles();
		for (File file : subFiles) {
			if (file.isFile()) {
				BufferedInputStream bis = new BufferedInputStream(new FileInputStream(file));
				BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(new File(dir, file.getName())));
				int b ;
				while ((b = bis.read()) != -1) {
					bos.write(b);
					
				}
				bis.close();
				bos.close();
			}else {
				copy(dir,file);
			}
		}
	}


##4.按层级打印文件夹
	
	public static void printFileLev(File file,int lev) {
		File[] subFiles = file.listFiles();
		for(File file : subFiles){
			for(int i = 0 ; i <= lev; i++) {
				System.out.print("\t");
			}
			Syso(file.getName());
			if(file.isDirectory){
				printFileLev(file,lev+1);			
			}
		}
	}
	