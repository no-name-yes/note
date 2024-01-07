### intro
tcp不能控制传输中的中间传输过程，故而TCP实现的拥堵控制是通过调节报文中的Windows大小来控制的


#### AIMD
aimd(additive-increase/multiplicative-decrease)和性增长/乘性降低
IF packet received: W <-- W + $\frac{1}{W}$     
IF packet is dropped: W <-- $\frac{W}{2}$               [^aimd增减]
W:sliding windows size 
cwnd: 拥堵窗口

throughtput(吞吐量):为$\frac{W}{RTT}$

aimd只控制已发送但未被接受的数据包的数量

single flow:
[ainimation eaxmple] (http://guido.appenzeller.net/anims/)
in single flow,RTT随着W的移动而偏移

multi flow:
大量的flow也遵守单个flow的aimd,但是此时多个流的RTT时间为一个常数(constant)在图像上表示为斜率一定(直线),而单个flow的RTT斜率为一个变量[^单个和多个流的吞吐量]


#### congestion control

##### TCP Tahoe
sender window = min(flow window,congestion window)
###### congestion window:
TWO states:
TCP在两种状态控制网络的拥堵状况:slow starup和congestion avoidance
slow starup(慢启动):在开始连接或者发送的包等待ack超时的情况,此时的congestion window大小是成每一个ack的MSS的指数性质增加   
congestion avoidance(拥堵避免):当拥堵窗口达到了阈值ssrh       是线性增长

###### timeout estimation

####### self-clocking

##### TCP reno

##### new TCP reno

#### thinking
可以阅读Van jacobson and Karels的论文"Congestion Avoidance and Control"


[^aimd增减]: W+1/W像一种试探,当整个W都接受到了ack后整个W大小就增加了1,当buffer达到瓶颈时立刻缩小一半来减少占用,有点像用二分查查的方式以有一个看得见的上限的消耗去查找


[^单个和多个流的吞吐量]在多个流中会有公平竞争的条件，多个流之间的竞争可能导致单个流的RTT增加，但这个影响相对均匀地分布在多个流之间。在相对稳定的网络环境下，多个流的RTT可以保持较为一致。