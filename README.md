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

  然后，要理解_capacity代表的含义。

  ![cs144-lab1-capacity](/Users/yangqian/study/study-record/cs144-lab1-capacity.png)

​		为了便于理解把绿色部分叫作lab0的ByteStream，即已经排好序的字节流，此时并没有读，只是将其写入。把红		色部分称为_unassembled_strs，即用map存储没有排好序的segment。

​		最后，考虑以下几种可能出现的情况：

​		1、index <=  _next_unassemble_index && index + data.size() > _next_unassemble_index

​		2、index > _next_unassemble_index

​						此时取距离index最近的前面一段数据和index值，以及取距离index最近的后面的一段数据和index值。

​						1）取index前面的数据

​									1⃣️ index大于前面数据的长度+index

​									此时说明没有重叠出现，不用处理。

​									2⃣️ index小于前面数据的长度+index

​									此时说明index的部分数据和已经存储在map里面的数据重叠，

​									将index后移到前面数据的长度+index处。

​			2）取index后面的数据

​									1⃣️ index+data.size()小于后面数据的index

​									此时说明后面部分没有重叠数据，不用处理。

​									2⃣️ index+data.size()大于后面数据的index

​									这种情况又分为两种子情况：

​									部分重叠，将后面数据的index移到index+data.size()处即可；

​									完全覆盖，此时需要map中覆盖的数据删除，同时需要不断往后判断，是否还有覆盖数据。

​	综上，上面的操作可以保证map中存放的segment之间不会有重复数据。

### Lab2

* 实验目的

  Lab2要求实现TCP Receiver，接收从TCP Sender传输过来的segment并将其组装成用户可读的ByteStream。

* 实验思路

### Lab3

### Lab4

### Lab5

### Lab6

### Lab7



