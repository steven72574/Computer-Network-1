# Computer-Network-1
通过发送请求获取服务器资源的 Web 浏览器等，都可称为客户端（client）。  
HTTP (HyperText Transfer Protocol)  
TCP/IP是互联网相关各类协议的总称  
包括四层：  
1.__应用层__：负责应用与电脑之间的通信，如HTTP，FTP(File Transfer Protocol),DNS(Domain Name System) ,DNS负责域名到IP地址间的解析服务   
2.__传输层__：负责为处于网络连接中的两台计算机之间的数据传输（包括分割数据包与合并数据包），有TCP(Transmission Contril Protocol)和UDP(User Data Control)   
3.__网络层__：处理网络上流动的数据包，网络层所起的作用就是在众多的选项内选择一条传输路线，IP(Internet Protocol)协议   
4.__链路层__：硬件上的范畴均在链路层的作用范围之内。  
![image](https://user-images.githubusercontent.com/83968454/203115774-e0858077-5424-4dd7-a3a5-f940ce49253c.png)  
TCP协议的三次握手策略   
其中SYN(synchronize),ACK(acknowledgement)  
![image](https://user-images.githubusercontent.com/83968454/203118058-c49b744e-3ed6-4ddf-8738-d566c4598ba7.png)  
### DNS服务示意  
![image](https://user-images.githubusercontent.com/83968454/203118677-d501a93d-b6c6-45ed-aa12-7f88409ca998.png)  
### URI 与 URL
URI 就是由某个协议方案表示的资源的定位标识符。协议方案是指访问资源所使用的协议类型名称如http，ftp。  
URI 用字符串标识某一互联网资源，而 URL表示资源的地点（互联网上所处的位置）。可见 **URL是 URI 的子集**。  
下面为URI的各种例子，前面是所使用的协议名称，后面是资源的定位标识符  
![image](https://user-images.githubusercontent.com/83968454/203120425-041f4013-5a61-4046-b709-3f2ec624b290.png)  
HTTP的持久连接   
![image](https://user-images.githubusercontent.com/83968454/203127328-2802454a-baad-416e-be48-c97c681d7bee.png)  
管线化（pipeline），发送请求后无需等待即可再次发送请求  
![image](https://user-images.githubusercontent.com/83968454/203127660-5ba8ef4c-2a16-4380-9f80-bc7291921b6e.png)  
HTTP 是无状态协议，它不对之前发生过的请求和响应的状态进行管理。也就是说，无法根据之前的状态进行本次的请求处理。  
因此每次跳转新页面要在每次请求报文中附加参数来管理登录状态。这就是Cookie做的事。  
当传输大容量数据时，也会将数据分割成多块，和TCP分割成数据包要区分开来  
HTTP/1.1允许一台HTTP服务器搭建多个web站点，在这之中使用的是虚拟主机的功能（如下图），此时，同个服务器的多个域名在DNS解析之后会  
映射到同一个IP地址，因此在发送请求时，必须在Host首部内完整指定主机名或者域名  
![image](https://user-images.githubusercontent.com/83968454/203134846-0230d553-2ddf-467e-82ff-84e6b82068e6.png)   
### 通信数据转发程序
1.__代理__： 客户端和服务器的中间人，接受客户端的请求并转发给服务器，以及将服务器传回的响应转发给客户。  
![image](https://user-images.githubusercontent.com/83968454/203136517-aad26e05-d2c0-47c0-a03f-bfaf76c8fea5.png)  
__缓存代理__：代理转发响应时，缓存代理（Caching Proxy）会预先将资源的副本（缓存）保存在代理服务器上。当代理再次接收到对相同资源的请求时，  
就可以不从源服务器那里获取资源，而是将之前缓存的资源作为响应返回，这样可以节省服务器带宽使用。  
__透明代理__:转发请求或响应时，不对报文做任何加工的代理类型被称为透明代理（Transparent Proxy）。反之，对报文内容进行加工的代理被称为非  
透明代理。  
2.__网关__：转发其他服务器通信数据的服务器，接收从客户端发送来的请求时，它就像自己拥有资源的源服务器一样对请求进行处理。有时客  
户端可能都不会察觉，自己的通信目标是一个网关。  
3.__隧道__：隧道是在相隔甚远的客户端和服务器两者之间进行中转，并保持双方通信连接的应用程序。  
HTTP结构（首部字段的顺序不影响，如通用首部字段可以在请求首部字段前）  
![image](https://user-images.githubusercontent.com/83968454/203138159-6d4b2a43-c797-4e9c-b0f3-400b13469ce8.png)  
![image](https://user-images.githubusercontent.com/83968454/203138074-1da20eb9-3a2a-4a9f-943a-fe9485659925.png)  


