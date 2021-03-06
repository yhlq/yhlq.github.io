---
layout: post
title: "python http实现共享文件"
date: 2019-12-05
description: 使用Python SimpleHTTPServer实现一个简单的Web Server，可以用来共享文件。
tag: 工具

---
# 简介
如果你急需一个简单的Web Server，但你又不想去下载并安装那些复杂的HTTP服务程序，比如：Apache，ISS等。那么，Python可能帮助你。使用Python可以完成一个简单的内建HTTP服务器。于是，你可以把你的目录和文件都以HTTP的方式展示出来。你唯一需要做的就是安装一个python。

# 实现
实际上来说，这是一个可以用来共享文件的非常有用的方式。实现一个微型的HTTP服务程序来说是很简单的事情，在Python下，只需要在命令行添加一行代码就可以实现。首先假设我们需要共享我们的目录 /home/haoel 而IP地址是192.168.1.1。代码如下：

*python2*
```
cd /home/haoel
python -m SimpleHTTPServer
```

*python3*

```
cd /home/haoel
python -m http.server
```
**默认端口为8000**

# 使用
这就行了，而我们的HTTP服务在8000号端口上侦听。你会得到下面的信息：
Serving HTTP on 0.0.0.0 port 8000 ...

你可以打开你的浏览器（IE或Firefox），然后输入下面的URL：
http://192.168.1.1:8000

如果你的目录下有一个叫 index.html 的文件名的文件，那么这个文件就会成为一个默认页，如果没有这个文件，那么，目录列表就会显示出来。

# 扩展
如果你想改变端口号，你可以使用如下的命令：

*python2*
```
python -m SimpleHTTPServer 8080
```

*python3*

```
python -m http.server 8080
```

如果你只想让这个HTTP服务器服务于本地环境，那么，你需要定制一下你的Python的程序，下面是一个示例：

```
import sys
import BaseHTTPServer
from SimpleHTTPServer import SimpleHTTPRequestHandler
HandlerClass = SimpleHTTPRequestHandler
ServerClass  = BaseHTTPServer.HTTPServer
Protocol     = "HTTP/1.0"
 
if sys.argv[1:]:
    port = int(sys.argv[1])
else:
    port = 8000
server_address = ('127.0.0.1', port)
 
HandlerClass.protocol_version = Protocol
httpd = ServerClass(server_address, HandlerClass)
 
sa = httpd.socket.getsockname()
print "Serving HTTP on", sa[0], "port", sa[1], "..."
httpd.serve_forever()
```

**注意：所有的这些东西都可以在 Windows 或 Cygwin 下工作。**
