## Java 进阶知识

### 异常

- 示例

```java
try{
  //业务逻辑代码
}catch(RuntimeException e){ //先catch子类错误
  System.out.println(e.getMessage()); //输出异常信息
  e.printStackTrace(); //把该异常的跟踪栈信息输出到控制台
}catch(Exception e){ //再catch父类错误
  System.out.println(e.getMessage()); //输出异常信息
}finally{
  //一般做回收资源的操作
}
```

```java
public void test() throws IOException{
	//出现IO错误就抛出，让上一级调用这个test方法的程序处理
  	//如果已经是最顶层的程序，比如main方法，那异常就会交给JVM处理，他会打印错误，并且中止程序
}
```

- 自定义的异常

```java
public class MyException extends Exception{
        public MyException(){
        }

        public MyException(String message){
            super(message);
        }
	}

    public class Test {
        public void display(int i) throws MyException{
            if(i == 0){
                throw new MyException("该值不能为0");
            }else{
                System.out.println( i / 2);
            }
        }

        public static void main(String[] args) {
            Test test = new Test();
            try {
                test.display(0);
            } catch (MyException e) {
                e.printStackTrace();
            }
        }
    }
```

- 注意点

  - 不要在finally块中处理返回值

  ```java
  try{
    //因为finally中包含了return语句
    //所以return true失去作用
    return true;
  }finally{
    return false;
  }
  ```

  - 不要在构造函数中抛出异常。
  - 尽可能的减小try块




### 泛型

- 泛型类

```java
//原来的样子
public class Container{
      private String key;
      private String value;
      public Container(String k,String v){
                key=k;
                value=v;
      }
      public String getKey(){
             return key;
      }
      public Stirng setKey(){
             this.key=key;
      }
      public String getValue(){
                return value;
      }
      public String setValue(){
                this.value=value;
      }
}
```

```java
//使用泛型来代替自己的变量类型
public class Container<k,V>{
        private k key;
        private V value;
        public Container(K k,V v){
                key=k;
                value=v;
        }
        public K getkey(){
                return key;
        }
        public V getValue(){
                  return value
        }
        public void setKey(){
                this.key=key;
        }
        public void setValue(){
              this.value=value;
        }
}
```

```java
//使用例子
public class Main{
        public static void main(String[] args){
                  Container<String,String> c1=new Container<String ,String>("name","hansheng");
                  Container<String,Integer> c2=new Container<String,Integer>("age",22);
                  Container<Double,Double> c3=new Container<Double,Double>(1.1,1.3);
                  System.out.println(c1.getKey() + " : " + c1.getValue());      
                  System.out.println(c2.getKey() + " : " + c2.getValue());                                                               
                  System.out.println(c3.getKey() + " : " + c3.getValue());
        }
}

输出：
name : findingsea
age : 24
1.1 : 2.2
```

- 泛型接口

```java
public interface Generator<T>{
          public T next();
}
//然后定义这个生成器类来实现这个接口
public class FruitGenerator implements Generator<String>{
          private String[] fruits=new String[]{"Apple","Banana","Pear"};
          @Override
          public String next(){
                    Ramdom rand=new Random();
                    return fruits[rand.nextInt(3)];
          }
}
```

- 泛型方法

```java
public class Main{
      public static <T> void out(T t){
                System.out.println(t);
      }
      public static void main(String[] args){
              out("hansheng");
              out(123);
      }
}
```

```java
public class Main {
	//不限个数的数组形式参数
    public static <T> void out(T... args) {
        for (T t : args) {
            System.out.println(t);
        }
    }

    public static void main(String[] args) {
        out("finding", 123, 11.11, true);
    }
}
```

- 泛型接口使用方法

```java
interface Info<T>{
        public T getVar();
}
class InfoImpl<T> implements Info<T>{
      private T var;
      public InfoImpl(T var){
                this.setVar(var);
      }
      public void setVar(T var){
                  this.var=var;
      }
      public T getVar(){
                  return this.var;
      }   
}
public class Test{
      public static void main(String args){
              Info<String> i=null;
              i=new InfoImpl<String>("hansheng");
              System.out.println("content"+i.getVar());
      }
}
```

- 类型判断

```java
Class c1=new ArrayList<Integer>().getClass();
Class c2=new ArrayList<String>().getClass();
System.out.println(c1==c2);
//返回true
```



### 多线程

- 通过实现Runable接口

```java
public class DisplayMessage implements Runnable
{
   private String message;
   public DisplayMessage(String message)
   {
      this.message = message;
   }
   public void run()
   {
      while(true)
      {
         System.out.println(message);
      }
   }
}
```

- 通过继承Thread类本身

```java
public class GuessANumber extends Thread
{
   private int number;
   public GuessANumber(int number)
   {
      this.number = number;
   }
   public void run()
   {
      System.out.println(number);
   }
}
```

- 测试

```java
public class ThreadClassDemo
{
   public static void main(String [] args)
   {
      Runnable hello = new DisplayMessage("Hello");
     //把接口传入线程，进行线程初始化
      Thread thread1 = new Thread(hello);
     //将该线程标记为守护线程或用户线程
      thread1.setDaemon(true);
     //改变线程名称，使之与参数 name 相同
      thread1.setName("hello");
     //使该线程开始执行
      thread1.start();
     
      Thread thread2 = new GuessANumber(27);
      thread2.start();
   }
}
```



### IO处理

![IO图](http://www.maijinta.cn/user/files/IO.jpeg)

- 字节和字符的关系
  - 1个字节＝8位
  - 1个字符＝2字节=16位
  - 一个汉字是2字符，全角符号也2字符，半角就一个字符
  - byte 1字节
  - short 2字节
  - int 4字节
  - long 8字节
  - char 2字节
  - float 4字节
  - double 8字节
- 相对路径和绝对路径

```java
publicstaticvoidtest1(){
  Filefile1=newFile(".\\test1.txt");
  Filefile2=newFile("D:\\workspace\\test\\test1.txt");
  System.out.println("-----默认相对路径：取得路径不同------");
  System.out.println(file1.getPath());
  System.out.println(file1.getAbsolutePath());
  System.out.println("-----默认绝对路径:取得路径相同------");
  System.out.println(file2.getPath());
  System.out.println(file2.getAbsolutePath());
}
```

```java
得到的结果：
-----默认相对路径：取得路径不同------
.\test1.txt
D:\workspace\test\.\test1.txt
-----默认绝对路径:取得路径相同------
D:\workspace\test\test1.txt
D:\workspace\test\test1.txt
```

```java
因为getPath()得到的是构造file的时候的路径。
getAbsolutePath()得到的是全路径
如果构造的时候就是全路径那直接返回全路径
如果构造的时候试相对路径，返回当前目录的路径+构造file时候的路径
```

- 字符流和字节流的主要区别
  - 字节流读取的时候，读到一个字节就返回一个字节；  字符流使用了字节流读到一个或多个字节（中文对应的字节数是两个，在UTF-8码表中是3个字节）时。先去查指定的编码表，将查到的字符返回。
  - 字节流可以处理所有类型数据，如：图片，MP3，AVI视频文件，而字符流只能处理字符数据。只要是处理纯文本数据，就要优先考虑使用字符流，除此之外都用字节流
- 字节流
- 字符流
- 相互转化

```java
//字节流转字符流
public class TestIO {
	public static void main(String[] args) throws IOException {
  	FileInputStream fis = new FileInputStream("c:\\abc.txt");// 字节流
	InputStreamReader isr = new InputStreamReader(fis);// 字符流
    BufferedReader br = new BufferedReader(isr);// 缓冲流
  	String str = null;
 	if ((str = br.readLine()) != null) {
      System.out.println(str);
    }
    br.close();
    isr.close();
    fis.close();
 	}
}
```

```java
//没有字符流转字节流，因为实际开发用不到，所有相关API也没有了
public class TestIO {
    public static void main(String[] args) throws IOException {
    FileReader fr = new FileReader("c:\\abc.txt");// 字符流
    BufferedReader br = new BufferedReader(fr);// 缓冲流
    String str = null;
    if ((str = br.readLine()) != null) {
    	System.out.println(str);
    }
    fr.close();
    br.close();
  ｝
｝
```



### 邮箱

- 准备
  - 要使用Java的邮箱功能需要javax.mail这个jar包
- SMTP
  - 简单邮件传输协议
- POP3
  - 邮局协议
- 最简单的邮件传输
  - 不包附件，只有正文部分，并且只是负责邮件的发送，因此只需要SMTP，当要读取邮件的时候就必须要使用POP3

```java
public boolean sendEmail(){    
	String FROM = "3427545623@163.com";//发件人的email
    String PWD = "***********";//发件人授权码(不同于密码)，开通SMTP服务后会需要设置授权码

	String HOST = "smtp.163.com";//设置邮件服务主机，每个服务商的邮件服务器地址都不一样
    String PROTOCOL = "smtp";//传输协议
    int PORT = 25;//端口号

	//创建Properties类用于保存邮箱环境的属性
    Properties props = new Properties();
    props.put("mail.smtp.host", HOST);//设置服务器地址
    props.put("mail.store.protocol" , PROTOCOL);//设置协议
	props.put("mail.smtp.port", PORT);//设置端口
    props.put("mail.smtp.auth", true);//表示SMTP发送邮件，必须进行身份验证

	//发送者的邮箱地址和口令也可以在这里设置，之后也可以拿出
    //props.put("mail.user", "3427545623@163.com");//此处填写你的账号
    //props.put("mail.password", "***********");// 发件人授权码,也就是STMP口令

	//实例化Authenticator这个抽象类，这里重写getPasswordAuthentication方法
    Authenticator authenticator = new Authenticator() {
        @Override
        protected PasswordAuthentication getPasswordAuthentication() {
          //传入发送者邮箱和密码
            return new PasswordAuthentication(FROM, PWD);
          //从环境属性中拿出
          //String userName = props.getProperty("mail.user");
          //String password = props.getProperty("mail.password");
          //return new PasswordAuthentication(userName, password);
        }
    };

	//使用环境属性和授权信息，创建邮件会话
	Session session = Session.getDefaultInstance(props,authenticator);

	try {
		//传入邮件会话来构造邮件信息对象
		Message msg = new MimeMessage(session);

        //设置Message属性
        msg.setFrom(new InternetAddress(FROM));//设置发送者
        InternetAddress address = new InternetAddress("593571421@qq.com");//获取收件人邮箱的网络地址
        msg.setRecipients(Message.RecipientType.TO, address);//设置收件人的地址
        msg.setSubject("账号激活邮件");//设置邮件标题
        msg.setSentDate(new Date());//设置发送时间
        msg.setContent("send successfully!","text/html;charset=utf-8");//设置邮件的内容体和内容格式

        Transport.send(msg);//发送邮件
        return true;
    }catch(MessagingException mex) {
        mex.printStackTrace();
        return false;
    }
}
```



### 验证码

- ​

### 反射

- ​

### 注解

- ​

### Socket

- ​

