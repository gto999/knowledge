## 从输入URL到页面加载完成的过程中都发生了什么事情？

#### 解析URL

当你在浏览器中输入URL并敲回车之后，浏览器会把URL分成几部分：

* 1、协议：从计算机获取资源的方式，常见的HTTP、FTP等
* 2、网络地址：域名或者IP，指示网络中的哪一台计算机
* 3、资源路径：指示在该计算机上获取哪一个资源

#### DNS域名解析

当浏览器发现网络地址并不是IP，而是域名的时候，浏览器会向DNS服务器发送请求，查找域名对应的IP，如果该DNS服务器没有找到该域名对应的IP，那吗会向上级请求，直到根节点，结果只有两个：要吗找到了，要吗找不到。
（你电脑里的网络设置里面有DNS的服务器IP）

扩展：例如百度、淘宝这些访问量及其大的网站，在DNS域名解析时，在不同的区域或不同网络下解析出来的IP可能是不同的，这就涉及负载均衡的第一步：在DNS解析域名时，将你的访问分配到不同的入口，同时尽可能保证你访问的入口是在所有入口中可能较快的一个。

#### 确定端口

如果网络地址中不包含端口，那么会使用协议默认的端口。HTTP协议默认端口是80，HTTPS协议默认端口是443

#### 发送HTTP请求

当浏览器对域名完成一系列的解析之后，就会构建一个HTTP请求，HTTP属于应用层协议，真正的数据传输是传输层协议TCP完成的，这就涉及到TCP建立连接的“三次握手”：

* 1、发送端发送带有 SYN 标志的数据包给接收端，并在一定的延迟时间内等待回复
* 2、接收端收到数据包后传回一个带有 SYN/ACK 标志的数据包以示确认传达信息
* 3、发送端收到信息后还会发送一个带有 ACK 标志的数据包给接收端以示握手成功，连接建立完成

#### 服务器处理并响应请求

服务器收到客户端发送的HTTP请求后，分析请求报文，并查找相应的请求资源，并返回响应报文。

响应报文中包含一个重要的信息，状态吗：

常见的 4 开头的状态吗一般表示请求出了问题，如 404 表示请求的资源不存在
3 开头的状态吗一般表示重定向，如 301表示永久重定向
5 开头的状态吗一般表示服务器出了问题，如 500 表示服务器出错
2 开头的一般代码成功，如 200

#### 页面渲染

请查看 [浏览器渲染页面的过程](/note/performance/render-page)

