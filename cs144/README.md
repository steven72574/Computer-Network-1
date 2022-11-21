b站视频课  
https://www.bilibili.com/video/BV137411Z7LR/?p=2&spm_id_from=pageDriver&vd_source=b3aa7c7adc98551fe4fc24f22a3e3c2b  
### 1-1 应用层的三个例子：
1.__world wide web (HTTP)__，客户端-服务器模型  
![image](https://user-images.githubusercontent.com/83968454/203172501-8138d361-26f2-411e-857a-cedbae94df75.png)

2.__BitTorrent__(种子，磁力链接),首先你拿到一个torrent，torrent记录着tracker的位置，当你向tracker发送请求时，可以返回一个称为群的集合，这里包含拥有该资源的其他客户端的地址，  
然后你便会向这些客户端发送请求，然后获得资源（响应），当一个新客户访问到你的计算机时，你会告诉这个新的客户其他客户端的地址，因此这个新客户又能从其他客户端下载资源。  
![image](https://user-images.githubusercontent.com/83968454/203171981-31145b35-a3ed-441b-b7f9-7cb0e8efd727.png)

3.__Skype__：一方在NAT后面，这里假设B在NAT后面，则B在登录skype之后，和中间服务器进行一个长连接，此时，若A（不在NAT后面）要呼叫B时，则A向Rendzvos发送请求，
并且借此与B进行连接。若两方都在NAT后面，则A和B都须与中间服务器进行长连接。  
![image](https://user-images.githubusercontent.com/83968454/203170783-83f8b5db-7284-49d4-abe3-08799d07a007.png)  
![image](https://user-images.githubusercontent.com/83968454/203171184-37011ca7-f8e8-4e0a-ba3d-339479fe727c.png)  

### 1-2 网络模型的四层  
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
 
### 1-3 IP服务


