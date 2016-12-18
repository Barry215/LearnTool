# web开发的历史与未来



## 网页的历史

### first

- 1990下半年，第一个浏览器(World Wide Web,同时也是WYSIWYG编辑器)、第一个web server, 第一版http协议（0.9,only one method）， by Tim Berners-Lee
- 第一个html格式：在第一个浏览器与第一个服务器之间，通过第一个http协议传输的文档的格式；事实 上的html是跟随着浏览器实现的演化而不断演化的
- html标准：mid-1993,fisrt html draft 诞生；1994 html2.0正式发布；用于协调各浏览器厂商的实现



### 浏览器、服务器、html及相关标准的演化

- `[`](undefined) 链接
- ``
- form and form based file upload
- frameset and iframe
- table and table based layout
- css
- javascript
- cookie
- 浏览器大战、web标准化、modern web standard design



### HTML5

- 空前统一的标准化，微软的屈服
- 从文档到应用
- 从page到api



### link

- 浏览器的历史 [https://en.wikipedia.org/wiki/History_of_the_web_browser](https://en.wikipedia.org/wiki/History_of_the_web_browser)
- first web browser [https://en.wikipedia.org/wiki/WorldWideWeb](https://en.wikipedia.org/wiki/WorldWideWeb)
- first web server [https://en.wikipedia.org/wiki/Web_server](https://en.wikipedia.org/wiki/Web_server)
- first http protocol [https://www.w3.org/Protocols/HTTP/AsImplemented.html](https://www.w3.org/Protocols/HTTP/AsImplemented.html)
- http [https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#History](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#History)
- html [https://en.wikipedia.org/wiki/HTML#History](https://en.wikipedia.org/wiki/HTML#History)
- 浏览器演变史 [http://blog.csdn.net/vanessa219/article/details/4601045](http://blog.csdn.net/vanessa219/article/details/4601045)
- 形形色色的浏览器 [http://liulanmi.com/](http://liulanmi.com/)



## 服务端页面生成

### 网页文件

![HTML](http://tmy-course.oss-cn-beijing.aliyuncs.com/web-history/Static-Page.png)

编辑网页，存为文件，上传到服务器



### CGI

![CGI](http://tmy-course.oss-cn-beijing.aliyuncs.com/web-history/CGI.png)

- CGI可以视作是访问WEB服务器的接口协议，利用进程间输入输出通信，和WebServer进行通信，从而动态（基于用户的请求）的生成页面 
  想想odbc与数据库的关系
- 任何编程语言都可以实现cgi：c语言、perl 
  编程复杂，因为这些语言并非为web而生



### 网络脚本语言

![PHP](http://tmy-course.oss-cn-beijing.aliyuncs.com/web-history/PHP.png)

- php： 专门为web而生的语言（脚本类型），提供与web server进行互动的各种驱动与库
- 各大语言厂商相继提出各种P,即服务端页面编程机制或环境，如IIS+asp、Servlet+jsp，实际上即面向web开发的专门实现
- 大大简化了动态页面的生成和编程



### SSH：Struts + spring + hibernate

![SSH](http://assets.tianmaying.com/md-image/600ed36961e2dbb3952809854b780b26.png)

- Struts对请求Url进行解析，通过Command模式把请求指配到Action对象上；并提供若干Intecepter构造自己的stack;允许通过xml配置文件的方式对页面流转流程进行灵活定义
- 通过spring进行注入，解决依赖性、控制反转Ioc等问题
- hibernate 解决数据库的存储与orm等编程的简化
- jsp 解决页面生成



### MVC

![RAILS](http://tmy-course.oss-cn-beijing.aliyuncs.com/web-history/MVC.png)

- router: 解析url请求，分派到相应的controller
- controller: 处理请求，调用model，验证业务逻辑及流程，生成view
- model: 执行业务逻辑、访问数据库
- view: 提供页面模板，动态绑定controller提供的数据，生成html页面
- ruby on rails是代表性的MVC框架，大大简化了服务端的web页面的生成



## 客户端页面生成

### javascript

- 客户端数据校验，譬如必填、数字文本类型
- 页面动态效果，譬如对话框、``、slide

### ajax

![AJAX](http://tmy-course.oss-cn-beijing.aliyuncs.com/web-history/AJAX.png)

- 基于服务端状态（即公共状态）进行局部更新 
  异步编程，动态刷新基于json数据而非html，提升通信效率客户端页面生成，局部更新
- jquery 为原生的javascript提供各种简化编程的库，譬如ajax、dom操作、动画等



### 前端MVC：Backbone/Angular/ember

![FMVC](http://tmy-course.oss-cn-beijing.aliyuncs.com/web-history/Frontend-MVC.png)

- 将mvc的设计模式引入到客户端,使js向结构化编程演进
- 大量功能前移到浏览器内完成，服务端逐渐简化为api server模式，即只生成json,html是在浏览器里动态生成。



### SPA：单页应用

![SPA](http://ww2.sinaimg.cn/large/63918611gw1e7ehv63rd4j20im0cjmxv.jpg)

- 后端：单个静态页面即首页 + json-based api server
- 前端：即首页里引入的各种js代码
- 优点： 
  反应迅速，交互体验好，适合ui操作密集型的应用，如游戏、在线设计类利于前后端的分离开发
- 缺点：SEO不友好；首屏问题



### Real Time Web APP

- 服务端：推送(push not pull)
- 客户端：轮询、长连接、WEB socket
- 数据驱动+DOM绑定+双向更新

### 云编程

- 云端编程：不是自行开发，而是使用类似leancloud.cn等云服务来提供各种api
- 多后端应用：既然前端与后端的通讯仅仅基于WEB API,则后端完全可以通过组合多个云服务来实现，譬如数据放couchDB，新闻放weibo、社交用微信、认证用oauth、搜索用google、各类业务诸如CMS、OA、CRM等等均有对应的云服务

#### link

- [http://www.tianmaying.com/tutorial/web-history](http://www.tianmaying.com/tutorial/web-history)
- [http://blog.jobbole.com/45169/](http://blog.jobbole.com/45169/)
- [http://www.zhihu.com/question/28207685](http://www.zhihu.com/question/28207685)
- [http://todomvc.com/](http://todomvc.com/)



## 服务端组件生成

### Isomorphic JavaScript

- node.js: javascript的迅猛发展，v8+node.js的出现，宣布js进入服务端编程领域
- ECMAScript6等新一代js语法标准，引入各类高级语言特性
- 出现express.js等类似传统服务端mvc的框架
- Isomorphic javascript: 前端+后端全部使用javacript技术栈进行开发 
  共享业务逻辑共享页面模板共享各种代码

### universal JavaScript

- 为解决spa的首屏问题，出现动态加载js的技术 
  如lazo.js, Rendr.js
- 出现页面组件化技术 
  不同于页面模板，仅生成html，而是同时生成html+js，即可重用的前端组件代码
- 通过在服务端使用页面组件化技术（这对使用node.js的后端应用而言，不言而喻），可用来解决seo问题 
  如react.js，不但可以浏览器端生成页面组件，也可在服务端生成组件(html+js)，从而搜索引擎可读取html，浏览器可执行js，各取所需，皆大欢喜
- 传统的后端编程框架纷纷将v8引擎嵌入自身，从而也可以调用react.js来进行js组件的server render 
  另一种做法是，将自身直接编译成js，譬如ruby的opa库,又或者另起炉灶的typescript

![universal javascript](http://www.capitalone.io/assets/posts/why-is-everyone-talking-about-isomorphic-javascript/Isomorphism-diagram.png)

### 前端vs后端

- 传统后端语言有成熟的编程模型与代码库
- 新型前端开发有html5支持的各种新特性和通讯效率
- 不要问我页面是在前端生成，还是在后端生成？答案是：在前端中做好前端，在后端中生成前端

#### links

- [http://www.capitalone.io/blog/why-is-everyone-talking-about-isomorphic-javascript/](http://www.capitalone.io/blog/why-is-everyone-talking-about-isomorphic-javascript/)
- [https://medium.com/@mjackson/universal-javascript-4761051b7ae9](https://medium.com/@mjackson/universal-javascript-4761051b7ae9)
- [http://isomorphic.net/](http://isomorphic.net/)



## 前端的跨界

### WEB is open,WEB is best!

- WEB应用开发催生了最灵活和最复杂的编程语言及设计模式、积累了最丰富和最广泛的开源代码、培育了最大和最活跃的开发人群和社区
- 将WEB技术运用到一切领域去！

### WEB在后端：服务WEB化

- 桌面应用后端的WEB化、云端化
- 各类传统服务云服务化，基于WEB API
- 移动应用的后端
- 物联网的后端
- ...

### WEB在前端:界面WEB化

- reapp.io: 使用javascipt + react.js开发移动WEB app
- react native: 使用react.js 生成原生的移动端UI，实现跨平台界面开发
- electron.js： 使用js+chromium开发跨平台的桌面应用
- 机顶盒应用开发
- WEB OS
- 物联网应用开发
- ....

## 结语

> WEB已死；WEB永生！

