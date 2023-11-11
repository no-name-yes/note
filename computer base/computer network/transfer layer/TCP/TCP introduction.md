

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