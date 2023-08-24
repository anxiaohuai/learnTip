## http协议开发

HTTP/1.1 - API

主要实现两个结构体 HttpRequest和HttpResponse，将请求协议和响应协议封装在这两个结构体内

## httpsession/httpconnection

Server的accept    session

Client的accept      connect

"HttpSession"和"HttpConnection"是两个不同的概念，它们在HTTP协议处理的不同阶段扮演不同的角色。

1. HttpSession继承自SocketStream，SocketStream继承自Stream，封装了read等函数:
   - HttpSession是在应用层与HTTP客户端进行通信的会话对象。它封装了与HTTP客户端的TCP连接，并提供了**接收HTTP请求和发送HTTP响应的功能**。
   - HttpSession主要用于处理一个完整的HTTP请求和响应的过程，它可以维护客户端与服务器之间的通信状态，处理会话相关的逻辑。
   - HttpSession通常是由**服务器端创建和管理的**，用于处理客户端与服务器之间的会话，可以包含多个HTTP请求和响应。
2. HttpConnection:
   - HttpConnection是在传输层基于TCP协议与服务器建立的连接。它提供了底层的数据传输能力，负责将HTTP请求和响应发送到服务器和接收服务器的响应。
   - HttpConnection主要负责处理HTTP的流式数据传输，它在应用层和传输层之间起到了桥梁的作用。
   - HttpConnection通常是由网络库或客户端创建和管理的，用于实现底层与服务器的连接，并负责处理数据的传输和处理。

总结： HttpSession和HttpConnection是两个不同的概念，它们在处理HTTP请求和响应的不同阶段扮演不同的角色。HttpSession位于应用层，用于处理会话和逻辑相关的操作，而HttpConnection位于传输层，用于实现底层数据的传输和处理。







## HTTPServer继承自TCPServer

- HttpServer类的构造函数带有一些参数，包括是否长连接、工作调度器、IO调度器和接收连接调度器。
- HttpServer类中还有一些成员函数：
  - getServletDispatch()：获取ServletDispatch对象的函数。
  - setServletDispatch()：设置ServletDispatch对象的函数。
  - setName()：重载TcpServer类的setName()函数。
  - handleClient()：重载TcpServer类的handleClient()函数。**调用HTTPsession的接收请求和返回响应**

该头文件主要定义了一个HttpServer类，该类继承自TcpServer类，用于构建一个HTTP服务器，并提供了一些功能函数。



## HTTPServlet

仿照java的servlet，实现了一套Servlet接口，实现了ServletDispatch，FunctionServlet。NotFoundServlet。支持uri的精准匹配，模糊匹配等功能。和HTTP模块，一起提供HTTP服务器功能

