# io
1、Java BIO：
同步并阻塞，服务器模式为一个连接一个线程，即客户端有连接请求时服务端就启动一个线程进行处理。
如果这个线程不做任何事情，会造成不必要的线程开销，可以通过 线程池 机制来改善。
2、Java NIO
同步非阻塞，服务器模式为一个请求一个线程，即客户端发送的连接请求都会注册到多路复用器上，
多路复用器轮询到 连接有IO请求时才启动一个线程进行处理。
3、Java AIO
异步非阻塞，服务器模式为一个有效请求一个线程，客户端的IO请求都是由OS先完成了再通知
服务器应用去启动线程进行处理。

3.5改善点
NIO比BIO的改善之处就是把一些无效的连接挡在了启动线程之前，减少了这部分资源的浪费，我们知道， 
每创建一个线程，就要为这个线程分配一定的内存空间。
AIO比NIO的改善之处就是将一些暂时可能的无效的请求挡在了启动线程之前，比如，
NIO的处理方式中，当一个请求来的话，开启线程进行处理，但这个请求所需要的资源还没有就绪，
此时必须等待后端的应用资源，这时线程就被阻塞了。

3.8适用场景分析：
BIO方式适用于连接数目比较小，且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，
程序直观简单易理解。
NIO方式适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，并发局限于应用中，
编程比较复杂，在Nginx，Netty中使用。
AIO方式适用于连接数目多且连接比较长（重操作）的架构，比如相册服务器，充分调用OS参与并发操作，
编程复杂，JDK7开始支持。

4、IO是面向流的,NIO是面向缓冲区的。
面向流意味着每次从流中读取一个或者多个字节，直至读取所有字节，它们没有缓存在任何地方。
面向缓冲意味着将数据读入缓冲器，使用通道进一步处理数据。使用通道和缓冲区处理数据。

•Java NIO使我们可以进行非阻塞IO操作。
比如说，单线程中从通道读取数据到buffer，同时可以继续做别的事情，当数据读取到buffer中后，线程再继续处理数据。
写数据也是一样的。
另外，非阻塞写也是如此。一个线程请求写入一些数据到某通道，但不需要等待它完全写入，这个线程同时可以去做别的事情。
•Java IO的各种流是阻塞的。
这意味着，当一个线程调用read() 或 write()时，该线程被阻塞，直到有一些数据被读取，或数据完全写入。
该线程在此期间不能再干任何事情了

5、选择器的概念
为了避免线程的上下文切换造成不必要的开销。
•选择器用于使用单个线程处理多个通道。因此，它需要较少的线程来处理这些通道。
•线程之间的切换对于操作系统来说是昂贵的。 因此，为了提高系统效率选择器是有用的。

6、NIO读取方式
从通道进行数据读取 ：创建一个缓冲区，然后请求通道读取数据。
从通道进行数据写入 ：创建一个缓冲区，填充数据，并要求通道写入数据。

7、通道的概念
•DatagramChannel UDP读写
•SocketChannel TCP读写
•FileChannel 文件读写
•ServerSocketChannel web服务

8、特地附上链接 http://www.cnblogs.com/snailclimb/p/NIO_Summary.html?utm_source=gold_browser_extension


9、对于文件的路径，我们经常发现有“\\” 和 “/”，根据相关查询得知：
一般可以认为“/” 的作用相当于 “\\”
在java中路径一般用"/"
windows中的路径一般用"\"
linux、unix中的路径一般用"/"
所以在java中写windows路径一般用  "/"或  将"\"转义一下，就成了"\\"
最好用“/”，因为java是跨平台的

“\”（在java代码里应该是\\）是windows环境下的路径分隔符，Linux和Unix下都是用“/”

而在windows下也能识别“/”。所以最好用“/”

File.separator
