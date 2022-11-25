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
1.数据链路层(Link)：如wifi，以太网  
![image](https://user-images.githubusercontent.com/83968454/203173145-39644d6f-bd26-4ad3-8054-47f883295f8e.png)  
2.网络层(Network)。使用IP协议，单位为数据报(Datagrams),结尾包含起点和终点的IP信息。特点是：__尽力__将数据报传输给目的地，但不保证完整性，期间
可能没有送达目的地，可能不按顺序传输，可能多传输了数据报，数据报也可能损坏。
![image](https://user-images.githubusercontent.com/83968454/203173294-c1d29ede-2177-43fe-a26a-067d548120cf.png)  
传输过程：路由器中接受来自链路层的数据报，然后交给路由器中的应用层，然后解析IP地址，根据IP地址往下一个路由传递，直到到达客户端  
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

