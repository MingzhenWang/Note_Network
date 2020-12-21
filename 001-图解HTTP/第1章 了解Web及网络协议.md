## 第1章 了解Web及网络基础

#### 目录

##### [1.1 使用HTTP访问Web](#anchor11)

##### [1.2 HTTP的诞生](#anchor12)
###### &ensp;&ensp;[1.2.1 为知识共享而规划Web](#anchor121)
###### &ensp;&ensp;[1.2.2 Web成长时代](#anchor122)
###### &ensp;&ensp;[1.2.3 驻足不前的HTTP](#anchor123)

##### [1.3 网络基础TCP/IP](#anchor13)
###### &ensp;&ensp;[1.3.1 TCP/IP协议族](#anchor131)
###### &ensp;&ensp;[1.3.2 TCP/IP的分层管理](#anchor132)
###### &ensp;&ensp;[1.3.3 TCP/IP的通信传输流](#anchor133)

##### [1.4 IP、TCP和DNS](#anchor14)
###### &ensp;&ensp;[1.4.1 负责传输的IP协议](#anchor141)
###### &ensp;&ensp;[1.4.2 确保可靠性的TCP协议](#anchor142)
###### &ensp;&ensp;[1.4.3 负责域名解析的DNS服务](#anchor143)

##### [1.5 各种协议与HTTP协议的关系](#anchor15)

##### [1.6 URI和URL](#anchor16)
###### &ensp;&ensp;[1.6.1 统一资源标识符](#anchor161)
###### &ensp;&ensp;[1.6.2 URI格式](#anchor162)


### <span id="anchor11">1.1 使用HTTP访问Web<span>
根据Web浏览器地址栏中指定的URL，Web浏览器从Web服务器端获取文件资源（resource）等信息，从而显示出Web页面。
**客户端（client）**：通过发送请求获取服务器资源的Web浏览器等
* Web使用HTTP协议作为规范，完成从客户端到服务器端的运作流程。
* HTTP协议：**HyperText Transfer Protocol**，超文本传输协议（超文本转移协议）
* Web是建议在HTTP协议上通信的
### <span id="anchor12">1.2 HTTP的诞生</span>
#### <span id="anchor121">1.2.1 为知识共享而规划Web<span>
1989年3月，互联网还只属于少数人，HTTP诞生了

* **CERN**（欧洲核子研究组织）的蒂姆·伯纳斯-李博士提出了一种能让**远隔两地的研究者们共享知识的设想**
* 最初的设想：借助多文档之间相互关联形成的超文本（HyperText），连成可相互参阅的WWW（World Wide Web，万维网）

##### 现在已经提出了3项WWW构建技术
* **HTML**：把SGML作为页面的文本标记语言
  * SGML：标准通用标记语言，Standard Generalized Markup Language
  * HTML：超文本标记语言，HyperText Markup Language
* **HTTP**：作为文档传递协议
* **URL**：指定文档所在地址
  * URL：统一资源定位符，Uniform Resource Locator

WWW：是Web浏览器当年用来浏览超文本的客户端应用程序的名称
现在用来表示这一系列的集合，也可简称Web。

#### <span id="anchor122">1.2.2 Web成长时代</span>
* **1990年11月**，CERN成功研发了世界上第一台Web服务器和Web浏览器
* **1990年**，针对HTML1.0草案进行了讨论，因存在多处模糊不清的部分，草案被直接废弃
  * HTML1.0：https://www.w3.org/MarkUp/draft-ietf-iiir-html-01.txt
* **1993年**，现代浏览器的祖先NCSA研发的Mosaic问世
  * NCSA：National Center for Supercomputer Applications，美国国家超级计算机应用中心
  * 以in-line（内联）等形式显示HTML图像，以此为优势流行起来
* **1993年秋**，Mosaic的Windows版和Macintosh版面世
  * 使用CGI技术的NCSA Web服务器、NCSA HTTPd 1.0基本同时期出现
  * NCSA Mosaic bounce page：http://archive.ncsa.illinois.edu/mosaic.html
  * The NCSA HTTPd Home Page（存档）：http://web.archive.org/web/20090426182129/http://hoohoo.ncsa.illinois.edu/
* **1994年12月**，网景通信公司发布Netscape Navigator 1.0
* **1995年**，微软公司发布Internet Explorer 1.0和2.0
* **紧接着**，Apache 0.2发布，HTML发布2.0版本
* **1995年起**，微软和网景，浏览器大战爆发，对Web标准化视而不见
* **2000年前后**，浏览器战争随网景公司衰落暂告一段落
* **2004年**，Mozilla基金会发布Firefox浏览器，第二次浏览器大战爆发
* **至今**，Internet Explorer 浏览器的版本从 6 升到 7 前后花费了 5 年时间。之后接连不断地发布了 8、9、10 版本。另外，Chrome、Opera、Safari 等浏览器也纷纷抢占市场份额。

#### <span id="anchor123">1.2.3 驻足不前的HTTP</span>
* **HTTP/0.9**
  * HTTP问世于1990年，并没有作为正式的标准被建立，这时的HTTP含有1.0之前版本的意思，因此成为0.9
* **HTTP/1.0**
  * 1996年5月，HTTP正式作为标准公布，该版本被命名为HTTP/1.0，并记载于RFC1945，该初期版本至今仍被广泛使用
  * RFC1945 - Hypertext Transfer Protocol -- HTTP/1.0
    * http://www.ietf.org/rfc/rfc1945.txt
* **HTTP/1.1**
  * 1997年1月，发布1.1，是目前的主流版本，当初的标准是RFC2068，之后发布的修订版RFC2616是当前最新版
  * RFC2616 - Hypertext Transfer Protocol -- HTTP/1.1
    * https://www.ietf.org/rfc/rfc2616.txt
* **HTTP/2.0**
  * 新一代2.0正在制订中，要达到较高的使用率，还需一段时间

##### 总结
HTTP协议的出现：主要是为了解决文本传输的难题。
由于协议本身非常简单，于是在此基础上设想了很多应用方法并投入了实际使用。
现在HTTP协议已经超出了Web这个框架的局限，被运用到了各个场景中

### <span id="anchor13">1.3 网络基础TCP/IP</span>
为了理解HTTP，我们需要事先了解下**TCP/IP协议族**
网络（包括互联网）是在TCP/IP协议族的基础上运作的，**HTTP属于它内部的一个子集**

#### <span id="anchor131">1.3.1 TCP/IP协议族</span>
计算机与网络设备要相互通信，双方必须基于相同的方法，比如
* 如何检测到通信目标
* 由哪一边先发起通信
* 使用哪种语言进行通信
* 怎样结束通信等

**协议（Protocol）**：不同的硬件、操作系统之间的通信，所有的一切都需要一种规则，即**协议**

##### TCP/IP有几种不同的理解
**1. TCP/IP是互联网相关的各类协议族的总称**
![](/001-图解HTTP/Pictures/1310.png)
协议中存在各式各样的内容，比如：
  * 从电缆的规格到IP地址的选定方法
  * 寻找异地用户的方法
  * 双方建立通信的顺序
  * Web页面显示需要处理的步骤，等

**2. TCP/IP是指TCP和IP两种协议**
**3. TCP/IP是在IP协议通信过程中，使用到的协议族的总称**

#### <span id="anchor132">1.3.2 TCP/IP的分层管理</span>
TCP/IP协议族里重要的一点就是分层，按层次分为以下四层
* 应用层
* 传输层
* 网络层
* 数据链路层

##### 1. 层次化的优势
* 修改的代价小
  * 如果只由一个协议统筹，某个地方需要改变设计时，必须把所有部分整体替换掉；分层之后只需把变动的层替换掉即可。各层之间的接口部分规划好之后，每个层的设计即可自由变动
* 设计相对简单
  * 各层只要考虑自己该做的事
    * 处于应用层上的应用可以只考虑分派给自己的任务，而不需要弄清对方在地球上哪个地方、对方的传输路线是怎样的、是否能确保传输送达等问题。
##### 2. 各层的作用
* **应用层**
  * 应用层决定了向用户**提供应用服务时通信**的活动
  * TCP/IP协议族中预存了各类通用的应用服务，比如：
    * **FTP**：文件传输协议，File Transfer Protocol
    * **DNS**：域名系统，，Domain Name System
    * **HTTP：该协议处于应用层**
* **传输层**
  * 传输层对上层应用层，提供处于网络连接中的两台计算机之间的数据传输
  * 在传输层有两个性质不同的协议：
    * **TCP**：传输控制协议，Transmission Control Protocol
    * **UDP**：用户数据报协议，User Data Protocol
* **网络层（网络互连层）**
  * 网络层用来处理在**网络上流动的数据包**，数据包是网络传输的最小单位
  * 该层规定了通过怎样的**传输路线**到达对方计算机，并把数据包传送给对方
  * 与对方计算机之间通过多台计算机或网络设备进行传输时，**网络层的作用**就是在众多选项中选择一条**传输路线**
* **链路层（数据链路层、网络接口层）**
  * **用来处理连接网络的硬件部分**
  * 包括控制操作系统、硬件的设备驱动、NIC（Network Internet Card，网络适配器即网卡）、及光纤等物理可见部分（还包括连接器等一切传输媒介）。**硬件上的范畴均在链路层的作用范围内**

#### <span id="anchor133">1.3.3 TCP/IP的通信传输流</span>
![](/001-图解HTTP/Pictures/1331.png)

利用TCP/IP协议族进行网络通信时，会通过分层顺序与对方进行通信。
以HTTP为例：
* 首先，作为发送端的客户端在应用层（HTTP协议）发出一个想看某个Web页面的HTTP请求
* 接着，为了传输方便，在传输层（TCP）把从应用层收到的数据（HTTP请求报文）进行分割，并在各个报文上打上**标记序号及端口号**后转发给网络层
* 在网络层（IP协议），增加作为**通信目的地**的MAC地址后，转发给链路层
* 发送网络的通信请求准备完成
* 接收端的服务器在链路层接收到数据，按序发送到上层，一直到应用层；传输到应用层，真正接收到由客户端发送的HTTP请求

![](/001-图解HTTP/Pictures/1332.png)

**发送端**在层与层之间传递数据时，每经过一层，会被打上一个**该层所属的首部信息**
**接收端**在层与层之间传递数据时，没经过一层，会**把对应的首部去掉**

**封装**：encapsulate，把数据信心包装起来的做法

### <span id="anchor14">1.4 IP、TCP和DNS</span>

下面针对在TCP/IP 协议族中与HTTP密不可分的3个协议进行说明

#### <span id="anchor141">1.4.1 负责传输的IP协议</span>
* IP（Internet Protocol）网际协议位于**网络层**
##### （1）IP协议的作用：把各种数据包传送给对方
要确保传送到对方那里，需要满足各种条件，两个重要的条件如下：
**IP地址**和M**AC地址**（Media Access Control Address，媒体存取控制地址，局域网地址）

##### （2）使用ARP协议凭借MAC地址进行通信
> ARP协议：Address Resolution Protocol，地址解析协议，可以根据通信方IP反查出对应MAC地址

* IP间的通信依赖于MAC地址
* 通信双方在同一局域网的情况很少，通常是通过多台计算机和网络设备中转才能连接到对方
* 中转时，使用ARP协议解析IP地址，以获取下一站中转设备的MAC地址

##### （3）路由选择（routing）
* 在到达通信目标前的中转过程，计算机和路由器等网络设备只能获悉很粗略的传输路线
* 计算机或者网络设备无法全面掌握互联网中的细节

![](/001-图解HTTP/Pictures/1410.png)


#### <span id="anchor142">1.4.2 确保可靠性的TCP协议</span>
* TCP协议位于**传输层**，提供可靠的字节流服务

##### （1）字节流服务（Byte Stream Service）
为了方便传输，将**大块的数据**分割成以**报文段为单位的数据包**进行管理。
* 可靠的传输服务：可以把数据准确可靠地传送给对方
* TCP 协议能够确认数据最终是否送达到对方。

##### （2）确认数据最终是否送达到对方
为了准确无误地将数据送达目标处，TCP协议采用了**三次握手策略（three-way handshaking）**
握手过程中使用了TCP的标志：SYN（synchronize）和ACK（acknowledgement）

* 发送端首先发送一个带有SYN标志的数据包给对方
* 接收端收到后，回传一个带有SYN/ACk标志的数据包以示传达确认信息
* 最后，发送端再回传一个带ACK标志的数据包，代表握手结束
* 若在握手过程中某个阶段莫名中断，TCP 协议会再次以相同的顺序发
送相同的数据包。

![](/001-图解HTTP/Pictures/1420.png)


#### <span id="anchor143">1.4.3 负责域名解析的DNS服务</span>
* DNS(Domain Name System)服务位于应用层，提供域名到IP地址之间的解析服务

* 计算机可以被赋予IP地址、主机名和域名

* 用户通常使用主机名或域名来访问对方的计算机，因为相比IP，更容易理解
* 但是让计算机去理解名称，相对变得困难

* 为了解决上述问题，DNS服务应运而生
* DNS协议可以**通过域名查找IP地址**，也可以**通过IP地址反查域名**

![](/001-图解HTTP/Pictures/1430.png)

### <span id="anchor15">1.5 各种协议与HTTP协议的关系</span>
![](/001-图解HTTP/Pictures/1501.png)
![](/001-图解HTTP/Pictures/1502.png)

### <span id="anchor16">1.6 URI和URL</span>
* URL：统一资源定位符，Uniform Resource Locator
* URI：统一资源标识符
#### <span id="anchor161">1.6.1 统一资源标识符</span>
URI是Uniform Resource Identifier的缩写，RFC2396分别对三个单词做了如下定义：

* **Uniform（统一的格式）**
  * 方便处理多种不同类型的资源
  * 加入新增的协议方案也更容易（如http：、ftp：）
* **Resource(资源，可标识的任何东西)**
  * 能够区别于其他类型的，全都可作为资源（如图像）
  * 资源可以是单一的或者多数的集合体
* **Identifier（标识符，标识可标识的对象）**

##### （1）URI定义
> 由**某个协议方案**表示的**资源**的**定位标识符**

##### （2）协议方案
* 采用HTTP时，协议方案就是HTTP。除此之外，还有ftp、mailto、telnet、file等
* 标准的URI协议方案有30种左右，由隶属于国际互联网资源管理的非营利社团 ICANN的IANA管理颁布
>ICANN：互联网名称与数字地址分配机构，Internet Corporation forAssigned Names and Numbers
>IANA：互联网号码分配局，Internet Assigned Numbers Authority
>IANA - Uniform Resource Identifier (URI) SCHEMES（统一资源标识符方案）
>>http://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml

##### （3）URI和URL的区别、联系
* **URI**用**字符串标识某一互联网资源**，**URL**表示**资源的地点**（互联网上所处的位置）
* URL是URI的子集，**URL就是用定位的方式实现的URI**。

【RFC3986：统一资源标识符（URI）通用语法】中列举了几种 URI 例子，如下所示：
```text
ftp://ftp.is.co.za/rfc/rfc1808.txt
http://www.ietf.org/rfc/rfc2396.txt
ldap://[2001:db8::7]/c=GB?objectClass?one
mailto:John.Doe@example.com
news:comp.infosystems.www.servers.unix
tel:+1-816-555-1212
telnet://192.0.2.16:80/
urn:oasis:names:specification:docbook:dtd:xml:4.1.2
```

#### <span id="anchor162">1.6.1 URI格式</span>

表示指定的URI，要使用覆盖全部必要信息的绝对URI、绝对URL以及相对URL。
* 相对URL，是指从浏览器中基本URI处指定的URL，形如/image/logo.gif

绝对URI格式如下：
![](/001-图解HTTP/Pictures/1610.png)

使用https:或http:等协议方案名获取访问资源时要指定协议类型，不区分字母大小写，最后附一个冒号（:）

* **登录信息（认证）-可选**
  * 2
* **服务器地址 -必填**
  * 可以是DNS可以解析的名称：类似hackr.jp
  * IPv4地址：类似192.168.1.1
  * IPv6地址：用方括号括起来，[0:0:0:0:0:0:0:1]
* **服务器端口号 -选填**
  * 指定服务器连接的网络端口号
  * 若省略则自动使用默认端口号
* **带层次的文件路径 -必填**
  * 指定服务器上的文件路径来定位特指的资源，与UNIX系统的文件目录结构相似
* **查询字符串 -可选**
  * 针对已指定的文件路径内的资源，可以使用**查询字符串传入任意参数**
* **片段标识符 -可选**
  * 使用片段标识符可标记出已获取资源中的子资源（文档内的某个位置）
  * RFC中并没有明确规定其使用方法

>RFC:征求修正意见书（Request for Comments），一些用来制定HTTP协议技术标准的文档
>RFC是互联网的设计文档，通常应用程序会遵照由RFC确定的标准实现；
>并不是所有的应用程序都符合RFC，不符合，可能无法通信

