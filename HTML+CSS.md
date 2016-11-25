## HTML和CSS介绍

### Web大概发展史

- Web1.0
  - 主流技术 —— HTML + CSS
- Web2.0
  - 主流技术 —— Ajax (JavaScript/DOM/异步数据请求)
- Web3.0
  - 主流技术 —— HTML5 + CSS3
    - HTML5亮点：Canvas、Web存储、Geolocation、Workers多线程处理、HTML5音视频
    - CSS3亮点：2D变形、设计动画等等新特性



### 网页组成

- 网页一般由下面3部分组成
  - HTML —— 网页具体内容和结构
  - CSS —— 网页的样式（网页美化的主要模块）
  - JavaScript —— 网页的交互效果，比如对用户鼠标事件做出响应



### HTML简介

- HTML（Hypertext Markup Language）超文本标记语言，本质其实就是文本，由浏览器负责将它解析成具体的网页内容。

- HTML语法松散，目前最新版本5.0，也称HTML5

- HTML和XML相似，也是由各种标签（元素、标记、节点）组成

  - XML

  ```xml
  <ROOT>
  	<XX/>
  	<XX>###</XX>
  </ROOT>
  ```

- HTML5新增了27个标签元素，废弃16个标签元素（涵盖了结构性标签、行内语义性标签、交互性标签、级块性标签）



### CSS简介

- CSS(Cascading Style Sheets)：层叠样式表，它用来控制HTML标签的样式，在美化网页中起到非常重要的作用

- CSS的编写格式是键值对的形式

  - 格式

    - 属性名 : 属性值

    ```css
    color:blue;
    background-color:green;
    font-size:15px;
    ```




### css书写形式

- 页内css

  ```css
  <style>
            /* 标签选择器 */
            /* div文字颜色为蓝色,字体大小25,边框为红色单边框 */
            div{
                color: blue;
                font-size: 25px;
                border:2px solid red;
            }
            /* p文字颜色为橘色,字体17,边框为紫色双边框宽度为5 */
            p{
                color: orange;
                font-size: 17px;
                border:5px double blueviolet;
            }
  </style>
  ```

- 外部css

  ```css
  <link rel="stylesheet" href="css/index.css">
  ```



### JavaScript

- javaScript是一门广泛用于浏览器客户端的脚本语言
- 由Netspace公司设计，与Sun公司合作，所以起名叫javaScript（抱大腿嫌疑）,一般都叫它JS
- 常见用途
  - HTML DOM操作（节点操作）如：增、删、改节点
  - 给HTML网页增加动态功能，如：动画
  - 事件处理 —— 如：监听鼠标点击、滑动等



### JS书写形式

- 页内JS：在当前网页的script标签中书写

  ```javascript
  <script type="text/javascript">
    
  </script>
  ```

- 外部JS

  ```javascript
  <script src="index.js"></script>
  ```



### 示例

#### 外部css：css/custom.css

```css
.a_style{
    font-size: 10px;
    color: dodgerblue;
}

.a_style:hover{
    font-size: 16px;
    color: green;
}

.a_style:visited{
    font-size: 10px;
    color: red;
}

table{
    background: #000;
    border: 1px solid white;
}

td,th{
    width: 90px;
    height:20px;
    line-height: 20px;
    background: white;
}

```



#### html

```html
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <title>table_work</title>
    <link href="css/custom.css" rel="stylesheet">
</head>
<body>
    <table>
        <caption>2013年我校在浙江省的招新计划</caption>
        <tr>
            <th>招新批次</th>
            <th>科类</th>
            <th>专业名称</th>
            <th>所属学院</th>
            <th>学制</th>
            <th>预交学费</th>
            <th>招新数量</th>
            <th>备注</th>
        </tr>
        <tr>
            <td rowspan="7">第一批理科录取</td>
            <td>文科类</td>
            <td>通信工程</td>
            <td>通信工程学院</td>
            <td>4</td>
            <td>4400</td>
            <td>20</td>
            <td rowspan="7">只招已参加学校三位一体的学生</td>
        </tr>
        <tr>
            <td>文科类</td>
            <td>通信工程</td>
            <td>通信工程学院</td>
            <td>4</td>
            <td>4400</td>
            <td>20</td>
        </tr>
        </tr>
            <td>文科类</td>
            <td>通信工程</td>
            <td>通信工程学院</td>
            <td>4</td>
            <td>4400</td>
            <td>20</td>
        </tr>
        </tr>
            <td>文科类</td>
            <td>通信工程</td>
            <td>通信工程学院</td>
            <td>4</td>
            <td>4400</td>
            <td>20</td>
        </tr>
        </tr>
            <td rowspan="2">理科类</td>
            <td>通信工程</td>
            <td>通信工程学院</td>
            <td>4</td>
            <td>4400</td>
            <td>20</td>
        </tr>
        </tr>
            <td>通信工程</td>
            <td>通信工程学院</td>
            <td>4</td>
            <td>4400</td>
            <td>20</td>
        </tr>
        </tr>
            <td>文科类</td>
            <td>通信工程</td>
            <td>通信工程学院</td>
            <td>4</td>
            <td>4400</td>
            <td>20</td>
        </tr>
    </table>
</body>
</html>
```



#### 效果图

![效果图](http://www.maijinta.cn/user/files/html_show.png)