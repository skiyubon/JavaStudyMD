# String  2016/11/5 10:30:04 (skiyubon)
----


##1.`String str = "afd"`

> 字符串一旦初始化就不能被更改!

##2.截取自字符串
    
    subString(int beginIndex);
    subString(int beginIndex, int endIndex);

##3.字符串转换字节数组 
    byte[]  getByte()
- 返回字节数组,依照GBK码表(一个中文两个字节),包括了ASC码表.
- -->GBK码表,中文的第一个字儿肯定是负数.

##4.字符串儿转换成字符数组
    char[] toCharArray()
- 字符串转换成字符数组.

##5.任意类型转换成字符串儿
    static String valueOf()
- 任意类型的参数转换成字符串.
  
    String(byte[])
- 通过使用平台的默认字符集解码指定的字节数组,构造一个新的字符串.

##6.拼接字符串儿
    concat(String str)
- 拼接两个字符串儿.

##7.字符串儿转换大小写
    toUpperCase(),toLowerCase()
- 将字符串儿转换成大小写.可以先截取substring()指定的字符再转换大小写然后用concat()拼接.

##8.实例:数组转换成字符串儿 int[ ]--->String
    int[] arr = {1,2,3};
    String s = "[";
    
    for(int i = 0; i < arr.length; i++) {
        if(i == arr.length-1){
            s = s + "]"                     //拼接成一个新的字符串儿并赋值给S,会产生垃圾.
        }else if{
            s = s + arr[i] + ", ";
        }
    }
- 弊端,每遍历数字并拼接一次就会创建新的字符串对象,也会产生垃圾.
- 所以用字符串缓冲区(可变字符串儿StringBuffer,StringBuilder)来做,就不会产生垃圾.

##9.String类的替换功能
    String replace(char old ,char new)
    String replace(String old , String new)
- 注意:**返回一个新的字符串儿,需要接受.**
- 如果不存在old字符(串儿),保留原字符(串儿)不改变.
    
##10.String 去除字符串两端空格
    String trim()
- 去除字符串儿两端的费空格

##11.String的按字典顺序比较
    int compareTo(String str)
    int compareToIgnoreCase(String str),忽略大写小.

-  按编码值比较.查找的是UniCode编码(包含ASC).
-  从前到后比较,前面一样就比较后一个.
-  如果都一样就比较了长度. 
-  底层是调用compare(String s1, string s2)方法,return 负数,0,正数.

##12.String的查找统计实例
    indexOf(String str) 第一次出现的索引
    indexOf(String str, int fromIndex) 从fromIndex开始,第一次出现的索引
    
    LastIndexOf(char ch) 返回指定字符在此字符串中最后一次出现处的索引
    LastIndexOf(char ch , int fromIndex)
    返回指定字符在此字符串中最后一次出现处的索引，从指定的索引处开始进行反向搜索

    String s1 ="woaiheima,heimafdasjffdas,jfiasjfjaiofji,";
    String s2 = "jf";    //查找s2在s1中出现的次数.
    int count = 0;
    int index = 0;
    while((index = s1.indexOf(s2)) != -1) {
        cunt++;
        s1 = s1.substring(index + s2.length);
    }
    syso(count);
    
