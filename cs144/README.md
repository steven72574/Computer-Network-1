b站视频课  
https://www.bilibili.com/video/BV137411Z7LR/?p=2&spm_id_from=pageDriver&vd_source=b3aa7c7adc98551fe4fc24f22a3e3c2b  
### 1-1：
三个例子：
1.__world wide web (HTTP)__，客户端-服务器模型  
![image](https://user-images.githubusercontent.com/83968454/203172501-8138d361-26f2-411e-857a-cedbae94df75.png)

2.__BitTorrent__(种子，磁力链接),首先你拿到一个torrent，torrent记录着tracker的位置，当你向tracker发送请求时，可以返回一个称为群的集合，这里包含拥有该资源的其他客户端的地址，  
然后你便会向这些客户端发送请求，然后获得资源（响应），当一个新客户访问到你的计算机时，你会告诉这个新的客户其他客户端的地址，因此这个新客户又能从其他客户端下载资源。  
![image](https://user-images.githubusercontent.com/83968454/203171981-31145b35-a3ed-441b-b7f9-7cb0e8efd727.png)

3.__Skype__：一方在NAT后面，这里假设B在NAT后面，则B在登录skype之后，和中间服务器进行一个长连接，此时，若A（不在NAT后面）要呼叫B时，则A向Rendzvos发送请求，
并且借此与B进行连接。若两方都在NAT后面，则A和B都须与中间服务器进行长连接。  
![image](https://user-images.githubusercontent.com/83968454/203170783-83f8b5db-7284-49d4-abe3-08799d07a007.png)  
![image](https://user-images.githubusercontent.com/83968454/203171184-37011ca7-f8e8-4e0a-ba3d-339479fe727c.png)  

