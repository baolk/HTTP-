图解HTTP

------

## 一、了解Web及网络基础

1. 概述

   客户端（client）通过发送请求获取服务器的资源（resource）

   通信使用的是HTTP协议（HyperText Transfer Protocol，超文本传输协议）来完成从客户端到服务器端等一系列流程

2. TCP/IP协议

   TCP/IP协议为4层，从上往下分别为应用层、传输层、网络层和数据链路层

   - 应用层：HTTP协议、DNS服务

   - 传输层：TCP和UDP协议

   - 网络层：IP

   - 链路层：网络连接硬件部分

   发送端从上往下每通过一层就增加首部，接收端从下往上每通过一层就删除首部

   ![截屏2020-09-02 下午3.08.46](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午3.08.46.png)

3. IP、TCP和DNS概念

   - IP（Internet Protocol）协议：将数据包传送给对方

   - TCP协议：提供可靠的字节流服务，为保证数据的准确性采用三次握手策略

   - DNS（Domain Name System）服务：提供域名到IP地址之间的解析服务

   ![截屏2020-09-02 下午3.17.15](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午3.17.15.png)

4. 各种协议与HTTP协议的关系

   - 请求过程：客户端--DNS--HTTP--TCP--IP--TCP--HTTP

   - 返回过程则相反

   ![截屏2020-09-02 下午3.18.32](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午3.18.32.png)

5. URI和URL

   - URL（Uniform Resource Locator）：统一资源定位符，表示资源的地址（互联网上所处的位置）

   - URI（Uniform Resource Identifier）：统一资源标识符，用字符串表示某一互联网资源

   - URL是URI的子集

   - URI的格式：

     绝对URI格式：

     ![截屏2020-09-02 下午3.35.32](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午3.35.32.png)

     相对URI格式：

     /index.htm

## 二、简单的HTTP协议

1. 请求报文由请求方法、请求URI、协议版本、请求首部字段（可选）和内容实体（可选）

   ![截屏2020-09-02 下午3.42.59](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午3.42.59.png)

2. 响应报文由协议版本、状态码、状态码的原因短语、响应首部字段（可选）和实体主体（可选）

   ![截屏2020-09-02 下午3.52.54](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午3.52.54.png)

3. HTTP是一种无状态（stateless）协议，即HTTP协议自身不对请求和响应的通信状态进行保存，因此引入了Cookie技术

4. 使用URI定位资源的方法：在请求报文中包含URI

   ![截屏2020-09-02 下午3.54.33](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午3.54.33.png)

5. HTTP方法：

   - GET：获取资源；

   - POST：传输实体主体；

   - PUT：传输文件（一般不使用，有安全隐患）；

   - HEAD：只获得报文首部；

     ![截屏2020-09-02 下午4.01.46](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午4.01.46.png)

   - DELETE：删除文件（一般不使用，有安全隐患）；

   - OPTION：询问支持的方法，查询针对请求URI指定的资源支持的方法；

     ![截屏2020-09-02 下午4.02.05](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午4.02.05.png)

   - TRACE：追踪路径（不常用）

   - CONNECT：要求用隧道协议连接代理，要求与代理服务器通信时建立隧道，主要使用SSL和TLS协议把通信内容加密后经网络隧道传输，格式如下：

     CONNECT代理服务器名：端口号HTTP版本

     ![截屏2020-09-02 下午4.04.36](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午4.04.36.png)

6. 在HTTP协议初期，每进行一次HTTP通信就要断开TCP连接，这增加了通信开销，为解决上述问题提出了持久连接，只要任意一端没用明确断开连接，则保持TCP连接状态

   ![截屏2020-09-02 下午4.18.22](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午4.18.22.png)

   管线化（pipelining）是指同时并行发送多个请求，而不需要一个接一个等待响应

   ![截屏2020-09-02 下午4.19.45](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午4.19.45.png)

7. 使用Cookie（曲奇）进行状态管理：

   - Cookie技术是指在请求和响应报文中写入Cookie信息来控制客户端的状态

   - Cookie会根据服务端发送的响应报文内的一个叫做Set-Cookie的首部字段信息，通知客户端保存Cookie，当下次客户端再往该服务器发送请求时，客户端会自动在请求报文中加入Cookie值后发送出去![截屏2020-09-02 下午4.27.50](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午4.27.50.png)

## 三、HTTP报文内的HTTP信息

1. HTTP可分为报文首部和报文主体两个部分，两者用空行（CR+LF）划分

2. 请求报文和响应报文结构如下：

   首部字段一般为：通用首部、请求首部、响应首部和实体首部

   ![截屏2020-09-02 下午7.38.21](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午7.38.21.png)

3. 报文主体和实体主体存在差异：通常报文主体等于实体主体，只有当传输中进行编码操作时，实体主体的内容发送变化，才与报文主体存在差异。

4. 内容编码：指明应用在实体内容上的编码格式，并保持实体信息原样压缩。

   常见的内容编码方式：gzip（GNU zip）、compress（UNIX系统的标准压缩）、deflate（zlib）、identity（不进行编码）

   ![截屏2020-09-02 下午8.08.58](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午8.08.58.png)

5. 分块传输编码（Chunked Transfer Coding）：在传呼大容量数据时，通过把数据分割成多块让浏览器逐步显示页面。

6. 获取部分内容的范围请求：即指定下载的实体范围

   ![截屏2020-09-02 下午8.20.08](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午8.20.08.png)

7. 内容协商（Content Negotiation）返回最合适的内容，以下字段作为判断的基准：

   - Accept
   - Accept-Charset
   - Accept-Encoding
   - Accept-Language
   - Content-Language

   内容协商技术包括：

   - 服务器驱动协商
   - 客户端驱动协商
   - 透明协商：前两者的结合

## 四、返回结果的HTTP状态码

1. 状态码的作用：当客户端向服务器发送请求时，用来描述返回的请求结果

2. 状态码的类别：

   ![截屏2020-09-02 下午8.37.04](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-02 下午8.37.04.png)

   几个常用的状态码：

   - 200 OK

     表示从客户端发送来的请求在服务端被正常处理

   - 204 No Content

     表示服务器接受的请求已被成功处理，但是在返回的响应报文中不含实体的主体部分

   - 206 Partial Content

     表示客户端进行了范围请求，而服务器成功执行了这部分的GET请求

   - 301 Moved Permanently

     表示永久重定向，即请求的资源被分配给新的URI，以后应该使用现在的URI访问资源

   - 302 Found

     表示临时性重定向，即请求的资源被分配给新的URI，希望用户（本次）能使用新的URI访问

   - 303 See Other

     与302类似，但明确规定使用GET方法定向获取请求资源

   - 304 Not Modified

     表示客户端发送附带条件的请求时，服务端允许请求访问资源，但请求未满足条件

   - 307 Temporary Redirect

     表示临时重定向，与302相同，但307会遵循浏览器标准，不会将POST变成GET

   - 400 Bad Request

     表示请求报文中存在语法错误，需修改请求内容后再次发送请求。另外，浏览器会像200一样对待该状态码

   - 401 Unauthorized 

     表示发送的请求需要有通过HTTP认证的认证信息，若之前已进行过1次请求，则表示用户认证失败

   - 403 Forbidden

     表示对请求资源的访问被服务器拒绝

   - 404 Not Found

     表示无法在服务器上找到请求的资源

   - 500 Internal Server Error

     表示服务器端在执行请求时发生错误

   - 503 Service Unavailable

     表示服务器暂时处于超负载或正在停机维护，现在无法处理请求

## 五、与HTTP协作的Web服务器

web服务器可以搭建多个独立域名的Web网站，也可以作为通信路径的中转服务器

1. 虽然物理层面只有一台服务器，但可以通过虚拟主机的功能实现多个域名。但存在一个问题，当多个域名使用DNS服务被解析之后，两者的访问IP地址会相同。

   因此需要在发送HTTP请求时，必须在Host首部内完整指定主机名或域名的URI

   ![截屏2020-09-03 下午6.46.32](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午6.46.32.png)

2. 在HTTP通信时，除了客户端和服务器之外，还有一些用于通信数据转发的应用程序，例如代理、网关和隧道。

   - 代理：是一种有转发功能的应用程序，扮演了位于服务端和客户端中间人的角色

     ![截屏2020-09-03 下午7.33.13](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午7.33.13.png)

     每次通过代理服务器转发请求或响应时，会追加Via首部信息

     使用代理服务器的理由是：利用缓存技术减少网络贷款的流量，组织内部针对特定网站的访问控制，以获取访问日志为主要目的

     代理按两种基准分类，一是是否使用缓存，而是是否修改报文

     - 缓存代理

       代理转发响应时，缓存代理（Caching Proxy）会预先将资源的副本保存在代理服务器上，当代理再次接受到对相同资源的请求时，就可以不通过源服务器而直接返回缓存资源

     - 透明代理

       转发请求或响应时，不对报文做任何加工的代理都被称为透明代理（Transparent Proxy），反之则称为非透明代理

   - 网关：是转发其他服务器通信数据的服务器，接受从客户端发送来的请求时，它就像自己拥有资源的源服务器一样对请求进行处理

     网关的工作机制和代理十分相似，而网关能使通信线路上的服务器提供非HTTP协议服务

     ![截屏2020-09-03 下午7.31.22](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午7.31.22.png)

   - 隧道：是在相隔甚远的客户端和服务器之间进行中转并保持双方通信连接的应用程序

     使用SS了等加密手段进行通信，为确保客户端与服务器之间进行安全通信

     ![截屏2020-09-03 下午7.32.53](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午7.32.53.png)

3. 缓存：是指代理服务器或客户端本地磁盘内保存的资源副本，利用缓存可以减少对源服务器的访问，因此节省了通信流量和通信时间

   - 缓存服务器是代理服务器的一种，流程如下：

   ![截屏2020-09-03 下午7.49.02](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午7.49.02.png)

   - 缓存具有一定的有效期限
   - 客户端的缓存被称为临时网络文件（Temporary Internet File）

## 六、HTTP首部

1. HTTP请求报文

![截屏2020-09-03 下午7.54.10](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午7.54.10.png)

2. HTTP响应报文

![截屏2020-09-03 下午7.54.51](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午7.54.51.png)

3. 4种HTTP首部字段类型
   - 通用首部字段（General Header Fields）：请求和响应报文都会使用
   - 请求首部字段（Request Header Fields）：请求报文使用的首部
   - 响应首部字段（Response Header Fields）：响应报文采用的首部
   - 实体首部字段（Entity Header Fields）：针对实体部分使用的首部

4. 常见的首部字段

   ![截屏2020-09-03 下午8.00.10](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午8.00.10.png)

   ![截屏2020-09-03 下午8.00.23](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午8.00.23.png)

   ![截屏2020-09-03 下午8.00.36](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午8.00.36.png)

   ![截屏2020-09-03 下午8.00.59](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-03 下午8.00.59.png)

5. HTTP首部字段将定义成缓存代理和非缓存代理的行为，分为两类：

   - 端到端首部（End-to-end Header）

     会转发到最终接受目标，且必须被转发

   - 逐跳首部（Hop-by-hop Header）

     只对单次转发有效，会因为缓存或代理而不再转发，且需要提供Connection首部字段

     除以下8个首部字段外，其他都属于端到端首部：

     - Connection
     - Keep-Alive
     - Proxy-Authenticate
     - Proxy-Authorization
     - Trailer
     - TE
     - Transfer-Encoding
     - Upgrade

6. 通用首部字段：指请求和响应双方都会使用的首部

   - Cache-Control：用来操作缓存的工作机制

     Cache-Control指令一览：

     ![截屏2020-09-04 上午9.36.09](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-04 上午9.36.09.png)

     ![截屏2020-09-04 上午9.36.19](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-04 上午9.36.19.png)

   - Connection：

     （1）控制不再转发给代理的首部字段

     ![截屏2020-09-04 上午9.40.35](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-04 上午9.40.35.png)

     （2）管理持久连接![截屏2020-09-04 上午9.52.52](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-04 上午9.52.52.png)

   - Date：表明创建HTTP报文的日期和时间

   - Transfer-Encoding：规定传输报文主体采用的编码方式

   - Upgrade：用于检测HTTP协议及其他协议是否可使用更高版本进行通信，该参数可以用来指定一个完全不同的通信协议

     ![截屏2020-09-04 上午10.03.19](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-04 上午10.03.19.png)

   - Via：追踪客户端与服务器之间的请求和响应报文的传输路径

     ![截屏2020-09-04 上午10.04.03](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-04 上午10.04.03.png)

   - Warning：提示用户一些与缓存相关的问题警告

     ![截屏2020-09-04 上午10.04.51](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-04 上午10.04.51.png)

7. 请求首部字段：从客户端往服务器端发送请求报文所使用的字段

   - Accept：可通知服务器，用户代理能够处理的媒体类型及媒体类型的相对优先级

     ![截屏2020-09-05 下午8.04.20](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午8.04.20.png)

   - Accept-Charset：可用来通知服务器用户代理支持的字符集及字符集的相对优先顺序，可一次性指定多种字符集，该首部字段应用于内容协商机制的服务器驱动协商

   - Accept-Encoding：用来告知服务器用户代理支持的内容编码及内容编码的优先级顺序。可一次性指定多种内容编码，有gzip、compress、deflate、identity

   - Accept-Language：用来告知服务器用户代理能够处理的自然语言集（指中文或英文等）

   - Authorization：是用来告知服务器，用户代理的认证信息（证书值）

   - Expect：告知服务器，期望出现的某种特定行为

   - From：用来告知服务器使用用户代理的用户的电子邮件地址

   - Host：告知服务器，请求的资源所处的互联网主机名和端口号

   - If-Match：属附带条件之一，它会告知服务器匹配资源所用的实体标记（ETag）值

   - If-Modified-Since：属附带条件之一，它会告知服务器若If-Modified-Since字段值早于资源的更新时间，则希望能处理该请求

   - If-None-Match：用于指定If-None-Match字段值的实体标记（ETag）值与请求资源的ETag不一致时，它就告知服务器处理该请求

   - If-Range：它告知服务器若指定的If-Range字段值（ETag值或者时间）和请求资源的ETag值或时间相一致时，则作为范围请求处理。反之，则返回全体资源。

   - If-Unmodified-Since：告知服务器，指定的请求资源只有在字段值内指定的日期时间之后，未发生更新的情况下，才能处理请求。如果在指定日期时间后发生了更新，则以状态码412 Precondition Failed作为响应返回。

   - Max-Forwards：通过TRACE方法或OPTIONS方法，发送包含首部字段Max-Forwards的请求时，该字段以十进制整数形式指定可经过的服务器最大数目。服务器在往下一个服务器转发请求之前，会将Max-Forwards的值减1后重新赋值。当服务器接收到Max-Forwards值为0的请求时，则不再进行转发，而是直接返回响应。

   - Proxy-Authorization：接收到从代理服务器发来的认证质询时，客户端会发送包含首部字段Proxy-Authorization的请求，以告知服务器认证所需要的信息

   - Range：告知服务器资源的指定范围

   - Referer：告知服务器请求的原始资源的URI

   - TE：告知服务器客户端能够处理响应的传输编码方式及相对优先级

   - User-Agent：创建请求的浏览器和用户代理名称等信息传达给服务器

8. 响应首部字段：由服务器向客户端返回响应报文所用的字段

   - Accept-Ranges：是用来告知客户端服务器是否能处理范围请求，以指定获取服务器端某个部分的资源，可指定的字段值有两种，可处理范围请求时指定其为bytes，反之则指定其为none。
   - Age：告知客户端，源服务器在多久前创建了响应。字段值的单位为秒。
   - ETag：告知客户端实体标识。它是一种可将资源以字符串形式做唯一性标识的方式。服务器会为每份资源分配对应的ETag值
   - Location：可以将响应接收方引导至某个与请求URI位置不同的资源
   - Proxy-Authenticate：会把由代理服务器所要求的认证信息发送给客户端
   - Retry-After：告知客户端应该在多久之后再次发送请求
   - Server：告知客户端当前服务器上安装的HTTP服务器应用程序的信息
   - Vary：可对缓存进行控制。源服务器会向代理服务器传达关于本地缓存使用方法的命令
   - WWW-Authenticate：用于HTTP访问认证。它会告知客户端适用于访问请求URI所指定资源的认证方案（Basic或是Digest）和带参数提示的质询（challenge）

9. 实体首部字段：

   - Allow：首部字段Allow用于通知客户端能够支持Request-URI指定资源的所有HTTP方法
   - Content-Encoding：告知客户端服务器对实体的主体部分选用的内容编码方式，可选字段
     - gzip
     - compress
     - deflate
     - identity
   - Content-Language：告知客户端，实体主体使用的自然语言（指中文或英文等语言）
   - Content-Length：表明了实体主体部分的大小（单位是字节）
   - Content-Location：表示的是报文主体返回资源对应的URI
   - Content-MD5：是一串由MD5算法生成的值，其目的在于检查报文主体在传输过程中是否保持完整，以及确认传输到达
   - Content-Range：能告知客户端作为响应返回的实体的哪个部分符合范围请求
   - Content-Type：说明了实体主体内对象的媒体类型
   - Expires：会将资源失效的日期告知客户端
   - Last-Modefied：指明资源最终修改的时间

10. 为Cookie服务的首部字段：

    ![截屏2020-09-05 下午7.48.48](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午7.48.48.png)

    - Set-Cookie：当服务器准备开始管理客户端状态时，会事先告知各种信息

      ![截屏2020-09-05 下午7.50.42](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午7.50.42.png)

    - Cookie：首部字段Cookie会告知服务器，会在请求中包含从服务器接受到的Cookie

11. 其他首部字段：

    - X-Frame-Options：响应首部，用来控制网站内容在其他Web网站的Frame标签内的显示问题，主要是为了防止点击劫持（clickjacking）攻击，有DENY拒绝和SANEORIGIN仅同源域名下的页面匹配时许可
    - X-XSS-Protection：响应首部，针对跨站脚本攻击（XSS）的一种对策，用于控制浏览器XSS防护机制的开关，0 将XSS过滤设置成无效状态，1将XSS过滤设置成有效状态
    - DNT（Do Not Track）：请求首部，拒绝个人信息被收集，0表示同意被追踪，1表示拒绝被追踪
    - P3P：响应首部，利用P3P技术保护用户隐私

## 七、确保Web安全的HTTPS

1. HTTP存在如下不足：

- 通信使用明文（不加密），内容可能被窃听

  TCP/IP是最有可能被窃听的网络，加密是最常用的技术，一般进行通信加密和内容加密两种

  - 通信加密：SSL（Secure Socket Layer）和TLS（Transport LayerSecurity），用SSL建立安全通信线路之后，就可以在这条线路上进行HTTP通信，与SSL组合使用的HTTP被称为HTTPS

    ![截屏2020-09-05 下午2.50.31](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午2.50.31.png)

  - 内容加密：为了做到有效的内容加密，要求客户端和服务器同时具有加密和解密机制，但仍有被篡改的风险

    ![截屏2020-09-05 下午2.53.59](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午2.53.59.png)

- 不验证通信方的身份，因此有可能遭遇伪装

  使用SSL不仅提供加密处理，还使用了一种被称为证书的手段，可用于确认双方

  ![截屏2020-09-05 下午2.55.50](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午2.55.50.png)

- 无法证明报文的完整性，所以有可能已遭篡改

  最常用的是MD5和SHA-1等散列值校验方法，但并不能100%确保结果正确，有必要使用HTTPS

2. HTTPS=HTTP+加密+认证+完整性保护

   ![截屏2020-09-05 下午3.00.57](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.00.57.png)

   HTTPS（HTTP Secure）是身披SSL外壳的HTTP，并不是一种新协议，只是HTTP通信接口部分用SSL和TLS协议代替。当使用SSL时，演变为HTTP先与SSL通信，再由SSL和TCP进行通信

   ![截屏2020-09-05 下午3.03.37](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.03.37.png)

3. 共享密钥（对称密钥）：加密密钥和解密密钥相同，这种方式被称为共享密钥

   ![截屏2020-09-05 下午3.07.58](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.07.58.png)

   公开密钥加密（公钥密码体系）：使用一对非对称密钥，分别为私有密钥和公开密钥；公开密钥进行加密，使用私有密钥进行解密

   ![截屏2020-09-05 下午3.11.31](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.11.31.png)

4. HTTPS采用混合加密机制：在交换密钥环节使用公开密钥加密方式，之后建立通信报文阶段使用共享密钥加密

   ![截屏2020-09-05 下午3.15.38](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.15.38.png)

5. 证明公开密钥正确性的证书

   公开密钥加密存在一些问题，即无法证明公开密钥本身就是货真价实的公开密钥，为解决这个问题，我们使用数字证书认证机构颁发的公开密钥证书

   ![截屏2020-09-05 下午3.19.11](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.19.11.png)

## 八、确认访问用户身份的认证

身份认证就是认证用户的真实身份

1. HTTP使用的认证方式

   - BASIC认证（基本认证）：使用不够便捷，无法达到多数Web网站的安全等级

   - DIGEST认证（摘要认证）：采用质询响应方式

     ![截屏2020-09-05 下午3.25.18](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.25.18.png)

   - SSL客户端认证：验证是否是已登陆的客户端

   - FormBase认证（基于表单认证）：BASIC和DIGEST认证不怎么使用，SSL客户端由于费用问题无法普及，FormBase最常用的认证方法，一般采用Cookie来管理Session（会话）![截屏2020-09-05 下午3.30.02](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.30.02.png)

## 九、基于HTTP的功能追加协议

1. Ajax（Asynchronous JavaScript and XML，异步JavaScript和XML技术）是一种有效利用JavaScript和DOM（Document Object Model，文档对象模型）的操作，以达到局部Web页面替换加载的异步通信手段，与以前的同步通信相比，它只更新一部分页面

   Ajax核心技术是XMLHttpRequest的API，通过JavaScript脚本语言调用和服务器进行HTTP通信，借助这种手段就能从加载完毕的Web页面上发起请求，只更新局部页面，但仍然有大量请求产生

   ![截屏2020-09-05 下午3.42.32](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.42.32.png)

2. Comet：一旦服务端有内容更新，直接给客户端返回响应，但一次连接的持续时间变长了，维持连接消耗了更多资源

   ![截屏2020-09-05 下午3.45.19](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午3.45.19.png)

3. SPDY在TCP/IP的应用层和传输层之间新加会话层，额外获得了以下功能：

   - 多路复用流：通过单一的TCP连接可以无限制处理多个HTTP请求，所有请求的处理都在一条TCP连接上
   - 赋予请求优先级：给请求逐个分配优先级顺序
   - 压缩HTTP首部：压缩HTTP请求和响应的首部
   - 推送功能：支持服务器主动向客户端推送数据
   - 服务器提示功能：服务器可以主动提示客户端请求所需的资源

4. WebSocket：使用浏览器进行全双工通信

   WebSocket是浏览器和服务器之间全双工通信标准，主要是为了解决Ajax和Comet里的XMLHttpRequest附带的缺陷所引起的问题，该协议的主要特点：

   - 推送功能：支持由服务器向客户端推送数据的推送功能，服务器可以直接发送数据而不必等待客户端的请求
   - 减少通信量：只要建立起WebSocket连接，就希望一直保持连接状态，而且WebSocket首部信息很小，通信量也相应减少了。

   为了实习WebSocket通信，在HTTP连接建立之后，需要完成一次握手的步骤

   - 握手请求：需要用到HTTP的Upgrade首部字段，告知服务器通信协议发生改变，以达到握手的目的

     ![截屏2020-09-05 下午7.25.55](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午7.25.55.png)

   - 握手响应：对于之前的请求，返回状态码101 Switching Protocols的响应

     ![截屏2020-09-05 下午7.26.56](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午7.26.56.png)

     Sec-WebSocket-Accept的字段值是由握手请求中的Sec-WebSocket-Key的字段值生成的

     成功握手确立WebSocket连接之后，通信时不再使用HTTP的数据帧，而采用WebSocket独立的数据帧

     ![截屏2020-09-05 下午7.27.52](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午7.27.52.png)

## 十、构建Web内容的技术

1. HTML（HyperText Markup Language，超文本标记语言）是为了发送Web上的超文本而开发的标记语言
2. CSS（Cascading Style Sheets，层叠样式表）
3. 动态HTML：指调用客户端脚本语言JavaScript实现对HTML的动态改造，使用DOM可以指定欲发生动态变化的HTML元素
4. XML（eXtensibel Markup Language，可拓展标记语言）是一种可以按应用目标进行拓展的通用标记语言，通过XML使互联网数据共享变得更容易
5. JSON（JavaScript Object Notation）是一种以JavaScript的对象表示法为基础的轻量级数据标记语言

## 十一、Web的攻击技术

1. HTTP协议并不存在安全性问题，协议本身不会成为攻击的对象。Web的攻击对象一般是应用HTTP协议的服务器和客户端，以及运行在服务器上的Web应用等资源才是攻击目标。

2. 针对Web应用的攻击模式：

   - 以服务器为目标的主动攻击

     代表：SQL注入攻击、OS命令注入攻击

   - 以服务器为目标的被动攻击

     是指利用圈套策略执行攻击代码的攻击模式，攻击者不直接对目标Web应用访问发起攻击

     代表：跨站脚本攻击、跨站点请求伪造

     ![截屏2020-09-05 下午6.24.53](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午6.24.53.png)

3. 因输出值转义不完全引发的安全漏洞

   为了保障Web应用的安全，通常会进行验证，分为以下两大类：

   - 客户端验证

   - 服务端验证：包括输入值验证、输出值转义

     ![截屏2020-09-05 下午6.30.12](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午6.30.12.png)

     当输出值转义不完全时，会因触发攻击者传入的攻击代码，而给输出对象带来损害

     1. 跨站脚本攻击（Cross-Site Scripting，XSS）

        是指通过存在安全漏洞的Web网站注册用户的浏览器内运行非法HTML标签或JavaScript进行的一种攻击；当用户在自己的浏览器运行攻击者编写的脚本陷阱，一不小心就会收到被动攻击，可能造成影响：

        - 利用虚假输入表单片区用户个人信息
        - 显示伪造的文章或图片

     2. SQL注入攻击（SQL Injection）

        是指针对Web应用使用的数据库，通过运行非法的SQL而产生的攻击，会造成的影响：

        - 非法查看或篡改数据库内的数据
        - 规避认证
        - 执行和数据库服务器业务关联的程序等

     3. OS命令注入攻击（OS Command Injection）

        是指通过Web应用，执行非法的操作系统命令达到攻击的目的

     4. HTTP首部注入攻击（HTTP Header Injection）

        是指攻击者通过在响应首部字段内插入换行，添加任意响应首部或主体的一种攻击，属于被动攻击，可能造成的危害：

        - 设置任何Cookie信息
        - 重定向至任意URL
        - 显示任意的主体

     5. 邮件首部注入攻击

        是指攻击者利用存在安全漏洞的Web网站对任意邮件地址发送广告邮件或病毒邮件

     6. 目录便利攻击

        是指对本无意公开的文件目录，通过非法截断其目录路径后，达到访问目的一种攻击

     7. 远程文件包含漏洞

        是指部分脚本内容需要从其他文件读入时，攻击者利用指定外部服务器的URL充当依赖文件，让脚本读取之后，就可以运行任何脚本的一种攻击

4. 因设置或设计上的缺陷引发的安全漏洞

   往往是指设置或设计上的缺陷引发的安全漏洞

   1. 强制浏览

      是指从安置在Web服务器的公开目录下的文件中，浏览那些原本非自愿公开的文件，存在扽影响：

      - 泄露顾客的个人信息等重要情报
      - 泄露原本需要具有访问权限的用户才可以查阅的信息内容
      - 泄露未外连到外界的文件

   2. 不正确的错误消息处理

      是指Web应用的错误信息内包含对攻击者有用的信息，产生影响：

      - Web应用抛出的错误消息
      - 数据库等系统抛出的错误消息

   3. 开放重定向

      是指对指定的任意URL作重定向跳转功能

5. 因会话管理疏忽引发的安全漏洞

   会话管理是用来管理用户状态的必备功能，管理疏忽会导致用户的认证状态被窃取

   1. 会话劫持（Session Hijack）

      是指攻击者通过某种手段拿到了用户的会话ID，并非法使用此会话ID伪装成用户，达到攻击的目的

      ![截屏2020-09-05 下午7.07.02](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午7.07.02.png)

      以下为几种可能获得会话ID的途径：

      - 通过非正规生产方法推测会话ID
      - 通过窃听或XSS攻击盗取会话ID
      - 通过会话固定攻击（Session Fixation）强行获取会话ID

   2. 会话固定攻击（Session Fixation）

      会话固定攻击会强制用户使用攻击者指定的会话ID，属于被动攻击

      ![截屏2020-09-05 下午7.11.10](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午7.11.10.png)

   3. 跨站点请求伪造（Cross-Site Request Forgeries，CSRF）

      是指攻击者通过设置好的陷阱，强制对已完成认证的用户进行非预期的个人信息或设定信息等某些状态更新，属于被动攻击，可能造成的影响：

      - 利用已通过认证的用户权限更新设定信息等
      - 利用已通过认证的用户权限购买商品
      - 利用已通过认证的用户权限在留言板上发表言论

6. 其他安全漏洞

   1. 密码破解

      - 通过网络的密码试错：穷举法、字典攻击

      - 对已加密密码的破解：攻击者得到密码也需要解密还原成明文

        ![截屏2020-09-05 下午7.20.47](/Users/dylan/Library/Application Support/typora-user-images/截屏2020-09-05 下午7.20.47.png)

        通常有以下几种方法：穷举法、字段攻击、彩虹表、拿到密钥、加密算法的漏洞

   2. 点击劫持：指利用透明的按钮或链接做成陷阱，覆盖在Web页面之上。然后诱使用户在不知情的情况下，点击那个链接访问内容的一种攻击手段

   3. DOS攻击：是一种让运行中的服务呈停止状态的攻击。有时也叫做服务停止攻击或拒绝服务攻击。

   4. 后门程序：是指开发设置的隐藏入口，可不按正常步骤使用受限功能。利用后门程序就能够使用原本受限制的功能。



