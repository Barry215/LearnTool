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

- ​

### IO处理

- ​

### 邮箱

- ​

### 验证码

- ​

### 反射

- ​

### 注解

- ​

### Socket

- ​

