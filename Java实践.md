## Java实践

### java设计模式

#### 简单工厂模式

- 思想
  - 当你有很多类似的类需要实例化的时候，你可以建造一个工厂，让工厂来生产(实例化)它们
- 举例
  - 自定义了很多异常，每次程序运行出错都需要生成不同类型的异常，我们可以用异常工厂来生产这些异常
  - 你是一个身怀满技的工人，想制作电脑做生意，但是电脑制作工艺更新太快，一个人学不过来，所以开一家工厂，让工厂来生产电脑，这样你就不用学这么多电脑制作的知识了。你只需要吩咐工厂生产。

#### 工厂模式

- 思想
  - 建立在简单工厂的思想下，我们把具体工厂生产实例的方法抽象出来，再建一个抽象型的工厂，用于制定生产规范
- 举例
  - 你现在有了一家生产电脑的大工厂，专门生产各种类型的电脑。后来，这家工厂太大，生产的电脑型号也太多，你为了管理和分工方便，把工厂拆分成苹果电脑工厂，平板电脑工厂，普通电脑工厂三家工厂，然后再创建一个工厂监制会，专门统一每个工厂必须要有的流程和加工。然后每个工厂都按照监制会的标准去生产不同类型的电脑。

#### 单例模式

- 思想
  - 这个世界上有些东西是独一无二的，我们必须保证它只能有一个实例。

- 特征

  - 单例类只能有一个实例
  - 单例类必须自行创建自己的唯一的实例
  - 单例类必须给所有其他对象提供这一实例
  - `Singleton`(单例):在单例类的内部实现只生成一个实例，同时它提供一个静态的`getInstance()`方法，让使用者可以访问它的唯一实例
  - 为了防止在外部对其实例化，将其构造函数设计为`私有`
  - 在单例类内部定义了一个`Singleton`类型的**静态**对象，作为外部共享的唯一实例。

- 举例
  - 你是个好男人，把工厂赚的钱都给了老婆，但是老婆只能有一个

- 实现方式

  - 线程不安全

  - ```java
    public class Singleton {
        private static Singleton instance;
        private Singleton (){}
        public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
        }
    }
    ```

  - synchronized [更多](http://www.jianshu.com/p/29854dc7bd86)

    - Java语言的关键字，当它用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码。

  - 用法

    - 修饰一个类，其作用的范围是synchronized后面括号括起来的部分，作用的对象是这个类的所有对象
    - 修饰一个方法，被修饰的方法称为同步方法，其作用的范围是整个方法，作用的对象是调用这个方法的对象
    - 修改一个静态的方法，其作用的范围是整个静态方法，作用的对象是这个类的所有对象
    - 修饰一个代码块，被修饰的代码块称为同步语句块，其作用的范围是大括号{}括起来的代码，作用的对象是调用这个代码块的对象

  - 线程安全

  - ```java
    public class Singleton {
        private static Singleton instance;
        private Singleton (){}
        public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
        }
    }
    ```


#### 建造者模式

- 思想
  - 在工厂模式下，多了一层导演者。可以简单理解成用户做一件事情，会先找外包公司，而不是直接找工厂。外包公司会根据用户的需求来选择合适的工厂来生产。
- 举例
  - 后来你年纪大了，工厂的事情管的太累，所以你让邀请一个人当这家公司的CEO，你当董事局主席。工厂的业务都是CEO来负责，无论多开了几家工厂，和你都没有关系。你有事的话就吩咐CEO就好。

#### 适配器模式

- 思想
  - 我们笔记本用的到充电器其实就是个适配器，笔记本电脑的工作电压是20V，而我国的家庭用电是220V，如何让20V的笔记本电脑能够在220V的电压下工作？就是靠这个充电器搞定的。在软件开发中，有时也存在类似这种不兼容的情况，我们也可以像引入一个电源适配器一样引入一个称之为适配器的角色来协调这些存在不兼容的结构，这种设计方案即为适配器模式。
- 举例
  - 你的公司遇到互联网大潮，需要转型到线上销售，但是你原来的公司没有电商部门，只有线下销售，所以你花重金请来了一个电商团队，帮你协调线上和线下的联合销售。

#### 学习资料

[设计模式总结](http://blog.csdn.net/chenssy/article/category/1424118)

[23种设计模式](http://wiki.jikexueyuan.com/project/java-design-pattern/)

[设计模式干货系列](http://www.jianshu.com/p/9bceeedaf658)



### 数据库

#### 主键

关系型数据库中的一条记录中有若干个属性，若其中某一个属性组(注意是组)能唯一标识一条记录，该属性组就可以成为一个主键比如 ：

> **学生表(学号，姓名，性别，班级)**
>
> 其中每个学生的学号是唯一的，学号就是一个主键。
>
> **用户表(用户名、密码、登录级别)**
>
> 其中用户名是唯一的, 用户名就是一个主键。
>
> 总之主键是能确定一条记录的唯一标识。

#### 外键

外键用于与另一张表的关联。是能确定另一张表记录的字段，用于保持数据的一致性。比如，A表中的一个字段，是B表的主键，那他就可以是A表的外键。

#### 基本的增删改查

- 增加：insert into table1(field1,field2) values(value1,value2)
- 删除：delete from table1 where 范围
- 更新：update table1 set field1=value1 where 范围
- 查询：select field1,field2 from table1 where 范围



### JDBC

#### 准备

导入相应jar包

#### 使用步骤

第一步：加载驱动类通过,java.lang.Class的静态方法forName(String className)实现

```java
Class.forName("com.mysql.jdbc.Driver");//这行语句需要捕获，也就是加上try catch
```

第二步：创建数据库的连接

1. 要连接数据库，需要向java.sql.DriverManager请求并获得Connection对象， 该对象就代表一个数据库的连接。使用DriverManager的getConnectin(String url , String username ,  String password )方法传入指定的欲连接的数据库的路径、数据库的用户名和密码来获得。 

```java
String url = "jdbc:mysql://localhost:3306/数据库名称" ;    
String username = "用户名" ;   
String password = "密码" ;   
try{   
    Connection conn = DriverManager.getConnection(url , username , password ) ;   
}catch(SQLException se){   
    System.out.println("数据库连接失败！");   
    se.printStackTrace() ;   
}   
```

第三步：创建语句

个人不推荐使用Statement,容易发生SQL注入的问题，推荐使用PreparedStatement，可以预编译数据库语句。

```java
String sql = "select field1, field2, field3 from table1"
PreparedStatement pre = conn.prepareStatement(sql);
ResultSet rs = pre.executeQuery();
while(rs.next()){
	System.out.println(rs.getInt("field1"));
  	//这里认为field1是int类型所以用getInt方法，其他类型也有相应的方法，使用的时候注意不要出错即可。
}
```

第四步：关闭JDBC对象

操作完成以后要把所有使用的JDBC对象全都关闭，以释放JDBC资源，关闭顺序和声明顺序相反

```java
try {
	if (rs!=null)
    	rs.close();
    } catch (SQLException e) {
        e.printStackTrace();
    } finally {
        try {
        	if (pre != null) {
				pre.close();
            }
        } catch (SQLException e) {
             e.printStackTrace();
        } finally {
             try {
             	if (conn!=null){
                	conn.close();
                }
              } catch (SQLException e) {
                e.printStackTrace();
              }
        }
}
```



### FTP

- 介绍
  - FTP 是File Transfer Protocol（文件传输协议）的英文简称，而中文简称为“文传协议”。用于Internet上的控制文件的双向传输。同时，它也是一个应用程序。基于不同的操作系统有不同的FTP应用程序，而所有这些应用程序都遵守同一种协议以传输文件。在FTP的使用当中，用户经常遇到两个概念："下载"和"上传"。"下载"文件就是从远程主机拷贝文件至自己的计算机上；"上传"文件就是将文件从自己的计算机中拷贝至远程主机上。用Internet语言来说，用户可通过客户机程序向（从）远程主机上传（下载）文件。
- ftp地址
  - [ftp://www.maijinta.top](ftp://www.maijinta.top)
  - 账号：www
  - 密码：23q9JI8BeNUY

![internet中的FTP和Http区别](http://www.maijinta.cn/user/files/internet.png)

- ftp和http的区别
  - Http，FTP是应用层协议，HTTP用来传输超文本而FTP用来传文件

### Linux

#### 简介

Linux是一种比Windows更加稳定，免费，性能高的操作系统。它被广泛用在服务器领域和移动端，比如安卓系统和嵌入式系统开发，所以我们学习网站开发，必须了解，并掌握Linux。

#### 特点

- 在linux中，一切设备，一切软硬件都被看作是文件。
- linux区分大小写
- \#(表示超级用户) 
- $(表示普通用户)
- 命令的参数可以一起使用，如`mkdir -vp`

#### 常用命令

##### 查看当前目录的绝对路径：`pwd`

##### 清屏：`clear`

##### 路径补全：`tab` 键

##### 测试网络是否连通：`ping`

```shell
ping www.baidu.com #向百度发送数据包，回收数据包
```

##### 远程访问服务器：`ssh`

```shell
 ssh root@172.11.1.67 #用root用户来登录远程服务器,然后会提示你输入密码
 logout #退出
```

##### 查看时间：`date`

```shell
#返回
2016年11月 3日 星期四 14时27分28秒 CST
```

##### 查看日期：`cal`

##### 查看有哪些用户登录了系统：`who`

##### 查看当前是哪个用户登录了系统：`whoami`

##### 查看历史命令：`history`

##### 查看命令帮助：`whatis`,`info`,`which`,`man`,`--help`

```shell
#使用方法
whatis command
info command
which command
man command
command -h
command -help
command --help
#在只记得部分命令关键字的场合，我们可通过man -k来搜索；
#需要知道某个命令的简要说明，可以使用whatis；而更详细的介绍，则可用info命令；
#查看命令在哪个位置，我们需要使用which；
#而对于命令的具体参数及使用方法，我们需要用到强大的man；
#会在终端列出所有可用的命令,可以使用任何命令的-h或-help选项来查看该命令的具体用法。
```

##### 查文件或目录的大小：`du`

```shell
du -h 文件名
#查看文件夹大小 du -h T01
#查看文件大小 du -h tt.txt
```

##### 查看文件与目录的命令：`ls`

```shell
ls -l #列出长数据串，包含文件的属性与权限数据等，可以简写成:ll
ls -a #列出全部的文件，连同隐藏文件（开头为.的文件）一起列出来（常用）  
ls -d #仅列出目录本身，而不是列出目录的文件数据  
ls -h #将文件容量以较易读的方式（GB，kB等）列出来  
ls -R #连同子目录的内容一起列出（递归列出），等于该目录下的所有文件都会显示出来
```

##### 切换目录：`cd`

```shell
cd				   # 切换到初始目录下
cd /               # 切换到根目录下
cd (directory)     # 切换到某个子目录下
cd /root/Docements # 切换到目录/root/Docements  
cd -               # 切换到上一次的目录
cd ..              # 切换到上层目录
cd ../path         # 切换到上层目录中的path目录中，“..”表示上一层目录
```

##### 覆盖文件内容：`echo`

```shell
#使用>指令覆盖文件原内容并重新输入内容，若文件不存在则创建文件。
echo "Raspberry" > test.txt
#使用>>指令向文件追加内容，原内容将保存。
echo "Intel Galileo" >> test.txt
```

##### 创建文件：`touch`

```shell
touch 文件名
#例如：
touch test.txt
```

##### 创建文件夹：`mkdir`

```shell
mkdir 文件夹 #创建文件夹
mkdir -p 目录 #此时若路径中的某些目录尚不存在,系统将自动建立好那些尚不存在的目录,即递归创建多个目录
mkdir -v 文件夹 #每次创建新目录都显示信息
```

##### 删除空目录：`rmdir`

```shell
#例如
rmdir d101 #删除空目录d101  
rmdir d102 d103 #同时删除两个空目录d102,d103  
rmdir -p d104/d105/ #删除d105目录后，若d104是空的，则连d104一起删除  
```

##### 搜寻指定的字符串：`grep`

```shell
grep "<string>" <file-name>
grep -i "<string>" <file-name>    #在搜寻时会忽略字符串的大小写。
grep -r "<string>" <file-name>    #则会在当前工作目录的文件中递归搜寻指定的字符串。
```

##### 查找某目录下文件：`find`

```shell
# 与时间有关的参数：  
find -mtime n : n为数字，意思为在n天之前的“一天内”被更改过的文件；  
find -mtime +n : 列出在n天之前（不含n天本身）被更改过的文件名；  
find -mtime -n : 列出在n天之内（含n天本身）被更改过的文件名；  
find -newer file : 列出比file还要新的文件名  
# 例如：  
find /root -mtime 0 # 在root目录下查找今天之内有改动的文件  

# 与用户或用户组名有关的参数：  
find -user name : 列出文件所有者为name的文件  
find -group name : 列出文件所属用户组为name的文件  
find -uid n : 列出文件所有者为用户ID为n的文件  
find -gid n : 列出文件所属用户组为用户组ID为n的文件  
# 例如：  
find /home/ljianhui -user ljianhui # 在目录/home/ljianhui中找出所有者为ljianhui的文件

# 与文件权限及名称有关的参数：
find -name filename ：找出文件名为filename的文件
find -size [+-]SIZE ：找出比SIZE还要大（+）或小（-）的文件  
find -tpye TYPE ：查找文件的类型为TYPE的文件，TYPE的值主要有：一般文件（f)、设备文件（b、c）、  
         目录（d）、连接文件（l）、socket（s）、FIFO管道文件（p）；  
find -perm mode ：查找文件权限刚好等于mode的文件，mode用数字表示，如 0755；  
find -perm -mode ：查找文件权限必须要全部包括mode权限的文件，mode用数字表示  
find -perm +mode ：查找文件权限包含任一mode的权限的文件，mode用数字表示  
# 例如：  
find / -name passwd # 查找文件名为passwd的文件  
find . -perm 0755 # 查找当前目录中文件权限的0755的文件  
find . -size +12k # 查找当前目录中大于12KB的文件，注意c表示byte
```

##### 复制文件：`cp`

```shell
cp -a #将文件的特性一起复制，相当于 -pdr 的意思
cp -p #连同文件的属性一起复制，而非使用默认方式，与-a相似，常用于备份  
cp -i #若目标文件已经存在时，在覆盖时会先询问操作的进行  
cp -d #若来源文件为连结文件的属性(link file)，则复制连结文件属性而非档案本身； 
cp -r #递归持续复制，用于目录的复制行为  
cp -u #目标文件与源文件有差异时才会复制
# 例如：
cp 源文件路径/源文件名 目标路径
cp T01/test.txt T02/  
cp -a file1 file2 #连同文件的所有特性把文件file1复制成文件file2  
cp file1 file2 file3 dir #把文件file1、file2、file3复制到目录dir中
```

##### 远程复制文件(夹)：`scp`

```shell
#必须在本地使用中这条命令，不能在服务器上用
scp [-r](递归复制) root@IP地址或域名:服务器文件(夹) 本地路径
scp -r root@172.11.1.112:/root/install.log /root/
```

##### 移动文件,目录或重命名：`mv`

```shell
-f #force强制的意思，如果目标文件已经存在，不会询问而直接覆盖  
-i #若目标文件已经存在，就会询问是否覆盖  
-u #若目标文件已经存在，且比目标文件新，才会更新
# 例如：
mv file1 file2 file3 dir # 把文件file1、file2、file3移动到目录dir中  
mv file1 file2 # 把文件file1重命名为file2
```

> 注：该命令可以把一个文件或多个文件一次移动一个文件夹中，但是最后一个目标文件一定要是“目录”。

##### 删除文件或目录：`rm`

```shell
rm -f #就是force的意思，忽略不存在的文件，不会出现警告消息  
rm -i #互动模式，在删除前会询问用户是否操作  
rm -r #递归删除，最常用于目录删除，它是一个非常危险的参数
# 例如：
rm -i file #删除文件file，在删除之前会询问是否进行该操作  
rm -fr dir #强制删除目录dir中的所有文件
```

##### 获取进程运行情况：`ps`

```shell
ps -A #所有的进程均显示出来  
ps -a #不与terminal有关的所有进程  
ps -u #有效用户的相关进程  
ps -x #一般与a参数一起使用，可列出较完整的信息  
ps -l #较长，较详细地将PID的信息列出
ps -ef #查看系统正在运行的进程
# 实例
ps aux  # 列出目前所有的正在内存当中的程序
ps ax   # 查看不与terminal有关的所有进程  
ps -lA  # 查看系统所有的进程数据  
ps axjf # 查看连同一部分进程树状态
```

##### 显示CPU占用量较大的进程：`top`

```shell
top    #top命令会默认按照CPU的占用情况，显示占用量较大的进程
top -u <username>    #查看某个用户的CPU使用排名情况。
```

##### 判断文件的基本数据：`file`

```shell
file filename
#例如：
file ger.txt
输出 ger.txt:ASCII text
```

> 因为在Linux下文件的类型并不是以后缀为分的，所以这个命令对我们来说就很有用了

##### 对文件进行打包：`tar`

```shell
tar -c ：新建打包文件  
tar -t ：查看打包文件的内容含有哪些文件名  
tar -x ：解打包或解压缩的功能，可以搭配-C（大写）指定解压的目录，注意-c,-t,-x不能同时出现在同一条命令中  
tar -j ：通过bzip2的支持进行压缩/解压缩  
tar -z ：通过gzip的支持进行压缩/解压缩  
tar -v ：在压缩/解压缩过程中，将正在处理的文件名显示出来  
tar -f filename ：filename为要处理的文件  
tar -C dir ：指定压缩/解压缩的目录dir
# 主要记住
压缩：tar -jcv -f filename.tar.bz2 要被处理的文件或目录名称  
查询：tar -jtv -f filename.tar.bz2  
解压：tar -jxv -f filename.tar.bz2 -C 欲解压缩的目录
# 打包并压缩
tar 参数 目标文件路径和包名 被打包的文件名称
tar -czvf t101.tar.gz T101 #将目录和文件打到当前目录下的t101.tar.gz压缩包中
tar -czvf /opt/t101.tar.gz T101 #将目录和文件打到/opt/t101.tgz压缩包中
tar -tzvf ./t101.tar.gz #查看t101.tar.gz压缩包中的内容
```

> 注：
>
> - 默认情况并不会压缩，如果指定了相应的参数，它还会调用相应的压缩程序（如gzip和bzip等）进行压缩和解压
> - 文件名并不定要以后缀tar.bz2结尾，这里主要是为了说明使用的压缩程序为bzip2

##### 查看文件的内容：`more`,`less`,`cat`,`head`,`tail`

```shell
more 文件名        #按回车一行，空格一页。不能向上下翻行。  
less 文件名        #按回车一行，空格一页。可以通过上下键上下翻行。按q就退出。  
cat 文件名         #查看文件的所有内容  
cat -n 文件名      #查看文件的所有内容，并显示行数   
head -n 文件名     #查看文件的前n行，n表示你要看的行数。  
tail -n 文件名     #查看文件的后n行
```

> 1. cat命令可以一次显示整个文件，如果文件比较大，使用不是很方便；
> 2. more命令可以让屏幕在显示满一屏幕时暂停，此时可按空格健继续显示下一个画面，或按Q键停止显示。
> 3. less命令也可以分页显示文件，和more命令的区别就在于它支持上下键卷动屏幕，当结束浏览时，只要在less命令的提示符“: ”下按Q键即可。

##### 改变文件所属用户组：`chgrp`

```shell
chgrp 组名 文件名
chgrp g1015 echo.sh
chgrp -R 组名 文件名
-R #进行递归的持续对所有文件和子目录更改  
# 例如：  
chgrp -R users ./dir # 递归地把dir目录下中的所有文件和子目录下所有文件的用户组修改为users
```

##### 改变文件的所有者：`chown`

```shell
#更改单个文件的属主：
#chown 用户名 文件名
chown wsg echo.sh

#更改文件夹的属主：
#语法：chown -R 用户名 文件名
chown -R u101 Desktop/ #单独更改文件夹的拥有者(-R表示文件夹的所有子内容全部更改,*表示所有本目录文件)

#同时更改文件的拥有者和所属组
#语法：chown 用户名:组名 文件名
chown u101:g1015 install.log.syslog #同时更改文件的拥有者和所属组

#同时更改文件夹和文件夹下的所有内容的拥有者和所属组
#语法：chown -R 用户名:组名 文件名
chown -R u101:g1015 test01 #同时更改文件的拥有者和所属组
```

##### 改变文件的权限：`chmod`

```shell
chmod 权限 文件名
如：chmod 755 filename
ls -l命令
获取：drwxr-xr-x  2 root root 4.0K 11-06 18:30 Desktop
解释：
r: read       可读
w: write      可写
x：execute    可执行
d表示是个普通文件夹
-表示普通文件
r用数字4表示，w用数字2表示，x用数字1表示。
第一个rwx，表示该文件所属的用户对其所拥有的操作权限
第二个rwx，表示与该文件所属用户在同组内的用户对其所拥有的操作权限
第三个rwx，表示不与该文件所属用户在同组内的用户对其所拥有的操作权限
第一个root:表示该文件夹属于哪个用户
第二个root:表示该文件夹属于哪个组

chmod -R xyz 文件或目录  
-R #进行递归的持续更改，即连同子目录下的所有文件都会更改
# 例如：  
chmod -R 755 file # 把file的文件权限改变为-rxwr-xr-x
# 同时，chmod还可以使用u（user）、g（group）、o（other）、a（all）和+（加入）、-（删除）、=（设置）跟rwx搭配来对文件的权限进行更改。
chmod g+w file # 向file的文件权限中加入用户组可写权限
```

##### 文本编辑：`vim`,`vi`

```shell
#Vim是从 vi 发展出来的一个文本编辑器
vim
#在命令行中输入vim,进入vim编辑器
vim filename
#用vim打开一个文件
i
#按一下i键,下端显示 --INSERT--
#插入命令,在vim中可能任意字符都有作用
Esc按键
#退出i(插入)命令进行其它命令使用
:w
#在编辑的过程中保存文件,相当于word中的ctrl+s
:w 文件名
#另存为
:wq
#保存文件并退出
:q!
#强制退出,不保存
u 
#撤消上一步操作
dd
#删除行
```

#### 更多命令

[29个你必须知道的Linux命令](http://www.jianshu.com/p/462c9e20ffb5)



### Git

#### 简介

Git是目前世界上最先进的分布式版本控制系统，以其优秀的控制能力独傲全球

#### 集中式版本控制系统-SVN,CVS

版本库是集中放在中央服务器的，而干活的时候，用的都是自己的电脑，所以首先要从中央服务器哪里得到最新的版本，然后干活，干完后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快，如果在互联网下，如果网速慢的话，就纳闷了。

#### 分布式版本控制系统-Git

分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

#### Git学习笔记

[window下配置SSH连接GitHub、GitHub配置ssh key](http://jingyan.baidu.com/article/a65957f4e91ccf24e77f9b11.html)

[Gi基本操作](http://www.jianshu.com/p/1d5e97222cad)

[工作区、暂存区和版本库的关系](http://www.jianshu.com/p/4416c3c61dba)

[撤销或回退版本](http://www.jianshu.com/p/f0d6a5a4325f)

[连接远程仓库](http://www.jianshu.com/p/8468d43074f3)

[协同工作](http://www.jianshu.com/p/e7ddad179c9d)

[搭建git服务器](http://www.jianshu.com/p/ee8c379ef888)

#### Git命令

![git](http://www.maijinta.cn/user/files/git.png)

- workspace: 本地的工作目录。（记作A）
- index：缓存区域，临时保存本地改动。（记作B）
- local repository: 本地仓库，只想最后一次提交HEAD。（记作C）
- remote repository：远程仓库。（记作D）

```shell
#初始化
git version #查看git版本
git init #创建
git clone /path/to/repository #检出
git config --global user.email "you@example.com" #配置email
git config --global user.name "Name" #配置用户名
ssh-keygen #创建SSH key
#原理：首先由用户生成一对密钥，然后将公钥保存在SSH服务器用户的目录下.ssh子目录中的authorized_key文件里(/root/.ssh/authorized_key).私钥保存在本地计算机.当用户登陆时,服务器检查authorized_key文件的公钥是否与用户的私钥对应,如果相符则允许登入,否则拒绝.由于私钥只有保存在用户的本地计算机中,因此入侵者就算得到用户口令,也不能登陆到服务器.

#操作
git add <file>  #文件添加，A → B
git add .       #所有文件添加，A → B

git commit -m "代码提交信息" #文件提交，B → C
git commit --amend         #与上次commit合并, *B → C

git push origin master     #推送至master分支, C → D
git pull                   #更新本地仓库至最新改动， D → A
git fetch                  #抓取远程仓库更新， D → C

git log     #查看提交记录
git status  #查看修改状态
git diff    #查看详细修改内容
git show    #显示某次提交的内容

#撤销操作
git reset <file>   #某个文件索引会回滚到最后一次提交， C → B
git reset          #索引会回滚到最后一次提交， C → B
git reset --hard   #索引会回滚到最后一次提交， C → B → A

#仅仅只是撤销已提交的版本库，不会修改暂存区和工作区
git reset --soft 版本库ID
#仅仅只是撤销已提交的版本库和暂存区，不会修改工作区
git reset --mixed 版本库ID
#彻底将工作区、暂存区和版本库记录恢复到指定的版本库
git reset --hard 版本库ID

git checkout                #从index复制到workspace， B → A
git checkout -- files       #文件从index复制到workspace， B → A
git checkout HEAD -- files  #文件从local repository复制到workspace， C → A

#分支相关
git checkout -b branch_name     #创建名叫“branch_name”的分支，并切换过去
git checkout master             #切换回主分支
git branch -d branch_name       #删除名叫“branch_name”的分支
git push origin branch_name     #推送分支到远端仓库
git merge branch_name           #合并分支branch_name到当前分支(如master)
git rebase                      #衍合，线性化的自动， D → A

#冲突处理
git diff #对比workspace与index
git diff HEAD #对于workspace与最后一次commit
git diff <source_branch> <target_branch> #对比差异
git add <filename> #修改完冲突，需要add以标记合并成功

#删除
git rm filename #移除文件(从暂存区和工作区中删除)
git rm --cached filename #移除文件(只从暂存区中删除)

#查看远端库
git remote

#其他
gitk #开启图形化git
git config color.ui true #彩色的 git 输出
git config format.pretty oneline #显示历史记录时，每个提交的信息只显示一行
git add -i #交互式添加文件到暂存区
```

#### Git忽略文件

在git中如果想忽略掉某个文件，不让这个文件提交到版本库中，可以使用修改根目录中 .gitignore 文件的方法（如无，则需自己手工建立此文件）

```shell
Git 中的文件忽略
1. 共享式忽略新建 .gitignore 文件，放在工程目录任意位置即可。.gitignore 文件可以忽略自己。忽略的文件，只针对未跟踪文件有效，对已加入版本库的文件无效。
2. 独享式忽略针对具体版本库 ：.git/info/exclude针对本地全局：git config --global core.excludefile ~/.gitignore
忽略的语法规则：
(#)表示注释
(*)  表示任意多个字符; 
(?) 代表一个字符;
 ([abc]) 代表可选字符范围
如果名称最前面是路径分隔符 (/) ，表示忽略的该文件在此目录下。
如果名称的最后面是 (/) ，表示忽略整个目录，但同名文件不忽略。
通过在名称前面加 (!) ，代表不忽略。
例子如下：
# 这行是注释
*.a                   # 忽略所有 .a 伟扩展名的文件
!lib.a                # 但是 lib.a 不忽略，即时之前设置了忽略所有的 .a
/TODO                 # 只忽略此目录下 TODO 文件，子目录的 TODO 不忽略 
build/                # 忽略所有的 build/ 目录下文件
doc/*.txt             # 忽略如 doc/notes.txt, 但是不忽略如 doc/server/arch.txt

#经测试发现，若要忽略一个文件夹下的部分文件夹，应该一个一个的标示。可能有更好的方法。
#若test下有多个文件和文件夹。若要ignore某些文件夹，应该这个配置.gitignore文件。
#若test下有test1，test2,test3文件。要track test3，则.gitignore文件为：
test/test1
test/test2
!test/test3
#若为：
test/
!test/test3 ，则不能track test3。
```

#### Git使用规范提醒

- 使用Git过程中，必须通过创建分支进行开发，坚决禁止在主干分支上直接开发。review的同事有责任检查其他同事是否遵循分支规范。
- 在Git中，默认是不会提交空目录的，如果想提交某个空目录到版本库中，需要在该目录下新建一个 .gitignore 的空白文件，就可以提交了
- 把外部文件纳入到自己的 Git 分支来的时候一定要记得是先比对，确认所有修改都是自己修改的，然后再纳入。不然，容易出现代码回溯
- 多人协作时，不要各自在自己的 Git 分支开发，然后发文件合并。正确的方法应该是开一个远程分支，然后一起在远程分支里协作。不然，容易出现代码回溯（即别人的代码被覆盖的情况）
- 每个人提交代码是一定要 git diff 看提交的东西是不是都是自己修改的。如果有不是自己修改的内容，很可能就是代码回溯
- review 代码的时候如果看到有被删除掉的代码，一定要确实是否是写代码的同事自己删除的。如果不是，很可能就是代码回溯

#### Git使用规范

Git 使用规范流程 - [http://www.ruanyifeng.com/blog/2015/08/git-use-process.html](http://www.ruanyifeng.com/blog/2015/08/git-use-process.html)
团队中的 Git 实践 - [https://ourai.ws/posts/working-with-git-in-team/](https://ourai.ws/posts/working-with-git-in-team/)
构家网 git 团队协作使用规范 v2 - [http://wenku.baidu.com/view/e1430d1b7f1922791788e81e](http://wenku.baidu.com/view/e1430d1b7f1922791788e81e)

#### 扩展阅读

Git Book - [https://git-scm.com/book/zh/](https://git-scm.com/book/zh/)
git简明指南 - [http://rogerdudler.github.io/git-guide/index.zh.html](http://rogerdudler.github.io/git-guide/index.zh.html)
常用 Git 命令清单 - [http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
猴子都能懂的GIT入门 - [http://backlogtool.com/git-guide/cn/](http://backlogtool.com/git-guide/cn/)
缪雪峰Git教程 - [http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)