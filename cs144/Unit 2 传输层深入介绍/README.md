__连接的建立__：首先，TCP建立从A到B的通信通道，然后建立从B到A的通信通道，在通道两端TCP会保留一个状态机来跟踪连接方式。建立连接是使用三次握手协议  
__连接的关闭(Connection Teardown)__:当AB之间数据传输完成之后，连接会关闭。首先A请求端，发送FIN标志的数据包到B，意味着A不会向B发送数据，但是B的数据可能还没发送完，因此向A发送一个（Data+）ACK，然后TCP连接尚不会断。当B发送完数据后，B最后会发送一个FIN的信息给A，A收到Fin后，返回B一个ACK信号进行确认。至此整个TCP连接关闭，状态机可以被移除。  
![image](https://user-images.githubusercontent.com/83968454/204130058-a67db5e8-39cb-4760-ba66-7aa5ee081fd7.png)  

字节流stream of bytes  
![image](https://user-images.githubusercontent.com/83968454/204064081-5f846c24-03b5-4ae1-a5a4-f03382b1f2df.png)  
A将流中的字节放入TCP段中，交给IP层，TCP也可以小到1字节，但是当数据量大的时候，这样不是很高效，因此可以填充tcp段一直到最大IP数据包的大小  
建立连接后，两端会有state machine状态机保持这个连接。
![image](https://user-images.githubusercontent.com/83968454/204064170-30d29f24-a529-46b9-8d49-be46151770b4.png)
### 2-1 TCP服务模型

![image](https://user-images.githubusercontent.com/83968454/204114503-0c47079c-29a1-4287-83c9-01658e880920.png)  
__Source Port__ :数值不能大于2^16-1。请求发出去后，响应的信息将会回到这个端口。当连接发起时，连接发起方会生成唯一的源端口号，因此连接与其他连接区分开  
__Sequence number__:指示在字节流中，TCP的第一个字节的位置（序列号的没太听懂）  
__Acknowledgment Sequence__: 确认已收到的字节。如为751，则表示前750个字节都已收到。    
__Checksum__:检验标头和数据是否损坏，后面会详细将如何检验。   
__Flags__  
ACK：表示Acknowledgment Sequence是有效的，我们正在确认至今为止收到的所有数据；  
SYN:三次握手的一部分  
FIN:指示连接的一个方向的关闭  
PSH：指示另一端的TCP层在数据到达后立刻传输数据，而不是等待更多数据。对于某些对时间有要求的数据比如按键，很有用。     
__Destination Port__ :应用程序的端口号，类似于Ip协议的IP地址，端口号是应用程序的地址。web端口号是80。IANA可以查端口号。ssh连接端口号是22，smtp邮件是23  
![image](https://user-images.githubusercontent.com/83968454/204129555-ac14b211-c7b0-4846-b327-0f64411c3c01.png)  

![image](https://user-images.githubusercontent.com/83968454/204130383-7a021ca1-dc6b-430f-b16d-bdead4517215.png)  

__Unique ID__，一个TCP连接由下面五个信息唯一标识。  
当发送方开始建立TCP连接时，会创建新的端口号，可以避免与另一个有着相同Unique ID 的TCP连接重复，新端口号最多允许64k个连接。但是当A主机突然发送很多连接时，也可能出现端口号重复的情况，因此A的端口号选择是随机的，能尽可能避免这种情况发生。  
![image](https://user-images.githubusercontent.com/83968454/204115169-2dcaf4c8-434a-4933-aa08-da764c2dad24.png)   

### 2-2 UDP服务模型
Length：Headers + data的长度  
Checksum: IPv4协议时，该字段是可选的，若没有，则全为0  
DNS就是使用UDP协议，简单快速，无需建立连接  
![image](https://user-images.githubusercontent.com/83968454/204115403-ecde7cf6-5752-4cb3-a191-75307d6a69b2.png)   
![image](https://user-images.githubusercontent.com/83968454/204115529-5b784338-4547-4f86-87b3-95fd53dd1f0b.png)  

### 2-3ICMP(Internet Control Message Protocol)
ICMP提供了在网络层的，去终端主机中的路径上的路由信息。  
ICMP报告错误信息以及帮助我们诊断信息  
ICMP在IP的上面，因此是传输层的机制。  
Ping和traceroute都依赖于ICMP  
![image](https://user-images.githubusercontent.com/83968454/206720721-78d6c1e1-50bb-48df-9f9b-7803f718b1dd.png)  
![image](https://user-images.githubusercontent.com/83968454/206720809-b7aeac94-ac2e-4d46-8079-f1bb68e58786.png)  
![image](https://user-images.githubusercontent.com/83968454/206721512-75da3479-fcad-4ece-b5db-65d4f8946505.png)  
![image](https://user-images.githubusercontent.com/83968454/206721578-84082eb5-3073-4d61-ade5-0e8b8dadeaaf.png)  
traceroute会发送TTL从1到n的消息，这样的话，当消息到第一个路由的时候，TTL变成0，第一个路由会往回发送一个ICMP消息，说这个包失效了，其中包含路由信息和时间  
![image](https://user-images.githubusercontent.com/83968454/206721732-a71b2e33-de5d-4bf7-88e0-51268c2caa85.png)

### 端到端原则
大意就是：不能指望网络帮你确保比如安全，如不丢包，如数据不被篡改等。程序员需要在两端也有这些措施才能确保万无一失。举了个例子：比如MIT相信了网络会有错误检测，因此在两端就没有进行错误的检测，最后导致很多源代码丢失。比如传输路径上的计算机D的内存有问题，会翻转一些bit，而D在发出去之后，E接收到没问题，因为这里只能检测数据包从D到E是没有问题的，不能检查出D里面发生的错误。
强端到端原则：
假定在传输过程中做的事很少，把那些确保安全和可靠性的功能都留给两个端系统去完成，这个能够提高效率和灵活性。
如果在传输过程中优化太多，那么这里就很容易牵一发而动全身，因为传输层假定了上一层和下一层在做什么。



