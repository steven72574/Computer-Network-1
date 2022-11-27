字节流stream of bytes
![image](https://user-images.githubusercontent.com/83968454/204064081-5f846c24-03b5-4ae1-a5a4-f03382b1f2df.png)
A将流中的字节放入TCP段中，交给IP层，TCP也可以小到1字节，但是当数据量大的时候，这样不是很高效，因此可以填充tcp段一直到最大IP数据包的大小  
建立连接后，两端会有state machine状态机保持这个连接。
![image](https://user-images.githubusercontent.com/83968454/204064170-30d29f24-a529-46b9-8d49-be46151770b4.png)
### 2-1 TCP服务模型

![image](https://user-images.githubusercontent.com/83968454/204114503-0c47079c-29a1-4287-83c9-01658e880920.png)
Source Port :数值不能大于2^16-1。请求发出去后，响应的信息将会回到这个端口。当连接发起时，连接发起方会生成唯一的源端口号，因此连接与其他连接区分开  
Sequence number:第一个字节的位置（序列号的没太听懂）  
Acknowledgment Sequence: 确认已收到的字节。如为751，则表示前750个字节都已收到。    
Checksum:检验标头和数据是否损坏，后面会详细将如何检验。   
Flags：ACK：表示Acknowledgment Sequence是有效的，我们正在确认至今为止收到的所有数据；  
SYN:三次握手的一部分  
FIN:指示连接的一个方向的关闭  
PSH：指示另一端的TCP层在数据到达后立刻传输数据，而不是等待更多数据。对于某些对时间有要求的数据比如按键，很有用。  
Destination Port :应用程序的端口号，类似于Ip协议的IP地址，端口号是应用程序的地址。web端口号是80。IANA可以查端口号。ssh连接端口号是22，smtp邮件是23  
![image](https://user-images.githubusercontent.com/83968454/204115169-2dcaf4c8-434a-4933-aa08-da764c2dad24.png)  
Unique ID，一个TCP连接由上面五个信息唯一标识。
当发送方开始建立TCP连接时，会创建新的端口号，可以避免与另一个有着相同Unique ID 的TCP连接重复，新端口号最多允许64k个连接。但是当A主机突然发送很多连接时，也可能出现端口号重复的情况，因此A的端口号选择是随机的，能尽可能避免这种情况发生。  
### 2-2 UDP服务模型
Length：Headers + data的长度  
Checksum: IPv4协议时，该字段是可选的，若没有，则全为0  
DNS就是使用UDP协议，简单快速，无需建立连接  
![image](https://user-images.githubusercontent.com/83968454/204115403-ecde7cf6-5752-4cb3-a191-75307d6a69b2.png)   
![image](https://user-images.githubusercontent.com/83968454/204115529-5b784338-4547-4f86-87b3-95fd53dd1f0b.png)  



