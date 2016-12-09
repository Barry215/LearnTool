## Java 基本知识和面向对象

### 基本数据类型和运算符

- byte
- short
- int
- int[]
- long
- boolean
- char
- char[]
- float
- double
- !
- %
- &&
- ||
- +
- //
- ++
- \- -




#### 注意点

| 数据类型    | 封装类       | 特点                                       |
| :------ | --------- | ---------------------------------------- |
| int     | Integer   | int初始化是0，Integer初始化是null。Integer是int的封装类，可以实现和字符串的转换 |
| char    | Character | char初始化是_，Character初始化是null              |
| long    | Long      | long初始化是0，Long初始化是null                   |
| byte    | Byte      | byte初始化是0，Byte初始化是null                   |
| short   | Short     | short初始化是0，Short初始化是null                 |
| float   | Float     | float初始化是0.0，Float初始化是null               |
| double  | Double    | double初始化是0.0，Double初始化是null             |
| boolean | Boolean   | boolean初始化是false，Boolean初始化是null         |

>  PS：泛型定义时也不支持数据类型，只能是类
>
> 如`List<int>`就不行，但是`List<Integer>`可以



### 判断，筛选和循环

- if

```java
public int say(int word){
  int a = word;
  if(a == 1){
      a = 0;
  }else{
      a = 2;
  }
  return a;
}
```

- switch


```java
switch(a){
  case 0:
    a = 1;
    break;
  case 1:
    a = 2;
    break;
  default:
    a = 0;
}
```

- for


```java
for(int i = 0;i<10;i++){
  System.out.println("我循环啦！");
  if(i == 3){
    System.out.println("跳出循环");
    continue;
  }
  System.out.println("C要大写！");
}
```

- while


```java
public void speak(int key){
  int a = key;
  while(a>0){
    a--;
    if(a == 5){
      System.out.println("跳出循环");
      break;
    }else if(a == 1){
      System.out.println("结束方法");
      return;
    }
  }
}
```

- foreach


```java
int[] bbs = {1,2,3,4,5};
for(int bb : bbs){
  System.out.println(bb);
}
```

- do while


```java
int a = 10;
do{
  a--;
  System.out.println("循环");
}while(a>3);
```

- 5 > 4 ? "y" : "n"   返回的是y




### 面向对象

- 思想
  - 万事万物都是对象
  - 每个对象都具有各自的状态特征（也可以称为属性）及行为特征（方法）
  - 比如我们考虑一只狗，那么它的     状态是：名称，品种，颜色      行为：吠叫，摇摆，跑等


```java
public class Dog{
   private String breed;
   private int age;
   private String color;

   public void barking(){
   }
   
   public void hungry(){
   }
   
   public void sleeping(){
   }
}
```



### 构造方法

- 介绍
  - 构造方法是一种特殊的方法
  - 构造方法的方法名必须与类名相同
  - 构造方法没有返回类型，也不能定义为void，在方法名前面不声明方法类型
  - 构造方法的主要作用是**完成对象的初始化工作**，它能够把定义对象时的参数传给对象的域


```java
public class Puppy{
   private String name;
  
   public Puppy(){
   }

   public Puppy(String name){
      this.name = name;
   }
}
```



### 继承

- 介绍
  - 继承一个类，子类会获得父类的所有成员变量和成员方法
  - 一个类只能继承一个父类，但是可以被多个子类继承

```java
public class Animal {
	public int age = 40;
	
	public int getAge(){
		return age;
	}
}
```

```java
public class Dog extends Animal {
	public int age = 18;
	public String name = "dog";

	@Override
	public int getAge() {
		return age;
	}
	
  	public void setName(String name){
      this.name = name;
  	}	
  
	public String getName(){
		return name;
	}
}
```

```java
public class Test{
  public static void main(String args[]){
    Dog d1 = new Dog();
    System.out.println(d1.getName());
    
    //把父类实例赋给子类变量——相当于说动物是狗
    //把子类实例赋给父类变量——相当于说狗是动物
    
    Dog d2 = new Animal(); //变量其实只是给你的实例起个名字而已，这里类型转化后，还是Animal类型
    d2.setName(30); //程序报错，因为d2的类型还是Animal，Animal没有setName的方法
    
     //父类对象由子类实例化
    Animal animal = new Dog();
    System.out.println(animal.age);
    System.out.println(animal.getAge());
    //System.out.println(animal.getName()); 错误，Animal没有getName的方法
   }
}
```

```java
结果：   //animal变量访问变量是看 声明的类型，访问方法是看 实例的方法！
	dog
  	40
	18
```

- instanceof 运算符
  - 左面的对象是右面的类创建的对象时,该运算符运算的结果是true,否则是false 
  - instanceof左边操作元显式声明的类型与右边操作元必须是同种类或右边是左边父类的继承关系

```java
public class Test{
  public static void main(String args[]){

      Animal a = new Animal();
      Dog d = new Dog();

      System.out.println(a instanceof Animal);
      System.out.println(d instanceof Animal);
   }
}
```

```java
结果：
	true
	true
```

- 重写
  - 在Java中，子类可继承父类中的方法，而不需要重新编写相同的方法。但有时子类并不想原封不动地继承父类的方法，而是想作一定的修改，这就需要采用方法的重写。方法重写又称方法覆盖。

### 修饰词

| 类型        | 同类   | 同包   | 不同包子类 | 不同包非子类 |
| --------- | ---- | ---- | ----- | ------ |
| private   | yes  |      |       |        |
| default   | yes  | yes  |       |        |
| protected | yes  | yes  | yes   |        |
| public    | yes  | yes  | yes   | yes    |

- private
  - 除了class自己之外，任何人都不可以直接使用
- default
  - 类可以访问在同一个包中的其他类(朋友)的成员
- protected
  - 只有相同的包下的类(朋友)和自己的子类(子女)才能访问
- public
  - 该数据成员、成员函数是对所有用户开放的，所有用户都可以直接进行调用
- final
  - final类不能被继承，没有子类，final类中的方法默认是final的
  - final方法不能被子类的方法覆盖，但可以被继承。
  - final成员变量或参数表示常量，只能被赋值一次，赋值后值不再改变。
  - final不能用于修饰构造方法。
- static
  -  static表示“全局”或者“静态”的意思，用来修饰成员变量和成员方法，也可以形成静态static代码块
  -  被static修饰的成员变量和成员方法独立于该类的任何对象，即**不需要实例化对象就能用类名.变量(方法)来使用**

```java
private static final String StaticFinalVar = "aaa"; 
```

- this
  - this是对象，this.成员变量，this.函数（哪个对象调用的，this就代表该对象）
  - 函数的参数与成员变量重名时，赋值语句使用 this.name = name; 
  - this(name); 根据this所带的参数判断调用哪个构造函数。
- super
  - super();  调用父类构造函数 
  - super.成员函数； 调用父类成员函数或变量

```java
public class test{
  private int num;
  private char c;
  
  //无参构造函数
  public test(){
    
  }
  
  //一个参数的构造函数
  public test(int num){
    this.num = num;
  }
  
  //两个参数的构造函数
  public test(int num,char ch){
    //这里调用了第一个构造方法，并且必须放在新的构造方法的第一行
    this(num);
    c = ch;
  }
  
  public int getNum(){
    return num;
  }
  
  public void setNum(int num){
    this.num = num;
  }
  
  public static void main(String []args) {
        test t = new test(8);
		System.out.println(t.getNum());
    }
}
```

```java
public class exam extends test{
  private int grade;
  
  public exam(){
    super();
  }
  
  public exam(int num){
    super(num);
  }
  
  public int query(int gradeSheet){
    //super.num = gradeSheet;
    super.setNum(gradeSheet);
	return super.getNum();
  }
  
  public static void main(String[] args) {
		exam e = new exam(3);
		System.out.println(e.getNum());
		
		int sheet = 95;
		e.query(sheet);
		System.out.println(e.getNum());
	}
}
```

```java
运行结果：
  3
  95
```



### 静态代码块

- static
  - 静态代码块里的使用的变量和方法也必须是static的
  - 静态代码块是在类加载时自动执行的，非静态代码块是在创建对象时自动执行的代码，不创建对象就不会执行该类的非静态代码块
  - 执行顺序：静态代码块------非静态代码块----构造函数


```java
public class StaticBlock {
	//静态代码块
     static {
         System.out.println("静态块");
     }
  	//非静态代码块
     {
         System.out.println("构造块，在类中定义");
     }
	//构造函数
     public StaticBlock() {
         System.out.println("构造方法执行");
     }

     public static void main(String[] args) {
         new StaticBlock();
         new StaticBlock();
     }

 }
```

```java
运行结果：
  静态块 
  构造块，在类中定义 
  构造方法执行 
  构造块，在类中定义 
  构造方法执行 
```

- 原理
  - 实例化有两个步骤：1、类加载  2、new 对象
  - 一个类在第一次被使用的时候会被类加载，然后在整个应用程序的生命周期当中不会再次被加载了，就加载这一次
  - 因为static{}是在类加载时候被加载的，所以static{}也只会被加载一次




### 数据结构

  ![collection](http://www.maijinta.cn/user/files/collection.png)

- Collection (接口)
- List (接口)
  - ArrayList (实现类)
    - 非线程安全
  - Vector (实现类)
    - 线程安全


```java
List<Object> objectList = new ArrayList<Object>();
Object object1 = new Object();
Object object2 = new Object();
objectList.add(object1);
object2 = objectList.get(0);
objectList.remove(0);
```

- Set (接口)
  - HashSet (实现类)
    - 不能有重复的元素


```java
Collection books = new HashSet();
books.add("01");
books.add("02");
```

- Iterator (接口)
  - **只能用于Collection的遍历**


```java
Iterator it = books.iterator();
while(it.hasNext()){
  String book = (String)it.next();
  it.remove();
}
```



 ![map](http://www.maijinta.cn/user/files/map.png)

- Map (接口)
  - HashMap (实现类)


```java
Map map = new HashMap();
map.put("boy","凯杰");
map.put("girl","青娜");
if(map.containKey("boy")){
  String name = map.get("boy");
  for(String type : map.keySet()){
    name = map.remove(type);
    System.out.println(name);
  }
}
```

- 遍历Map

```java
Map<String, String> map = new HashMap<String, String>();
for (Map.Entry<String, String> entry : map.entrySet()) {
	entry.getKey();
	entry.getValue();
}
```

```java
Iterator<Map.Entry<String, String>> iterator = map.entrySet().iterator();
while (iterator.hasNext()) {
	Map.Entry<String, String> entry = iterator.next();
	entry.getKey();
	entry.getValue();
}
```





### 接口和抽象类

- interface
  - 接口是抽象方法的集合。一个类实现一个接口，从而继承接口的抽象方法
  - 不能实例化一个接口
  - 接口不包含任何构造函数
  - 所有在接口中的方法都是抽象的
  - 一个接口可以扩展多个接口
  - 在接口中的每个方法也隐式抽象的，所以abstract关键字不需要
  - 在接口中的方法是隐式公开的，即默认是public，不能写成private


```java
//电脑类
public class Computer {  
    //定义一个接口类型的成员变量
    private ConnectToUsb connectToUsb;  
  
  	//获得接口对象
    public ConnectToUsb getConnectToUsb() {  
        return connectToUsb;  
    }  
    //赋值给接口  
    public void setConnectToUsb(ConnectToUsb connectToUsb) {  
        this.connectToUsb = connectToUsb;  
    }  
    
    public void connect() {  
        //调用接口的方法
        connectToUsb.connect();  
    }  
}  
```

```java
//USB接口
public interface ConnectToUsb {  
    public abstract void connect();  
}  
```

```java
//MP3实现了USB接口的方法
public class MpThree implements ConnectToUsb{  
    @Override  
    public void connect() {  
        System.out.println("MP3 To Connect!");  
    }  
}  
```

```java
//测试
public class Test {  
    public static void main(String[] args) {  
        Computer c = new Computer();  
        MpThree m = new MpThree();  
        c.setConnectToUsb(m);  
        c.connect();  
    }  
}  

结果：MP3 To Connect!
```

- abstract
  - 如果我们要定义的一个类的时候，没有足够的信息来描述一个具体的对象，还需要其他的具体类来支持
  - 这个时候我们可以考虑使用抽象类。在类定义的前面增加abstract关键字，就表明一个类是抽象类。
  - 抽象类除了不能实例化对象之外，类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。
  - 由于抽象类不能实例化对象，所以抽象类必须被继承，才能被使用。


```java
//形状父类
public abstract class Shapes {
    public int x, y;
    public int width, height;
    public Shapes(int x, int y, int width, int height) {
       this.x = x;
       this.y = y;
       this.width = width;
       this.height = height;
    }
    //计算面积
    abstract double getArea();
    //计算周长
    abstract double getPerimeter();
}
```

```java
public class Circle extends Shapes {
    public double r;
    public double getArea() {
       return (r * r * Math.PI);
    }
    public double getPerimeter() {
       return (2 * Math.PI * r);
    }
    public Circle(int x, int y, int width, int heigh) {
       //调用父类构造函数
       super(x, y, width, heigh);
       r = (double) width / 2.0;
    }
}
```

- 区别
  - 接口作用
    - 在业务逻辑设计的时候，可以只关注逻辑，不去写具体实现。等到接口写完后，你完全可以把具体实现交给其他人做，其他人按照你的业务逻辑就能完成。
    - 当知道**一件事肯定要多次被做**或者**将来功能扩展的时候会被做**，但是每次做的方法都不一样的时候，你可以写个接口，相当于声明了这个方法，而具体实现可以等用的时候再写，这样可以使代码更加简洁明了。
  - 抽象类作用
    - 多个类把共同的代码片段的抽取出来，做成一个基类。
    - 相同行为，不同代码的成员方法，可以用抽象方法来代替，不去具体实现。
    - 相同的代码，基类可以统一来具体实现了，节约了子类的代码
  - 两者区别
    - 接口更加零散，他专注于概括不同的方法。抽象类更加像一个基类，为不同的子类做一个总的基础。
    - 抽象类是对**类**的抽象，而接口是对**行为**的抽象




### 多态

- 多态的思想
  - 继承，接口实现
    - 狗是动物，猫是动物，鱼是动物
    - 吃可以是吃饭，吃零食，吃大餐
  - 重载
    - 一个方法可以有一个参数，两次参数或无数个参数，也可以是不同的返回类型，但方法名要一样
  - 运算符重载
    - 运算符两边的东西不一样，作用也不一样
- 示例
  - 例子太多，就不举啦😀




### 字符类

- String和char[]


```java
String str = "GG";
char[] bm;
bm = str.toCharArray();
//将 String 字符串 str 转换成数组
str = String.valueOf(bm);
//将 char 数组 bm 转换成字符串
```

- String是一个引用类型，不是基本数据类型
- StringBuffer
  - 线程安全的
- StringBuilder
  - 线程非安全的，会造成死锁
- StringBuffer与StringBuilder
  - StringBuilder >  StringBuffer
  - 他们是字符串变量，是可改变的对象，每当我们用它们对字符串做操作时，实际上是在一个对象上操作的，不像String一样创建一些对象进行操作，所以速度就快了。
  - 如果要操作少量的数据用 = String
  - 如果单线程操作字符串缓冲区 下操作大量数据 = StringBuilder
  - 如果多线程操作字符串缓冲区 下操作大量数据 = StringBuffer


- StringAPI


```java
char charAt(int index) //返回指定索引处的 char 值。
String concat(String str) //将指定字符串连接到此字符串的结尾。
boolean	contains(CharSequence s) //当且仅当此字符串包含指定的 char 值序列时，返回 true。
boolean	equals(Object anObject) //将此字符串与指定的对象比较。
int	indexOf(String str) //返回指定字符在此字符串中第一次出现处的索引(从0开始)。
int lastindexOf(String str) //返回指定字符在此字符串中最后一次出现处的索引。
boolean	isEmpty() //当且仅当 length() 为 0 时返回 true。
int	length() //返回此字符串的长度。
String replace(char oldChar, char newChar) // 返回一个新的字符串，替换此字符串中出现的所有oldChar
String trim() //返回字符串的副本，忽略前导空白和尾部空白。
```


### 枚举类

- enum


```java
public enum Color {  
  RED, GREEN, BLANK, YELLOW  
} 
```

```java
public enum Signal {
  GREEN, YELLOW, RED
}

public class TrafficLight {
	Signal color = Signal.RED;

	public void change() {
		switch (color) {
		case RED:
			color = Signal.GREEN;
			break;
		case YELLOW:
			color = Signal.RED;
			break;
		case GREEN:
			color = Signal.YELLOW;
			break;
		}
	}
}
```

```java
public enum Color {
  	//实例的对象
	RED("红色", 1), GREEN("绿色", 2), BLANK("白色", 3), YELLO("黄色", 4);//注意封号
	// 成员变量
	private String name;
	private int index;

	// 构造方法
	private Color(String name, int index) {
		this.name = name;
		this.index = index;
	}

	// 普通方法
	public static String getName(int index) {
		for (Color c : Color.values()) {
			if (c.getIndex() == index) {
				return c.name;
			}
		}
		return null;
	}

	// get set 方法
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getIndex() {
		return index;
	}

	public void setIndex(int index) {
		this.index = index;
	}
}
```

```java
public class Main {

	public static void main(String[] args) {
		Color c = Color.RED;
		System.out.println(c.getName());
	}
}
```

```java
结果：
	红色
```




### 时间类

- Date

```java
public class Main {
	public static void main(String[] args) {
		Date d = new Date();
		System.out.println(d.getTime()); //1970年到现在的毫秒数
		System.out.println(d.getDate()); //今天的日期
		System.out.println(d.getDay()); //今天的星期号
		System.out.println(d.getHours()); //现在的小时数
      	······
	}
}
```

```java
结果：
	1477131413252
	22
	6
	18
```

- SimpleDateFormat
  - 一个格式化的时间工具类
- String转Date

```java
public static void main(String[] args) {
	try {
		String dateString = "2016-10-22 19:43:00";
		DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		Date date = df.parse(dateString);
      	System.out.println(date);
	} catch (ParseException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
}
//Sat Oct 22 19:43:00 CST 2016
```

- Date转String

```java
public static void main(String[] args) {
	String time = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(new Date());
	System.out.println(time);
}
//2016-10-22 18:25:49
```



### 加密类

- Hash 算法
  - 它的算法的特征是不可逆性，并且在计算的时候所有的数据都参与了运算，其中任何一个数据变化了都会导致计算出来的Hash值完全不同，所以通常用来校验数据是否正确或用作身份验证。
- MD5
  - 最常用的哈希算法

```java
public String getMD5(String s) {
        char hexDigits[]{'0','1','2','3','4','5','6','7','8','9','A','B','C','D','E','F'};  
  		try {
            byte[] btInput = s.getBytes("utf-8");
            MessageDigest mdInst = MessageDigest.getInstance("MD5");
            mdInst.update(btInput);
            byte[] md = mdInst.digest();
            int j = md.length;
            char str[] = new char[j * 2];
            int k = 0;
            for (int i = 0; i < j; i++) {
                byte byte0 = md[i];
                str[k++] = hexDigits[byte0 >>> 4 & 0xf];
                str[k++] = hexDigits[byte0 & 0xf];
            }
            return new String(str);
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }
```

- SHA 
  - SHA加密原理又叫安全哈希加密技术，是当今世界最先进的加密算法
- MD5和SHA的区别
  - MD5比SHA快，SHA比MD5强度高，更安全
- salt 盐值
  - 混淆原数据的值