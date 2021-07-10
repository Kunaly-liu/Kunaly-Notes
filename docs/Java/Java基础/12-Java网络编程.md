# Java网络编程

[本文相关代码](https://gitee.com/kunaly/kunaly-notes/raw/main/docs/Java/Java%E5%9F%BA%E7%A1%80/Codes/NetDemo.zip)

## 1.  概述

### 1.1  计算机网络简介

　计算机网络是通过传输介质、通信设施和网络通信协议，把分散在不同地点的计算机设备互连起来的，实现资源共享和数据传输的系统。网络编程就是编写程序使互联网的两个（或多个）设备（如计算机）之间进行数据传输。Java语言对网络编程提供了良好的支持。通过其提供的接口我们可以很方便地进行网络编程。

### 1.2  网络分层

​		通过网络发送数据是一项复杂的操作，必须仔细地协调网络的物理特性以及所发送数据的逻辑特征。通过网络将数据从一台主机发送到另外的主机，这个过程是通过计算机网络通信来完成。

　　网络通信的不同方面被分解为多个层，层与层之间用接口连接。通信的双方具有相同的层次，层次实现的功能由协议数据单元（PDU）来描述。不同系统中的同一层构成对等层，对等层之间通过对等层协议进行通信，理解批次定义好的规则和约定。每一层表示为物理硬件（即线缆和电流）与所传输信息之间的不同抽象层次。在理论上，每一层只与紧挨其上和其下的层对话。将网络分层，这样就可以修改甚至替换某一层的软件，只要层与层之间的接口保持不变，就不会影响到其他层。

　　计算机网络体系结构是计算机网络层次和协议的集合，网络体系结构对计算机网络实现的功能，以及网络协议、层次、接口和服务进行了描述，但并不涉及具体的实现。接口是同一节点内相邻层之间交换信息的连接处，也叫服务访问点（SAP）。

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1217276-20190503122042374-56172361.png)



世界上第一个网络体系结构由IBM公司提出（1974年，SNA），以后其他公司也相继提出自己的网络体系结构。为了促进计算机网络的发展，国际标准化组织ISO在现有网络的基础上，提出了不基于具体机型、操作系统或公司的网络体系结构，称为开放系统互连参考模型，即OSI/RM（Open System Interconnection Reference Model）。

　　ISO制定的OSI参考模型过于庞大、复杂招致了许多批评。与此相对，美国国防部提出了TCP/IP协议栈参考模型，简化了OSI参考模型，由于TCP/IP协议栈的简单，获得了广泛的应用，并成为后续因特网使用的参考模型。

### 1.3 OSI参考模型

OSI模型把网络通信的工作分为7层，分别是物理层、数据链路层、网络层、传输层、会话层、表示层和应用层。

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/54fbb2fb43166d2259d200b3442309f79052d26b)

各层的作用：

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1639925-20191106134509444-1655245651.png)

- 物理层

　　物理层处于OSI的最底层，是整个开放系统的基础。物理层涉及通信信道上传输的原始比特流（bits），它的功能主要是为数据端设备提供传送数据的通路以及传输数据。

- 数据链路层

　　数据链路层的主要任务是实现计算机网络中相邻节点之间的可靠传输，把原始的、有差错的物理传输线加上数据链路协议以后，构成逻辑上可靠的数据链路。需要完成的功能有链路管理、成帧、差错控制以及流量控制等。其中成帧是对物理层的原始比特流进行界定，数据链路层也能够对帧的丢失进行处理。

- 网络层

　　网络层涉及源主机节点到目的主机节点之间可靠的网络传输，它需要完成的功能主要包括路由选择、网络寻址、流量控制、拥塞控制、网络互连等。

- 传输层

　　传输层起着承上启下的作用，涉及源端节点到目的端节点之间可靠的信息传输。传输层需要解决跨越网络连接的建立和释放，对底层不可靠的网络，建立连接时需要三次握手，释放连接时需要四次挥手。　　

- 会话层和表示层

　　会话层的主要功能是负责应用程序之间建立、维持和中断会话，同时也提供对设备和结点之间的会话控制，协调系统和服务之间的交流，并通过提供单工、半双工和全双工3种不同的通信方式，使系统和服务之间有序地进行通信。

　　表示层关心所传输数据信息的格式定义，其主要功能是把应用层提供的信息变换为能够共同理解的形式，提供字符代码、数据格式、控制信息格式、加密等的统一表示。

- 应用层

　　应用层为OSI的最高层，是直接为应用进程提供服务的。其作用是在实现多个系统应用进程相互通信的同时，完成一系列业务处理所需的服务。

### 1.4 TCP/IP参考模型

　TCP/IP，即Transmission Control Protocol/Internet Protocol的简写，中译名为传输控制协议/因特网互联协议，是Internet最基本的协议，Internet国际互联网络的基础。

　　TCP/IP协议是一个开放的网络协议簇，它的名字主要取自最重要的网络层IP协议和传输层TCP协议。TCP/IP协议定义了电子设备如何连入因特网，以及数据如何在它们之间传输的标准。TCP/IP参考模型采用4层的层级结构，每一层都呼叫它的下一层所提供的协议来完成自己的需求，这4个层次分别是：网络接口层、网络层（IP层）、传输层（TCP层）、应用层。

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1e30e924b899a9012db25350c05fa87d0308f526.jpeg)

- 网络接口层

　　TCP/IP协议对网络接口层没有给出具体的描述，网络接口层对应着OSI参考模型的物理层和数据链路层

- 网络层（IP层）

　　网络层是整个TCP/IP协议栈的核心。它的功能是把分组发往目标网络或主机。同时，为了尽快地发送分组，可能需要沿不同的路径同时进行分组传递。因此，分组到达的顺序和发送的顺序可能不同，这就需要上层必须对分组进行排序。网络层除了需要完成路由的功能外，也可以完成将不同类型的网络（异构网）互连的任务。除此之外，互联网层还需要完成拥塞控制的功能。

- 传输层（TCP层）

　　TCP层负责在应用进程之间建立端到端的连接和可靠通信，它只存在与端节点中。TCP层涉及两个协议，TCP和UDP。其中，TCP协议提供面向连接的服务，提供按字节流的有序、可靠传输，可以实现连接管理、差错控制、流量控制、拥塞控制等。UDP协议提供无连接的服务，用于不需要或无法实现面向连接的网络应用中。

- 应用层

　　应用层为Internet中的各种网络应用提供服务。

### 1.5 网络协议

　如同人与人之间相互交流是需要遵循一定的规则（如语言）一样，计算机之间能够进行相互通信是因为它们都共同遵守一定的规则，即网络协议。

　　OSI参考模型和TCP/IP模型在不同的层次中有许多不同的网络协议，如图所示：

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1217276-20190503164338008-348345936.png)

网络协议之间的关系图如下：

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1217276-20190503165942538-1220277464.png)



####  1.5.1 IP协议（Internet protocol）

 　IP协议的作用在于把各种数据包准备无误的传递给对方，其中两个重要的条件是IP地址和MAC地址。由于IP地址是稀有资源，不可能每个人都拥有一个IP地址，所以我们通常的IP地址是路由器给我们生成的IP地址，路由器里面会记录我们的MAC地址。而MAC地址是全球唯一的。举例，IP地址就如同是我们居住小区的地址，而MAC地址就是我们住的那栋楼那个房间那个人。IP地址采用的IPv4格式，目前正在向IPv6过渡。

#### 1.5.2 TCP协议（Transmission Control Protocol）

　　TCP（传输控制协议）是面向连接的传输层协议。TCP层是位于IP层之上，应用层之下的中间层。不同主机的应用层之间经常需要可靠的、像管道一样的连接，但是IP层不提供这样的流机制，而是提供不可靠的包交换。TCP协议采用字节流传输数据。

#### 1.5.3 TCP的报文格式

　　TCP报文段包括协议首部和数据两部分，协议首部的固定部分是20个字节，首部的固定部分后面是选项部分。

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1217276-20190504001611594-373661106.jpg)

下面是报文段首部各个字段的含义：

1. **源端口号以及目的端口号**：各占2个字节，端口是传输层和应用层的服务接口，用于寻找发送端和接收端的进程，一般来讲，通过端口号和IP地址，可以唯一确定一个TCP连接，在网络编程中，通常被称为一个socket接口。
2. **序号**：Seq序号，占4个字节、32位。用来标识从TCP发送端向TCP接收端发送的数据字节流。发起方发送数据时对此进行标记。
3. **确认序号**：Ack序号，占4个字节、32位。包含发送确认的一端所期望收到的下一个序号。只有ACK标记位为1时，确认序号字段才有效，因此，确认序号应该是上次已经成功收到数据字节序号加1，即Ack=Seq + 1。
4. **数据偏移**：占4个字节，用于指出TCP首部长度，若不存在选项，则这个值为20字节，数据偏移的最大值为60字节。
5. **保留字段**占6位，暂时可忽略，值全为0。
6. 标志位，6个
   - URG(紧急)：为1时表明紧急指针字段有效
   - ACK(确认)：为1时表明确认号字段有效
   - PSH(推送)：为1时接收方应尽快将这个报文段交给应用层
   - RST(复位)：为1时表明TCP连接出现故障必须重建连接
   - SYN(同步)：在连接建立时用来同步序号
   - FIN(终止)：为1时表明发送端数据发送完毕要求释放连接
7.  **接收窗口：**占2个字节，用于流量控制和拥塞控制，表示当前接收缓冲区的大小。在计算机网络中，通常是用接收方的接收能力的大小来控制发送方的数据发送量。TCP连接的一端根据缓冲区大小确定自己的接收窗口值，告诉对方，使对方可以确定发送数据的字节数。
8. **校验和：**占2个字节，范围包括首部和数据两部分。
9. 选项是可选的，默认情况是不选。

### 1.6 TCP三次握手与四次挥手

​		TCP是面向连接的协议，因此每个TCP连接都有3个阶段：连接建立、数据传送和连接释放。连接建立经历三个步骤，通常称为“三次握手”。

　**TCP三次握手过程**如下：

　　![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1217276-20190503210424740-1764008697.jpg)

1. 第一次握手（客户端发送请求）

　　  客户机发送连接请求报文段到服务器，并进入SYN_SENT状态，等待服务器确认。发送连接请求报文段内容：SYN=1，seq=x；SYN=1意思是一个TCP的SYN标志位置为1的包，指明客户端打算连接的服务器的端口；seq=x表示客户端初始序号x，保存在包头的序列号（Sequence Number）字段里。

2. 第二次握手（服务端回传确认）

　　  服务器收到客户端连接请求报文，如果同意建立连接，向客户机发回确认报文段（ACK）应答，并为该TCP连接分配TCP缓存和变量。服务器发回确认报文段内容：SYN=1，ACK=1，seq=y，ack=x+1；SYN标志位和ACK标志位均为1，同时将确认序号（Acknowledgement Number）设置为客户的ISN加1，即x+1；seq=y为服务端初始序号y。

3. 第三次握手（客户端回传确认）

　　  客户机收到服务器的确认报文段后，向服务器给出确认报文段（ACK），并且也要给该连接分配缓存和变量。此包发送完毕，客户端和服务器进入ESTABLISHED（TCP连接成功）状态，完成三次握手。客户端发回确认报文段内容：ACK=1，seq=x+1，ack=y+1；ACK=1为确认报文段；seq=x+1为客户端序号加1；ack=y+1,为服务器发来的ACK的初始序号字段+1。

　　注意：握手过程中传送的包里不包含数据，三次握手完毕后，客户端与服务器才正式开始传送数据。



　**TCP四次挥手过程**如下：

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1217276-20190503231436105-1355677452.png)

　由于TCP连接是全双工的，因此每个方向都必须单独进行关闭。这原则是当一方完成它的数据发送任务后就能发送一个FIN来终止这个方向的连接。收到一个FIN只意味着这一方向上没有数据流动，一个TCP连接在收到一个FIN后仍能发送数据。首先进行关闭的一方将执行主动关闭，而另一方执行被动关闭。

1. TCP客户端发送一个FIN，用来关闭客户端到服务端的数据传送，客户端进入FIN_WAIT_1状态。发送报文段内容：FIN=1，seq=u；FIN=1表示请求切断连接；seq=u为客户端请求初始序号。

2. 服务端收到这个FIN，它发回一个ACK给客户端，确认序号为收到的序号加1。和SYN一样，一个FIN将占用一个序号；服务端进入CLOSE_WAIT状态。发送报文段内容：ACK=1，seq=v，ack=u+1；ACK=1为确认报文；seq=v为服务器确认初始序号；ack=u+1为客户端初始序号加1。

3. 服务器关闭客户端的连接后，发送一个FIN给客户端，服务端进入LAST_ACK状态。发送报文段内容：FIN=1，ACK=1，seq=w，ack=u+1；FIN=1为请求切断连接，ACK=1为确认报文，seq=w为服务端请求切断初始序号。

4. 客户端收到FIN后，客户端进入TIME_WAIT状态，接着发回一个ACK报文给服务端确认，并将确认序号设置为收到序号加1，服务端进入CLOSED状态，完成四次挥手。发送报文内容：ACK=1，seq=u+1，ack=w+1；ACK=1为确认报文，seq=u+1为客户端初始序号加1，ack=w+1为服务器初始序号加1。

   

> 注意：为什么连接的时候是三次握手，关闭的时候却是四次挥手？
>
> 　　　因为当服务端收到客户端的SYN连接请求报文后，可以直接发送SYN+ACK报文。其中ACK报文是用来应答的，SYN报文是用来同步的。但是关闭连接时，当服务端收到FIN报文时，很可能并不会立即关闭socket，所以只能先回复一个ACK报文，告诉客户端，“你发的FIN报文，我收到了”。只有等到服务端所有的报文都发送完了，我才能发送FIN报文，因此不能一起发送，故需要四步挥手。

### 1.7 UDP协议（User Datagram Protocol）

　UDP，用户数据报协议，它是TCP/IP协议簇中无连接的运输层协议。

1. UDP是一个非连接的协议，传输数据之前源端和终端不建立连接，当它想传送时就简单地去抓取来自应用程序的数据，并尽可能快地把它扔到网络上。在发送端，UDP传送数据的速度仅仅是受应用程序生成数据的速度、计算机的能力和传输带宽的限制；在接收端，UDP把每个消息段放在队列中，应用程序每次从队列中读一个消息段。
2. 由于传输数据不建立连接，因此也就不需要维护连接状态，包括收发状态等，因此一台服务器可同时向多个客户端传输相同的消息。
3. UDP信息包的标题很短，只有8个字节，相对于TCP的20个字节信息包的额外开销很小。
4. 吞吐量不受拥挤控制算法的调节，只受应用软件生成数据的速率、传输带宽、源端和终端主机性能的限制。
5. UDP使用尽量最大努力交付，即不保证可靠交付，因此主机不需要维持复杂的链接状态表。
6. UDP是面向报文的。发送方的UDP对应用程序交下来的报文，在添加首部受就向下交付给IP层。既不拆分，也不合并，而是保留这些报文的边界，因此，应用程序需要选择合适的报文大小。

**UDP协议格式**

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1217276-20190504154900038-1234898266.png)

　UDP协议由两部分组成：首部和数据。其中，首部仅有8个字节，包括源端口和目的端口、长度（UDP用于数据报的长度）、校验和。

### 1.8 TCP与UDP的区别

1. TCP基于连接，UDP是无连接的；
2. 对系统资源的要求，TCP较多，UDP较少；
3. UDP程序结构较简单；
4. TCP是流模式，而UDP是数据报模式；
5. TCP保证数据正确性，而UDP可能丢包；TCP保证数据顺序，而UDP不保证；

### 1.9 HTTP协议（Hypertext Transfer Protocol）

HTTP，超文本传输协议，它是互联网上应用最为广泛的一种网络协议。HTTP是一种应用层协议，它是基于TCP协议之上的请求/响应式的协议。HTTP协议是Web浏览器和Web服务器之间通信的标准协议。HTTP指定客户端与服务器如何建立连接、客户端如何从服务器请求数据，服务器如何响应请求，以及最后如何关闭连接。HTTP连接使用TCP/IP来传输数据。

　　对于从客户端到服务器的每一个请求，都有4个步骤：

1. 默认情况下，客户端在端口80打开与服务器的一个TCP连接，URL中还可以指定其他端口。
2. 客户端向服务器发送消息，请求指定路径上的资源。这个资源包括一个首部，可选地（取决于请求的性质）还可以有一个空行，后面是这个请求的数据。
3. 服务器向客户端发送响应。响应以响应码开头，后面是包含数据的首部、一个空行以及所请求的文档或错误消息。
4. 服务器关闭连接。

　　现在使用的HTTP协议是HTTP/1.1版本，1997年之前采用的是HTTP1.0版本。HTTP连接在1.0版本中采用非持续连接工作方式，1.1版本采用的是持续连接工作方式，持续连接是指服务器在发送响应后仍然在一段时间内保持这条由TCP运输层协议建立起来的连接，使客户端和服务器可以继续在这条连接上传输HTTP报文。

　　是否采用持续连接工作方式，1.0中默认是关闭的，需要在HTTP头加入“Connection:Keep-Alive”，才能启用Keep-Alive。HTTP1.1中默认启用Keep-Alive，如果加入“Connection:close”，才关闭。目前大部分浏览器都是用HTTP1.1协议，也就是说默认都会发起Keep-Alive的连接请求了，所以是否能完成一个完整的Keep-Alive连接就看服务器设置情况。

### 1.10 HTTP和HTTPS的区别

HTTPS（全称：Hyper Text Transfer Protocol over Secure Socket Layer），是以安全为目标的HTTP通道，简单来说就是HTTP的安全版。即HTTP下加入SSL层，HTTPS的安全基础是SSL，因此加密的详细内容就需要SSL。它是一个URL scheme（抽象标识符体系），句法类同http:体系，用于安全的HTTP数据传输。https:URL表明它使用了HTTP，但HTTPS存在不同于HTTP的默认端口及一个加密/身份验证层（在HTTP与TCP之间）。

　　超文本传输协议HTTP协议被用于在Web浏览器和网站服务器之间传递信息。HTTP协议以明文方式发送内容，不提供任何方式的数据加密，如果攻击者截取了Web浏览器和网站服务器之间的传输报文，就可以直接读懂其中的信息，因此HTTP协议不适合传输一些敏感信息，比如信用开号、密码等。

　　为了解决HTTP协议的这一缺陷，需要使用另一种协议：安全套接字层超文本传输协议HTTPS。为了数据传输的安全，HTTPS在HTTP的基础上加入了SSL协议，SSL依靠证书来验证服务器的身份，并为浏览器和服务器之间的通信加密。

　　HTTPS和HTTP的区别主要为以下四点：

- https协议需要到ca申请证书，一般免费证书很少，需要缴费。
- http是超文本传输协议，信息是明文传输，https则是具有安全性的ssl加密传输协议。
- http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。
- http的连接很简单，是无状态的；https协议是有ssl+http协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。

### 1.11 HTTP和TCP/IP协议的关系

网络中有一段比较容易理解的介绍：

　　“我们在传输数据时，可以只使用（传输层）TCP/IP协议，但是那样的话，如果没有应用层，便无法识别数据内容，如果想要使传输的数据有意义，则必须使用到应用层协议，应用层协议有很多，比如HTTP、FTP、TELNET等，也可以自己定义应用层协议。WEB使用HTTP协议作应用层协议，以封装HTTP文本信息，然后使用TCP/IP做传输层协议将它发到网络上。”

## 2. Java 网络编程

### 2.1 Socket概述

​	Java的网络编程主要涉及到的内容是Socket编程。Socket，套接字，就是两台主机之间逻辑连接的端点。TCP/IP协议是传输层协议，主要解决数据如何在网络中传输，而HTTP是应用层协议，主要解决如何包装数据。Socket是通信的基石，是支持TCP/IP协议的网络通信的基本操作单元。它是网络通信过程中端点的抽象表示，包含进行网络通信必须的五种信息：连接使用的协议、本地主机的IP地址、本地进程的协议端口、远程主机的IP地址、远程进程的协议端口。

　　应用层通过传输层进行数据通信时，TCP会遇到同时为多个应用程序进程提供并发服务的问题。多个TCP连接或多个应用程序进程可能需要通过同一个TCP协议端口传输数据。为了区别不同的应用程序进程和连接，许多计算机操作系统为应用程序与TCP/IP协议交互提供了套接字（Socket）接口。应用层可以和传输层通过Socket接口，区分来自不同应用程序进程或网络连接的通信，实现数据传输的并发服务。

　　Socket，实际上是对TCP/IP协议的封装，Socket本身并不是协议，而是一个调用接口（API），通过Socket，我们才能使用TCP/IP协议。实际上，Socket跟TCP/IP协议没有必然的关系，Socket编程接口在设计的时候，就希望也能适应其他的网络协议。所以说，Socket的出现，只是使得程序员更方便地使用TCP/IP协议栈而已，是对TCP/IP协议的抽象，从而形成了我们知道的一些最基本的函数接口，比如create、listen、accept、send、read和write等等。网络有一段关于socket和TCP/IP协议关系的说法比较容易理解：

　　“TCP/IP只是一个协议栈，就像操作系统的运行机制一样，必须要具体实现，同时还要提供对外的操作接口。这个就像操作系统会提供标准的编程接口，比如win32编程接口一样，TCP/IP也要提供可供程序员做网络开发所用的接口，这就是Socket编程接口。” 

 　实际上，传输层的TCP是基于网络层的IP协议的，而应用层的HTTP协议又是基于传输层的TCP协议的，而Socket本身不算是协议，就像上面所说，它只是提供了一个针对TCP或者UDP编程的接口。socket是对端口通信开发的工具,它要更底层一些。

### 2.2 Socket 整体流程

​	Socket编程主要涉及到客户端和服务端两个方面，首先是在服务器端创建一个服务器套接字（ServerSocket），并把它附加到一个端口上，服务器从这个端口监听连接。端口号的范围是0到65536，但是0到1024是为特权服务保留的端口号，我们可以选择任意一个当前没有被其他进程使用的端口。

　　客户端请求与服务器进行连接的时候，根据服务器的域名或者IP地址，加上端口号，打开一个套接字。当服务器接受连接后，服务器和客户端之间的通信就像输入输出流一样进行操作。

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1217276-20190505145914692-1580218673.png)

### 2.3 InetAddress 类

```java
package com.kun.api;

import java.net.InetAddress;
import java.net.UnknownHostException;

/**
 * InetAddress的使用
 */
public class InetAddressDemo {
    public static void main(String[] args) throws UnknownHostException {
        //获取本机的InetAddress对象
        InetAddress localHost = InetAddress.getLocalHost();
        System.out.println(localHost);

        //根据指定主机名 获取InetAddress对象
        InetAddress localHost1 = InetAddress.getByName("LAPTOP-PRHA00NF");
        System.out.println(localHost1);

        //根据域名返回
        InetAddress host = InetAddress.getByName("www.baidu.com");
        System.out.println(host);
        String hostAddress = host.getHostAddress();

        System.out.println("host对应的ip："+hostAddress+"，主机名："+host.getHostName());
    }
}
```

### 2.4 TCP 通信例子

#### demo1：单向通信

```java
package com.kun.socket;

import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class TcpServer01 {

    public static void main(String[] args) throws IOException {
        //1.在本机的9999端口监听，等待连接
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("服务端，在9999端口监听，等待连接。。。");
        //2.当没有客户端连接9999端口时，程序阻塞，等待连接
        //  如果有客户端连接，返回Socket对象，程序继续
        Socket socket = serverSocket.accept();
        System.out.println("socket = "+ socket.getClass());
        
        //3.通过socket.getInputStream()读取客户端写入到数据通道的数据
        InputStream inputStream = socket.getInputStream();
        //4.IO读取
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1){
            System.out.println(new String(buf,0,readLen));
        }

        //5.关闭流对象和socket
        inputStream.close();
        socket.close();
        serverSocket.close();
    }
}
```

```java
package com.kun.socket;

import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;
import java.net.UnknownHostException;

public class TcpClient01 {
    public static void main(String[] args) throws IOException {
        //1.连接服务器（ip + 端口）
        Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("客户端 socket返回："+socket.getClass());
        //2.连接成功，生成socket,通过socket.getOutputStream()得到和socket相关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        //3.通过输出流，写入数据到数据通道
        outputStream.write("hello server".getBytes());
        //设置结束标记
        socket.shutdownOutput();
        //4.关闭流对象和socket
        outputStream.close();
        socket.close();
        System.out.println("客户端退出。");
    }
}
```

#### demo2：双向通信

```java
package com.kun.socket;

import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class TcpServer02 {

    public static void main(String[] args) throws IOException {
        //1.在本机的9999端口监听，等待连接
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("服务端，在9999端口监听，等待连接。。。");
        //2.当没有客户端连接9999端口时，程序阻塞，等待连接
        //  如果有客户端连接，返回Socket对象，程序继续
        Socket socket = serverSocket.accept();
        System.out.println("socket = "+ socket.getClass());
        
        //3.通过socket.getInputStream()读取客户端写入到数据通道的数据
        InputStream inputStream = socket.getInputStream();
        //4.IO读取
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1){
            System.out.println(new String(buf,0,readLen));
        }
        //5.获取socket相关的输出流
        OutputStream outputStream = socket.getOutputStream();
        outputStream.write("hello too, client".getBytes());
        socket.shutdownOutput();

        //6.关闭流对象和socket
        outputStream.close();
        inputStream.close();
        socket.close();
        serverSocket.close();

    }

}
```

```java
package com.kun.socket;

import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;

public class TcpClient02 {
    public static void main(String[] args) throws IOException {
        //1.连接服务器（ip + 端口）
        Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("客户端 socket返回："+socket.getClass());
        //2.连接成功，生成socket,通过socket.getOutputStream()得到和socket相关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        //3.通过输出流，写入数据到数据通道
        outputStream.write("hello server".getBytes());
        //设置结束标记
        socket.shutdownOutput();
        //4.获取socket相关联的输入流对象，读取数据
        InputStream inputStream = socket.getInputStream();
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1){
            System.out.println(new String(buf,0,readLen));
        }
        //5.关闭流对象和socket
        inputStream.close();
        outputStream.close();
        socket.close();
        System.out.println("客户端退出。");
    }
}
```

#### demo3：双向通信（使用字符流）

```java
package com.kun.socket;

import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class TcpServer03 {

    public static void main(String[] args) throws IOException {
        //1.在本机的9999端口监听，等待连接
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("服务端，在9999端口监听，等待连接。。。");
        //2.当没有客户端连接9999端口时，程序阻塞，等待连接
        //  如果有客户端连接，返回Socket对象，程序继续
        Socket socket = serverSocket.accept();
        System.out.println("socket = "+ socket.getClass());
        
        //3.通过socket.getInputStream()读取客户端写入到数据通道的数据
        InputStream inputStream = socket.getInputStream();
        //4.IO读取,使用字符流
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
        String s = bufferedReader.readLine();
        System.out.println(s);

        //5.获取socket相关的输出流
        OutputStream outputStream = socket.getOutputStream();
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream));
        bufferedWriter.write("hello too,client by writer.");
        bufferedWriter.newLine();  //插入一个换行表示写数据结束
        bufferedWriter.flush();  //手动刷新

        //6.关闭流对象和socket
        bufferedReader.close();
        bufferedWriter.close();
        socket.close();
        serverSocket.close();
    }
}
```

```java
package com.kun.socket;

import java.io.*;
import java.net.InetAddress;
import java.net.Socket;

public class TcpClient03 {
    public static void main(String[] args) throws IOException {
        //1.连接服务器（ip + 端口）
        Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("客户端 socket返回："+socket.getClass());
        //2.连接成功，生成socket,通过socket.getOutputStream()得到和socket相关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        //3.通过输出流，写入数据到数据通道
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream));
        bufferedWriter.write("hello server 字符流");
        bufferedWriter.newLine(); //插入一个换行符表示写入内容的结束，要求对方使用readLine()
        bufferedWriter.flush(); //字符流需要手动刷新

        //4.获取socket相关联的输入流对象，读取数据
        InputStream inputStream = socket.getInputStream();
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
        String s = bufferedReader.readLine();
        System.out.println(s);

        //5.关闭流对象和socket
        bufferedReader.close();
        bufferedWriter.close();
        socket.close();
        System.out.println("客户端退出。");
    }
}
```

#### demo4：TCP实现文件上传

服务器端：

​		编写一个服务器端程序，用来接收图片。创建一个监听指定端口号的ServerSocket服务端对象，在while(true)无限循环中持续调用ServerSocket的accept()方法来接收客户端的请求，每当和一个客户端建立连接后，就开启一个新的线程和这个客户端进行交互。在处理文件上传功能的ServerThread线程管理类中，先进行客户端文件上传保存处理，确定了文件保存目录和文件命名方式，然后进行保存处理，最后又通过客户端输出流，向客户端输出“上传成功”的信息进行响应。从运行结果可以看出，服务器端进入阻塞状态，等待客户端连接。

```java
package com.kun.tcpupload;

import java.io.File;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

class ServerThread implements Runnable {
    private Socket socket;
    public ServerThread(Socket socket) {
        this.socket = socket;
    }
    public void run() {
        String ip = socket.getInetAddress().getHostAddress();
        int count = 1;
        try {
            File parentFile = new File("NetDemo\\src\\com\\kun\\tcpupload\\");
            if (!parentFile.exists()) {
                parentFile.mkdir();
            }
            File file = new File(parentFile, ip + "(" + count + ").jpg");
            while  (file.exists()) {
                file = new File(parentFile, ip + "(" + (count++) + ").jpg");
            }
            InputStream in = socket.getInputStream();
            FileOutputStream fos = new FileOutputStream(file);
            byte[] buf = new byte[1024];
            int len = 0;
            while ((len = in.read(buf)) != -1) {
                fos.write(buf, 0, len);
            }
            OutputStream out = socket.getOutputStream();
            out.write("上传成功".getBytes());
            in.close();
            fos.close();
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

public class UploadTcpServer {
    public static void main(String[] args) throws Exception {
        @SuppressWarnings("resource")
        ServerSocket serverSocket = new ServerSocket(10001);
        while (true) {
            Socket client = serverSocket.accept();
            new Thread(new ServerThread(client)).start();
        }
    }
}
```

客户端：	

  	创建了Socket对象，指定连接服务器的IP地址和端口号，然后分别通过Socket的输出流对象向服务端上传图片和输入流对象获取服务端响应信息。其中，向服务端上传的源图片地址为D:\\Test\\a.jpg,即D盘根目录下的a.jpg图片，在上传之前一定要确保图片存在。另外，在向服务端上传完毕图片后要调用Socket的shutDownOutput()方法。关闭客户端的输出流。

```java
package com.kun.tcpupload;
import java.io.FileInputStream;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;

public class UploadTcpClient {
    public static void main(String[] args) throws Exception {
        Socket client = new Socket(InetAddress.getLocalHost(),10001);
        OutputStream out = client.getOutputStream();
        FileInputStream fis = new FileInputStream("D:\\Test\\a.jpg");
        byte[] buf = new byte[1024];
        int len= 0;
        System.out.println("连接到服务器端，开始文件上传！");
        while ((len = fis.read(buf)) != -1) {
            out.write(buf, 0, len);
        }
        client.shutdownOutput();
        InputStream is = client.getInputStream();
        byte[] bufMsg= new byte[1024];
        int len2 = is.read(bufMsg);
        while (len2 != -1){
            System.out.println(new String(bufMsg, 0, len2));
            len2 = is.read(bufMsg);
        }
        out.close();
        is.close();
        fis.close();
        client.close();
    }
}
```

上传成功：

![image-20210521170607758](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210521170607758.png)



### 2.5 UDP 通信的例子

**UDP简介：**

- UDP协议的全称是用户数据报，在网络中它与TCP协议一样用于处理数据报。在OSI模型中，UDP位于第四层——传输层，处于IP协议额上一层。UDP有不提供数据报分组、组装以及不能对数据报排序的缺点。当报文发送之后，是无法得知其是否安全完整到达的。

- 由于UDP不属于连接性协议的特性，因此具有资源消耗小、处理速度快的优点，所以通过音频、视频和普通数据在传送时使用UDP较多，因为它们即使偶尔丢失一两个数据包，也不会对接收结果产生太大影响。

- 使用java.net包下的DatagramSocket和DatagramPacket类，可以非常方便地控制用户数据报文。下面就对这两个类进行案例介绍

  **DatagramPacket**
  	表示数据报包，用来实现无连接的包的投递服务。这些数据包选择不同的路由，经过计算机的存储转发，最终到达目的计算机。所以到达的数据包和发送时的顺序不一定会相同。

> 利用UDP通信功能，用DatagramPacket类与DatagramSocket类的常用方法，模拟实现一个功能完善的聊天程序。

#### demo1：UDP双向通信

```java
package com.kun.udp;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

/**
 * UDP服务器端
 */
public class UdpServer01 {
    public static void main(String[] args) throws IOException {
        /*
         * 接收客户端发送的数据
         */
        // 1.创建服务器端DatagramSocket，指定端口
        DatagramSocket socket = new DatagramSocket(8800);
        // 2.创建数据报，用于接收客户端发送的数据
        byte[] data = new byte[1024];// 创建字节数组，指定接收的数据包的大小
        DatagramPacket packet = new DatagramPacket(data, data.length);
        // 3.接收客户端发送的数据
        System.out.println("****服务器端已经启动，等待客户端发送数据");
        socket.receive(packet);// 此方法在接收到数据报之前会一直阻塞
        // 4.读取数据
        String info = new String(data, 0, packet.getLength());
        System.out.println("我是服务器，客户端说：" + info);

        /*
         * 向客户端响应数据
         */
        // 1.定义客户端的地址、端口号、数据
        InetAddress address = packet.getAddress();
        int port = packet.getPort();
        byte[] data2 = "欢迎您!".getBytes();
        // 2.创建数据报，包含响应的数据信息
        DatagramPacket packet2 = new DatagramPacket(data2, data2.length, address, port);
        // 3.响应客户端
        socket.send(packet2);
        // 4.关闭资源
        socket.close();
    }
}
```

```java
package com.kun.udp;
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

/*
 * 客户端
 */
public class UdpClient01 {
    public static void main(String[] args) throws IOException {
        /*
         * 向服务器端发送数据
         */
        // 1.定义服务器的地址、端口号、数据
        InetAddress address = InetAddress.getByName("localhost");
        int port = 8800;
        byte[] data = "用户名：admin;密码：123".getBytes();
        // 2.创建数据报，包含发送的数据信息
        DatagramPacket packet = new DatagramPacket(data, data.length, address, port);
        // 3.创建DatagramSocket对象
        DatagramSocket socket = new DatagramSocket();
        // 4.向服务器端发送数据报
        socket.send(packet);

        /*
         * 接收服务器端响应的数据
         */
        // 1.创建数据报，用于接收服务器端响应的数据
        byte[] data2 = new byte[1024];
        DatagramPacket packet2 = new DatagramPacket(data2, data2.length);
        // 2.接收服务器响应的数据
        socket.receive(packet2);
        // 3.读取数据
        String reply = new String(data2, 0, packet2.getLength());
        System.out.println("我是客户端，服务器说：" + reply);
        // 4.关闭资源
        socket.close();
    }
}
```

#### demo2：UDP聊天室

1. 实现聊天窗口界面，首先创建两个名称为ChatRoom1和ChatRoom2的程序入口类,在该类的main()方法中获取当前服务所在端口号、聊天对象服务所在端口号,并创建DatagramSocket信息收发对象,以及通过多线程实现发送端和接收端功能,如下图所示：

```java
package com.kun.udp.chat;

import java.net.DatagramSocket;
import java.net.SocketException;
import java.util.Scanner;

/**
 * 实现聊天窗口界面，首先创建一个名称为ChatRoom的程序入口类,
 * 在该类的main()方法中获取当前服务所在端口号、聊天对象服务所在端口号,
 * 并创建DatagramSocket信息收发对象,以及通过多线程实现发送端和接收端功能
 */
public class ChatRoom1 {
    public static void main(String[] args) {
        @SuppressWarnings("resource")
        Scanner sc = new Scanner(System.in);
        System.out.print("请输入聊天服务当前启动端口号：");
        int serverPort = sc.nextInt();
        System.out.print("请输入聊天服务发送信息对象的目标端口号：");
        int targetPort = sc.nextInt();
        System.out.println("聊天系统初始化完成并启动！！！");
        try {
            DatagramSocket socket = new DatagramSocket(serverPort);
            new Thread(new ChatReceiver(socket), "接收服务").start();
            new Thread(new ChatSend(socket,targetPort),"发送服务").start();
        } catch (SocketException e) {
            e.printStackTrace();
        }
    }
}
```

```java
package com.kun.udp.chat;

import java.net.DatagramSocket;
import java.net.SocketException;
import java.util.Scanner;

/**
 * 实现聊天窗口界面，首先创建一个名称为ChatRoom的程序入口类,
 * 在该类的main()方法中获取当前服务所在端口号、聊天对象服务所在端口号,
 * 并创建DatagramSocket信息收发对象,以及通过多线程实现发送端和接收端功能
 */
public class ChatRoom2 {
    public static void main(String[] args) {
        @SuppressWarnings("resource")
        Scanner sc = new Scanner(System.in);
        System.out.print("请输入聊天服务当前启动端口号：");
        int serverPort = sc.nextInt();
        System.out.print("请输入聊天服务发送信息对象的目标端口号：");
        int targetPort = sc.nextInt();
        System.out.println("聊天系统初始化完成并启动！！！");
        try {
            DatagramSocket socket = new DatagramSocket(serverPort);
            new Thread(new ChatReceiver(socket), "接收服务").start();
            new Thread(new ChatSend(socket,targetPort),"发送服务").start();
        } catch (SocketException e) {
            e.printStackTrace();
        }
    }
}
```

2. 实现聊天程序发送信息功能。创建一个ChatSend类，作为聊天程序的发送端，用于向指定的聊天程序发送聊天信息。具体如下图：

```java
package com.kun.udp.chat;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.util.Scanner;

/**
 * 实现聊天程序发送信息功能
 */
public class ChatSend implements Runnable {
    private DatagramSocket client;
    private int targetPort;
    public ChatSend(DatagramSocket client,int targetPort) {
        this.client = client;
        this.targetPort = targetPort;
    }
    public void run() {
        try {
            @SuppressWarnings("resource")
            Scanner sc = new Scanner(System.in);
            while (true) {
                String data = sc.nextLine();
                byte[] buf = data.getBytes();
                DatagramPacket packet = new DatagramPacket(buf, buf.length,
                        InetAddress.getByName("127.0.0.255"),targetPort);
                client.send(packet);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

3. 实现聊天程序接收信息功能。创建一个ChatReceiver类作为聊天程序的接收端，用于接收其他用户发送的聊天信息。如下图所示:

```java
package com.kun.udp.chat;

import java.net.DatagramPacket;
import java.net.DatagramSocket;

/**
 * 实现聊天程序接收信息功能
 */
public class ChatReceiver implements Runnable {
    private DatagramSocket server;
    public ChatReceiver(DatagramSocket server) {
        this.server = server;
    }
    public void run() {
        try {
            byte[] buf = new byte[1024];
            DatagramPacket packet = new DatagramPacket(buf, buf.length);
            while (true) {
                server.receive(packet);
                String str = new String(packet.getData(), 0, packet.getLength());
                System.out.println("收到" + packet.getAddress()+":"+packet.getPort()+ " 发送的数据:" + str);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

分别启动ChatRoom1和ChatRoom2，运行结果如下：

![image-20210521172117519](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210521172117519.png)![image-20210521172129286](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210521172129286.png)

## 📚 References

- https://www.cnblogs.com/gh110/p/12158125.html
- https://blog.csdn.net/weixin_42882887/article/details/86598410

  

