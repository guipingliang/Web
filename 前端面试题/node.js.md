### 1.什么是node.js

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230920202750247.png" alt="image-20230920202750247" style="zoom:80%;" />

### 2.**什么是** **fs** **文件系统模块**

fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求

- fs.readFile() ： <b><font color='black' size=3 face="">读取</font></b> 指定文件中的内容
-  fs.writeFile()：向指定的文件中 <b><font color='black' size=3 face="">写入</font></b> 内容

### 3.**fs.readFile() 的语法格式**

```html
fs.readFile(path[,options],callback)
```

- 参数1： <b><font color='red' size=3 face="">必选</font></b> 参数，字符串，表示文件的路径
- 参数2：可选参数，表示以什么 <b><font color='red' size=3 face="">编码格式</font></b> 来读取文件
- 参数3： <b><font color='red' size=3 face="">必选</font></b> 参数，文件读取完成后，通过回调函数拿到读取的结果

### 4.**fs.writeFile****()** **的语法格式**

```
fs.writeFile(file,data[,options],callback)
```

- 参数1： <b><font color='red' size=3 face="">必选</font></b> 参数，需要指定一个文件路径的字符串，表示文件的存放路径
- 参数2： <b><font color='red' size=3 face="">必选</font></b> 参数，表示要写入的内容
- 参数3： **<b><font color='red' size=3 face="">可选</font></b> **参数，表示以什么格式写入文件内容，默认值是 utf8
- 参数4：**必选**参数，文件写入完成后的回调函数

### 5.**什么是** **path** **路径模块**

 <b><font color='red' size=3 face="">处理路径的模块</font></b> 。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

- path.join() 方法，用来 <b><font color='red' size=3 face="">将多个路径片段拼接成一个完整的路径字符串</font></b> 
- path.basename() 方法，用来从路径字符串中，将文件名**解析**出来

```html
const path = require('path')
```

### 6.**路径拼接**

#### path.join()的语法格式

把多个路径片段拼接为完整的路径字符串

```html
path.join([...paths])
```

参数解读：...paths <string> 路径片段的序列   返回值: <string>

 <b><font color='red' size=3 face="">今后凡是涉及到路径拼接的操作，都要使用 path.join() 方法进行处理</font></b> 。不要直接使用 + 进行字符串的拼接。

#### **path.basename() 的语法格式**

<font color='red'>**可以从一个文件路径中，获取到文件的名称部分**</font>

```
path.basename(path[,ext])
```

参数解读：

- path<string> <font color='red'>**必须**</font>参数，表示一个路径的字符串
- ext <string> 可选参数，表示文件扩展名
- 返回: <string> 表示路径中的最后一部分

#### path.extname()的语法格式

<font color='red'>**获取路径中的扩展名部分**</font>

```html
path.extname(path)
```

参数解读：

- path <string>必选参数，表示一个路径的字符串
- 返回: <string> 返回得到的扩展名字符串

```vue
//代码示例
const fpath = '/a/b/b/index.html' //路径字符串

const fext = path.extname(fpath)
console.log(fext) //输出.html
```

### 7.http模块

**客户端：**在网络节点中，负责消费资源的电脑

**服务端：**负责对外提供网络资源的电脑

**http模块概念**：用来 <b><font color='red' size=3 face="">创建 web 服务器的模块</font></b> 。通过 http 模块提供的<font color='red'> http.createServer() </font>方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。 

如果要希望使用 http 模块创建 Web 服务器，则需要先导入它：

```html
const http = require('http')
```

#### 7.1服务器和普通电脑的**区别**

 <b><font color='red' size=3 face="">服务器是否安装了 web 服务器软件</font></b> ，例如：IIS、Apache 等。通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器。

在 Node.js 中，我们不需要使用 IIS、Apache 等这些第三方 web 服务器软件。因为我们可以基于 Node.js 提供的 http 模块，**通过几行简单的代码，就能轻松的手写一个服务器软件**，从而对外提供 web 服务

#### 7.2**创建** **web** **服务器的基本步骤**

1） <b><font color='red' size=3 face="">导入</font></b> http模块

2） <b><font color='black' size=3 face="">创建web服务器实例</font></b> 

3）为服务器实例绑定 <b><font color='red' size=3 face="">request</font></b> 事件， <b><font color='SEAGREEN' size=3 face="">监听客户端的请求</font></b> 

4）启动服务器 

```
//步骤1：导入http模块
const http = require ('http')

//步骤2：创建web服务器实例，调用 http.createServer() 方法
cosnt server = http.createServer()

//步骤3 - 为服务器实例绑定 request 事件
//使用服务器实例的 .on() 方法，为服务器绑定一个request 事件
server.on('request',(req.res)=>{
	//只要有客户端来请求我们自己的服务器，就会触发request事件，从而调动这个事件处理函数
	console.log('启动服务器端')
})

//步骤4 - 启动服务器
//调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例：
//调用 server.listen(端口号，cb回调) 方法，即可启动web服务器
server.listrn(80,()=>{
	cosole.log('http server running at http://127.0.0.1')
})



```

#### 7.3**根据不同的** **url** **响应不同的** **html** **内容**

**核心实现步骤**

①获取 <b><font color='red' size=3 face="">请求的 url 地址</font></b> 

②设置 <b><font color='red' size=3 face="">默认的响应内容</font></b> 为 404 Not found

③判断用户请求的是否为  <b><font color='red' size=3 face="">/ </font></b> 或  <b><font color='red' size=3 face="">/index.html</font></b>  首页

④判断用户请求的是否为 <b><font color='red' size=3 face=""> /about.html </font></b> 关于页面

⑤设置 <b><font color='red' size=3 face=""> Content-Type</font></b>  响应头，防止中文乱码

⑥使用 <b><font color='red' size=3 face=""> res.end()</font></b>  把内容响应给客户端

### 8.**模块化**

①提高了代码的 <b><font color='blue' size=3 face="">复用性</font></b> 

②提高了代码的 <b><font color='red' size=3 face="">可维护性</font></b> 

③可以实现 <b><font color='red' size=3 face="">按需加载</font></b> 

### 9. Node.js中模块的分类

1） <b><font color='blue' size=3 face="">内置模块</font></b> （内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）

2） <b><font color='red' size=3 face="">自定义模块</font></b> （用户创建的每个 .js 文件，都是自定义模块）

3） <b><font color='red' size=3 face="">第三方模块</font></b> （由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）

### 10.node_modules 与和package-lock.json 

 <b><font color='red' size=3 face="">node_modules </font></b>： 文件夹用来存放所有已安装到项目中的包。require() 导入第三方包时，就是从这个目录中查找并加载包

 <b><font color='red' size=3 face="">package-lock.json</font></b>  ：配置文件用来记录 node_modules 目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等 

### 11.**包管理配置文件**package.json 

- 项目的名称、版本号、描述等
- 项目中都用到了哪些包
- 哪些包只在开发期间会用到
- 那些包在开发和部署时都需要用到

### 12.**快速创建** **package.json**

```html
//作用：在执行命令所处的目录中，快速创建package.json
npm init -y
```

### 13.**dependencies** **节点**

 <b><font color='red' size=3 face="">记录使用 npm install 命令安装了哪些包。</font></b> 

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921144431815.png" alt="image-20230921144431815" style="zoom:80%;" />

### 14.一次性安装所有的包

可以运行 <b><font color='red' size=3 face=""> npm install 命令（或 npm i）</font></b> 一次性安装所有的依赖包：

```
//执行 npm install 命令时，npm 包管理工具会先读取package.json 中的dependencies节点，
//读取到记录的所有依赖包名称和版本号之后，npm包管理工具会把这些包一次性下载到项目中
npm install 
```

**卸载包**

```
npm uninstall moment
```

注意：npm uninstall 命令执行成功后，会把卸载的包， <b><font color='red' size=3 face="">自动从 package.json 的 dependencies 中移除掉</font></b> 

### 15.**devDependencies** **节点**

  <b><font color='blue' size=3 face="">开发依赖包</font></b> ：如果某些包**只在项目开发阶段**会用到，在**项目上线之后不会用到**，则建议把这些包记录到 <b><font color='red' size=3 face=""> devDependencies</font></b>  节点中。

 <b><font color='blue' size=3 face="">核心依赖包</font></b> ：如果 <b><font color='red' size=3 face="">某些包在开发和项目上线之后都需要用到</font></b> ，则建议把这些包记录到 <b><font color='red' size=3 face=""> dependencies</font></b>  节点中

将包记录到 devDependencies 节点中：

```
//安装指定的包，并记录在devDependencies中，开发依赖包
 npm i 包名 -D

//注意：上述命令是简写形式
npm install 包名 --save-dev
```

### 16.**Express** **简介**

使用 Express，我们可以方便、快速的创建 Web 网站的服务器或 API 接口的服务器

```
//安装
npm i express@4.17.1

//2.创建基本的web服务器
//导入 express 
const express = require('express')
//创建 web 服务器
const app = express()
//调用 app.listen(端口号，启动成功后的回调函数)，启动服务器
app.listen(80,()=>{
	console.log('express server running at http://127.0.0.1')
})
```

 <b><font color='red' size=3 face="">**.** **监听** **GET** **请求**</font></b> 

监听客户端的 GET 请求

![image-20230921150831405](C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921150831405.png)

 <b><font color='red' size=3 face="">**监听** **POST** **请求**</font></b> 

监听客户端的 POST 请求

![image-20230921150901234](C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921150901234.png)

**express.static****()**

创建一个 <b><font color='red' size=3 face="">静态资源服务器</font></b> ，例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了

```
app.use(express.static('public'))
```

| app.get()            | 监听客户端的 GET 请求                                        |
| -------------------- | ------------------------------------------------------------ |
| **app.post()**       | **监听客户端的 POST 请求**                                   |
| **res.send()**       | **把处理好的内容，发送给客户端**                             |
| **req.query**        | **访问到客户端通过查询字符串的形式，发送到服务器的参数**     |
| **req.params**       | **访问到 URL 中，通过 : 匹配到的动态参数**                   |
| **express.static()** | **创建一个 <b><font color='red' size=3 face="">静态资源服务器</font></b>** |

### 17.**路由的使用**

![image-20230921153803922](C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921153803922.png)

![image-20230921153822676](C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921153822676.png)

### 18.**. next** **函数的作用**

实现多个中间件连续调用的关键，它表示 <b><font color='red' size=3 face="">把流转关系转交给下一个中间件或路由</font></b> .

<img src="C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921154159195.png" alt="image-20230921154159195" style="zoom:67%;" />

### 19.**接口的****跨域问题**

解决接口跨域问题的方案主要有两种：

① CORS（主流的解决方案，推荐使用）

② JSONP（有缺陷的解决方案：只支持 GET 请求）

### 20.**使用** **cors** **中间件解决跨域问题**

使用步骤分为如下 3 步：

①运行 npm install cors 安装中间件

②使用  <b><font color='red' size=3 face="">const cors = require('cors') </font></b> 导入中间件

③在路由之前调用 <b><font color='red' size=3 face=""> app.use(cors())</font></b>  配置中间件

### 21.**什么是** **CORS**

CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，**这些** **HTTP** **响应头决定浏览器是否阻止前端** **JS** **代码跨域获取资源**。

浏览器的 <b><font color='red' size=3 face="">同源安全策略</font></b> 默认会阻止网页“跨域”获取资源。但如果 <b><font color='red' size=3 face="">接口服务器配置了 CORS 相关的 HTTP 响应头</font></b> ，就可以 <b><font color='red' size=3 face="">解除浏览器端的跨域访问限制</font></b> 

### 22.**CORS** **响应头部** 

 <b><font color='black' size=3 face="">Access-Control-Allow-Origin</font></b> 

响应头部中可以携带一个 **Access-Control-Allow-Origin** 字段，其语法如下:

```
 Access-Control-Allow-Origin:<origin> | * 
```

origin 参数的值指定了允许访问该资源的外域 URL

![image-20230921160418922](C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921160418922.png)

如果指定了 Access-Control-Allow-Origin 字段的值为通配符 *****，表示允许来自任何域的请求，示例代码如下：

```
res.setHeader('Access-Control-Allow-Origin','*')
```

#### **CORS** **响应头部** **- Access-Control-Allow-Headers**

默认情况下，CORS **仅**支持客户端向服务器发送如下的  <b><font color='red' size=3 face="">9 </font></b> 个请求头：

Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、 <b><font color='red' size=3 face="">Content-Type</font></b>  （值仅限于 **text/plain、multipart/form-data、application/x-www-form-urlencoded** 三者之一）

如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！

#### **CORS** **响应头部** **- Access-Control-Allow-**Method

默认情况下，CORS  <b><font color='blue' size=3 face="">仅支持客户端发起 GET、POST、HEAD</font></b>  请求。

如果客户端希望通过 <b><font color='red' size=3 face=""> PUT、DELETE</font></b>  等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来**指明实际请求所允许使用的 HTTP 方法** 

![image-20230921160847348](C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230921160847348.png)

### 21. CORS请求的分类

根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类

#### **简单请求**

同时满足以下两大条件的请求，就属于简单请求:

① 请求方式： <b><font color='red' size=3 face="">GET、POST、HEAD </font></b> 三者之一

② <b><font color='red' size=3 face=""> HTTP 头部信息</font></b> 不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-form-urlencoded、multipart/form-data、text/plain)

#### **预检请求**

只要符合以下任何一个条件的请求，都需要进行预检请求

①请求方式为 GET、POST、HEAD  <b><font color='red' size=3 face="">之外</font></b> 的请求 Method 类型

② 请求头中 <b><font color='red' size=3 face="">包含自定义头部字段</font></b> 

③ 向服务器发送了 **application/json** 格式的数据 

在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。

### 22.简单请求和预检请求的区别

**简单请求的特点**：客户端与服务器之间只会发生一次请求。

**预检请求的特点**：客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求。

### 23.**JSONP** **接口**

 <b><font color='red' size=3 face="">概念</font></b> ：浏览器端通过 <script> 标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 JSONP。

特点：

①JSONP 不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象。

②JSONP  <b><font color='red' size=3 face="">仅支持 GET </font></b> 请求，不支持 POST、PUT、DELETE 等请求。