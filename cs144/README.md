b站视频课  
https://www.bilibili.com/video/BV137411Z7LR/?p=2&spm_id_from=pageDriver&vd_source=b3aa7c7adc98551fe4fc24f22a3e3c2b  
## 1-1 应用层的三个例子：
1.__world wide web (HTTP)__，客户端-服务器模型  
![image](https://user-images.githubusercontent.com/83968454/203172501-8138d361-26f2-411e-857a-cedbae94df75.png)

2.__BitTorrent__(种子，磁力链接),首先你拿到一个torrent，torrent记录着tracker的位置，当你向tracker发送请求时，可以返回一个称为群的集合，这里包含拥有该资源的其他客户端的地址，  
然后你便会向这些客户端发送请求，然后获得资源（响应），当一个新客户访问到你的计算机时，你会告诉这个新的客户其他客户端的地址，因此这个新客户又能从其他客户端下载资源。  
![image](https://user-images.githubusercontent.com/83968454/203171981-31145b35-a3ed-441b-b7f9-7cb0e8efd727.png)

3.__Skype__：一方在NAT后面，这里假设B在NAT后面，则B在登录skype之后，和中间服务器进行一个长连接，此时，若A（不在NAT后面）要呼叫B时，则A向Rendzvos发送请求，
并且借此与B进行连接。若两方都在NAT后面，则A和B都须与中间服务器进行长连接。  
![image](https://user-images.githubusercontent.com/83968454/203170783-83f8b5db-7284-49d4-abe3-08799d07a007.png)  
![image](https://user-images.githubusercontent.com/83968454/203171184-37011ca7-f8e8-4e0a-ba3d-339479fe727c.png)  

## 1-2 网络模型的四层  
![image](https://user-images.githubusercontent.com/83968454/203173073-93e89051-396e-4fed-898a-57d161e8b63d.png)  
### 各层使用的单位  
1、 应用层的PDU 称为数据(data)；  
2、 传输层的PDU 称为数据段(segment)；  
3、 网络层的PDU 称为数据包(packet)；  
4、网络接口层得PDU 称为帧(Frames)；  
5、介质实际传输实际使用的PDU 称为比特（位）。 
### 各层介绍  
1.数据链路层(Link)：如wifi，以太网  
![image](https://user-images.githubusercontent.com/83968454/203173145-39644d6f-bd26-4ad3-8054-47f883295f8e.png)  
2.网络层(Network)。使用IP协议，单位为数据报(packet),结尾包含起点和终点的IP信息。特点是：__尽力__ 将数据报传输给目的地，但不保证完整性，期间
可能没有送达目的地，可能不按顺序传输，可能多传输了数据报，数据报也可能损坏。
![image](https://user-images.githubusercontent.com/83968454/203173294-c1d29ede-2177-43fe-a26a-067d548120cf.png)  
传输过程：路由器中接受来自链路层的帧，然后交给路由器中的网络层，然后解析IP地址，根据IP地址往下一个路由传递，直到到达客户端  
![image](https://user-images.githubusercontent.com/83968454/203173943-53f681a9-0945-406b-b022-9e728ce0cb5e.png)  
3.传输层(Transport):控制拥塞，使用TCP(Transmission Control Protocol)协议，确保一端的应用程序发送的数据以正确的顺序，不丢包，无损坏地传递到另一端的应用程序。
但是有例外，比如视频通话，丢包的情况并不会太影响通话质量，可能知识视频分辨率变低，但是如果丢包时再重复去请求，此时会造成卡顿和不必要的资源浪费。
此时可以UDP协议，该协议不保证传输的可靠性，只负责传输数据。
4.应用层：如HTTP,BitTorent,skype
 
## 1-3 详细介绍IP协议
打包图示  
![image](https://user-images.githubusercontent.com/83968454/203178498-17155990-00cf-4fdd-a3d0-65e3ccbf1bb0.png)  
Hop-by-Hop routing:逐跳传输  
在中间路由器发生拥堵时，路由会拒绝接受新的数据报，因此产生丢包，而发送者不知道这个过程。  
而错的路由列表可能导致数据报没有被送到目的端，而IP不能保证这些不会发生  
![image](https://user-images.githubusercontent.com/83968454/203179640-311f21ba-21ea-4a64-a384-dbef9eeec166.png)  
### IP服务模型几个必须功能  
1.必须能阻止数据报一直循环。解决办法：通过在数据报报头加一个跳数字段（也成为生存时间,time to live），记录该数据报经过了多少个路由，一般从128开始递减  
2.如果包太大，则要把他分小。以太网每次最大只能传输1500字节的数据，因此每个包不能超过这个值。  
3.报头有校验文件，使得传输到错误目的地的概率降低  
4.允许新的IP版本，如IPv6。因为IPv4(32 bit 地址)的IP快被分配完毕了，现在慢慢过渡到IPv6（128 bit 地址）  
5.允许向报头（header）添加新选项。  
以下是IP的报头实例，Data是从传输层传过来的数据。其中  
Destination IP Address和 Source IP Address 是最重要的两个  
Protocol ID:指的是传输层用的协议（一共有140种不同的协议值），比如6是TCP协议，下面Data部分可以被TCP协议解析  
Version:表示是IPv4还是IPv6   
Total Packet Length ：包括报头和所有数据总长可以达到64kBytes  
TTL：防止数据报在路由之间无限循环，占用资源，到达0时，路由会丢弃该数据报  
Packet ID , Flags , Fragment Offset :用于帮助将数据报分成更小的部分  
Type of Service 提示该数据报的重要性  
Header Length：报头长度，报头还可能包含可选的其他字段  
Ckecksum 对整个报头计算校核，防止报头是损坏的  
![image](https://user-images.githubusercontent.com/83968454/203182201-8b97c0c2-4191-476d-9ed5-eec47b65494c.png)  

## 1-4 数据包的一生
路由器存有转发表（forwarding table）存储ip地址，当一个包到达路由时，若此时没有比默认路由default route更具体的路由，则会选择默认路由，默认路由一般连接着更大的网络。比如在达姆图书馆使用图书馆wifi，此时图书馆的路由器会存有通往学校别的地方的路由地址，如机械院，计算机院的IP地址，如果客户端访问的目的地不是学校，则图书馆路由会选择默认路由，以通往更大的网络。
wireshark抓包
三次握手建立连接之后，客户端才向服务器发送GET请求  
![image](https://user-images.githubusercontent.com/83968454/203993088-b6e1d045-73c8-4394-bc65-94490eeee5ab.png)  
以及通过 traceroute 查看访问一个网站所经过的路由  
![image](https://user-images.githubusercontent.com/83968454/203994498-d9e72885-8ad6-4f79-a4a8-129447ed5693.png)  

## 1-5
对于每个到达的包，单独地为它选择出口路径，如果该路径是空闲的，则传送过去，否则等待空闲时传送。交换机会有  
分组交换有两个很好的特性：  
1.单独为每个数据包做出决策  
2.不需要数据包上保存额外的信息，而且一个人使用时，不会占用线路，另一个人还是可以使用  
![image](https://user-images.githubusercontent.com/83968454/203995393-11335d42-82a1-472b-9d74-ddaef44c817d.png)  
数据流定义：是有着相同起点和终点的一系列数据包的集合，比如 TCP连接  
![image](https://user-images.githubusercontent.com/83968454/203996758-74a27687-43f2-4c8f-9f08-6d4ef0ac41e2.png)  
路由器不存储数据流的状态，不用存储是谁建立了连接，这样的话，一个路由器能多人同时使用，并且路由器不会需要巨大算力去管理这些状态   
### 总结：  
1.分组交换packet switching很简单，他独立地发送包，不需要了解什么是流flows  
2.分组交换很高效，它可以让大家在有着许多流flow的同一条线路中共享容量  
分组交换是建立网络最常用的方法  
![image](https://user-images.githubusercontent.com/83968454/203997753-4e63eda9-8ddd-4f0a-9f92-dcb61bcd9282.png)  

## 1-6 Layering
分层是个很重要的概念，在程序设计中很常使用  
希望每一层隐藏一些实现细节，对外只显示其实现的功能  
![image](https://user-images.githubusercontent.com/83968454/204008096-da6bac23-cc26-40e5-8afe-fde13dd9283c.png)  
## 1-7
封装的灵活性。  
封装是便于分层，以及方便分层的实现
TLS为加密  
![image](https://user-images.githubusercontent.com/83968454/204012655-438dd8b4-87cd-47e6-9a02-c6d33617c891.png)  

## 1-8字节储存顺序
看不懂，先跳过

## 1-9 IPv4
ip地址是四个8位的值组成，8位也就是2^8 == 256，因此单个范围为0-255  
Netmask 网络掩码，可以告诉哪些ip是在同一个网络中的，  
255.255.255.0 换成位就是 11111111.11111111.11111111.00000000  
255.255.252.0 换成位就是 11111111.11111111.11111100.00000000  
若本机IP为 192.168.0.100对于 255.255.255.0的子网掩码来说，如果我要发送的数据目的地Ip地址是以192.168.0开头的，则直接发送即可，不需要通过路由器往外部发送。  
``` java
//A 为 A电脑的IP地址 ，B为B电脑的IP地址
if(A & Netmask == B & Netmask)
    //则AB在同一网络中
```
位运算
![image](https://user-images.githubusercontent.com/83968454/204020259-b799f60a-e6ae-4b47-a0e4-77c5927db937.png)

![image](https://user-images.githubusercontent.com/83968454/204019509-df3a4b80-f366-4634-be92-aff2a1785b45.png)

### CIDR-Classless Inter-Domain Routing  

翻译过来就是：无类域间路由，它是一种IP寻址方案，它改进了IP地址的分配。它取代了基于A、B、C类的旧系统，极大地延长了IPv4的使用寿命，减缓了路由表的增长速度。  
地址是 address,count 的对，其中 count 是 2 的幂 ，表示了子网掩码的长度  
171.64.0.0/16 表示位于171.64.0.0 到171.64.255.255之间的地址。相当于前16位地址不变  
A/24 相当于前24位不变，因此描述256个地址  
下图中 A/24 24为子网掩码位长度  
![image](https://user-images.githubusercontent.com/83968454/204024561-6ea011d7-e7f1-4837-9799-bddba860b4be.png)  

## 1-10
转发表是CIDR的集合  
最长前缀匹配 longest prefix match,是ip路由器决定如何转发地址的算法  
比如 171.33.0.1 都能符合下面的IP，但是 link为5的IP匹配的前缀长度为16 比0.0.0.0 匹配的前缀长度为0 要长。因此路由会选择link 5发出去。  
![image](https://user-images.githubusercontent.com/83968454/204025908-30e27ac0-0b7f-413e-b669-90b9f57b51af.png)  

![image](https://user-images.githubusercontent.com/83968454/204025164-de8e8159-3047-4bdd-ae30-aa4416148e8a.png)  
### 小练习  
![image](https://user-images.githubusercontent.com/83968454/204028454-b9a8795b-c005-474e-8057-88008907f868.png)  
答案  
转发表中，63.19.5.0/30后面的30表示必须前30位相同，否则不匹配  
A -> 3  
B -> 4  
C -> 1  
D -> 1  
E -> 2  

## 1-11 Address Resolution Protocol  
ARP,地址解析协议是一个通过解析 __网络层地址__, __即IP__ 来找寻 __数据链路层地址__ 的网络传输协议，它在IPv4中极其重要。    
IP地址是网络层地址，描述了主机，也就是网络层的唯一目的地  
link address 描述了特定的网卡：发送和接收链路层数据 — — 帧的设备。  
以太网有48位地址，买网卡的时候以经配备好唯一的以太网地址   
地址是6个8位的组的形式以16进制表示，比如 0：18：e7:f3:ce:1a  
![image](https://user-images.githubusercontent.com/83968454/204031987-8e7fc809-f5d1-4ce6-8484-ca807e8e2907.png)   
网关或路由器有多个接口，每个都有自己的链路层地址，以及网络层地址，如下图，gateway有两个不同的链路层地址和网络层地址  
下图A在向B发送数据时，由于子网掩码255.255.255.0告诉它 ，该IP不在同一网络中，因此要通过网关进行转发，此时他的网络层地址为171.43.22.5，但是链路层目的地地址是网关的链路层地址，即0：18：e7:f3:ce:1a  
那如何得到这个网关的地址呢？在这个过程，我们需要将网络层的地址映射到其对应的链路层的地址上，这就是 __ARP__，__地址解析协议__。    
![image](https://user-images.githubusercontent.com/83968454/204034588-3514ee4f-b7ec-4a6d-bbdc-813e56e0c311.png)  
ARP是一个简单的 请求-应答协议  
每个节点（网关、路由器）保存了该网络上的IP地址到链路层的映射的缓存，如果当前节点没有缓存该IP地址的映射，则会发一个请求，询问有该IP地址节点，而有该IP地址的节点会做出响应，响应包括对应的链路层地址。  
为了使每个节点都能听到该请求，这个节点会将请求发送到链路层广播地址（link layer broadcast address）。发送请求时，会包含请求者的网络地址和链路层地址，因此，当节点听到请求时，能更新存在缓存中的映射。 
ARP字段如下图  
Hardware 说明此请求或响应应用于哪个链路层  
Protocol说的是用的那个协议  
Opcode 说明是请求还是响应  
Hardware address 硬件地址，数据链路层地址  
Protocol address IP地址  

![image](https://user-images.githubusercontent.com/83968454/204062640-23d28ea2-5efa-4d73-bae8-036c1e5d9184.png)  
__例子__  
hardware : 1 (Ethernet)  
Protocol : 0X0800(IP)  
hardware length :6(48bit Ethernet)  
Protocol length : 4(32bit IP)  
OPcode : 1(requst)  
Hardware soure:68:a8:6d:05:85:22  
Protocol soure:192.1168.0.5  
Hardware destination: ?  
Protocol destination: 192.168.0.1  

客户端会在网络上发送这个帧，网络中的每个节点会收到它并且更新其链接地址的映射  客户端会发送带有Hardware destination为ff:ff:ff:ff:ff:ff的请求，网关发现该请求是针对自己的IP地址的，因此产生答复  
![image](https://user-images.githubusercontent.com/83968454/204063013-68bc9b2d-cb07-4a74-a537-c9a8c8b9e7ad.png)    
