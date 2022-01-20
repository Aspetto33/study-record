# computer networking

## cs144

### Lab0

* VM设置静态IP地址

  [参考ubuntu设置静态IP地址](https://www.myfreax.com/how-to-configure-static-ip-address-on-ubuntu-20-04/)	

* Clion远程开发

  [参考Clion远程开发](https://cloud.tencent.com/developer/article/1406250)

  

* Writing Webget

  可以参考Tcp sockets的[example](https://cs144.github.io/doc/lab1/class_t_c_p_socket.html#details)

  看一下TCPSocket和Address类

  

* An in-memory reliable byte stream

  实现一个缓冲池，可以进行字节读写

  最重要的是选择合适的数据结构实现缓冲池

  因为要实现读写，所以可以使用deque

  

### Lab1

- 实验目的

  Lab1的主要目的是实现TCP Receiver端的StreamReassembler。

  TCP Sender端发送过来的数据是被切割成一块一块的，且有顺序	的segment。但是因为underlying network 传输的是尽最大努力交付的datagrams，所以会出现如下三种情况：

  > short packets of data that can be lost, reordered, altered, or duplicated. 

  因此TCP Receiver端需要有一个将TCP Sender端发送过来的数据重组的StreamReassembler。

- 实验思路

  首先，选择合适的数据结构存储传递过来的segment，因为每个segment是由index和data组成的（特殊的结束字节有一个eof标志位，代表结束字节）。基于此，选择std::map。同时map的查找时间复杂度为O(logn)。

  然后要理解_capacity代表的含义。

### Lab2

### Lab3

### Lab4

### Lab5

### Lab6

### Lab7



