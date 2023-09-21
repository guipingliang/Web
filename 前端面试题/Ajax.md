### 1.什么是Ajax

全称是 Asynchronous Javascript And XML（异步 JavaScript 和 XML）

在网页中利用 XMLHttpRequest 对象和服务器进行数据交互的方式，就是Ajax。

Ajax能让我们轻松实现网页与服务器之间的数据交互。

### 2.*jQuery中的Ajax*

jQuery 中发起 Ajax 请求最常用的三个方法:$.get(), $.post(),    $.ajax()

### 3.**$.get()函数的语法**

```
$.get(url, [data], [callback])

```

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921165505230.png" alt="image-20230921165505230" style="zoom:80%;" />

### 4.**$.post()函数的语法**

```
$.post(url, [data], [callback])

```

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921165612539.png" alt="image-20230921165612539" style="zoom:80%;" />

### 5.**$.ajax()函数的语法**

```html
$.ajax({
   type: '', // 请求的方式，例如 GET 或 POST
   url: '',  // 请求的 URL 地址
   data: { },// 这次请求要携带的数据
   success: function(res) { } // 请求成功之后的回调函数
})

```

```html
$.ajax({
   type: 'GET', // 请求的方式
   url: 'http://www.liulongbin.top:3006/api/getbooks',  // 请求的 URL 地址
   data: { id: 1 },// 这次请求要携带的数据
   success: function(res) { // 请求成功之后的回调函数
       console.log(res)
   }
})
```

### 6.**enctype**

enctype 属性用来规定在**发送表单数据之前如何对数据进行编码**

| 值                                | 描述                                                       |
| --------------------------------- | ---------------------------------------------------------- |
| application/x-www-form-urlencoded | 在发送前编码所有字符（默认）                               |
| multipart/form-data               | 不对字符编码，在使用包含文件上传控件的表单时，必须使用该值 |
| text/plain                        | 空格转换为 “+” 加号，但不对特殊字符编码。（很少用）        |

在涉及到**文件上传**的操作时，**必须**将 enctype 的值设置为 <b><font color='red' size=3 face=""> multipart/form-data</font></b> 

如果表单的提交不涉及到文件上传操作，则直接将 enctype 的值设置为 application/x-www-form-urlencoded 即可

### 7.**serialize()**函数

可以一次性获取到表单中的所有的数据。

```
$(selector).serialize()
```

### 8.**什么是**XMLHttpRequest

XMLHttpRequest（简称 xhr）是浏览器提供的 Javascript 对象，通过它，可以**请求服务器上的数据资源**。之前所学的 jQuery 中的 Ajax 函数，就是基于 xhr 对象封装出来的

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921171004842.png" alt="image-20230921171004842" style="zoom:80%;" />

### 9.使用xhr发起get请求

步骤：

①创建 xhr 对象

②调用 xhr.open() 函数

③调用 xhr.send() 函数

④监听 xhr.onreadystatechange 事件

```html
// 1. 创建 XHR 对象
var xhr = new XMLHttpRequest()
// 2. 调用 open 函数，指定 请求方式 与 URL地址
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks')
// 3. 调用 send 函数，发起 Ajax 请求
xhr.send()
// 4. 监听 onreadystatechange 事件
xhr.onreadystatechange = function() {
    // 4.1 监听 xhr 对象的请求状态 readyState ；与服务器响应的状态 status
    if (xhr.readyState === 4 && xhr.status === 200) {
        // 4.2 打印服务器响应回来的数据
        console.log(xhr.responseText)
    }
}
```

### 10.xhr对象的readyState属性

XMLHttpRequest 对象的 readyState 属性，用来表示**当前** **Ajax** **请求所处的状态**。每个 Ajax 请求必然处于以下状态中的一个。

| 值   | 状态                                                | 描述                                                         |
| ---- | --------------------------------------------------- | ------------------------------------------------------------ |
| 0    | UNSENT                                              | XMLHttpRequest 对象已被创建，但尚未调用 open方法             |
| 1    | OPENED                                              | open() 方法已经被调用                                        |
| 2    | HEADERS_RECEIVED                                    | send() 方法已经被调用，响应头也已经被接收                    |
| 3    | LOADING                                             | 数据接收中，此时 response 属性中已经包含部分数据             |
| 4    | <b><font color='red' size=3 face="">DONE</font></b> | <b><font color='red' size=3 face="">Ajax 请求完成</font></b> ，这意味着数据传输已经彻底 <b><font color='red' size=3 face="">完成或失败</font></b> |

### 11.使用xhr发起带参数的GET请求

 <b><font color='SEAGREEN' size=3 face="">使用 xhr 对象发起带参数的 GET 请求时，只需在调用 xhr.open 期间，为 URL 地址指定参数即可</font></b> 

```
// ...省略不必要的代码
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks?id=1')
// ...省略不必要的代码
```

### 13.使用xhr发起POST请求

步骤：

①创建 xhr 对象

②调用 xhr.open() 函数

③**设置** **Content-Type** **属性**（固定写法）

④调用 xhr.send() 函数，**同时指定要发送的数据**

⑤监听 xhr.onreadystatechange 事件

```ajax
// 1. 创建 xhr 对象
var xhr = new XMLHttpRequest()

// 2. 调用 open()
xhr.open('POST', 'http://www.liulongbin.top:3006/api/addbook')

// 3. 设置 Content-Type 属性（固定写法）
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')

// 4. 调用 send()，同时将数据以查询字符串的形式，提交给服务器
xhr.send('bookname=水浒传&author=施耐庵&publisher=天津图书出版社')

// 5. 监听 onreadystatechange 事件
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(xhr.responseText)
    }
}
```

### 14.**什么是数据交换格式**

 <b><font color='red' size=3 face="">服务器端与客户端之间进行数据传输与交换的格式</font></b> 

### 15.什么是XML

英文全称是 E**X**tensible **M**arkup **L**anguage，即**可扩展标记语言**。因此，XML 和 HTML 类似，也是一种标记语言。

```xml
//XML语言
<note>
  <to>ls</to>
  <from>zs</from>
  <heading>通知</heading>
  <body>晚上开会</body>
</note>
```

### 16.XML 和HTML的区别

HTML 被设计用来描述网页上的**内容**，是网页内容的载体。

XML 被设计用来**传输和存储数据**，是数据的载体。

### 17.XML缺点

①XML 格式臃肿，和数据无关的代码多，体积大，传输效率低

②在 Javascript 中解析 XML 比较麻烦

### 18.什么是JSON

 <b><font color='red' size=3 face="">概念</font></b> ：JSON 的英文全称是 JavaScript Object Notation，即“ <b><font color='red' size=3 face="">JavaScript 对象表示法</font></b> ”。简单来讲，JSON 就是 Javascript 对象和数组的字符串表示法，它使用文本表示一个 <b><font color='red' size=3 face=""> JS 对象或数组的信息</font></b> ，因此，**JSON** **的本质是字符串**。

优点：JSON 是一种轻量级的文本数据交换格式，在作用上类似于 XML，专门用于存储和传输数据，但是 <b><font color='red' size=3 face=""> JSON 比 XML 更小、更快、更易解析。</font></b> 

### 19.JSON的两种结构

1）**对象结构**

对象结构在 JSON 中表示为 { } 括起来的内容。数据结构为 { key: value, key: value, … } 的键值对结构。其中，key 必须是使用英文的双引号包裹的字符串，value 的数据类型可以是 <b><font color='red' size=3 face="">数字、字符串、布尔值、null、数组、对象</font></b> 6种类型。

```json
{
    name: "zs",
    'age': 20,
    "gender": '男',
    "address": undefined,
    "hobby": ["吃饭", "睡觉", '打豆豆']
    say: function() {}
}
{
    "name": "zs",
    "age": 20,
    "gender": "男",
    "address": null,
    "hobby": ["吃饭", "睡觉", "打豆豆"]
}
```

2）**数组结构**：数组结构在 JSON 中表示为 [ ] 括起来的内容。数据结构为 [ "java", "javascript", 30, true … ] 。数组中数据的类型可以是 <b><font color='red' size=3 face="">数字、字符串、布尔值、null、数组、对象</font></b> 6种类型。

```json
[ "java", "python", "php" ]
[ 100, 200, 300.5 ]
[ true, false, null ]
[ { "name": "zs", "age": 20}, { "name": "ls", "age": 30} ]
[ [ "苹果", "榴莲", "椰子" ], [ 4, 50, 5 ] ]
```

### 20.json的语法注意

①属性名必须使用双引号包裹

②字符串类型的值必须使用双引号包裹

③JSON 中不允许使用单引号表示字符串

④JSON 中不能写注释

⑤JSON 的最外层必须是对象或数组格式

⑥不能使用 undefined 或函数作为 JSON 的值

 <b><font color='blue' size=3 face="">JSON 的作用</font></b> ：在计算机与网络之间存储和传输数据。

 <b><font color='blue' size=3 face="">JSON 的本质</font></b> ：用字符串来表示 Javascript 对象数据或数组数据

### 21.json和js对象的关系

JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。

```json
//这是一个对象
var obj = {a: 'Hello', b: 'World'}

//这是一个 JSON 字符串，本质是一个字符串
var json = '{"a": "Hello", "b": "World"}' 
```

### 22.json和js对象的互换

 <b><font color='blue' size=3 face="">从 JSON 字符串转换为 JS 对象，使用 JSON.parse() 方法</font></b> 

```json
var obj = JSON.parse('{"a": "Hello", "b": "World"}')
//结果是 {a: 'Hello', b: 'World'}
```

 <b><font color='blue' size=3 face="">从 JS 对象转换为 JSON 字符串，使用 JSON.stringify() 方法</font></b> 

```json
var json = JSON.stringify({a: 'Hello', b: 'World'})
//结果是 '{"a": "Hello", "b": "World"}'
```

### 23.序列化和反序列化

把数据对象转换为字符串的过程，叫做**序列化**，例如：调用  <b><font color='blue' size=3 face="">JSON.stringify() </font></b> 函数的操作，叫做 JSON 序列化。

把字符串转换为数据对象的过程，叫做**反序列化**，例如：调用 <b><font color='blue' size=3 face=""> JSON.parse() </font></b> 函数的操作，叫做 JSON 反序列化。

### 24.XMLHttpRequest Level2

新功能：

①可以设置 HTTP 请求的时限：增加了 timeout 属性

②可以使用 FormData 对象管理表单数据

③可以上传文件

④可以获得数据传输的进度信息

### 25.什么是axios

axios是专注于网络数据请求的库

### 26.axios发起GET请求

```js
axios.get('url', { params: { /*参数*/ } }).then(callback)

// 请求的 URL 地址
 var url = 'http://www.liulongbin.top:3006/api/get'
 // 请求的参数对象
 var paramsObj = { name: 'zs', age: 20 }
 // 调用 axios.get() 发起 GET 请求
 axios.get(url, { params: paramsObj }).then(function(res) {
     // res.data 是服务器返回的数据
     var result = res.data
     console.log(res)
 })
```

### 27.axios发起post请求

```js
 axios.post('url', { /*参数*/ }).then(callback)

// 请求的 URL 地址
 var url = 'http://www.liulongbin.top:3006/api/post'
 // 要提交到服务器的数据
 var dataObj = { location: '北京', address: '顺义' }
 // 调用 axios.post() 发起 POST 请求
 axios.post(url, dataObj).then(function(res) {
     // res.data 是服务器返回的数据
     var result = res.data
     console.log(result)
 })
```

### 28.直接使用axios发起请求

```js
 axios({
     method: '请求类型',
     url: '请求的URL地址',
     data: { /* POST数据 */ },
     params: { /* GET参数 */ }
 }) .then(callback)
```

### 29.直接使用axios发起get、post请求

```js
 axios({
     method: 'GET',
     url: 'http://www.liulongbin.top:3006/api/get',
     params: { // GET 参数要通过 params 属性提供
         name: 'zs',
         age: 20
     }
 }).then(function(res) {
     console.log(res.data)
 })

 axios({
     method: 'POST',
     url: 'http://www.liulongbin.top:3006/api/post',
     data: { // POST 数据要通过 data 属性提供
         bookname: '程序员的自我修养',
         price: 666
     }
 }).then(function(res) {
     console.log(res.data)
 })
```

### 30.什么是通信

**信息的传递和交换**

通信三要素：通信的主体、内容、方式

### 31.**什么是通信协议**

**通信协议**（Communication Protocol）是指通信的双方完成通信所必须遵守的规则和约定。

通俗的理解：通信双方采用约定好的格式来发送和接收消息，这种事先约定好的通信格式，就叫做通信协议。

### 32.**互联网中的通信协议**

网页内容又叫做**超文本**，因此网页内容的传输协议又叫做**超文本传输协议**（HyperText Transfer Protocol） ，简称 **HTTP** **协议**

### 33.什么是HTTP请求消息

由于 HTTP 协议属于客户端浏览器和服务器之间的通信协议。因此，客户端发起的请求叫做 **HTTP** **请求**，客户端发送到服务器的消息，叫做 **HTTP** **请求消息**

​	注意：HTTP 请求消息又叫做 <b><font color='red' size=3 face=""> HTTP 请求报文</font></b> 。

### 34.HTTP请求消息的组成部分

HTTP 请求消息由 <b><font color='red' size=3 face="">请求行（request line）、请求头部（ header ） 、空行 和 请求体 </font></b> 4 个部分组成 

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921193617401.png" alt="image-20230921193617401" style="zoom:80%;" />

#### 请求行

**请求行**由 <b><font color='red' size=3 face="">请求方式、URL 和 HTTP 协议版本 </font></b> 3 个部分组成，他们之间使用空格隔开

#### **请求头部**

**请求头部**用来描述客户端的基本信息，从而把客户端相关的信息告知服务器。比如：User-Agent 用来说明当前是什么类型的浏览器；Content-Type 用来描述发送到服务器的数据格式；Accept 用来描述客户端能够接收什么类型的返回内容；Accept-Language 用来描述客户端期望接收哪种人类语言的文本内容。

请求头部由多行 键/值对 组成，每行的键和值之间用英文的冒号分隔。

| **头部字段**    | **说明**                                       |
| --------------- | ---------------------------------------------- |
| Host            | 要请求的服务器域名                             |
| Connection      | 客户端与服务器的连接方式(close  或  keepalive) |
| Content-Length  | 用来描述请求体的大小                           |
| Accept          | 客户端可识别的响应内容类型列表                 |
| User-Agent      | 产生请求的浏览器类型                           |
| Content-Type    | 客户端告诉服务器实际发送的数据类型             |
| Accept-Encoding | 客户端可接收的内容压缩编码形式                 |
| Accept-Language | 用户期望获得的自然语言的优先顺序               |

#### 空行

最后一个请求头字段的后面是一个**空行**，通知服务器请求头部至此结束。

请求消息中的空行，用来分隔请求头部与请求体。

#### 请求体

请求体中存放的，是要通过  <b><font color='red' size=3 face="">POST</font></b>  方式提交到服务器的数据

注意：只有 POST 请求才有请求体，GET 请求没有请求体

### 35.什么是HTTP响应消息

响应消息就是服务器响应给客户端的消息内容，也叫作响应报文。

### 36.http响应消息的组成部分

HTTP响应消息由 <b><font color='red' size=3 face="">状态行、响应头部、空行 和 响应体</font></b>  4 个部分组成

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921194541300.png" alt="image-20230921194541300" style="zoom:80%;" />

#### 状态行

**状态行**由  <b><font color='red' size=3 face="">HTTP 协议版本、状态码和状态码的描述文本</font></b>  3 个部分组成，他们之间使用空格隔开

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921194848797.png" alt="image-20230921194848797" style="zoom:80%;" />

#### 响应头部

**响应头部**用来描述服务器的基本信息。响应头部由多行 键/值对 组成，每行的键和值之间用英文的冒号分隔。

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921195017213.png" alt="image-20230921195017213" style="zoom:80%;" />

#### 空行

在最后一个响应头部字段结束之后，会紧跟一个**空行**，用来通知客户端响应头部至此结束。

响应消息中的空行，用来分隔响应头部与响应体。

#### 响应体

响应体中存放的，是服务器响应给客户端的资源内容。

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921195101222.png" alt="image-20230921195101222" style="zoom:80%;" />

### 37.什么是http请求方法

HTTP 请求方法，属于 HTTP 协议中的一部分，请求方法的作用是：用来表明要对服务器上的资源执行的操作。最常用的请求方法是 <b><font color='red' size=3 face=""> GET 和 POST</font></b> 。

#### http请求方法

| **序号** | **方法**                                                | **描述**                                                     |
| -------- | ------------------------------------------------------- | ------------------------------------------------------------ |
| 1        | <b><font color='red' size=3 face="">GET</font></b>      | <b><font color='red' size=3 face=""> (查询)</font></b> 发送请求来获得服务器上的资源，请求体中不会包含请求数据，请求数据放在协议头中。 |
| 2        | <b><font color='red' size=3 face="">  POST  </font></b> | <b><font color='red' size=3 face=""> (新增)</font></b> 向服务器提交资源（例如提交表单或上传文件）。数据被包含在请求体中提交给服务器。 |
| 3        | <b><font color='red' size=3 face="">  PUT </font></b>   | <b><font color='red' size=3 face=""> (修改)</font></b> 向服务器提交资源，并使用提交的新资源，替换掉服务器对应的旧资源。 |
| 4        | <b><font color='red' size=3 face=""> DELETE</font></b>  | <b><font color='red' size=3 face=""> (删除)</font></b> 请求服务器删除指定的资源。 |
| 5        | HEAD                                                    | HEAD  方法请求一个与 GET 请求的响应相同的响应，但没有响应体。 |
| 6        | OPTIONS                                                 | 获取http服务器支持的http请求方法，允许客户端查看服务器的性能，比如ajax跨域时的预检等。 |
| 7        | CONNECT                                                 | 建立一个到由目标资源标识的服务器的隧道。                     |
| 8        | TRACE                                                   | 沿着到目标资源的路径执行一个消息环回测试，主要用于测试或诊断。 |
| 9        | PATCH                                                   | 是对  PUT 方法的补充，用来对已知资源进行局部更新 。          |

### 38.什么是http状态响应码

用来标识响应的状态

 <b><font color='black' size=3 face="">HTTP 状态码共分为 5 种类型：</font></b> 

| **分类** | **分类描述**                                                 |
| -------- | ------------------------------------------------------------ |
| 1**      | 信息，服务器收到请求，需要请求者继续执行操作（实际开发中很少遇到  1**  类型的状态码） |
| 2**      | 成功，操作被成功接收并处理                                   |
| 3**      | 重定向，需要进一步的操作以完成请求                           |
| 4**      | 客户端错误，请求包含语法错误或无法完成请求                   |
| 5**      | 服务器错误，服务器在处理请求的过程中发生了错误               |

| **状态码** | **状态码英文名称** | **中文描述**                                                 |
| ---------- | ------------------ | ------------------------------------------------------------ |
| 200        | OK                 | 请求成功。一般用于  GET 与 POST  请求                        |
| 201        | Created            | 已创建。成功请求并创建了新的资源，通常用于  POST 或 PUT  请求 |

| 301  | Moved  Permanently | 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替 |
| ---- | ------------------ | ------------------------------------------------------------ |
| 302  | Found              | 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI |
| 304  | Not  Modified      | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源（响应消息中不包含响应体）。客户端通常会缓存访问过的资源。 |

| 400  | Bad  Request     | 1、语义有误，当前请求无法被服务器理解。除非进行修改，否则客户端不应该重复提交这个请求。  2、请求参数有误。 |
| ---- | ---------------- | ------------------------------------------------------------ |
| 401  | Unauthorized     | 当前请求需要用户验证。                                       |
| 403  | Forbidden        | 服务器已经理解请求，但是拒绝执行它。                         |
| 404  | Not Found        | 服务器无法根据客户端的请求找到资源（网页）。                 |
| 408  | Request  Timeout | 请求超时。服务器等待客户端发送的请求时间过长，超时。         |

| 500  | Internal  Server Error | <b><font color='black' size=3 face=""> 服务器内部错误，无法完成请求。</font></b> |
| ---- | ---------------------- | ------------------------------------------------------------ |
| 501  | Not  Implemented       | 服务器不支持该请求方法，无法完成请求。只有  GET 和 HEAD  请求方法是要求每个服务器必须支持的，其它请求方法在不支持的服务器上会返回501 |
| 503  | Service  Unavailable   | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。       |

### 39.什么是同源

两个页面的 <b><font color='red' size=3 face="">协议，域名和端口</font></b> 都相同，则两个页面具有**相同的源**

### 40.什么是同源策略

**同源策略**（英文全称 Same origin policy）是浏览器提供的一个安全功能。

MDN 官方给定的概念： <b><font color='black' size=3 face="">同源策略限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的重要安全机制。</font></b> 

通俗的理解：浏览器规定，A 网站的 JavaScript，不允许和非同源的网站 C 之间，进行资源的交互，例如：

①无法读取非同源网页的 Cookie、LocalStorage 和 IndexedDB

②无法接触非同源网页的 DOM

③无法向非同源地址发送 Ajax 请求

### 41.什么是跨域

**同源**指的是两个 URL 的协议、域名、端口一致，反之，则是**跨域**。

出现跨域的根本原因：**浏览器的同源策略**不允许非同源的 URL 之间进行资源的交互。

### 42.如何实现跨域数据请求

现如今，实现跨域数据请求，最主要的两种解决方案，分别是 <b><font color='red' size=3 face=""> JSONP 和 CORS</font></b> 。

 <b><font color='red' size=3 face="">JSONP：</font></b> 出现的早，兼容性好（兼容低版本IE）。是前端程序员为了解决跨域问题，被迫想出来的一种临时解决方案。 <b><font color='black' size=3 face="">缺点是只支持 GET 请求，不支持 POST 请求</font></b> 。

 <b><font color='red' size=3 face="">CORS：</font></b> 出现的较晚，它是 W3C 标准，属于跨域 Ajax 请求的根本解决方案。**支持 GET 和 POST 请求**。缺点是不兼容某些低版本的浏览器。 

### 43.什么是jsonp

**JSONP (JSON with Padding) 是 JSON 的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题**

由于浏览器同源策略的限制，网页中无法通过 Ajax 请求非同源的接口数据。但是 <script> 标签不受浏览器同源策略的影响，可以通过 src 属性，请求非同源的 js 脚本。

因此，JSONP 的实现原理，就是通过 <script> 标签的 src 属性，请求跨域的数据接口，并通过**函数调用**的形式，接收跨域接口响应回来的数据。

注意：**JSONP** **和** **Ajax** **之间没有任何关系**，不能把 JSONP 请求数据的方式叫做 Ajax，因为 JSONP 没有用到 XMLHttpRequest 这个对象。