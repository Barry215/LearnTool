## WEB后台知识



### Web服务器

**Web服务器作用**

专门处理客户端的HTTP请求，返回响应内容，使浏览器可以浏览网站的内容



#### Apache服务器

Apache是一个用C语言编写的web服务器环境程序，启用它可以作为web服务器使用，不过只支持静态网页（HTML）



#### Tomcat服务器

Tomcat是用Java语言编写的运行在Apache上的应用服务器，支持动态页面（ASP, PHP, JSP)

它是一个servlet容器，可以认为是apache的扩展，但是可以独立于apache运行。  

![](http://www.maijinta.cn/user/files/tomcat.png)



### Servlet

#### 简介

很久之前，我们的网页都是静态的，就是我们所看到的页面在编写好之后总是唯一的。后来有人便提出动态页面的概念，相应的就提出了Servlet。可以根据客户端的请求来判断返回什么页面。



#### 作用

负责处理客户请求，当客户请求来到时，Servlet容器获取请求，然后调用某个Servlet，并把Servlet的执行结果返回给客户。



#### Servlet 生命周期

- Servlet 通过调用 **init ()** 方法进行初始化
- Servlet 调用 **service()** 方法来处理客户端的请求
- Servlet 通过调用 **destroy()** 方法终止（结束）
- 最后，Servlet 是由 JVM 的垃圾回收器进行垃圾回收的




##### init() 方法

init 方法被设计成只调用一次。它在第一次创建 Servlet 时被调用，在后续每次用户请求时不再调用。因此，它是用于一次性初始化。

当用户调用一个 Servlet 时，就会创建一个 Servlet 实例，每一个用户请求都会产生一个新的线程，适当的时候移交给 doGet 或 doPost 方法。init() 方法简单地创建或加载一些数据，这些数据将被用于 Servlet 的整个生命周期。

init 方法的定义如下：

```java
public void init() throws ServletException {
  // 初始化代码...
}
```



##### service() 方法

service() 方法是执行实际任务的主要方法。Servlet 容器（即 Web 服务器）调用 service() 方法来处理来自客户端（浏览器）的请求，并把格式化的响应写回给客户端。

每次服务器接收到一个 Servlet 请求时，服务器会产生一个新的线程并调用服务。service() 方法检查 HTTP 请求类型（GET、POST、PUT、DELETE 等），并在适当的时候调用 doGet、doPost、doPut，doDelete 等方法。

下面是该方法的特征：

```java
public void service(ServletRequest request, ServletResponse response) 
	throws ServletException, IOException{
}
```

service() 方法由容器调用，service 方法在适当的时候调用 doGet、doPost、doPut、doDelete 等方法。所以，您不用对 service() 方法做任何动作，您只需要根据来自客户端的请求类型来重载 doGet() 或 doPost() 即可。

doGet() 和 doPost() 方法是每次服务请求中最常用的方法。下面是这两种方法的特征。



##### doGet() 方法

GET 请求来自于一个 URL 的正常请求，或者来自于一个未指定 METHOD 的 HTML 表单，它由 doGet() 方法处理。

```java
public void doGet(HttpServletRequest request,HttpServletResponse response)
    throws ServletException, IOException {
    // Servlet 代码
}
```



##### doPost() 方法

POST 请求来自于一个特别指定了 METHOD 为 POST 的 HTML 表单，它由 doPost() 方法处理。

```java
public void doPost(HttpServletRequest request,HttpServletResponse response)
    throws ServletException, IOException {
    // Servlet 代码
}
```



##### destroy() 方法

destroy() 方法只会被调用一次，在 Servlet 生命周期结束时被调用。destroy() 方法可以让您的 Servlet 关闭数据库连接、停止后台线程、把 Cookie 列表或点击计数器写入到磁盘，并执行其他类似的清理活动。

在调用 destroy() 方法之后，servlet 对象被标记为垃圾回收。destroy 方法定义如下所示：

```java
  public void destroy() {
    // 终止化代码...
  }
```



##### 具体流程

1. web client发送一个request请求。
2. Servlet容器接收我们这个请求，把web client的请求的信息封装成一个HttpServletRequest对象，以及HttpServletResponse对象。
3. Servlet容器把我们的HttpServletRequest对象，以及HttpServletResponse对象封装成一个参数传递给我们的httpservlet的service()方法。
4. 在service()里面我们通过读取我们的httpServletRequst里面的信息进行一些操作，然后写入一些信息进入我们的HttpServletResponse对象中。
5. 我们的servlet容器把我们的HttpServletResponse返回给我们的webclint。




##### 配置

**XML配置**

```xml
<servlet> 
	<servlet-name>Test</servlet-name> 
	<servlet-class>package.TestServlet</servlet-class> 
</servlet> 

<servlet-mapping> 
	<servlet-name>Test</servlet-name> 
	<url-pattern>/UrlTest</url-pattern> 
</servlet-mapping>
```



**注解配置**

Servlet 3.0提供了注解(annotation)，使得不再需要在web.xml文件中进行Servlet的部署描述

```java
@WebServlet(name="Servlet3Demo",urlPatterns="/Servlet3Demo")
```

> 注解WebServlet用来描述一个Servlet
>
> name描述Servlet的名字(可选) 
>
> urlPatterns定义访问的URL



### Jsp

#### 简介

JSP动态网页技术，是可以把Java语言嵌入到HTML页面上。

那时候Servlet是个大忙人，它既要处理显示效果，又要处理数据，又要处理页面跳转，耦合度高，不方便代码维护，为了解决这个问题，SUN公司联合其他公司制定了JSP动态网页技术标准。事实上jsp是一个特殊的Servlet实例，它跟其他Servlet一样被Servlet容器执行，在这之前它需要先被jsp容器转换成Servlet，这个过程是在服务器端产生的，在第一次编译之后该Servlet实例便常驻内存。



#### jsp的运行机制

1. jsp容器判断URL中对应的Servlet实例是否存在Servlet队列，实则执行第五步，否则执行第二步。
2. jsp容器将jsp文件转换成Servlet源程序(.java)。
3. jsp容器将Servlet源程序编译成字节码文件(.class)。
4. Servlet容器加载字节码，创建该Servlet实例(该实例实际是返回给客户端的显示效果),此时会调用`jspInit()`进行初始化。
5. jsp容器将响应返回到到客户端。




#### 注释

注释有以下两种：

- HTML注释：`<!-- 注释内容 -->`，这种方法注释在查看HTML源代码时可以被显示
- jsp注释：`<%-- 注释内容 --%>`，通过这种方法注释用户是看不到的




#### 编译指令

>  通知jsp引擎的消息

作用：设置jsp程序的属性以及由该jsp生成的serverlet里的属性



常用的编译指令有:

- page:该指令是针对当前页面的指令
- include :用于指定如何包含另一个页面
- taglib:用于定义和访问自定义标签




#### page 指令

page指令主要用于定义当前jsp的全局指令，包括当前jsp所使用的脚本语言类型，需要导入Java包的列表等等,一般情况下page编译指令位于页面的最上方，一个页面可以有多个编译配置指令。



##### JSP 的page模版

最常用的是`import`，`contentType`，`pageEncoding`

```xml
<%@ page contentType="text/html;charset=UTF-8" pageEncoding="UTF-8" %>
```



##### 指令解释

- language：

  声明当前JSP页面使用的脚本语言的种类。目前该属性的值只能为java，默认值也为java，所以通常无须设置。


- import：

  用来导入包。默认导入的包有：java.lang.*, javax.servlet.*, javax.servlet.http.*, javax,.servlet.jsp.*.

  导入多个包时用一个import指令，各个包之间用“,”隔开。


- contentType：

  告知客户端，服务器对此次请求响应的正文格式(MIME类型)和编码字符集。默认为contentType="text/html;charset=UTF-8ISO-8859-1"。如设置为：contentType="text/html;charset=UTF-8"，就是告诉客户端，服务器响应的正文文件格式为text/html，这样客户端就会用默认的浏览器方式打开文件，而不用别的应用程序。charset=UTF-8告知客户端浏览器，服务器返回的文件编码格式为UTF-8，浏览器将按照UTF-8格式进行解码并且以UTF-8字符集进行页面显示。contentType的作用本质上相当于模拟了一个Http协议的消息头。contentType虽然写在JSP文件中，但是因为JSP文件其实并不能直接响应客户端请求，它必须编译成对应的Servlet以后才能响应请求。所以本质上这个contentType是针对Servlet的设置，即Servlet告诉客户端，我返回的文件(以流的形式,response.getWriter())的MIME类型为text/html,文件的编码字符集为UTF-8。


- pageEncoding：

  设定JSP源文件保存时所使用的编码。因为JSP文件要想响应客户端的请求，它就必须先被编译成一个Servlet，而Servlet是一个Java类，Java类在内存中是以Unicode进行编码的，如果JSP引擎(将JSP翻译成对应的Servlet)不知道JSP的编码格式，就无法进行解码，然后将其转换成内存中的Unicode编码。注意区分contentType的charset和pageEncoding，charset是响应时Servlet(JSP已经编译成了Servlet)告诉客户端浏览器”我“是以这种字符编码的，”你“也要以这种字符解码并显示，整个过程涉及服务器和客户端两方面，而pageEncoding是服务器端JSP文件告诉JSP引擎要以何种编码进行解码，即此时JSP还没被编译成Servlet，它是被编译成Servlet的前提准备工作，整个过程都发生在服务器端，与客户端无关。


- session：

  设定这个JSP页面是否支持session机制，默认为true，所以一般不需要设置，保持默认值即可。


- errorPage：

  指定错误处理页面的地址。如果本页面产生了异常或者错误，而该JSP页面没有对应的处理代码，此时就会自动调用该属性所指向的JSP页面。


- isErrorPage：

  和errorPage属性配合使用。设置本JSP页面是否为错误处理页面。


- buffer：

  指定输出缓冲区的大小。JSP的隐含对象out(JSP有九大隐含对象或者说内置对象)用于缓存JSP(其实是Servlet)对客户端浏览器的输出，默认值为8KB，可以设置为none，也可以设置为其他的值，单位为KB。


- autoFlush：

  当输出缓冲区即将溢出时，是否需要强制输出缓冲区的内容。设置为true时可以正常输出，设置为false时，则会在buffer溢出时产生一个异常。默认为true。


- isELIgnored：

  如果设定为真，那么JSP中的EL表达式被当成字符串处理。

  比如下面这个表达式${2000/20}在isELIgnored＝"true"时输出为${2000/20}，而isELIgnored＝"false"时输出为100.0。默认为false。




#### include 指令

include是jsp的静态包含指令，使用此指令可将一个外部文件包含到jsp程序中。外部文件可以是html文件也可以是jsp文件。



##### 注意

1. 假如是jsp文件，在导入进来之前会先解析jsp文件中的语句。
2. 在include指令中包含页面和被包含页面同一类型的参数不能被定义两次。



##### 语法

`<%@ include file = "path"%>`

该指令只有一个属性file，该指令用于指向要加载的文件的相对地址



#### taglib 指令

taglib指令是用来引用标签库并设置标签库前缀，说白了就是自定义自己的jsp标记。



##### 格式

`<%@ taglib uri="标签库地址" prefix = "标签库前缀" %>`



##### 举例

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
```



##### 使用标记方式

`<标签库前缀:标签名 参数>`



#### jsp 脚本元素

jsp脚本元素有以下三种：

1. jsp声明语句
2. jsp表达式
3. jsp Scriptlets



##### jsp声明语句

jsp声明语句用于声明变量和方法，在jsp声明语句中声明的变量和方法对作为servlet的成员变量，在整个页面都有效。格式如下：
`<%! 声明变量或方法 %>`



##### jsp表达式

jsp表达式要求该表达式存在一个确定的值，该值会被显示在HTML页面上。格式如下：
`<%= 表达式 %>`



##### jsp Scriptlets

jsp Scriptlets是一段java代码段。当需要对页面输出内容进行一些复杂的操作的时候就需要用到jsp Scriptlets，在jsp Scriptlets声明的变量在调用的时候分配内存，调用结束内存释放。jsp Scriptlets格式如下：
`<% java代码片段 %>`



#### jsp 动作标签

##### 介绍

**编译指令**是通知servlet引擎处理消息，只在jsp被转化成servlet的时候起作用。
**动作指令**是在jsp被客户端请求时动态执行的。也就是说：每次客户端请求时都有可能被执行一次。

动作元素只有一种语法，它符合XML标准：

```jsp
<jsp:action_name attribute="value" />
```



jsp动作标签有以下几种(不全)：

- `<jsp:include>`
- `<jsp:forward>`
- `<jsp:param>`
- `<jsp:plugin>`
- `<jsp:useBean>`
- `<jsp:setProperty>`
- `<jsp:getProperty>`




##### `<jsp:include>`

包含标签，但它和包含指令不一样。

**区别**

**包含指令**是将包含页面整合进jsp页面中再编译。

**包含标签**包含的文件和原来的jsp文件是两个独立的文件，在运行时单独对包含文件进行编译，把结果发送到客户端。只有在运行jsp页面的时候才会加载这些包含文件。

**格式**
`<jsp:include page="被包含的页面" flush="true|false"></jsp:include>` 

1. page:是被包含的文件的相对地址。 
2. flush:指定当缓冲区满时，是否将其清空。默认值为false。




##### `<jsp:forward>`

转发标签，当代码运行到该标签会在服务器内重新链接到指定的地址，之后的代码不被执行。

**格式**

`<jsp:forward page="转发的地址"></jsp:forward>`



##### `<jsp:param>`

传递参数的标签。它是以"名-值"对的形式来表示参数的。

**格式**
`<jsp:param name="参数名" value="参数值">`

**举例**

向`<jsp:include>`包含的文件传递参数

```jsp
<jsp:include page="page name" flush="false"> 
  <jsp:param name="parameter name" value="parameter value"></jsp:param>
  ...
</jsp:include>
```


向`<jsp:forward>`页面传递参数

```jsp
<jsp:forward page="forward target"> 
  <jsp:param name="parameter name" value="parameter value"></jsp:param> 
  ...
</jsp:forward>
```

**获取**

index.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<jsp:forward page="login.jsp">
    <jsp:param name="userName" value="icarus"/>
    <jsp:param name="password" value="123456"/>
</jsp:forward>
```

login.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Login</title>
</head>
<body>
<%--登陆页面--%>
<%
    String userName=request.getParameter("userName");
    String password=request.getParameter("password");
    out.println(userName);
    out.print("<br/>");
    out.println(password);
%>
</body>
</html>
```



##### `<jsp:plugin>`

可以将服务器端的javaBean或Applet下载到本地客户端执行。语法格式如下：

```jsp
<jsp:plugin type="bean|applet" code="classFileName" codeBase="classFileURL">
...
</jsp:plugin>
```

- type：指定插件类型。是Bean还是Applet。
- code：指定执行的类名。必须以扩展名".class"结尾。
- codeBase：指定被执行的java类所在目录。此外``
  相关的参数还有很多，这里只是举例必不可少的三个。




##### `<jsp:useBean>`

用来装载一个将在jsp页面中使用的javaBean。



**JavaBean**是特殊的Java类，使用Java语言书写，并且遵守JavaBean API规范。

接下来给出的是JavaBean与其它Java类相比而言独一无二的特征：

- 提供一个默认的无参构造函数。
- 需要被序列化并且实现了Serializable接口。
  - Serializable接口是启用其序列化功能的接口。
  - 序列化的目的是将数据分解成字节流，以便存储在文件中或在网络上传输
- 可能有一系列可读写属性。
- 可能有一系列的"getter"或"setter"方法。



语法格式如下：

```jsp
<jsp:useBean id="beanInstanceName"class="package.class"scope="page|request|session|application"></jsp:useBean>
```

- id：指定javaBean的实例名。
- class：指定javaBean的全限类名。
- scope：指定javaBean的作用域。 
  - page：指定javaBean实例只在本页面有限。 
  - request：指定JavaBean实例仅在本次请求有效。 
  - session：指定javaBean实例在本次会话有效。 
  - application：指定javaBean实例在本应用内一直有效。




##### `<jsp:setProperty>`

用于设置Bean内属性的值，它通过调用Bean的setter方法设置属性值。

**语法**

```jsp
<jsp:setProperty name="beanInstanceName" property="propertyName" value="propertyValue"></jsp:setProperty>
```



##### `<jsp:getProperty>`

用于获取bean的属性值。语法格式如下：

```jsp
<jsp:getProperty name="beanInstanceName" property="propertyName"></jsp:getProperty>
```



**注意**

> bean中可以没有属性的声明，但必须有setter和getter方法，因为`<jsp:setProperty>`和`<jsp:getProperty>`是通过调用bean实例中的setter方法和getter方法实现取值和赋值工作的。



**举例**

javaBean，User类

```java
public class User implements Serializable{
	private String userName;
    private String password;
    public User(){}
  
    public User(String userName,String password){
        this.userName=userName;
        this.password=password;
    }

    public String getUserName() {
        return userName;
    }

    public String getPassword() {
        return password;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

register.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>register</title>
</head>
<body>


<form action="do_register.jsp" method="post">
    用户名：<input type="text" name="userName"/>
    密码：<input type="password" name="password"/>
    <input type="submit" value="提交"/>
</form>

</body>
</html>
```

do_register.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
<title>do_register</title>
</head>
<body>

<jsp:useBean id="user" class="com.frank.User"/> 
  
<jsp:setProperty name="user" property="userName"/>
<jsp:setProperty name="user" property="password"/>


<p>用户名: 
   <jsp:getProperty name="user" property="userName"/>
</p>
<p>密码: 
   <jsp:getProperty name="user" property="password"/>
</p>

</body>
</html>

```



####  jsp 的四个作用域 

- page
- request
- session
- application



##### 区别

1. page指当前页面有效。在一个jsp页面里有效
2. request 指在一次请求的全过程中有效，即从http请求到服务器处理结束，返回响应的整个过程，存放在HttpServletRequest对象中。在这个过程中可以使用forward方式跳转多个jsp。在这些页面里你都可以使用这个变量。
3. Session是用户全局变量，在整个会话期间都有效。只要页面不关闭就一直有效（或者直到用户一直未活动导致会话过期，默认session过期时间为30分钟，或调用HttpSession的invalidate()方法）。存放在HttpSession对象中 
4. application是程序全局变量，对每个用户每个页面都有效。存放在ServletContext对象中。它的存活时间是最长的，如果不进行手工删除，它们就一直可以使用 

##### 总结

当数据只需要在下一个forward有用时，用request就够了。
若数据不只是在下一个forward有用时，就用session。
若数据包含上下文，环境信息之类的，用application。



#### HTTP协议的无状态性

因为HTTP协议是无状态的，也就是说当用户发送一次请求给服务器之后，服务器响应客户端的请求，当同一个客户端再次发送请求给服务器时，服务器并不知道这个请求是同一个客户端发送的。而要保存用户的状态，涉及到两种技术，`Session`和`Cookie`，其中`Session`是保存在服务器端的，会随着会话的结束而销毁，而`Cookie`保存在客户端，可以保存较长一段时间，但是就因为`Cookie`保存在客户端，因此有不安全的风险。



#### jsp 九大内置对象

jsp内置对象由jsp规范进行初始化，主要有以下几种：

- request
- response
- pageContext
- session
- application
- out
- config
- page
- exception




##### request对象

用于封装请求数据。一般用户在表单填写的数据会被封装成request对象，通过post方法传递给目标页面。request还相应提供了一些方法用于访问这些数据。主要方法有以下几个： 

- `void setAttribute(attributeName, attributeValue)`：用于设置属性值。 
- `Object getAttribute(attributeName, attributeValue)`：用于获取属性值。 
- `String getParameter("parameterName")`：获取参数值。 
- `Enumeration getParameterNames()`：获取所有的参数名的集合。 
- `String[] getParameterValues("parameterName")`：获取parameterName的所有属性值的数组。 
- `Map getParameterMap()`：获取所有属性名和属性值的Map对象。 
- `void setCharacterEncoding()`：设置编码格式。
- `getCookies`：获取所有Cookie对象
- `getSession`：获取和请求相关的会话
- `getRemoteAddr`：获取客户端的IP地址
- `getProtocol`：获取客户端向服务器端传送数据的协议名称
- `getMethod`：获取客户端向服务器端传送数据的方法
- `getInputStream`：返回请求输入流,获取请求中的数据



**注意**

getParameter和getAttribute区别

1. 当两个Web组件之间为链接关系时，被链接的组件通过getParameter()方法来获得请求参数，
2. 当两个Web组件之间为转发关系时，转发目标组件通过getAttribute()方法来和转发源组件共享request范围内的数据。

**总结**

- 一般通过表单和链接传递的参数使用getParameter
- 通过request.setAttribute("name","jerry")的方式赋值的使用request.getAttribute("name")

**参考**

[JSP中getParameter和getAttribute区别](http://blog.csdn.net/gavinloo/article/details/6552319)



##### response对象

用于封装响应数据，其作用域是本页面。主要方法如下： 

- `void addCookie(Cookie cookie)`：添加一个Cookie对象，用于在客户端保存特定信息。 
- `void addHeader(name, value`)：添加一个HTTP头信息，该头信息会被发送到客户端。 
- `setHeader`：设置指定名字的Http文件头信息
- `void containsHeader(name)`：判断是否含有名为"name"的头信息。 
- `void sendError(int)`：向客户端发送错误的状态码。 
- `void sendRedirect(url)`：向客户端发送重定向的url链接，让客户端跳转到该链接。 
- `void setContentType(contentType)`：设置MIME类型和编码方式。
- `getOutputStream`：返回到客户端的输出流对象




##### session对象

会话对象，用来记录每个客户端的访问状态。主要方法如下： 

- `Object getAttribute(name)`：获取session范围内名为name的属性值。 
- `void setAttribute(name, value)`：设置session范围内的属性。 
- `void removeAttribute(name)`：删除session范围内名为name的属性。 
- `Enumeration getAttributeNames()`：获取session中保存的所有属性名。 
- `long getCreationTime()`：返回session被创建的时间。 
- `String getId()`：返回session被创建时jsp容器分配的唯一标识。 
- `long getLastAccessedTime()`：返回最后一次通过session发送请求的时间。 
- `int getMaxInactiveInterval()`：返回session的失效时间，即两次请求间隔多长时间该session被取消，单位为秒。 
- `boolean isNew()`：判断是否是新的session。 
- `void invalidate()`：清空session内容。




##### application对象

用于获取和设置servlet相关信息，application的生命周期是从服务器启动直到服务器关闭。主要方法如下： 

- `void setAttribute(name, value)`：以"键-值"对的形式将一个对象的值存入application对象中。 
- `Object getAttribute(name)`：获取application中保存的属性的值。
- `getAttributeNames`：获取应用对象中所有属性的名字
- `getInitParameter`：返回应用对象中指定名字的初始参数值
- `getServletInfo`：返回Servlet编译器中当前版本信息




##### out对象

一个缓冲的输出流，用来向客户端返回信息。由于向客户端输出信息总是要连接，所以向客户端输出总是采用缓冲的形式。主要方法有以下几个： 

- `public void clear()`：清除缓冲区的内容，但不将缓冲区的内容输出到客户端。 
- `public void clearBuffer()`：清除缓冲区的内容，且将缓冲区的内容输出到客户端。 
- `public void close()`：关闭输出流并输出缓冲区的数据。
- `public void flush()`：输出缓冲区的数据。 
- `public int getBufferSize()`：获取缓冲区大小。 
- `public int getRemaining()`：获取剩余缓冲区大小。 
- `public boolean isAutoFlush()`：缓冲区是否进行自动清除。 
- `public void newLine()`：输出一个换行符。 
- `public void print(String)`：打印信息。 
- `public void println(String)`：打印信息并换行。
- `public void write(String)`：输出字符信息。




**注意**

out.print 和 out.write区别

jsp中的out对象是JspWriter类型的，JspWriter继承了java.io.Writer。
write方法是在在父类Writer中定义的，print方法是在子类JspWriter中定义的。
重载的print方法可以将各种类型的数据转换成字符串的形式输出。
而重载的write方法只能输出字符／字符数组／字符串等与字符相关的数据。
而且如果使用这两种方法输出值为null的字符串对象，那么print方法输出的结果是＂null＂，而write方法则会抛出NullPoiterException异常．



##### config对象

是ServletConfig类的一个实例，在servlet初始化时可以通过config对象想servlet传递信息。主要方法如下： 

- `String getServletName()`：获得servlet名称。 
- `ServletContext getServletContext()`：获得一个包含服务器相关信息的ServletContext对象。 
- `String getInitParameter(name)`：获得servlet初始化参数。 
- `Enumeration getInitParameterNames()`：获得servlet初始化时所有参数的名字的枚举对象。




##### page对象

是指当前的jsp页面本身，他是java.lang.Object类的对象，通过page对象可以很方便地调用servlet中定义的方法。常用方法如下： 

- `class getClass()`：返回当前的类名。 
- `int getHashCode()`：返回当前类的哈希码。 
- `String toString()`：将此对象转换成字符串。 
- `boolean equals(object)`：比较两个对象是否是相等。 
- `void copy(object)`：将该对象复制到指定的object对象中。




##### exception对象

java.lang.Throwable类的对象，用来处理页面错误和异常。常用方法如下： 

- `String getMessage()`：返回异常对象的异常信息。 
- `String getLocalizedMessage()`：返回本地化语言的异常信息。 
- `void printStackTrace()`：打印异常的栈反向追踪痕迹。 
- `String toString()`：返回异常的简单描述。

**注意**

使用异常对象时，应将page的isErrorPage属性设置为"true"，此时jsp是一个处理异常的页面



##### pageContext对象

pageContetx对象是jsp页面中所有对象功能的最大集成着。

使用他可以访问所有的jsp内置对象。常用方法如下： 

- `forward`：重定向到另一页面或Servlet组件
- `getAttribute`：获取某范围中指定名字的属性值
- `findAttribute`：按范围搜索指定名字的属性
- `removeAttribute`：删除某范围中指定名字的属性
- `setAttribute`：设定某范围中指定名字的属性值
- `getException`：返回当前异常对象
- `getRequest`：返回当前请求对象
- `getResponse`：返回当前响应对象
- `getServletConfig`：返回当前页面的ServletConfig对象
- `getServletContext`：返回所有页面共享的ServletContext对象
- `getSession`：返回当前页面的会话对象




#### Forward和Redirect

##### Forward

**实现语句**
 `request.getRequestDispatcher(path).forward(request, response)`

 **转发时传递对象**

当前Servlet对象中可以通过以下方法存储对象
`request.setAttribute(String, Object)`
转发目的地Servlet可以通过以下方法获取对象
`request.getAttribute(String)` 

> 要注意的是，获取的对象类型为`object`要进行类型转换。 



**也可以用jsp动作来实现转发**
`<jsp:forward page="apage.jsp" />`



##### Redirect

**实现语句**
`response.sendRedirect(path)`



**在jsp页面中实现重定向**
<%response.sendRedirect("new.jsp");//重定向到new.jsp%>



##### 转发和重定向的区别

- 转发时URL不改变；重定向时URL改变。
- 转发只发出一次请求；重定向发出两次请求。
- 转发在服务器端完成，故又称为服务器端跳转；重定向在客户端完成，故又称客户端跳转。



**转发和重定向示意图**

![](http://www.maijinta.cn/user/files/Forward_Redirect.png)





### Cookie

#### 作用

主要功能是用户登录，在用户登录时提示用户是否记住登录信息，当用户选择记住登录信息时，会将用户的登录信息保存在Cookie中，以后用户再进入登录页面时会自动为用户写入用户的登录信息。



#### 常用的方法

| 方法                                       | 说明                    |
| ---------------------------------------- | --------------------- |
| response.addCookie(cooke)                | 写入Cookie对象            |
| Cookie[] cookies = request.getCookies()  | 读取Cookie对象            |
| void setMaxAge(int expiry)               | 设置Cookie有效期，以秒为单位     |
| void setValue(String value)              | Cookie创建后，对Cookie进行赋值 |
| String getName()                         | 获取Cookie名称            |
| String getValue()                        | 获取Cookie的值            |
| int getMaxAge()                          | 获取Cookie的有效时间，以秒为单位   |
| Cookie cookie = new Cookie(String key, String value) | 创建一个新的Cookie对象        |



#### 举例

login.jsp

```jsp
<%@ page language="java" import="java.net.*" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>登录</title>
</head>
<body>
	<h1>请登录</h1>
	<hr/>
	<%
		request.setCharacterEncoding("UTF-8");
		
		String userName = "";
		String password = "";
		
		//获取cookie对象
		Cookie[] cookies = request.getCookies();
		if(null != cookies && cookies.length > 0) {
			for(Cookie c : cookies) {
				if("userName".equals(c.getName())) {
					//为了防止读取到的cookie值为乱码，
					//将cookie的值使用URLDecoder.decode(String str, String encoding)进行转码
					userName = URLDecoder.decode(c.getValue(), "UTF-8");
				} else if("password".equals(c.getName())) {
					password = URLDecoder.decode(c.getValue(), "UTF-8");
				}
			}
		}
	%>
	<form action="dologin.jsp" action="post">
		<table>
			<tr>
				<td>用户名：</td>
				<td><input type="text" name="userName" value="<%=userName %>" /></td>
			</tr>
			<tr>
				<td>密码：</td>
				<td><input type="password" name="password" value="<%=password %>" /></td>
			</tr>
			<tr>
				<td colspan="2"><input type="checkbox" name="isRemeber" value="remeber" checked="checked">十天内免登录</td>
			</tr>
			<tr>
				<td colspan="2"><input type="submit" value="登录"></td>
			</tr>
		</table>
	</form>
</body>
</html>
```

在这个页面中我们看到取出Cookie中保存的内容时用到了一个URLDecoder.decode(String str, String encoding)方法，这是因为根据RFC 2109中的规定，在Cookie中只能包含ASCII的编码，中文很显然不是ASCII编码的，为了防止出现乱码，需要进行一次转码，而要将中文存入Cookie的方法将在下面看到。

用户在登录页面写入相关信息并提交之后交给dologin.jsp进行处理，主要是根据用户的选择判断是否将用户的登录信息存入Cookie中，如果需要，则将登录信息写入Cookie。

dologin.jsp

```jsp
<%@ page language="java" import="java.net.*" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>登录成功</title>
</head>
<body>
	<h1>登录成功</h1>
	<hr/>
	<%
		request.setCharacterEncoding("UTF-8");
		
		String userName = "";
		String password = "";
		String[] isRemeber = request.getParameterValues("isRemeber");
		
		if(null != isRemeber && isRemeber.length > 0) {
			//获取userName和password的值，为了防止给cookie赋值时出现乱码异常，
			//使用URLEncoder.encode(String str, String encoding)转码
			userName = URLEncoder.encode(request.getParameter("userName"), "UTF-8");
			password = URLEncoder.encode(request.getParameter("password"), "UTF-8");
			
			//定义cookie
			Cookie userNameCookie = new Cookie("userName", userName);
			Cookie passwordCookie = new Cookie("password", password);
			
			//设置cookie的有效时间
			userNameCookie.setMaxAge(60 * 60 * 24 * 10);
			passwordCookie.setMaxAge(60 * 60 * 24 * 10);
			
			//写入cookie对象
			response.addCookie(userNameCookie);
			response.addCookie(passwordCookie);
		} else {
			Cookie[] cookies = request.getCookies();
			if(null != cookies && cookies.length > 0) {
				for(Cookie c : cookies) {
					if("userName".equals(c.getName()) || "password".equals(c.getName())) {
						c.setMaxAge(0);
                      //写入cookie对象
						response.addCookie(c);
					}
				}
			}
		}
	%>
</body>
</html>
```



### 过滤器

#### 介绍

过滤器是一个服务器端的组件，它可以截取客户端的请求和服务端的响应信息，并对这些信息进行过滤。



#### 过滤器的工作原理

![](http://www.maijinta.cn/user/files/filter.png)



#### 过滤器的生命周期

过滤器的生命周期分为四个阶段：实例化、初始化、过滤和销毁：

实例化是指在Web工程的web.xml文件里声明一个过滤器，在声明了过滤器之后，Web容器会创建一个过滤器的实例；

初始化是指在创建了过滤器实例之后，服务器会执行过滤器中的init()方法，这是过滤器的初始化方法；

初始化之后过滤器就可以对请求和响应进行过滤了，过滤主要调用的是过滤器的doFilter()方法；

最后当服务器停止时，会将过滤器销毁，销毁过滤器前主要调用过滤器的destory()方法，释放资源。



#### 过滤器的常用方法

过滤器最常用的方法有三个：init()、doFilter()和destory()

1）init()方法：这是过滤器的初始化方法，在Web容器创建了过滤器实例之后将调用这个方法进行一些初始化的操作，这个方法可以读取web.xml中为过滤器定义的一些初始化参数。

2）doFilter()方法：这是过滤器的核心方法，表示将请求传给下一个过滤器或目标资源，当过滤器收到响应之后再执行FilterChain.doFilter()之后的内容。

3）destory()方法：这是Web容器在销毁过滤器实例前调用的方法，主要用来释放过滤器的资源等。



#### 举例

```java
public class EncodingFilter implements Filter {

    //保存当前应用的字符集名称
    private String charEncoding=null;
  
    public void init(FilterConfig config) throws ServletException {
        //获取配置好的编码格式
        charEncoding=config.getInitParameter("encoding");
        //未设置编码信息则抛出异常
        if (charEncoding==null){
            throw new ServletException("EncodingFilter中的编码信息设置为空！！！");
        }
    }

    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
        //如果当前默认的编码值与请求中的编码值不一致，
        //则将请求中的编码设置为默认的编码
        if (!charEncoding.equals(req.getCharacterEncoding())){
            req.setCharacterEncoding(charEncoding);
        }
        //将响应信息的编码格式也设置为默认格式
        resp.setCharacterEncoding(charEncoding);
        chain.doFilter(req,resp);
    }

    public void destroy() {
    }

}
```

#### XML配置

> 如果有多个过滤器，那么过滤器执行的顺序按照XML里的先后顺序

```xml
	<filter>
        <filter-name>EncodingFilter</filter-name>
        <filter-class>com.icarus.filter.EncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>EncodingFilter</filter-name>
        <!--设置需要过滤的url-->
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```



#### 过滤器链

当用户发送请求请求Web资源时，过滤器1会首先获取用户的请求，对请求进行过滤，然后执行FilterChain.doFilter()将请求发送给过滤器2，过滤器2在过滤了用户请求之后执行FilterChain.doFilter()方法请求实际的Web资源，Web资源的响应将首先被过滤器2获取，在过滤器2对响应进行过滤之后将响应传递给过滤器1，在过滤器1过滤之后才将响应发送给用户。

![](http://www.maijinta.cn/user/files/doFilter.png)



### 监听器

#### 介绍

监听器是Servlet规范中定义的一种特殊类，用于监听ServletContext、HttpSession和ServletRequest等域对象的创建和销毁事件，它还可以监听域对象的属性发生修改的事件，可以在事件发生前或者发生后做一些必要的处理。

#### 用法

在Servlet中要创建监听器类首先需要新建一个类并继承相应的监听器接口，实现接口中定义的方法，然后在web.xml文件中注册相应的监听器即可。如果一个web.xml文件中注册了多个监听器，则监听器的启动顺序按照在web.xml中的注册顺序启动。如果一个web.xml文件中同时定义了监听器、过滤器和Servlet，那么web容器会先加载监听器、再加载过滤器最后加载Servlet。



#### 监听器的分类

按照监听的事件可以将监听器划分为以下三类：

- 监听域对象**自身的创建和销毁的事件**监听器；
- 监听域对象中**属性的增加和删除的事件**监听器；
- 监听**绑定到HttpSession域中某个对象状态的事件**监听器。
  - HttpSession中对象的状态有两种：绑定与解除绑定、钝化与活化。
  - 绑定与解除绑定是指在HttpSession中将某个对象设置为属性值或者移除某个属性的值。
  - 钝化是指服务器会将不常使用的Session对象暂时序列化到系统文件或数据库中，而活化就是将暂存在系统文件或数据库中的Session对象反序列化到服务器中。



按照监听对象可以分成以下三类：

| 监听对象           | 监听接口                            | 监听事件                         |
| -------------- | ------------------------------- | ---------------------------- |
| ServletRequest | ServletRequestListener          | ServletRequestEvent          |
|                | ServletRequestAttributeListener | ServletRequestAttributeEvent |



| 监听对象        | 监听接口                          | 监听事件                    |
| ----------- | ----------------------------- | ----------------------- |
| HttpSession | HttpSessionListener           | HttpSessionEvent        |
|             | HttpSessionActivationListener | HttpSessionEvent        |
|             | HttpSessionAttributeListener  | HttpSessionBindingEvent |
|             | HttpSessionBindingListener    | HttpSessionBindingEvent |



| 监听对象           | 监听接口                            | 监听事件                         |
| -------------- | ------------------------------- | ---------------------------- |
| ServletContext | ServletContextListener          | ServletContextEvent          |
|                | ServletContextAttributeListener | ServletContextAttributeEvent |



#### 举例

```java
public class SessionListener implements ServletContextListener,
        HttpSessionListener, HttpSessionAttributeListener {

    private ServletContext application;


    // Public constructor is required by servlet spec
    public SessionListener() {
    }

    // -------------------------------------------------------
    // ServletContextListener implementation
    // -------------------------------------------------------
    public void contextInitialized(ServletContextEvent sce) {
      /* This method is called when the servlet context is
         initialized(when the Web application is deployed). 
         You can initialize servlet context related data here.
      */
      application = sce.getServletContext();
    }

    public void contextDestroyed(ServletContextEvent sce) {
      /* This method is invoked when the Servlet Context 
         (the Web application) is undeployed or 
         Application Server shuts down.
      */
    }

    // -------------------------------------------------------
    // HttpSessionListener implementation
    // -------------------------------------------------------
    public void sessionCreated(HttpSessionEvent se) {
      /* Session is created. */

    }

    public void sessionDestroyed(HttpSessionEvent se) {
      /* Session is destroyed. */
    }

    // -------------------------------------------------------
    // HttpSessionAttributeListener implementation
    // -------------------------------------------------------

    public void attributeAdded(HttpSessionBindingEvent sbe) {
      /* This method is called when an attribute 
         is added to a session.
      */
        List<String> userList = new ArrayList<>();
        application.setAttribute("userList",userList);
        userList.add(String.valueOf(sbe.getValue()));
        System.out.println("第一次加入username");

    }

    public void attributeRemoved(HttpSessionBindingEvent sbe) {
      /* This method is called when an attribute
         is removed from a session.
      */
    }

    public void attributeReplaced(HttpSessionBindingEvent sbe) {
      /* This method is invoked when an attibute
         is replaced in a session.
      */
        List<String> userList = (List<String>) application.getAttribute("userList");
        String newValue= String.valueOf(sbe.getSession().getAttribute(sbe.getName()));
        userList.add(newValue);
        System.out.println("再次加入username");
    }
}
```



#### XML配置

```xml
<listener>
	<listener-class>
		com.frank.listener.SessionListener
	</listener-class>
</listener>
```



### EL表达式

#### 语法

`${expr}`



#### 举例

**获取某个域内的元素**

`${sessionScope.user.sex}`

上述EL范例的意思是：从Session的范围中，取得用户的性别。

假若依照之前JSP Scriptlet的写法如下：

User user =(User)session.getAttribute("user");

String sex =user.getSex( );

两者相比较之下，可以发现EL 的语法比传统JSP Scriptlet 更为方便、简洁。



**数学表达式**

- ${(1 + 2) * 3}等于9
- ${1 + (2 * 3)} 等于7



**是否忽略EL表达式**

```jsp
<%@ page isELIgnored ="true|false" %>
```

设为true，EL表达式就会被忽略，若设为false，则容器将会计算EL表达式。



#### 基础操作符

| 操作符        | 描述                 |
| ---------- | ------------------ |
| .          | 访问一个Bean属性或者一个映射条目 |
| [ ]        | 访问一个数组或者链表的元素      |
| ( )        | 组织一个子表达式以改变优先级     |
| +          | 加                  |
| -          | 减或负                |
| *          | 乘                  |
| / or div   | 除                  |
| % or mod   | 取模                 |
| == or eq   | 测试是否相等             |
| != or ne   | 测试是否不等             |
| < or lt    | 测试是否小于             |
| > or gt    | 测试是否大于             |
| <= or le   | 测试是否小于等于           |
| >= or ge   | 测试是否大于等于           |
| && or and  | 测试逻辑与              |
| \|\| or or | 测试逻辑或              |
| ! or not   | 测试取反               |
| empty      | 测试是否空值             |



##### .与 [ ] 运算符

EL 提供 . 和 [ ] 两种运算符来导航数据。

下列两者所代表的意思是一样的：

${sessionScope.user.sex}等于${sessionScope.user["sex"]}



**. **和 [ ] 也可以一起同时使用，如下：

${sessionScope.shoppingCart[0].price}

回传结果为shoppingCart中第一项物品的价格。



不过，以下两种情况，两者会有差异：

1. 当要存取的属性名称中包含一些特殊字符，如. 或 – 等并非字母或数字的符号，就一定要使用 [ ]

例如：${user.My-Name }

上述是不正确的方式，应当改为：${user["My-Name"] }

2. 我们来考虑下列情况：

${sessionScope.user[data]}

此时，data 是一个变量，假若data的值为"sex"时，那上述的例子等于${sessionScope.user.sex}；

假若data 的值为"name"时，它就等于${sessionScope.user.name}。

因此，如果要动态取值时，就可以用上述的方法来做，但**. **无法做到动态取值。



#### EL 变量

EL 存取变量数据的方法很简单，例如：${username}。它的意思是取出某一范围中名称为username的变量。

因为我们并没有指定哪一个范围的username，所以它的默认值会先从Page 范围找，假如找不到，

再依序到Request、Session、Application范围。假如途中找到username，就直接回传，不再继续找下去，

但是假如全部的范围都没有找到时，就回传null，当然EL表达式还会做出优化，页面上显示空白，而不是打印输出NULL。

| 属性范围（jstl名称） | EL中的名称           |
| ------------ | ---------------- |
| Page         | PageScope        |
| Request      | RequestScope     |
| Session      | SessionScope     |
| Application  | ApplicationScope |



#### EL隐含对象

| 隐含对象             | 描述                 |
| ---------------- | ------------------ |
| pageScope        | page 作用域           |
| requestScope     | request 作用域        |
| sessionScope     | session 作用域        |
| applicationScope | application 作用域    |
| param            | Request 对象的参数，字符串  |
| paramValues      | Request对象的参数，字符串集合 |
| header           | HTTP 信息头，字符串       |
| headerValues     | HTTP 信息头，字符串集合     |
| initParam        | 上下文初始化参数           |
| cookie           | Cookie值            |
| pageContext      | 当前页面的pageContext   |



##### pageContext对象

pageContext对象是JSP中pageContext对象的引用。通过pageContext对象，您可以访问request对象。比如，访问request对象传入的查询字符串，就像这样：${pageContext.request.queryString}



##### Scope对象

pageScope，requestScope，sessionScope，applicationScope变量用来访问存储在各个作用域层次的变量。

举例来说，如果您需要显式访问在applicationScope层的box变量，可以这样来访问：${applicationScope.box}。



##### param和paramValues对象

param对象返回单一的字符串，而paramValues对象则返回一个字符串数组

param和paramValues对象用来访问参数值，通过使用request.getParameter方法和request.getParameterValues方法。

举例来说，访问一个名为order的参数，可以这样使用表达式：${param.order}，或者${param["order"]}。



##### header和headerValues对象

header对象返回单一值，而headerValues则返回一个字符串数组

header和headerValues对象用来访问信息头，通过使用 request.getHeader方法和request.getHeaders方法。

举例来说：

要访问一个名为user-agent的信息头，可以这样使用表达式：${header.user-agent}，或者${header["user-agent"]}



### JSTL标签

(全名：java standard tag libarary - java标准标签库)

JSP标准标签库（JSTL）是一个JSP标签集合，它封装了JSP应用的通用核心功能。



根据JSTL标签所提供的功能，可以将其分为5个类别。

- 核心标签
- 格式化标签
- SQL 标签
- XML 标签
- JSTL 函数



#### 核心标签

核心标签是最常用的JSTL标签。引用核心标签库的语法如下：

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
```

| 标签                                       | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| `<c:set></c:set>`                        | 用于保存数据                                   |
| ` <c:out value=*""*></c:out>`            | 用于在JSP中显示数据，就像<%= ... >                  |
| `<c:if test=*""*></c:if>`                | 单条件判断                                    |
| `<c:choose></c:choose>`                  | 本身只当做`<c:when>`和`<c:otherwise>`的父标签      |
| ` <c:when test=*""*></c:when>`           | ` <c:choose>`的子标签，用来判断条件是否成立             |
| `<c:otherwise></c:otherwise>`            | `<c:choose>`的子标签，接在`<c:when>`标签后，当`<c:when>`标签判断为false时被执行 |
| `<c:forEach></c:forEach>`                | 基础迭代标签，接受多种集合类型                          |
| ` <c:forTokens items=*""* delims=*""*></c:forTokens>` | 根据指定的分隔符来分隔内容并迭代输出                       |
| `<c:redirect></c:redirect>`              | 重定向至一个新的URL                              |



##### `<c:if>` 标签

```jsp
<c:if test="${not empty item.publish_time}">
内容
</c:if>
<c:if test="${item['domain']!=null}">
内容
</c:if>
<c:if test="${!empty permissionMap}"> 
内容
</c:if>
```



##### `<c:forEach/>`标签

```jsp
标签的语法定义如下所示
<c:forEach var="每个变量名字"   items="要迭代的list"   varStatus="每个对象的状态"
begin="循环从哪儿开始"    end="循环到哪儿结束"    step="循环的步长">
循环要输出的东西
</c:forEach>

举例
<c:forEach items="${domainList }" var="item">
<tr>
	<td align="center" valign="middle">${item["domain"]==null?"&nbsp;":item["domain"]}</td>
	<td align="center" valign="middle">
  		<fmt:formatDate value="${item['bind_date']}" pattern="yyyy-MM-dd HH:mm:ss"/>
	</td>
	<td align="center" valign="middle">
    	<c:if test="${item['domain']!=null}">
    		<a href="javascript:;" id="${item['domain']}" class="del">&nbsp;</a>
    	</c:if>
   </td>
</tr>  
</c:forEach>
```



##### `<c:choose>` `<c:when>` `<c:otherwise>`  标签

```jsp
<c:set var="score">85</c:set>
<c:choose>
  <c:when test="${score>=90}">
    你的成绩为优秀！
  </c:when>
  <c:when test="${score>=70&&score<90}">
    您的成绩为良好!
  </c:when>
  <c:when test="${score>60&&score<70}">
    您的成绩为及格
  </c:when>
  <c:otherwise>
    对不起，您没有通过考试！
  </c:otherwise>
</c:choose>
```



#### 格式化标签

JSTL格式化标签用来格式化并输出文本、日期、时间、数字。引用格式化标签库的语法如下：

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
```

| 标签                      | 描述                   |
| ----------------------- | -------------------- |
| `<fmt:formatNumber>`    | 使用指定的格式或精度格式化数字      |
| `<fmt:parseNumber>`     | 解析一个代表着数字，货币或百分比的字符串 |
| `<fmt:formatDate>`      | 使用指定的风格或模式格式化日期和时间   |
| `<fmt:parseDate>`       | 解析一个代表着日期或时间的字符串     |
| `<fmt:bundle>`          | 绑定资源                 |
| `<fmt:setLocale>`       | 指定地区                 |
| `<fmt:setBundle>`       | 绑定资源                 |
| `<fmt:timeZone>`        | 指定时区                 |
| `<fmt:setTimeZone>`     | 指定时区                 |
| `<fmt:message>`         | 显示资源配置文件信息           |
| `<fmt:requestEncoding>` | 设置request的字符编码       |



#### SQL标签

JSTL SQL标签库提供了与关系型数据库（Oracle，MySQL，SQL Server等等）进行交互的标签。引用SQL标签库的语法如下：

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%>
```

| 标签                    | 描述                                     |
| --------------------- | -------------------------------------- |
| `<sql:setDataSource>` | 指定数据源                                  |
| `<sql:query>`         | 运行SQL查询语句                              |
| `<sql:update>`        | 运行SQL更新语句                              |
| `<sql:param>`         | 将SQL语句中的参数设为指定值                        |
| `<sql:dateParam>`     | 将SQL语句中的日期参数设为指定的java.util.Date 对象值    |
| `<sql:transaction>`   | 在共享数据库连接中提供嵌套的数据库行为元素，将所有语句以一个事务的形式来运行 |



#### XML 标签

JSTL XML标签库提供了创建和操作XML文档的标签。引用XML标签库的语法如下：

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/xml" prefix="x"%>
```

| 标签        | 描述                          |
| --------- | --------------------------- |
| `<x:out>` | 与<%= ... >,类似，不过只用于XPath表达式 |



#### JSTL函数

JSTL包含一系列标准函数，大部分是通用的字符串处理函数。引用JSTL函数库的语法如下：

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn"%>
```

| 函数              | 描述                |
| --------------- | ----------------- |
| `fn:contains()` | 测试输入的字符串是否包含指定的子串 |