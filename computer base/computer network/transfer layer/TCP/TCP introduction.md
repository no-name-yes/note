

![[Pasted image 20231110154536.png]]
### TCP service model

byte stream delivery service
reliable delivery
    1.ack(确认收到)
    2.checksum(检验和)
    3.sequence number(数据包序号)
    4.flow-control(流控制 避免如发送方发送数据速率大于接收方数据接收速率数据溢出等情况)
in sequence(有序)
(congestion control)前三个都是对应用程序提供的服务这个不是






### TCP header







### setup and teardown
![[TCP FSM diagram2.png]]
#### setup
established之上的状态过程
注意tcp setuo中的ack为sequnce+1
例子:3 steps handshake
endpoint A to server B:
A:syn Sequnce(a)  ---->   B
A   <------ B: syn Sequnce(b) + ack(a+1)
A:  Sequnce(a+1) ack(b+1)------>B

可能有四个报文的建立(即双方都active(主动的)发送一个tcp连接请求)
例子:
A: syn Sequnce(a)----->B
A  <------------- B:syn Sequnce(b)
A: syn Sequnce(a) ack(b+1)----->B
A <--------------- B: syn Sequnce(b) ack(b+1)


#### teardown
established之下的状态过程

在客户端主动调用close函数后会在把报文段的fin字段置位,此时发出fin自己不在发送消息进入fin wait 1阶段,此时可能收到另一方的回复;1.也收到fin报文说明另一方也主动的关闭了tcp连接,此时发送ack进入closing状态,2.收到fin+ack报文说明另一方收到了己方发送的fin回复了ack并且也关闭了连接,此时发送ack同意关闭进入time wait状态3.只收到了ack报文,说明对方还没有发送完消息,此时进入fin wait2状态等待对方的消息发送完毕和对方的fin报文,此时对方对应的是图上的passive close中的close wiat的状态.