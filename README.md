# ThriftFrontEndTest
### Thrift前端代码示例
本项目示例和TestThrift项目（https://github.com/KingWang93/TestThrift） 是配套的，属于前端代码，可以配合TestThrift项目完成前后端http请求过程，下面将整个流程（前后端）展示如下：
### 1.	下载Thrift,windows比较简单，有预编译的exe
https://thrift.apache.org/docs/install/windows
### 2.	下载测试用的thrift文件，从这里就看thrfit语法怎么写，主要就是struct和enum，服务叫service，service和struct可以用继承
https://git-wip-us.apache.org/repos/asf?p=thrift.git;a=blob_plain;f=tutorial/shared.thrift
https://git-wip-us.apache.org/repos/asf?p=thrift.git;a=blob_plain;f=tutorial/tutorial.thrift
### 3.	上面下载的exe和thrift文件放同一目录，在命令行执行以下命令
thrift-0.10.0.exe -r --gen js --gen java tutorial.thrift
### 4.	生成两个文件夹，gen-java和gen-js。把gen-java的代码拷贝到Eclipse工程中
### 5.	添加引用Jar包，需要手工编译Java依赖包。下载Apache Ant把bin目录加入环境变量,并通过下面链接下载thrift: 
http://www.apache.org/dyn/closer.cgi?path=/thrift/0.10.0/thrift-0.10.0.tar.gz
cmd进入\thrift-0.10.0\lib\java，ant即可,完成后jar包在build子目录，把libthrift-0.10.0.jar和lib子目录下的jar包都拷贝出来，添加到上面测试工程依赖
### 6.	加上具体实现服务的类，对于这个例子，thrift提供了一个样板实现
https://git1-us-west.apache.org/repos/asf?p=thrift.git;a=blob_plain;f=tutorial/java/src/CalculatorHandler.java;hb=HEAD
### 7.	写一个Java Server的启动类，可参考
这个可以可以从http://www.apache.org/dyn/closer.cgi?path=/thrift/0.10.0/thrift-0.10.0.tar.gz 下载下来的文件目录下（thrift-0.10.0\tutorial\js\src下）有个httpd.java文件，这个利用了httpcore的jar包。实现创建httpserver的功能。
### 8.	cross-region问题，参考
https://stackoverflow.com/questions/8153832/xmlhttprequest-changes-post-to-option
https://stackoverflow.com/questions/25727306/request-header-field-access-control-allow-headers-is-not-allowed-by-access-contr
js部分需要支持options请求里，在response里加上response.addHeader("Access-Control-Allow-Origin", "*")，改造下httpd.java
### 9.	启动这个Java Server端的启动类，至此Java服务端完成配置
### 10.	把thrift-0.10.0\lib\js\src下的thrift.js拷贝到gen-js里面
### 11.	建一个html文件，测试Javascript端，这里有别人写好的例子，可参考
https://github.com/LukeOwncloud/ThriftJavaJavascriptDemo/blob/master/index.html
### 12.	var transport = new Thrift.Transport(X)部分，X参数为后端的服务，这里对应的是后端Java类HttpD里面的IP端口，
http://127.0.0.1:8088/service 把这个html放在一个Tomcat服务下访问

### 注意事项
上面讲解的是利用httpd.java实现thrift远程调用的后端功能。
其实在TestThrift项目下还利用vertx实现了创建httpserver的功能，具体参看后端代码。

