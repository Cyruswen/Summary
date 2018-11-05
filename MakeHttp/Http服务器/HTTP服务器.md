## HTTP服务器

### 一、采用的相关重要协议

1. http协议  
2. TCP协议 
3. DNS协议

### 二、各协议的作用

- **HTTP**

  > 针对目标web服务器生成HTTP请求报文

- TCP

  > 为了方便通信，将HTTP请求按序号分为多个报文段，把每个报文段可靠的传送给对方。

- IP

  > 搜索对方IP地址，一边中转一边传送

- TCP

  > 接受报文段，并按原来的顺序重组请求报文

- HTTP

  > 对web服务器请求的内容进行处理

### 三、HTTP协议的特点

- 无连接,每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用
  这种方式可以节省传输时间。(http/1.0具有的功能，http/1.1兼容)
- 无状态
- 简单快速,HTTP服务器的程序规模小,因而通信速度很快。
- 灵活,HTTP允许传输任意类型的数据对象,正在传输的类型由Content-Type加以标记
- 协议本身并不会保留你之前的一切请求或者响应，这是为了更快的处理大量的事务，确保协议的可伸缩性
- HTTP/1.1版本中给出一种持续连接的机制。
- HTTP（超文本传输协议）是基于TCP的连接方式进行网络连接。

### 四、浏览器的URL格式

​	**http://host[":"port][abs_path]**

- http表示要通过HTTP协议来定位网络资源
- host表示合法的Internet主机域名或者IP地址
- port指定一个端口号，缺省80
- abs_path制定请求资源的URL
- 如果URL中没有给出abs_path，那么当它作为请求URI时，必须以“/”的形式给出，通常这个工作浏览器自动帮
  我们完成。

### 五、HTTP的请求与响应

![http请求和响应](/home/kaikai/Pictures/markimg/http请求和响应.png)



#### 1. HTTP的请求方法

- GET

  > 获取资源，获取被URI标识的资源

- POST

  > POST 主要用来传输数据，而 GET 主要用来获取资源。

- PUT

  > 上传文件，由于自身不带验证机制，任何人都可以上传文件，因此存在安全性问题，一般不使用该方法。

- HEAD

  > 和 GET 方法一样，但是不返回报文实体主体部分。
  >
  > 主要用于确认 URL 的有效性以及资源更新的日期时间等。

- DELETE

  > 与 PUT 功能相反，并且同样不带验证机制。

- PATCH

  > 对资源进行部分修改

- OPTIONS

  > 查询指定的 URL 能够支持的方法。
  >
  > 会返回 Allow: GET, POST, HEAD, OPTIONS 这样的内容.

- CONNECT

  > 要求在与代理服务器通信时建立隧道

  > 使用 SSL（Secure Sockets Layer，安全套接层）和 TLS（Transport Layer Security，传输层安全）协议把通信内容加密后经网络隧道传输。

- TRACE

  > 服务器会将通信路径返回给客户端。
  >
  > 发送请求时，在 Max-Forwards 首部字段中填入数值，每经过一个服务器就会减 1，当数值为 0 时就停止传输。
  >
  > 通常不会使用 TRACE，并且它容易受到 XST 攻击（Cross-Site Tracing，跨站追踪）。

- LINK

- UNLINK



#### 2. HTTP响应状态码

**1xx 信息**

- **100 Continue** ：表明到目前为止都很正常，客户端可以继续发送请求或者忽略这个响应。

**2xx 成功**

- **200 OK**
- **204 No Content** ：请求已经成功处理，但是返回的响应报文不包含实体的主体部分。一般在只需要从客户端往服务器发送信息，而不需要返回数据时使用。
- **206 Partial Content** ：表示客户端进行了范围请求。响应报文包含由 Content-Range 指定范围的实体内容。

**3xx 重定向**

- **301 Moved Permanently** ：永久性重定向  需要进行书签引用的变更
- **302 Found** ：临时性重定向 不需要对书签引用变更
- **303 See Other** ：和 302 有着相同的功能，但是 303 明确要求客户端应该采用 GET 方法获取资源。
- 注：虽然 HTTP 协议规定 301、302 状态下重定向时不允许把 POST 方法改成 GET 方法，但是大多数浏览器都会在 301、302 和 303 状态下的重定向把 POST 方法改成 GET 方法。
- **304 Not Modified** ：如果请求报文首部包含一些条件，例如：If-Match，If-Modified-Since，If-None-Match，If-Range，If-Unmodified-Since，如果不满足条件，则服务器会返回 304 状态码。
- **307 Temporary Redirect** ：临时重定向，与 302 的含义类似，但是 307 要求浏览器不会把重定向请求的 POST 方法改成 GET 方法。

**4xx 客户端错误**

- **400 Bad Request** ：请求报文中存在语法错误。
- **401 Unauthorized** ：该状态码表示发送的请求需要有认证信息（BASIC 认证、DIGEST 认证）。如果之前已进行过一次请求，则表示用户认证失败。
- **403 Forbidden** ：请求被拒绝，服务器端没有必要给出拒绝的详细理由。
- **404 Not Found**

**5xx 服务器错误**

- **500 Internal Server Error** ：服务器正在执行请求时发生错误。
- **503 Service Unavailable** ：服务器暂时处于超负载或正在进行停机维护，现在无法处理请求。



### 六、HTTP CGI机制

​	CGI(Common Gateway Interface) 是WWW技术中最重要的技术之一，有着不可替代的重要地位。CGI是外部应用程序（CGI程序）与WEB服务器之间的接口标准，是在CGI程序和Web服务器之间传递信息的过程。其实，要真正理解CGI并不简单，首先我们从现象入手，浏览器除了从服务器下获得资源（网页，图片，文字等），有时候还有能上传一些东西（提交表单，注册用户之类的），看看我们目前的http只能进行获得资源，并不能够进行上传资源，所以目前http并不具有交互式。为了让我们的网站能够实现交互式，我们需要使用CGI完成，时刻记着，我们目前是要写一个http，所以，CGI的所有交互细节，都需要我们来完成。
​	理论上，可以使用任何语言来编写CGI程序。注意，http提供CGI机制，和CGI程序是两码事，就好比学校（http）提供教学（CGI机制）平台，学生（CGI程序）来学习。

**1. 我们首先来理解一下GET和POST方法的区别**

> GET方法从浏览器传参数给http服务器时，是需要将参数跟到URI后面。

如：

```
https://www.baidu.com/s?
ie=utf8&f=3&rsv_bp=0&rsv_idx=1&tn=baidu&wd=ascii%E7%A0%81%E8%A1%A8&rsv_pq=c3b36e65000029a8&rsv_t=8c2a6N4WqJp6pn8wSPmrfETVJGIgC9hW6F041xz47x0FaHjFC3UE2gh9Ofk&rqlang=cn&rsv_enter=1&rsv_sug3=2&rsv_sug1=1&rsv_sug7=100&rsv_sug2=1&prefixsug=as&rsp=0&inputT=2214&rsv_sug4=2214
```

> POST方法从浏览器传参数给http服务器时，是需要将参数放的请求正文的。



- GET方法，如果没有传参，http按照一般的方式进行，返回资源即可.
- GET方法，如果有参数传入，http就需要按照CGI方式处理参数，并将执行结果（期望资源）返回给浏
  览器。
- POST方法,一般都需要使用CGI方式来进行处理。



具体流程见盗图如下：

​	![CGI流程图](/home/kaikai/Pictures/markimg/cgi流程.png)

