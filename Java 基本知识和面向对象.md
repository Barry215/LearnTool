## Java 基本知识和面向对象

### 基本数据类型和运算符

- int
- String
- long
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



### 判断，筛选和循环

- if

```java
int a = 0;
if(a == 1){
    a = 0;
}else{
	a = 2;
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
   	break;
}
```

- for


```java
for(int i = 0;i<10;i++){
  System.out.println("我循环啦！");
  if(a == 3){
    System.out.println("跳出循环");
    continue;
  }
  System.out.println("C要大写！");
}
```

- while


```java
int a = 10;
while(a>0){
  a--;
  if(a == 3){
    System.out.println("跳出循环");
    break;
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

- 5 > 4 ? "y" : "n"



### 数据结构

- list
  - ArrayList
- set
- map
  - HashMap



### 私有和公有

- public
- private
- protected
- final
- static



### 静态代码块

- static
- 作用
- [示例](http://www.jb51.net/article/36038.htm)



### 面向对象

- 思想
- 应用
- 示例



### 接口和抽象类

- interface
- abstract
- 应用场景
- 示例



### 多态和继承

- 多态的思想
- 继承的思想
- 示例



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

- String既是一个类，也是数据类型
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
int	indexOf(int ch) //返回指定字符在此字符串中第一次出现处的索引。
boolean	isEmpty() //当且仅当 length() 为 0 时返回 true。
int	length() //返回此字符串的长度。
String replace(char oldChar, char newChar) // 返回一个新的字符串，替换此字符串中出现的所有oldChar
String trim() //返回字符串的副本，忽略前导空白和尾部空白。
```


### 枚举类

- enum
- 示例



### 时间类

- Date
- simpledateformat
- DateAPI



### 加密类

- MD5
- Hash
- SHA
- salt