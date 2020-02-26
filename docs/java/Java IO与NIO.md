<!-- MarkdownTOC -->
- [IO流学习总结](#io%e6%b5%81%e5%ad%a6%e4%b9%a0%e6%80%bb%e7%bb%93)
  - [一　Java IO，硬骨头也能变软](#%e4%b8%80-java-io%e7%a1%ac%e9%aa%a8%e5%a4%b4%e4%b9%9f%e8%83%bd%e5%8f%98%e8%bd%af)
  - [二　java IO体系的学习总结](#%e4%ba%8c-java-io%e4%bd%93%e7%b3%bb%e7%9a%84%e5%ad%a6%e4%b9%a0%e6%80%bb%e7%bb%93)
- [NIO与AIO学习总结](#nio%e4%b8%8eaio%e5%ad%a6%e4%b9%a0%e6%80%bb%e7%bb%93)
  - [一 Java NIO 概览](#%e4%b8%80-java-nio-%e6%a6%82%e8%a7%88)
  - [二 Java NIO 之 Buffer(缓冲区)](#%e4%ba%8c-java-nio-%e4%b9%8b-buffer%e7%bc%93%e5%86%b2%e5%8c%ba)
  - [三 Java NIO 之 Channel（通道）](#%e4%b8%89-java-nio-%e4%b9%8b-channel%e9%80%9a%e9%81%93)
  - [四 Java NIO之Selector（选择器）](#%e5%9b%9b-java-nio%e4%b9%8bselector%e9%80%89%e6%8b%a9%e5%99%a8)
  - [五 Java NIO之拥抱Path和Files](#%e4%ba%94-java-nio%e4%b9%8b%e6%8b%a5%e6%8a%b1path%e5%92%8cfiles)
  - [六 NIO学习总结以及NIO新特性介绍](#%e5%85%ad-nio%e5%ad%a6%e4%b9%a0%e6%80%bb%e7%bb%93%e4%bb%a5%e5%8f%8anio%e6%96%b0%e7%89%b9%e6%80%a7%e4%bb%8b%e7%bb%8d)
  - [七 Java NIO AsynchronousFileChannel异步文件通](#%e4%b8%83-java-nio-asynchronousfilechannel%e5%bc%82%e6%ad%a5%e6%96%87%e4%bb%b6%e9%80%9a)
- [推荐阅读](#%e6%8e%a8%e8%8d%90%e9%98%85%e8%af%bb)
  - [在 Java 7 中体会 NIO.2 异步执行的快乐](#%e5%9c%a8-java-7-%e4%b8%ad%e4%bd%93%e4%bc%9a-nio2-%e5%bc%82%e6%ad%a5%e6%89%a7%e8%a1%8c%e7%9a%84%e5%bf%ab%e4%b9%90)
  - [Java AIO总结与示例](#java-aio%e6%80%bb%e7%bb%93%e4%b8%8e%e7%a4%ba%e4%be%8b)
<!-- /MarkdownTOC -->




## IO流学习总结

### [一　Java IO，硬骨头也能变软]()

**（1） 按操作方式分类结构图：**

![IO-操作方式分类](../../media/pictures/Java/IO-操作方式分类.png)


**（2）按操作对象分类结构图**

![IO-操作对象分类](../../media/pictures/Java/IO-操作对象分类.png)

### [二　java IO体系的学习总结]() 
1. **IO流的分类：**
   - 按照流的流向分，可以分为输入流和输出流；
   - 按照操作单元划分，可以划分为字节流和字符流；
   - 按照流的角色划分为节点流和处理流。
2. **流的原理浅析:**

   java Io流共涉及40多个类，这些类看上去很杂乱，但实际上很有规则，而且彼此之间存在非常紧密的联系， Java Io流的40多个类都是从如下4个抽象类基类中派生出来的。

   - **InputStream/Reader**: 所有的输入流的基类，前者是字节输入流，后者是字符输入流。
   - **OutputStream/Writer**: 所有输出流的基类，前者是字节输出流，后者是字符输出流。
3. **常用的io流的用法** 


## NIO与AIO学习总结


### [一 Java NIO 概览]()

1.  **NIO简介**:

    Java NIO 是 java 1.4, 之后新出的一套IO接口NIO中的N可以理解为Non-blocking，不单纯是New。

2.  **NIO的特性/NIO与IO区别:**
    -   1)IO是面向流的，NIO是面向缓冲区的；
    -   2)IO流是阻塞的，NIO流是不阻塞的;
    -   3)NIO有选择器，而IO没有。
3.  **读数据和写数据方式:**
    - 从通道进行数据读取 ：创建一个缓冲区，然后请求通道读取数据。

    - 从通道进行数据写入 ：创建一个缓冲区，填充数据，并要求通道写入数据。

4.  **NIO核心组件简单介绍**
    - **Channels**
    - **Buffers**
    - **Selectors**


### [二 Java NIO 之 Buffer(缓冲区)]()

1. **Buffer(缓冲区)介绍:**
   - Java NIO Buffers用于和NIO Channel交互。 我们从Channel中读取数据到buffers里，从Buffer把数据写入到Channels；
   - Buffer本质上就是一块内存区；
   - 一个Buffer有三个属性是必须掌握的，分别是：capacity容量、position位置、limit限制。
2. **Buffer的常见方法**
    - Buffer clear()
    - Buffer flip()
    - Buffer rewind()
    - Buffer position(int newPosition)
3. **Buffer的使用方式/方法介绍:**
    - 分配缓冲区（Allocating a Buffer）:
    ```java
    ByteBuffer buf = ByteBuffer.allocate(28);//以ByteBuffer为例子
    ```
    - 写入数据到缓冲区（Writing Data to a Buffer）
    
     **写数据到Buffer有两种方法：**
    
      1.从Channel中写数据到Buffer
      ```java
      int bytesRead = inChannel.read(buf); //read into buffer.
      ```
      2.通过put写数据：
      ```java
      buf.put(127);
      ```

4. **Buffer常用方法测试**
   
    说实话，NIO编程真的难，通过后面这个测试例子，你可能才能勉强理解前面说的Buffer方法的作用。


### [三 Java NIO 之 Channel（通道）]()


1.  **Channel（通道）介绍**
     - 通常来说NIO中的所有IO都是从 Channel（通道） 开始的。 
     - NIO Channel通道和流的区别：
2. **FileChannel的使用**
3. **SocketChannel和ServerSocketChannel的使用**
4.  **️DatagramChannel的使用**
5.  **Scatter / Gather**
    - Scatter: 从一个Channel读取的信息分散到N个缓冲区中(Buufer).
    - Gather: 将N个Buffer里面内容按照顺序发送到一个Channel.
6. **通道之间的数据传输**
   - 在Java NIO中如果一个channel是FileChannel类型的，那么他可以直接把数据传输到另一个channel。
   - transferFrom() :transferFrom方法把数据从通道源传输到FileChannel
   - transferTo() :transferTo方法把FileChannel数据传输到另一个channel
   

### [四 Java NIO之Selector（选择器）]()


1. **Selector（选择器）介绍**
   - Selector 一般称 为选择器 ，当然你也可以翻译为 多路复用器 。它是Java NIO核心组件中的一个，用于检查一个或多个NIO Channel（通道）的状态是否处于可读、可写。如此可以实现单线程管理多个channels,也就是可以管理多个网络链接。
   - 使用Selector的好处在于： 使用更少的线程来就可以来处理通道了， 相比使用多个线程，避免了线程上下文切换带来的开销。
2. **Selector（选择器）的使用方法介绍**
   - Selector的创建
   ```java
   Selector selector = Selector.open();
   ```
   - 注册Channel到Selector(Channel必须是非阻塞的)
   ```java
   channel.configureBlocking(false);
   SelectionKey key = channel.register(selector, Selectionkey.OP_READ);
   ```
   -  SelectionKey介绍
   
      一个SelectionKey键表示了一个特定的通道对象和一个特定的选择器对象之间的注册关系。
   - 从Selector中选择channel(Selecting Channels via a Selector)
   
     选择器维护注册过的通道的集合，并且这种注册关系都被封装在SelectionKey当中.
   - 停止选择的方法
     
     wakeup()方法 和close()方法。
3.  **模板代码**

    有了模板代码我们在编写程序时，大多数时间都是在模板代码中添加相应的业务代码。
4. **客户端与服务端简单交互实例**



### [五 Java NIO之拥抱Path和Files]()

**一 文件I/O基石：Path：**
- 创建一个Path
- File和Path之间的转换，File和URI之间的转换
- 获取Path的相关信息
- 移除Path中的冗余项

**二 拥抱Files类：**
-  Files.exists() 检测文件路径是否存在
-  Files.createFile() 创建文件
-  Files.createDirectories()和Files.createDirectory()创建文件夹
-  Files.delete()方法 可以删除一个文件或目录
-  Files.copy()方法可以吧一个文件从一个地址复制到另一个位置
-   获取文件属性
-   遍历一个文件夹
-   Files.walkFileTree()遍历整个目录

### [六 NIO学习总结以及NIO新特性介绍]()

- **内存映射：**

这个功能主要是为了提高大文件的读写速度而设计的。内存映射文件(memory-mappedfile)能让你创建和修改那些大到无法读入内存的文件。有了内存映射文件，你就可以认为文件已经全部读进了内存，然后把它当成一个非常大的数组来访问了。将文件的一段区域映射到内存中，比传统的文件处理速度要快很多。内存映射文件它虽然最终也是要从磁盘读取数据，但是它并不需要将数据读取到OS内核缓冲区，而是直接将进程的用户私有地址空间中的一部分区域与文件对象建立起映射关系，就好像直接从内存中读、写文件一样，速度当然快了。

### [七 Java NIO AsynchronousFileChannel异步文件通]()

Java7中新增了AsynchronousFileChannel作为nio的一部分。AsynchronousFileChannel使得数据可以进行异步读写。



## 推荐阅读

### [在 Java 7 中体会 NIO.2 异步执行的快乐](https://www.ibm.com/developerworks/cn/java/j-lo-nio2/index.html)

### [Java AIO总结与示例](https://blog.csdn.net/x_i_y_u_e/article/details/52223406)
AIO是异步IO的缩写，虽然NIO在网络操作中，提供了非阻塞的方法，但是NIO的IO行为还是同步的。对于NIO来说，我们的业务线程是在IO操作准备好时，得到通知，接着就由这个线程自行进行IO操作，IO操作本身是同步的。

