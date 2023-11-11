### Stop and wait
![[Pasted image 20231111092036.png]]



problem:如果使用stop and wait 就要一个一个数据包来确认导致对通信链路的利用率低,传输速率慢,如一个10mbps，RTT50ms 的链路使用stop and wait传输大小为10KB的包利用率为(10kb*20)/10m=2% , 所以现在的协议大多数使用滑动窗口来传递多个包增加效率


### sliding windows
Sender:
每一个segment有一个序号
send window size(SWS滑动窗口大小)
Last acknowledgment received(LAR最后接收ack序号)
Last segment sent(LSS最后发送序号)
维护窗口使LSS-LAR+1<=SWS 

Receiver:
Receive window size(RWS接收窗口大小)
Last acceptable segment(LAS最后接收到的序号)
Last segment received(LSR最后已接收(已发送ack)序号)
维护窗口使LAS-LSR+1<=RWS 


RWS<=SWS
当接收方的窗口接收多个segment时,序列靠前的包被丢失了后面的在窗口范围内的包会缓存当接收了前面缺失的包后会发送现在已有包的最大序号如接收2,3,4,5其中3需要重新接收发送ack2当收到3后发送ack5