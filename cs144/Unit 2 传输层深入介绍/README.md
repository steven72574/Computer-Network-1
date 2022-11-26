字节流stream of bytes
![image](https://user-images.githubusercontent.com/83968454/204064081-5f846c24-03b5-4ae1-a5a4-f03382b1f2df.png)
A将流中的字节放入TCP段中，交给IP层，TCP也可以小到1字节，但是当数据量大的时候，这样不是很高效，因此可以填充tcp段一直到最大IP数据包的大小  
建立连接后，两端会有state machine状态机保持这个连接。
![image](https://user-images.githubusercontent.com/83968454/204064170-30d29f24-a529-46b9-8d49-be46151770b4.png)

