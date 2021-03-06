# 正则表达式
## 正则表达式的获取功能
    Pattern和Matcher的结合使用.
    
    String str = "我的手机号码是13838383381"
    String regex = "1[3578]\\d{9}";
    Pattern p = Pattern.compile(regex); //获取正则表达式
    Matcher m = p.matcher(str);         //获取匹配器
    boolean b = m.matches();

    检验邮箱的功能
    String str = "haoyishen@itcast.cn"

    String regex = "[a-zA-Z_0-9]+@[a-zA-Z_0-9]+(\\.[a-zA-Z_0-9]{2,3})+";
    String regex = "\\w+@\\w+(\\.\\w{2,3})+";
    
##预定义字符类
    .       任何字符
    \d      数字[0-9]
    \D      非数字[^0-9]
    \w      单词字符[a-zA-Z_0-9]
    \W      非单词字符[^\w]
    \s      空白字符[\t\n\x0b\f\r]
    \S      非空白单词[^\s]
  
##数量词
    ?       一次或一次也没有
    *       零次或者多次
    +       一次或者多次
    {n}     恰好n次
    {n,}    至少n次
    {n,m}   至少n次,但是不超过m次

##分组和捕获
    1     ((A)(B(C))) 
    2     (A) 
    3     (B(C)) 
    4     (C) 

> 之所以这样命名捕获组是因为在匹配中，保存了与这些组匹配的输入序列的每个子序列。捕获的子序列稍后可以通过 Back 引用在表达式中使用，也可以在匹配操作完成后从匹配器获取。 



> 与组关联的捕获输入始终是与组最近匹配的子序列。如果由于量化的缘故再次计算了组，则在第二次计算失败时将保留其以前捕获的值（如果有的话）例如，将字符串 "aba" 与表达式 (a(b)?)+ 相匹配，会将第二组设置为 "b"。在每个匹配的开头，所有捕获的输入都会被丢弃.

> 以 (?) 开头的组是纯的非捕获 组，它不捕获文本，也不针对组合计进行计数。 

