# Socket
## 创建Socket
```c
    #include <sys/socket.h>//linux
    int socket(int domain, int type, int protocol);
    //domain  socket中使用的协议族
    //type   socket数据传输类型信息
    //protocol  计算机间通信中使用的协议信息
```
### 协议族
| 名称       | 协议族   |
| --------   | -----:  |
| PF_INET     | IPv4互联网协议族 |
| PF_INET6        |   IPv6互联网协议族    |
| PF_LOCAL        |    本地通信的UNIX协议族    |
| PF_PACKET        |    底层嵌套字的协议族    |
| PF_IPX        |    IPX Novell协议族    |
### Socket类型
#### Socket类型1：面向连接的Socket(SOCK_STREAM)
特点：
1. 传输过程中数据不会丢失。
2. 按序传输数据。
3. 传输的数据不存在数据边界。
注：面向连接的Socket只能和另一个同样特性的Socket连接。
#### Socket类型2：面向消息的Socket(SOCK_DGRAM)
特点：
1. 强调快速传输而非传输顺序。
2. 不保证传输数据的稳定性。
3. 传输的数据有数据边界。
4. 限制每次传输的数据大小。
### 协议的最终选择
该参数只有在同一协议族中存在多个数据传输方式相同的协议的情况下才有意义。
如在满足IPv4协议族中面向连接的Socket的前提情况下，可以选择IPPROTO_TCP，该Socket为TCP套接字。
```c
int tcp_socket=socket(PF_INET,SOCK_STREAM,IPPROTO_TCP);
```
相应的UDP套接字应如下定义：
```c
int ud_socket=socket(PF_INET,SOCK_DGRAM,IPPROTO_UDP);
```

