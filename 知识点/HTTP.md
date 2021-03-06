# HTTP协议  
HTTP（超文本传输协议）是一个基于请求与响应模式的、无状态的、应用层的协议，常基于TCP的连接方式，HTTP1.1版本中给出一种持续连接的机制，绝大多数的Web开发，都是构建在HTTP协议之上的Web应用。
1. 常用的HTTP请求方法  
* GET：用于请求访问已经被URL识别的资源，可以通过URL传递参数给服务器
* POST： 用于传输信息给服务器
* OPTIONS：查看相应的URL支持的HTTP方法
* PUT：传输文件，报文主体包含文件内容，保存到对应URL位置
* HEAD：获得报文首部，与GET方法类似，只是不返回报文主体，一般用于验证URL是否有效
* DELETE：删除文件，与PUT方法相反，删除对应URL位置的文件
2. GET与POST的区别
* GET：主要从服务器获取资源；传输数据置于URL后，用户可见，不安全；受URL长度限制，传输数据小，但效率高；只能支持ASCII字符，传输中文可能乱码。
* POST：主要向服务器发送数据；数组封存在请求实体中，用户不可见；可传输大量数据；支持标准字符集，可以正确传递中文。
3. HTTP请求报文与响应报文
* 请求报文头包含三部分  
a、请求行：请求方法，URL，HTTP版本  
b、请求首部字段  
c、请求内容实体
* 响应报文包含三部分  
a、响应行：HTTP版本，状态码，状态码的原因短语  
b、响应首部字段  
c、响应内容实体
4. HTTP1.1版本新特性
* 默认持久连接节省通信量，只要客户端服务端任意一端没有明确提出断开TCP连接，就一直保持连接，可以发送多次HTTP请求
* 管线化，客户端可以同时发出多个HTTP请求，而不用等待响应
* 断点续传原理
5. HTTP与HTTPS
* HTTP通信过程中使用明文，内容可能被窃听；不验证通信方身份，容易遭到伪造；无法验证报文完整性，可能被篡改。
* HTTPS是在HTTP基础上加上加密处理 + 认证 + 完整性保护
6. 输入URL到页面加载显示完成发生了什么?[详解](https://segmentfault.com/a/1190000006879700)
* DNS解析——>TCP连接——>发送HTTP请求——>服务器处理请求并返回报文——>浏览器解析渲染页面——>连接结束