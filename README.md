# FastCGITree
CGI,FastCGI技术研究


![](https://i.imgur.com/yODVpMw.png)

<pre>
      早期的web服务器简单的响应浏览器发送的Http请求，并将存储在服务器上的html文件返回给
   浏览器，也就是静态html.
      随着网络越来越复杂，出现了动态技术，但是服务器并不能执行运行php,asp这样的脚本文件，
   需要把asp,php发送给第三方，需要一个约定来协商web服务器发送的数据，以及第三方需要返回的
   数据的格式，这个约定就是CGI,common gateway interface.
</pre>

![](https://i.imgur.com/5jTkX0j.png)

<pre>
CGI
      CGI的工作原理是每当客户请求CGI的时候，WEB服务器就请求操作系统生成一个新的CGI解释器
   进程，CGI的一个进程则处理完一个请求后退出，下一个请求来时再创建新进程。当然这样在访问量
   很少时没什么问题。可是当访问量很大，并发存在，这种方式就不合适了，称为了性能的瓶颈。
</pre>

<pre>
FastCGI
     Fast CGI像是一个常驻型的CGI，它可以一直执行着，只要激活后，不会每次都花费时间去fork
  一个子进程。

     一般情况下，Fast CGI的工作流程如下：
         1）Web Server启动时载入FastCGI进程管理器。
         2）Fast CGI进程管理器自身初始化，启动多个CGI解释器进程并等待来自Web Server的连接。
         3）当客户端请求到达Web Server时，FastCGI进程管理器选择并连接到一个CGI解释器，
         Web Server将CGI环境变量和标准输入发送到FastCGI子进程。
         5）FastCGI子进程完成处理后将标准输出和错误信息从同一连接返回给Web Server。当
         Fast CGI子进程关闭连接时，请求便告知处理完成。FastCGI子进程接着等待并处理来自
         Fast CGI进程管理器的下一个连接。
</pre>